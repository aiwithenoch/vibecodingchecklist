# Performance and Rendering Review

This is a **supplementary review procedure** for the existing engineering checklist, not a new counted topic. It expands evidence for latency, caching, database query optimization, N+1 queries, pagination, load testing, memory leaks, and non-functional requirements. It applies to traditional code and AI-generated code, across frontend frameworks.

**Do not optimize by slogan.** First establish what is slow, for which user journey, device, network, and cache state. Mark each check PASS, FAIL, UNKNOWN, or N/A with evidence. A code pattern is not proof of a production bottleneck, and the absence of an obvious pattern is not proof of performance.

## 1. Establish a repeatable baseline before editing

- [ ] Name the exact slow journey and visible milestone: initial usable screen, a search result, scrolling a feed, opening a course, or a user action. Record the route, account role, data volume, browser/device, viewport, and build/commit.
- [ ] Separate a **cold visit** (cache disabled or empty) from a **warm repeat visit**. Do not compare one cold load with one warm load and call the change an improvement.
- [ ] In the browser Network panel, record the initial navigation through the first useful screen. Capture request count, transfer and decoded sizes where available, timing/waterfall, initiator, resource type, and failed requests. Filter images, scripts, fonts, APIs, and third-party embeds separately.
- [ ] Distinguish requests made before the first screen from requests caused by scrolling, hovering, route prefetching, service workers, or background polling. Hover-triggered prefetch may be intentional; verify whether it helps the real interaction and whether it fires too early or repeatedly.
- [ ] Capture a Performance profile and screenshots for the same journey. Check largest contentful paint (LCP), layout shifts (CLS), interaction latency (INP or the browser trace equivalent), long tasks, scripting, style/layout/paint, and main-thread idle time. Use the profiler to decide whether the bottleneck is network, backend, JavaScript, layout, or paint.
- [ ] Record a memory baseline, perform the same navigation/scroll/interactions for a sustained session, then compare memory and listener/timer/observer counts if tooling allows. One large allocation or an open tab alone does not prove a leak.
- [ ] Repeat on a representative mobile viewport and a constrained network/CPU profile. Use production-like data and permissions where safe; a developer laptop, sample data, and warm cache are not representative of all members.
- [ ] Save the exact commands, trace/HAR/screenshots, tested data size, and before/after numbers. Do not export cookies, authorization headers, personal data, or secrets in a HAR or screenshot.

Chrome's Network panel is useful for verifying what was requested, when, how large it was, and what initiated it; the Performance panel is needed for CPU/layout/rendering evidence too. See [Chrome DevTools Network reference](https://developer.chrome.com/docs/devtools/network/reference/) and [Chrome DevTools Performance reference](https://developer.chrome.com/docs/devtools/performance/reference/).

## 2. Images: request fewer bytes without hiding needed content

- [ ] Classify images by importance. The likely largest above-the-fold/LCP image should not be accidentally lazy-loaded. Below-the-fold, nonessential images can use browser-native lazy loading. Avoid marking every image eager or every image lazy without considering its position and role.
- [ ] Give images accurate intrinsic width and height, or reserve the correct layout using CSS aspect-ratio or a fixed-size container. This lets the browser reserve layout space and reduces layout shifts. For lazy images, dimensions also prevent zero-size layout cases in which an offscreen image may never intersect.
- [ ] Use responsive variants (for example srcset and sizes), server/CDN thumbnails, and reasonable encoding/quality so a 32–100 CSS-pixel avatar does not download a multi-megapixel original. Test actual transferred bytes, not just the source URL or CSS dimensions.
- [ ] Limit high fetch priority to the genuinely critical initial image. Confirm that image transformations/CDN features are enabled in the deployed plan and test the untransformed fallback. Do not trade an image optimization for a failed request or broken avatar.
- [ ] On a cold reload, verify offscreen image requests are deferred until the browser's near-viewport threshold; scroll slowly and quickly to check that images appear in time. Browser distance thresholds vary. If images appear to load eagerly, inspect request initiators, preload/prefetch hints, CSS background images, viewport geometry, browser thresholds, and whether components are all mounted; do not assume missing dimensions are the only possible cause.
- [ ] Check image errors, fallback sources, alt text, aspect ratio, object-fit/crop, and layout stability on narrow and wide screens. Avoid duplicate retries or an image fallback loop.

Modern browsers implement native lazy loading with browser-defined thresholds. Width/height are recommended to reserve aspect ratio and prevent layout shifts; they are not a universal explanation for every eager network request. Consult [MDN: img element, loading, dimensions, fetch priority, and responsive image attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img) and [MDN: lazy loading](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Lazy_loading).

## 3. Video, embeds, and other expensive media

- [ ] Do not initialize many third-party players or iframes above the fold when a thumbnail or click-to-play card will satisfy the initial screen. Use native iframe lazy loading where appropriate, or mount the player when close to view/when requested, with a visible poster and a fallback.
- [ ] Choose video preload deliberately (often none or metadata for feeds, depending on product behavior), and test on mobile/data-limited networks. A metadata request is still a request; multiple videos can add up.
- [ ] Make each media box's aspect ratio known before the resource arrives. Test media that fails, is blocked by browser privacy controls, or requires authentication. Do not hide controls or accessibility labels as an optimization.
- [ ] Verify that scrolling through a feed does not create dozens of players, audio contexts, decoders, or continuing network streams. Pause/release media when it leaves the intended active state if product behavior permits.

## 4. Bound data work at the database, API, and UI

- [ ] Trace each screen from UI to API/database. Count requests and payloads. Check for N+1 behavior (one query per displayed row); prefer a join, aggregation, or bounded batch by IDs when the database/API semantics allow it.
- [ ] Request only fields used by that view. Avoid broad select-all queries when large text, JSON attachments, or nested relations are not needed. Inspect nested one-to-many relations because a single request can still return a large payload; a batch query is not automatically a small query.
- [ ] Apply appropriate filters and limits at the server/database. If users need more than one page, implement a stable continuation mechanism (usually cursor/keyset pagination for changing feeds) with deterministic ordering and de-duplication. Do not fetch the whole table and merely hide all but 20 rows in the browser.
- [ ] Verify that each limit has a continuation path or is an intentional product maximum. A hard limit that silently hides older results is a correctness bug, not successful pagination.
- [ ] Keep pagination stable while new rows arrive; test duplicate, missing, and reordered items, filter changes, back navigation, refresh, and concurrent updates. Ensure authorization and tenant isolation apply to every page, not only the first one.
- [ ] Measure database plans and row counts before adding indexes. Index actual filter/order paths after checking the query plan and write/storage trade-offs. Do not add an index merely because a checklist names one.
- [ ] Separate backend/data loading from rendering. A list virtualizer reduces mounted DOM and rendering work; it does **not** make an unbounded database query, huge API response, or large in-memory array cheap.
- [ ] Cache only where freshness, user/tenant isolation, invalidation, and memory bounds are understood. A per-tab cache is not a shared cache, and a cache does not remove the need for bounded queries.

Use the existing [pagination and bounded queries](ESSENTIALS.md) topic and [database index, query optimization, and N+1 checks](111-CONCEPTS.md) rather than adding fashionable infrastructure by default.

## 5. Large lists and virtualization: conditional, not automatic

Virtualization (rendering visible items plus a small nearby buffer) can help when a measured large list is spending substantial time or memory in DOM/render work. It is not mandatory for every application or every list.

- [ ] First measure list size, node count, scripting/layout/paint time, memory, scroll frame drops, and real target devices. Try simpler options first when they address the evidence: bound the server result, use cursor pagination, defer offscreen media, reduce needless per-row work, or use CSS containment where appropriate.
- [ ] If virtualization is justified, use a maintained framework-appropriate implementation instead of improvised scroll handlers. Choose the correct model for fixed/variable-height rows, grids, or masonry; a row virtualizer does not automatically work for a masonry layout.
- [ ] Render the visible range plus an overscan buffer large enough for viewport size, scroll speed, item height, and network latency. Load ahead of the visible boundary when required. Tune from tests across breakpoints; do not hard-code “12 nodes/items” as a universal target.
- [ ] Keep stable item keys and preserve scroll position, focus, open menus, form state, and deep links while items mount/unmount. Make all content reachable by keyboard and assistive technology, or choose a simpler paginated layout that preserves semantics.
- [ ] Verify no blank gaps, flicker, duplicate or missing items, stuck loading, jump-to-top, wrong row/column order, or regressions when scrolling both directions, quickly flinging, resizing, zooming, changing filters, and navigating away/back.
- [ ] Avoid mount-triggered fade/stagger animations on every recycled item. Re-entry should not replay distracting animation, reset useful state, refetch needlessly, or leave stale closures/listeners. Respect reduced-motion settings.
- [ ] Re-check memory and request counts after virtualization. Removing and re-adding DOM nodes does not guarantee an image stays cached or that memory falls; browser caches, decoded bitmaps, component state, and application arrays have different lifetimes.
- [ ] If virtualization fails accessibility, interaction, or stability tests, roll back to bounded pagination or a simpler list. A lower DOM count is not a win if users cannot read or reach the content.

The [Vue performance guide](https://vuejs.org/guide/best-practices/performance.html#virtualize-large-lists) describes virtualization as an optimization for large lists and points to established libraries; treat measured need and correct layout semantics as prerequisites.

## 6. Rendering, rerenders, and resource lifecycle

- [ ] Use a framework profiler to identify expensive component renders and reactive updates. Check render frequency and cost before adding memoization, splitting components, or rewriting state.
- [ ] Look for repeated work in computed lists, sorting/filtering, mapping/grouping, and template expressions. Prefer a single-pass map/group when the measured input size makes repeated scans expensive; do not optimize tiny arrays without evidence.
- [ ] Pair each manually registered event listener with a matching cleanup, including matching callback/options. Clear timers; unsubscribe from stores/realtime channels; disconnect observers; abort fetches on unmount or when their result is obsolete; revoke object URLs and close explicitly allocated image/worker resources.
- [ ] Test mount → navigate away → mount again and repeat. Confirm event handlers and observers are not duplicated, stale requests cannot overwrite the active route, and old DOM/data are collectible. App-lifetime listeners are valid when they intentionally live for the app lifetime; do not label every global listener a leak.
- [ ] Check recursive watchers, reactive feedback loops, repeated polling, and callbacks that schedule themselves. Confirm they have a clear stop condition and bounded concurrency.
- [ ] Use memoization only when the profiler shows expensive repeated computation/rendering and the cache lifetime is understood. Inline objects or functions are not automatically a performance defect.
- [ ] Move CPU-bound work to a worker only when profiling confirms main-thread blocking and the task can be safely moved. “Async” does not make synchronous CPU work cheaper. Background queues suit server work that should not block a request, but add operational complexity and are not a frontend rendering fix.
- [ ] For Vue, verify lifecycle cleanup with the appropriate unmount hooks; for React or another framework, use its own lifecycle and cleanup contract. Do not copy React useEffect/useState prescriptions into Vue code.

See [MDN: removing event listeners and AbortSignal cleanup](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener) and framework documentation for the exact lifecycle behavior.

## 7. Acceptance and regression matrix

For every change, compare the same baseline and preserve the evidence. Mark N/A only with a reason.

| Scenario | What to verify |
| --- | --- |
| Cold first visit | First useful screen, LCP, initial requests/bytes, no unnecessary below-fold media |
| Warm repeat visit | Cache behavior is expected; no request storm or stale private data |
| Mobile / constrained network | Layout reserves image/media space; content arrives before it is needed |
| Slow and fast scroll | No blank content, flashing, jank, or stuck pagination |
| Scroll up and down | Previously viewed items remain correct; state and focus do not reset unexpectedly |
| Long session / route remount | Memory, listeners, timers, observers, and media resources do not grow without bound |
| Large realistic dataset | Server work and UI render remain bounded; pagination/virtualization do not omit results |
| Failure / offline / blocked third-party media | Useful fallback appears; core page stays usable; retry does not duplicate requests |
| Accessibility | Keyboard, focus, labels, reduced motion, and assistive-technology reading order remain usable |

Set budgets with product owners using real traffic and service requirements. Report before/after measurements and device/network conditions; do not invent universal milliseconds, item counts, or DOM caps.

## 8. Detailed review of the supplied 00:00–29:00 video transcript

This timecoded map preserves the transcript's technical claims, sequence, implementation attempts, and caveats so a reviewer can separate useful evidence from overgeneralization. The transcript describes a Lovable/React example; it is not an audited measurement of every app.

- **00:00–00:32 — Symptom and first hypothesis.** The presenter sees a slow initial display, content flashing, and images reloading, then opens browser developer tools. This establishes a symptom to investigate, not its cause.
- **00:33–01:06 — Network inspection and hover behavior.** Hovering over image cards appears to trigger prefetching; the presenter considers this potentially intentional. They reload to separate hover activity from first-load behavior. Keep interaction-triggered requests separate from the initial waterfall.
- **01:07–01:43 — Many initial image requests.** The presenter reports that nearly all images are fetched on initial load and proposes lazy loading. Record image count/bytes and request initiators before deciding whether this is excessive for the actual viewport.
- **01:44–02:57 — Add native lazy loading, then observe unexpected requests.** The transcript says adding a lazy attribute did not seem to stop many images loading. It also describes a later reload/scroll where new images apparently do not load. The sequence is not a clean controlled test; inspect markup, component mounting, browser thresholds, actual scroll container, preloads, and network logs.
- **02:58–04:51 — Possible causes, not yet verified.** The presenter raises header prefetching and missing image dimensions; an AI assistant claims the browser needs dimensions to know which images are below the fold. The useful actions are to inspect sources and reserve the right layout size. The claim should not be simplified into “dimensions alone fix all eager loading”: native loading thresholds and zero-size lazy-image edge cases vary, and eager requests can have other causes.
- **04:52–06:35 — Dimensions, aspect ratio, optional observer, and a second test.** The AI plan proposes width/height, aspect ratio, and optionally IntersectionObserver; the implementation first adds dimensions, then the presenter reports fewer initial requests and more as scrolling. This is a self-reported outcome without request counts or timing data. Native browser lazy loading is the default starting point; use a custom observer only for a measured control requirement and clean it up.
- **06:36–07:22 — Machine/browser slowdown and pause.** The presenter's camera/computer slows during the exercise, and they pause before continuing. This is not sufficient to attribute the slowdown to the application; dev-tool overhead, recording, memory pressure, or the host machine may contribute.
- **07:23–09:10 — Re-render and leak investigation.** The transcript asks an AI tool to review rerenders, listeners, memory, lazy loading, and inline style objects. The tool identifies a possible unremoved scroll listener and React-specific state/effect/context concerns. Treat all as hypotheses until the target code and profiler show them. Listener cleanup is real lifecycle hygiene, but one listener or inline object does not prove a leak or slow page.
- **09:11–12:21 — Generalized memory-leak claims and another scroll check.** The presenter strongly suggests recursive work, unclosed listeners, repeated rerenders, and memory exhaustion, then sees images load while scrolling and calls the result performant. No heap timeline, listener count, repeated-mount test, network comparison, or controlled camera comparison is shown. “Ask AI to find memory leaks” is not a test; verify allocations and cleanup in code and tools.
- **12:22–13:35 — DOM count and proposed virtual-scroll limit.** The presenter sees around 100 list items and proposes virtualization, with “never more than 12” as an example. Large DOMs can be expensive, but 12 is arbitrary and content-dependent. Virtualization only bounds mounted DOM; it does not automatically bound fetched data or JS memory.
- **13:36–15:23 — First virtualizer attempt.** The goal is to remove offscreen list items while scrolling, expecting image cache reuse. The example’s scroll handlers fail to work reliably, the list flashes, and the presenter says the execution is poor. Browser cache may help on re-entry, but it is not guaranteed; test network, decoded image memory, state preservation, and scroll behavior.
- **15:24–18:30 — Animation, state, closure, and masonry/row mismatch.** The AI review identifies repeated fade-in/stagger animations on remount, state reset when items leave/re-enter, possible captured virtualizer state, and incompatibility between masonry/column layout and row-based offsets. The next plan increases overscan and changes transitions. These are concrete regression modes: use correct geometry, stable keys, cleanup, and no repeated mount animation; test instead of assuming the plan works.
- **18:31–20:25 — Loading stalls and speculative diagnosis.** Scrolling appears stuck after the first section and new content does not load. The presenter speculates about event/virtual-scroll integration and model knowledge. The lesson is to instrument the visible range and continuation trigger, reproduce the stuck point, and verify requests and item indices; speculation does not establish a cause.
- **20:26–22:29 — Responsive overscan and load-ahead idea.** The presenter says each app “needs” virtual scrolling, then qualifies buffer size by screen size and asks to load content shortly before it is visible without long animations. The responsive buffer and prefetch-ahead ideas can be useful for justified virtualization; “every app needs it” is overbroad.
- **23:09–23:42 — Skeleton and grid issues.** A later result reportedly adds skeletons and smoother scrolling, but the grid loads sideways and content geometry remains awkward. Skeletons are helpful only when truthful and stable; they do not fix slow data. Test the actual layout and loading order.
- **23:43–25:32 — Replace masonry/grid behavior.** The presenter requests a normal grid and top-to-bottom loading. A later assistant says it will calculate complete visible rows. Row grouping is correct only if the chosen layout is truly row-based at each breakpoint; masonry needs a compatible virtualizer or a different layout.
- **25:33–26:47 — Visible range and scroll-direction demo.** The presenter reports smooth loading and both downward/upward recycling. This is qualitative; verify fast scroll, slow scroll, resize, filters, focus, and keyboard navigation, not just a single desktop demonstration.
- **26:48–29:00 — DOM inspection and final cleanup reminder.** The presenter watches items enter and leave the DOM and reiterates checking for leaks. Confirm memory and resource lifecycle over repeatable sessions; a low visible node count is not enough to claim the application is performant.

### What the transcript does not establish

It contains no controlled before/after timings, LCP/INP/CLS values, transferred-byte totals, device/network profile, sample size, heap timeline, production traffic, or verified library/configuration. It does not prove that a particular implementation fixed a real app. The exact hard-coded virtualizer cap and the claims that every app needs it, that any scroll observer implies a leak, or that asynchronous code makes CPU work faster are not universal rules. Reproduce and measure the target app.

## References

- [MDN: img element, dimensions, loading, and responsive image selection](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img)
- [MDN: lazy loading](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Lazy_loading)
- [MDN: Intersection Observer unobserve](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/unobserve)
- [MDN: removeEventListener and AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
- [Vue: Performance best practices and large-list virtualization](https://vuejs.org/guide/best-practices/performance.html#virtualize-large-lists)
- [Chrome DevTools: Network reference](https://developer.chrome.com/docs/devtools/network/reference/)
- [Chrome DevTools: Performance reference](https://developer.chrome.com/docs/devtools/performance/reference/)
