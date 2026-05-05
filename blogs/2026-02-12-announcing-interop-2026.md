---
title: "Announcing Interop 2026"
url: "https://webkit.org/blog/17818/announcing-interop-2026/"
date: "Thu, 12 Feb 2026 17:00:59 +0000"
author: ""
feed_url: "https://webkit.org/feed/"
---
<p>Exciting news for web developers, designers, and browser enthusiasts alike — <a href="https://wpt.fyi/interop-2026">Interop 2026</a> is here, continuing the mission of improving cross-browser interoperability. For the fifth year in a row, we are pleased to collaborate with <a href="https://web.dev/blog/interop-2026">Google</a>, <a href="https://igalia.com/news/interop-2026.html">Igalia</a>, <a href="https://blogs.windows.com/msedgedev/2026/02/12/microsoft-edge-and-interop-2026/">Microsoft</a>, and <a href="https://hacks.mozilla.org/2026/02/launching-interop-2026/">Mozilla</a> to make web technology more consistent and reliable across our browsers.</p>
<h3><a name="introducing-interop-2026"></a>Introducing Interop 2026</h3>
<p>Making your website work in every browser can be a challenge, especially if browser engines have implemented the same web technology in slightly different ways. The Interop Project tackles this challenge by bringing the major browser engines together to improve the same set of features during the same year. Each feature is judged on whether or not it fully aligns with its official web standard — the formal technical specifications that define how each web technology should work. This helps accelerate progress toward a more reliable, consistent platform to build on.</p>
<p>Safari has already implemented many of the features included in Interop 2026. In fact, we were the first browser to ship <code>contrast-color()</code>, Media pseudo-classes, <code>shape()</code>, and Scoped Custom Element Registries. Plus, we have support for Anchor Positioning, Style Queries, Custom Highlights, Scroll Snap, View Transitions and much more. We’re excited that these technologies are being included as focus areas in Interop 2026, ensuring they get implemented across all browsers and any remaining interoperability gaps are closed.</p>
<p>We will also be focused on adding support for the following features: advanced <code>attr()</code>, the <code>getAllRecords()</code> method for IndexedDB, WebTransport, and the JavaScript Promise Integration API for Wasm. Together, these four areas make up 20% of the Interop 2026 score. They are exciting new features that solve real needs.</p>
<h3><a name="focus-areas-for-2026"></a>Focus Areas for 2026</h3>
<p>The Interop Project measures interoperability through Web Platform Tests — automated tests that check whether browsers conform to web standards. Interop 2026 is ambitious, covering twenty focus areas. Fifteen are brand new. And five are carryovers from <a href="https://wpt.fyi/interop-2025">Interop 2025</a>.</p>
<ul class="interop-index">
<li><a href="#anchor-positioning">Anchor Positioning</a></li>
<li><a href="#advanced-attr">Advanced <code>attr()</code></a></li>
<li><a href="#container-style-queries">Container Style Queries</a></li>
<li><a href="#contrast-color"><code>contrast-color()</code></a></li>
<li><a href="#css-zoom">CSS Zoom</a></li>
<li><a href="#custom-highlights">Custom Highlights</a></li>
<li><a href="#dialog-and-popover-additions">Dialog and popover additions</a></li>
<li><a href="#fetch-uploads-and-ranges">Fetch Uploads and Ranges</a></li>
<li><a href="#getallrecords-for-indexeddb"><code>getAllRecords()</code> for IndexedDB</a></li>
<li><a href="#jspi-for-wasm">JSPI for Wasm</a></li>
<li><a href="#media-pseudo-classes">Media pseudo-classes</a></li>
<li><a href="#navigation-api">Navigation API</a></li>
<li><a href="#scoped-custom-element-registries">Scoped Custom Element Registries</a></li>
<li><a href="#scroll-driven-animations">Scroll-driven Animations</a></li>
<li><a href="#scroll-snap">Scroll Snap</a></li>
<li><a href="#shape"><code>shape()</code></a></li>
<li><a href="#view-transitions">View Transitions</a></li>
<li><a href="#web-compat">Web Compat</a></li>
<li><a href="#webrtc">WebRTC</a></li>
<li><a href="#webtransport">WebTransport</a></li>
</ul>
<h2><a name="anchor-positioning"></a>Anchor positioning</h2>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Anchor_positioning">Anchor positioning</a> is a carryover from Interop 2025, where significant progress was made to empower developers to position elements relative to each other. This year’s focus will be on clarifying the spec, resolving test issues, and increasing the reliability of this powerful layout feature.</p>
<h2><a name="advanced-attr"></a>Advanced attr()</h2>
<p>The CSS <a href="https://developer.mozilla.org/docs/Web/CSS/attr"><code>attr()</code></a> function lets you bridge the gap between structural data and visual presentation by pulling values directly from HTML attributes into your CSS, making styles more dynamic and context-aware without the overhead of JavaScript. While <code>attr()</code> has long been supported for the <code>content</code> property, advanced <code>attr()</code> extends it to work across all CSS properties with type conversion — letting you use HTML attribute values as colors, lengths, angles, and other data types. Now that security concerns have been worked through in the specification, browser makers are united in our excitement to ship this long-awaited capability with strong interoperability.</p>
<h2><a name="container-style-queries"></a>Container style queries</h2>
<p>Style queries let you apply styles conditionally, based on the value of a custom property (aka, variable) as defined at a certain container. Similar to how Container size queries let your CSS respond to the size of the container, style queries let it respond to theme values, state flags, and other contextual data.</p>
<pre><code class="css"><span class="keyword">@container</span> <span class="keyword">style</span>(<span class="keyword">--theme</span>: <span class="keyword">dark</span>) {
  .<span class="attribute">card</span> {
    <span class="attribute">background</span>: <span class="string">#1a1a1a</span>;
    <span class="attribute">color</span>: <span class="string">#ffffff</span>;
  }
}
</code></pre>
<p>Style queries started shipping in recent years, including in Safari 18.0. Interop 2026 will help ensure this powerful tool works consistently everywhere.</p>
<h2><a name="contrast-color"></a>contrast-color()</h2>
<p>The <a href="https://developer.mozilla.org/docs/Web/CSS/color_value/contrast-color"><code>contrast-color()</code></a> function in CSS returns a color — either black or white. It puts the burden on the browser to choose whichever has higher contrast with the color specified in the function.</p>
<pre><code class="css"><span class="keyword builtin">.button</span> {
  <span class="attribute">background</span>: <span class="identifier">var</span>(<span class="identifier">--brand-color</span>);
  <span class="attribute">color</span>: <span class="identifier">contrast-color</span>(<span class="identifier">var</span>(<span class="identifier">--brand-color</span>));
}
</code></pre>
<p>By having the browser make the choice, you can architect your design system in a simpler fashion. You don’t need to manually define every color pairing. Safari and Firefox both shipped support in 2025, and now Interop 2026 will ensure this powerful function works consistently across all browsers.</p>
<p>Note, <code>contrast-color()</code> does not magically solve all accessibility concerns. Read about all the details in <a href="https://webkit.org/blog/16929/contrast-color/"><em>How to have the browser pick a contrasting color in CSS</em></a>.</p>
<h2><a name="css-zoom"></a>CSS Zoom</h2>
<p>The <a href="https://developer.mozilla.org/docs/Web/CSS/zoom">CSS <code>zoom</code></a> property scales an element and its contents, affecting layout and making the element take up more (or less) space. Unlike <code>transform: scale()</code>, which is purely visual, <code>zoom</code> changes how the element participates in layout.</p>
<pre><code class="css"><span class="keyword builtin">.card</span> {
  <span class="attribute">zoom</span>: <span class="number">1.5</span>; <span class="comment">/* Element is 150% larger and takes up more space */</span>
}
</code></pre>
<p>While <code>zoom</code> was supported in browsers for years as a non-standard property, it’s been plagued by inconsistencies in edge cases and how it interacts with other layout features. Now that it’s standardized, CSS zoom returns as a focus area in Interop 2026, continuing from 2025.</p>
<h2><a name="custom-highlights"></a>Custom Highlights</h2>
<p>The <a href="https://developer.mozilla.org/docs/Web/API/CSS_Custom_Highlight_API">CSS Custom Highlight API</a> lets you style arbitrary text ranges without adding extra elements to the DOM. Using JavaScript, you create a highlight range, then style it with the pseudo-elements.</p>
<p>The <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::highlight"><code>::highlight()</code></a> pseudo-element is perfect for highlighting in-page search results, customizing syntax highlighting in code editors, creating an app that allows collaborative editing with user cursors, or any situation where you need to visually mark text without changing the document structure. The <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::target-text"><code>::target-text</code></a> pseudo-element styles the text that’s scrolled to when a user taps a <a href="https://developer.mozilla.org/en-US/docs/Web/URI/Reference/Fragment/Text_fragments">link with a text fragment</a>.</p>
<p>With implementations progressing across browsers, Interop 2026 ensures these highlighting capabilities work consistently, giving you reliable tools for text-based interactions.</p>
<h2><a name="dialog-and-popover-additions"></a>Dialog and popover additions</h2>
<p>The <a href="https://developer.mozilla.org/docs/Web/HTML/Element/dialog"><code>&lt;dialog&gt;</code></a> element and <a href="https://developer.mozilla.org/docs/Web/API/Popover_API">popover</a> attribute have transformed how developers build overlays on the web. Dialog was part of Interop 2022 and Popover was in Interop 2024. This year, three recent enhancements to these features make up this focus area for Interop 2026.</p>
<p>The <code>closedby</code> attribute lets you control how users can dismiss dialogs:</p>
<pre><code class="html"><span class="tag">&lt;<span class="keyword">dialog</span> <span class="keyword attribute">closedby</span>=<span class="attribute value string">"any"</span>&gt;</span>
<span class="comment">&lt;!-- Can be closed by clicking outside or pressing Escape --&gt;</span>
<span class="tag">&lt;/<span class="keyword">dialog</span>&gt;</span>
</code></pre>
<p>The <code>popover="hint"</code> attribute creates subordinate popovers that don’t dismiss other auto popovers — perfect for tooltips:</p>
<pre><code class="html"><span class="tag">&lt;<span class="keyword">div</span> <span class="keyword attribute">popover</span>=<span class="attribute value string">"hint"</span> <span class="keyword attribute">id</span>=<span class="attribute value string">"tooltip"</span>&gt;</span>
  This tooltip won’t close the menu!
<span class="tag">&lt;/<span class="keyword">div</span>&gt;</span>
</code></pre>
<p>The <code>:open</code> pseudo-class matches elements with open states, working with <code>&lt;dialog&gt;</code>, <code>&lt;details&gt;</code>, and <code>&lt;select&gt;</code>:</p>
<pre><code class="css"><span class="keyword">dialog</span><span class="preprocessor">:open</span> {
  <span class="attribute">animation</span>: <span class="identifier">slideIn</span> <span class="number">0.3s</span>;
}
</code></pre>
<p>Together, these additions make building accessible, user-friendly UI overlays easier than ever.</p>
<h2><a name="fetch-uploads-and-ranges"></a>Fetch uploads and ranges</h2>
<p>The <a href="https://developer.mozilla.org/docs/Web/API/Fetch_API"><code>fetch()</code></a> method is getting three new powerful capabilities for handling uploads and partial content.</p>
<p>ReadableStream request bodies enable true streaming uploads, letting you upload large files or real-time data without loading everything into memory first:</p>
<pre><code class="js"><span class="identifier">await</span> <span class="identifier">fetch</span>(<span class="char">'/upload'</span>, {
  <span class="identifier">method</span><span class="operator">:</span> <span class="char">'POST'</span>,
  <span class="identifier">body</span><span class="operator">:</span> <span class="identifier">readableStream</span>,
  <span class="identifier">duplex</span><span class="operator">:</span> <span class="char">'half'</span>
});
</code></pre>
<p>Enhanced <a href="https://developer.mozilla.org/en-US/docs/Web/API/FormData">FormData</a> support improves multipart uploads and responses.</p>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Range">Range header</a> support allows partial content requests, essential for video streaming and resumable downloads:</p>
<pre><code class="js"><span class="identifier">fetch</span>(<span class="char">'/video.mp4'</span>, {
  <span class="identifier">headers</span><span class="operator">:</span> { <span class="char">'Range'</span><span class="operator">:</span> <span class="char">'bytes=0-1023'</span> }
});
</code></pre>
<p>These enhancements bring <code>fetch()</code> up to par with more specialized APIs, reducing the need for custom solutions.</p>
<h2><a name="getallrecords-for-indexeddb"></a>getAllRecords() for IndexedDB</h2>
<p><a href="https://developer.mozilla.org/docs/Web/API/IndexedDB_API">IndexedDB</a> is a low-level API that lets you store large amounts of structured data in the browser, including files and blobs. It’s been supported in browsers for <a href="https://caniuse.com/?search=indexdb">many years</a>.</p>
<p>Now, IndexedDB is getting a significant performance boost with the new <a href="https://developer.mozilla.org/docs/Web/API/IDBObjectStore/getAllRecords"><code>getAllRecords()</code></a> methods for <code>IDBObjectStore</code> and <code>IDBIndex</code>. These methods allow you to retrieve records in batches and in reverse order:</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">records</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">objectStore</span>.<span class="identifier">getAllRecords</span>({
  <span class="identifier">query</span><span class="operator">:</span> <span class="identifier">IDBKeyRange</span>.<span class="identifier">bound</span>(<span class="char">'A'</span>, <span class="char">'M'</span>),
  <span class="identifier">count</span><span class="operator">:</span> <span class="number">100</span>,
  <span class="identifier">direction</span><span class="operator">:</span> <span class="char">'prev'</span>
});
</code></pre>
<p>It’s just this new method that’s being included in Interop 2026. The score only reports the percentage of <code>getAllRecords()</code> tests that are passing  — not all IndexDB tests.</p>
<h2><a name="jspi-for-wasm"></a>JSPI for Wasm</h2>
<p><a href="https://webassembly.org/">WebAssembly</a> has opened the door for running high-performance applications in the browser — games, productivity tools, scientific simulations, and more. But there’s been a fundamental mismatch. Many of these applications were originally written for environments where operations like file I/O or network requests are synchronous (blocking), while the web is fundamentally asynchronous.</p>
<p>The <a href="https://v8.dev/blog/jspi">JavaScript Promise Integration API (JSPI)</a> bridges this gap. It lets WebAssembly code that expects synchronous operations work smoothly with JavaScript’s Promise-based async APIs, without requiring you to rewrite the entire application. This means you can port existing C, C++, or Rust applications to the web more easily, unlocking a wider range of software that can run in the browser.</p>
<p>Interop 2026 will ensure JSPI works consistently across browsers, making WebAssembly a more viable platform for complex applications.</p>
<h2><a name="media-pseudo-classes"></a>Media pseudo-classes</h2>
<p>We’ve proposed media pseudo-classes for inclusion in the Interop Project for many years in a row. We are excited that it’s being included this year!</p>
<p>Seven CSS pseudo-classes let you apply CSS based on the playback state of <code>&lt;audio&gt;</code> and <code>&lt;video&gt;</code> elements:</p>
<ul>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:playing"><code>:playing</code></a> — media is currently playing</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:paused"><code>:paused</code></a> — media is paused</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:seeking"><code>:seeking</code></a> — user is seeking to a new position</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:buffering"><code>:buffering</code></a> — media is buffering</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:stalled"><code>:stalled</code></a> — playback has stalled</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:muted"><code>:muted</code></a> — audio is muted</li>
<li><a href="https://developer.mozilla.org/docs/Web/CSS/:volume-locked"><code>:volume-locked</code></a> — volume cannot be changed</li>
</ul>
<p>These all shipped in Safari many years ago, but without support in any other browser, most developers don’t use them — or even know they exist. Instead developers need JavaScript to sync UI state with media playback state.</p>
<p>It’s far simpler and more efficient to use media state pseudo-classes in CSS.</p>
<pre><code class="css"><span class="keyword">video</span><span class="preprocessor">:buffering</span>::<span class="keyword">after</span> {
  <span class="attribute">content</span>: <span class="string">"Loading..."</span>;
}
<span class="keyword">audio</span><span class="preprocessor">:muted</span> {
  <span class="attribute">opacity</span>: <span class="number">0.5</span>;
}
</code></pre>
<p>They are especially powerful combined with <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:has"><code>:has()</code></a>, since it unlocks the ability to style anything on the page based on playback state, not just elements that are descendants of the media player.</p>
<pre><code class="css"><span class="keyword">article</span><span class="preprocessor">:has</span>(<span class="keyword">video</span><span class="preprocessor">:playing</span>) {
  <span class="attribute">background-color</span>: <span class="identifier">var</span>(<span class="identifier">--backgroundColor</span>); 
  <span class="attribute">color</span>: <span class="identifier">contrast-color</span>(<span class="identifier">var</span>(<span class="identifier">--backgroundColor</span>));
  <span class="attribute">transition</span>: <span class="identifier">background-color</span> <span class="number">0.5s</span> <span class="identifier">ease</span>;
}
</code></pre>
<p>Learn more about the power of <code>:has()</code> in <em><a href="https://webkit.org/blog/13096/css-has-pseudo-class/">Using :has() as a CSS Parent Selector and much more</a></em>.</p>
<h2><a name="navigation-api"></a>Navigation API</h2>
<p>If you’ve built single-page applications, you may have experienced the pain of managing navigation state with <code>history.pushState()</code> and <code>popstate</code> events. <a href="https://developer.mozilla.org/docs/Web/API/Navigation_API">Navigation API</a> gives you a cleaner, more powerful way to intercept and control navigation.</p>
<p>This focus area is a continuation of Interop 2025, where significant progress was made to empower developers to initiate, intercept, and modify browser navigation actions. This year continues work on interoperability, to get the overall score up from the 92.3% test pass result during Interop 2025. Plus, there’s one new feature being added — the <a href="https://developer.mozilla.org/en-US/docs/Web/API/NavigationPrecommitController"><code>precommitHandler</code></a> option. It lets you defer navigation until critical resources are ready, preventing jarring flashes of incomplete content.</p>
<pre><code class="js"><span class="identifier">navigation</span>.<span class="identifier">addEventListener</span>(<span class="char">'navigate'</span>, (<span class="identifier">e</span>) <span class="operator">=</span><span class="operator">&gt;</span> {
  <span class="identifier">e</span>.<span class="identifier">intercept</span>({
    <span class="identifier">async</span> <span class="identifier">precommitHandler</span>() {
      <span class="comment">// Load critical resources before commit
</span>      <span class="identifier">await</span> <span class="identifier">loadCriticalData</span>();
    },
    <span class="identifier">async</span> <span class="identifier">handler</span>() {
      <span class="comment">// Render the new view
</span>      <span class="identifier">renderPage</span>();
    }
  });
});
</code></pre>
<p>Interop 2026 will ensure Navigation API works reliably across browsers, a solid foundation for web applications.</p>
<h2><a name="scoped-custom-element-registries"></a>Scoped custom element registries</h2>
<p>Working with web components, you may have run into a frustrating limitation: the global <code>customElements</code> registry only allows one definition per tag name across your entire application. When two different libraries both define a <code>&lt;my-button&gt;</code> component, they conflict.</p>
<p>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/CustomElementRegistry"><code>CustomElementRegistry()</code></a> constructor solves this by letting you create scoped registries. Different parts of your application — or different shadow roots — can have their own definitions for the same tag name.</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">registry</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">CustomElementRegistry</span>();
<span class="identifier">registry</span>.<span class="identifier">define</span>(<span class="char">'my-button'</span>, <span class="identifier">MyButtonV2</span>);
<span class="identifier">shadowRoot</span>.<span class="identifier">registry</span> <span class="operator">=</span> <span class="identifier">registry</span>;
</code></pre>
<p>This is especially valuable for microfrontends, component libraries, and any situation where you’re integrating third-party web components.</p>
<p>Safari 26.0 was the first <a href="https://caniuse.com/wf-scoped-custom-element-registries">browser to ship</a> Scoped custom element registries. Inclusion in Interop 2026 will help ensure this capability works consistently across all browsers.</p>
<h2><a name="scroll-driven-animations"></a>Scroll-driven Animations</h2>
<p><a href="https://developer.mozilla.org/docs/Web/CSS/CSS_scroll-driven_animations">Scroll-driven animations</a> let you more easily create animations that respond to scroll position, now entirely in CSS. As a user scrolls, the animation progresses — no JavaScript needed. You can build scroll-triggered reveals, progress indicators, parallax effects, and interactive storytelling experiences.</p>
<p>Define animations with standard CSS keyframes, then connect them to scroll using <code>animation-timeline</code>:</p>
<pre><code class="css"><span class="keyword builtin">.reveal</span> {
  <span class="attribute">animation</span>: <span class="identifier">fade-in</span> <span class="identifier">linear</span> <span class="identifier">forwards</span>;
  <span class="attribute">animation-timeline</span>: <span class="identifier">view</span>();
  <span class="attribute">animation-range</span>: <span class="identifier">entry</span> <span class="number">0%</span> <span class="identifier">entry</span> <span class="number">100%</span>;
}

<span class="keyword">@keyframes</span> <span class="keyword">fade-in</span> {
  <span class="attribute">from</span> { <span class="attribute">opacity</span>: <span class="number">0</span>; }
  <span class="keyword">to</span> { <span class="attribute">opacity</span>: <span class="number">1</span>; }
}
</code></pre>
<p>Use <code>view()</code> to trigger animations as elements enter and exit the viewport, or <code>scroll()</code> to tie animations to a scrolling container’s position. Learn much more in <a href="https://webkit.org/blog/17101/a-guide-to-scroll-driven-animations-with-just-css/"><em>A guide to Scroll-driven Animations with just CSS</em></a><em>.</em></p>
<p>We shipped support for scroll-driven animations in Safari 26.0. Interop 2026 will help ensure this feature works consistently across all browsers.</p>
<h2><a name="scroll-snap"></a>Scroll Snap</h2>
<p><a href="https://developer.mozilla.org/docs/Web/CSS/CSS_scroll_snap">CSS Scroll Snap</a> controls the panning and scrolling behavior within a scroll container, creating carousel-like experiences:</p>
<pre><code class="css"><span class="keyword builtin">.carousel</span> {
  <span class="attribute">scroll-snap-type</span>: <span class="identifier">x</span> <span class="identifier">mandatory</span>;
  <span class="attribute">overflow-x</span>: <span class="identifier">scroll</span>;
}
<span class="keyword builtin">.carousel</span> &gt; * {
  <span class="attribute">scroll-snap-align</span>: <span class="identifier">center</span>;
}
</code></pre>
<p>Scroll Snap has been <a href="https://caniuse.com/css-snappoints">supported</a> in all modern browsers for many years. But like many of the older CSS specifications, multiple rounds of changes to the specification while early versions were already shipping in browsers created a deep lack of interoperability. With a far more mature web standard, it’s time to circle back and improve interoperability. This is the power of the Interop Project — focusing all the browser teams on a particular feature, and using automated tests to find inconsistencies and disagreements.</p>
<h2><a name="shape"></a>shape()</h2>
<p>For years, when you wanted to create a complex clipping path to use with <code>clip-path</code> or <code>shape-outside</code> you’ve been limited to <code>polygon()</code>, which only supports straight lines, or SVG paths, which aren’t responsive to element size changes.</p>
<p>Now, the <a href="https://developer.mozilla.org/docs/Web/CSS/basic-shape/shape"><code>shape()</code></a> function lets you create complex shapes with path-like commands (<code>move</code>, <code>line</code>, <code>curve</code>). It gives you the best of both worlds — curves like SVG paths, but with percentage-based coordinates that adapt as elements resize.</p>
<pre><code class="css"><span class="keyword builtin">.element</span> {
  <span class="attribute">clip-path</span>: <span class="identifier">shape</span>(
    <span class="identifier">from</span> <span class="number">0%</span> <span class="number">0%</span>,
    <span class="identifier">line</span> <span class="identifier">to</span> <span class="number">100%</span> <span class="number">0%</span>,
    <span class="identifier">line</span> <span class="identifier">to</span> <span class="number">100%</span> <span class="number">100%</span>,
    <span class="identifier">curve</span> <span class="identifier">to</span> <span class="number">0%</span> <span class="number">100%</span> <span class="identifier">via</span> <span class="number">50%</span> <span class="number">150%</span>,
    <span class="identifier">close</span>
  );
}
</code></pre>
<p>We shipped support for the <code>shape()</code> function in Safari 18.4. And we look forward to Interop 2026 improving browser implementations so you can confidently use it to render of complex, responsive curves.</p>
<h2><a name="view-transitions"></a>View transitions</h2>
<p><a href="https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API">View Transitions</a> was a focus area in Interop 2025, narrowly defined to include <a href="https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API">same-document view transitions</a> and <code>view-transition-class</code>. These features allow for smooth, animated transitions between UI states within a single page, as well as flexible control over styling those transitions.</p>
<p>While Safari finished Interop 2025 with a score of 99.2% for view transitions, the overall interoperability score is at 90.8% — so the group decided to continue the effort, carrying over the tests from 2025.</p>
<p>For Interop 2026, the focus area expands to also include <a href="https://webkit.org/blog/16967/two-lines-of-cross-document-view-transitions-code-you-can-use-on-every-website-today/">cross-document view transitions</a>. This allows you to create smooth, animated transitions in the moments between pages as users navigate your site, rather than an abrupt jump when new page loads. Cross-document view transitions shipped in Safari 18.2. Learn more about it in <a href="https://webkit.org/blog/16967/two-lines-of-cross-document-view-transitions-code-you-can-use-on-every-website-today/"><em>Two lines of Cross-Document View Transitions code you can use on every website today</em></a>.</p>
<h2><a name="web-compat"></a>Web Compat</h2>
<p>Web compatibility refers to whether or not a real world website works correctly in a particular browser. When a site works in one browser, but not another — that’s a “compat” problem. This focus area is made up of a small collection of Web Platform Tests selected because the fact they fail in some browsers causes real websites to not work <em>in other browsers</em> — thus creating problems for both web developers and users.</p>
<p>Each time Web Compat has been a focus area as part of the Interop Project, it’s targeted a different set of compat challenges. This year, Interop 2026’s web compatibility work includes:</p>
<ul>
<li><a href="https://tc39.es/ecma262/#cyclic-module-record">ESM module loading</a>, ensuring cyclic module records and multiple top-level awaits work consistently.</li>
<li><a href="https://html.spec.whatwg.org/#event-loop-processing-model">Timing of scroll events relative to animation events</a>, used to make sure scroll and animation events fire in a predictable, interoperable order.</li>
<li>Support for <a href="https://developer.mozilla.org/docs/Web/CSS/user-select"><code>user-select</code></a>, rather than just <code>-webkit-user-select</code>. It controls whether users can select text. </li>
</ul>
<h2><a name="webrtc"></a>WebRTC</h2>
<p><a href="https://developer.mozilla.org/docs/Web/API/WebRTC_API">WebRTC</a> (Web Real-Time Communication) enables real-time audio, video, and data communication directly between browsers, without requiring plugins or intermediate servers. You can build video conferencing apps, live streaming platforms, peer-to-peer file sharing, and collaborative tools.</p>
<p>Having reached a 91.6% pass rate, WebRTC continues as a focus area in 2026, building on the progress made during Interop 2025. We’re looking forward to fixing the long tail of interop issues of the main spec for WebRTC.</p>
<h2><a name="webtransport"></a>WebTransport</h2>
<p><a href="https://developer.mozilla.org/docs/Web/API/WebTransport_API">WebTransport</a> provides a modern way to transmit data between client and server using the HTTP/3 protocol. It gives you low-latency bidirectional communication with multiple streams over a single connection. You get both unreliable datagram support (like UDP) for speed and reliable stream support (like TCP) for guaranteed delivery.</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">transport</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">WebTransport</span>(<span class="char">'https://example.com/endpoint'</span>);
<span class="identifier">await</span> <span class="identifier">transport</span>.<span class="identifier">ready</span>;
<span class="keyword type">const</span> <span class="identifier">stream</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">transport</span>.<span class="identifier">createBidirectionalStream</span>();
<span class="comment">// Stream data efficiently
</span></code></pre>
<p>WebTransport is ideal for gaming, real-time collaboration tools, and applications where you need more control than WebSocket provides but don’t want to manage WebRTC’s complexity. Being part of Interop 2026 ensures WebTransport works consistently across all browsers, making it a reliable choice for real-time data transmission.</p>
<h2><a name="investigation-efforts-a-look-ahead"></a>Investigation Efforts: A Look Ahead</h2>
<p>In addition to the focus areas, the Interop Project includes four investigation areas. These are projects where teams gather to assess the current state of testing infrastructure and sort through issues that are blocking progress.</p>
<h3><a name="accessibility-testing"></a>Accessibility testing</h3>
<p>Continuing from previous years, the Accessibility Testing investigation aims to work towards generating consistent accessibility trees across browsers. This effort will improve the WPT testing infrastructure for accessibility on top of the foundation from Interop 2024. This work ensures that accessibility features are reliable and consistent, helping developers create more inclusive web experiences.</p>
<h3><a name="jpeg-xl"></a>JPEG XL</h3>
<p><a href="https://jpegxl.info/">JPEG XL</a> is a next-generation raster graphics format that supports animation, alpha transparency, and lossy as well as lossless compression. We shipped support for it in Safari 17.0. This investigation will focus on making the feature properly testable by developing comprehensive test suites, opening up the possibility that JPEG XL could be a focus area in the future.</p>
<h3><a name="mobile-testing"></a>Mobile testing</h3>
<p>The Mobile Testing investigation continues work started in 2025. This year, we will focus on improving infrastructure for mobile-specific features like dynamic viewport changes which are crucial for building responsive mobile web experience that billions of users rely on every day.</p>
<h3><a name="webvtt"></a>WebVTT</h3>
<p>Continuing from 2025, the WebVTT investigation addresses a critical challenge facing the web platform. Developers cite WebVTT’s inconsistent behavior across browsers as a major reason for choosing other subtitling and captioning solutions. Our investment in WebVTT last year primarily consisted of validating and fixing the existing test suite, as well as making any necessary spec changes along the way.  We are excited to continue that effort this year to ensure synchronized text tracks and closed captioning work seamlessly across the web.</p>
<h2><a name="a-more-interoperable-web"></a>A more interoperable web</h2>
<p>Interop 2026 brings together twenty focus areas that matter to you as a web developer. Some, like <code>attr()</code> and <code>contrast-color()</code>, give you more flexible ways to architect your CSS. Others, like Scroll-Driven Animations and View Transitions, let you create smoother, more engaging experiences without reaching for JavaScript. Features like WebTransport and the Navigation API give you more powerful tools for building modern web applications.</p>
<p>Just as important are the focus areas working to fix long-standing inconsistencies — ensuring Scroll Snap works reliably, bringing all browsers up to speed on <code>shape()</code>, and solving real-world compatibility problems that have been frustrating developers and breaking sites.</p>
<p>The WebKit team is committed to making these features work consistently across all browsers. Whether you’re building a design system, a single-page application, a video streaming platform, or anything in between, Interop 2026 is working to give you a more reliable foundation to build on.</p>
<p>Here’s to another year of making the web better, together!</p>
