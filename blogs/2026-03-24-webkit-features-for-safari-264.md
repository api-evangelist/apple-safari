---
title: "WebKit Features for Safari 26.4"
url: "https://webkit.org/blog/17862/webkit-features-for-safari-26-4/"
date: "Tue, 24 Mar 2026 17:00:30 +0000"
author: ""
feed_url: "https://webkit.org/feed/"
---
<p>March has a way of bringing a lot of new things to WebKit — and this year is no exception. With 44 features, 191 fixes and one deprecation, Safari 26.4 is a release packed with web technology.</p>
<p>What’s most exciting? CSS Grid Lanes brings masonry-style layouts to the web platform — a long-awaited solution for building rich visual galleries and much more. WebTransport provides a modern alternative to WebSocket, opening the door to low-latency experiences like multiplayer games, live collaboration tools, and improved video conferencing. And Keyboard Lock API gives web apps better control over keyboard shortcuts.</p>
<p>Beyond the headliners, the heart of this release is focused on what web developers ask for most. We hear you loud and clear. Results from 2025 developer surveys made it clear you want time to catch up with new features, not be swamped with more. You want existing features to work consistently across every browser. You asked for browser engineers working on WebKit to help you by squashing bugs and closing gaps in spec coverage. That’s what this release aims to do.</p>
<p>Most of the features listed in the <a href="https://developer.apple.com/documentation/safari-release-notes/safari-26_4-release-notes">Safari 26.4 release notes</a> are not entirely new. Many update features where the behavior didn’t quite match the latest web standard. Others make specific combinations of existing features work better together. Here’s one example — we shipped support for the CSS <code>min()</code> and <code>max()</code> functions in 2018, almost two years before any other browser. And we shipped the HTML <code>sizes</code> attribute for responsive images even longer ago, back in 2014. But until now, you couldn’t use <code>min()</code>, <code>max()</code>, or <code>clamp()</code> inside of the <code>sizes</code> attribute in WebKit. In Safari 26.4, you can.</p>
<p>And then there are the bug fixes — hundreds of them across the platform. WebKit engineers went deep to improve specific areas like SVG, Tables, MathML, and CSS Zoom. And we’re continuing our multi-year rewrite of the layout engine. Blocks-in-inline layout is complete in Safari 26.4, work on Flexbox continues, and we’ve now begun rewriting CSS Grid.</p>
<p>As we continue this work, we greatly value your input. If something has been bothering you, it’s worth testing in Safari 26.4 to see if it’s been fixed. If the bug is still there, please file it at <a href="https://bugs.webkit.org/">bugs.webkit.org</a>. Or if it’s already filed, add additional comments to the existing issue describing your experience and why fixing it matters for you. When multiple websites signal that something needs fixing, that helps. The more concrete you can be — a brief story about why this hurts your users, a link to a real website affected, a snippet of code or reduced test case — the better equipped we are to prioritize and fix what matters most. We are paying attention, even if our response shows up as a shipped fix rather than a reply in the issue.</p>
<p>We care deeply about the experience people have when using Safari. And we care about the experience people have when using any of the millions of iOS, iPadOS, macOS, visionOS, and watchOS apps that are built using WebKit and JavaScriptCore. When our customers open a news app, a shopping app, a travel app, a banking app — there’s a good chance the interface they’re interacting with is powered by the same HTML, CSS, and JavaScript you write every day when making web apps and websites that live at a URL. Every rendering fix, every improved feature, every performance gain we ship benefits everything touched by the web platform.</p>
<p>We are passionate about making experiences our customers love, no matter how they use their device. Web designers and developers are central to those experiences. You are our partners. We truly hope this release makes a real difference in your success.</p>
<h2><a name="css"></a>CSS</h2>
<h3><a name="grid-lanes"></a>Grid Lanes</h3>
<figure class=""><source media="(prefers-color-scheme: dark)" type="image/png" /><img alt="Safari window showing photo gallery laid out with Grid Lanes, alternating narrow and wide columns, with photos of all sorts of aspect ratios neatly aligned in columns" class="aligncenter size-full wp-image-17877" height="1330" src="https://webkit.org/wp-content/uploads/gridlanes-for264-light.webp" width="2000" /></figure>
<p>Safari 26.4 adds support for <a href="https://webkit.org/blog/17660/introducing-css-grid-lanes/">Grid Lanes</a>. It’s a new layout system that extends CSS Grid with powerful capabilities for creating flexible, flowing layouts. You might be familiar with the patterns it can create. Often called “masonry” or “waterfall” layouts, they were made popular like sites like Pinterest and attainable with Javascript libraries like <a href="https://masonry.desandro.com/">masonry.js</a>. Now this capability is available in CSS with  <code>display: grid-lanes</code>.</p>
<p>And it can do much more than just the classic layout. At its root, Grid Lanes provides a way to pack content of different aspect ratios into either columns or rows. And does so in a way where users can tab through all the visible content, and where new content can be lazy-loaded at the end.</p>
<p>Grid Lanes builds on the foundation of CSS Grid, giving it powerful track sizing and explicit placement capabilities.</p>
<pre><code class="css"><span class="keyword builtin">.container</span> {
  <span class="attribute">display</span>: <span class="identifier">grid-lanes</span>;
  <span class="attribute">grid-template-columns</span>: <span class="identifier">repeat</span>(<span class="identifier">auto-fill</span>, <span class="identifier">minmax</span>(<span class="number">200px</span>, <span class="number">1</span><span class="identifier">fr</span>));
}
</code></pre>
<p>Safari 26.4 supports the recently-finalized core syntax for Grid Lanes (see <a href="https://webkit.org/blog/17660/introducing-css-grid-lanes/"><em>Introducing CSS Grid Lanes</em></a>), including support for <code>flow-tolerance</code>, which gives you control over how aggressively each item tries to “change lanes” to be closest to the start. This affects how much the placement of consecutive items shifts back and forth across the page — a particularly important consideration for accessibility. Try tuning the value, and see how it affects item placement and keyboard navigation across items.</p>
<p>Grid Lanes opens up new possibilities for layouts that have been difficult to achieve with existing CSS. In addition to the Pinterest-style masonry layouts, you can use it to create dynamic arrangements of content in either columns or rows. Check out our <a href="https://webkit.org/demos/grid3/">Grid Lanes demos</a> for more ideas. Learn about browser support &amp; progressive enhancement strategies in <a href="https://webkit.org/blog/17758/when-will-css-grid-lanes-arrive-how-long-until-we-can-use-it/"><em>When will CSS Grid Lanes arrive? How long until we can use it?</em></a></p>
<p>We also added support for Grid Lanes to Web Inspector.</p>
<figure class=""><source media="(prefers-color-scheme: dark)" type="image/png" /><img alt="Same example of Grid Lanes layout, a gallery of photos. This time, with the Web Inspector open to the Grid layout tooling, with item numbers marked on the screen." class="aligncenter size-full wp-image-17880" height="1505" src="https://webkit.org/wp-content/uploads/gridlanes-inspector-light-scaled.webp" width="2560" /></figure>
<p>The Grid Inspector now supports CSS Grid Lanes with order number overlays that show the placement sequence of grid items. You can toggle order number visibility in the settings and visualize gaps between items arranged by Grid Lanes. Auto-completion for <code>grid-lanes</code> and <code>inline-grid-lanes</code> values in the <code>display</code> property makes it easier to experiment with these new layout options. Learn more in <a href="https://webkit.org/blog/17746/new-safari-developer-tools-provide-insight-into-css-grid-lanes/"><em>New Safari developer tools provide insight into CSS Grid Lanes</em></a>.</p>
<h3><a name="name-only-container-queries"></a>Name-Only Container Queries</h3>
<p>Safari 26.4 adds support for name-only <code>@container</code> queries, allowing you to target named containers without specifying any size conditions. Previously, container queries required both a container name and a condition — like <code>@container sidebar (min-width: 300px)</code>. Now you can query just the container name:</p>
<pre><code class="css"><span class="keyword">@container</span> <span class="keyword">sidebar</span> {
  .<span class="attribute">card</span> {
    <span class="attribute">padding</span>: <span class="number">1</span><span class="identifier">rem</span>;
  }
}
</code></pre>
<p>This is useful when you want to apply styles based on which container an element is inside, regardless of that container’s size. It’s particularly handy for component variants or when you’re using container queries more for scoping styles than for responsive behavior. You still define the container name the same way:</p>
<pre><code class="css"><span class="keyword builtin">.sidebar</span> {
  <span class="attribute">container-name</span>: <span class="identifier">sidebar</span>;
  <span class="attribute">container-type</span>: <span class="identifier">inline-size</span>;
}
</code></pre>
<p>Now you can target elements inside that container without worrying about size breakpoints, giving you more flexibility in how you structure your component styles.</p>
<h3><a name="custom-cursors-on-marker"></a>Custom Cursors on ::marker</h3>
<p>Safari 26.4 adds support for the <code>cursor</code> property on the <code>::marker</code> pseudo-element, letting you customize pointer behavior for list markers.</p>
<pre><code class="css"><span class="keyword">li</span>::<span class="keyword">marker</span> {
  <span class="attribute">cursor</span>: <span class="identifier">pointer</span>;
}
</code></pre>
<p>This is one step toward making <code>::marker</code> more flexible.</p>
<h3><a name="math-typography"></a>Math Typography</h3>
<p>Safari 26.4 adds several improvements for mathematical typography, making it easier to display and style mathematical notation on the web.</p>
<p>The <code>math-depth</code> property gives you control over the sizing of nested mathematical expressions. In complex formulas with fractions, superscripts, and subscripts, <code>math-depth</code> automatically scales nested elements appropriately, ensuring readability while maintaining proper mathematical hierarchy.</p>
<p>Safari 26.4 also adds support for <code>font-size: math</code>, which applies proper scaling logic for mathematical content. This works together with <code>math-depth</code> to ensure formulas render at the right size relative to surrounding text.</p>
<p class="codepen" style="height: 640px; display: flex; border: 2px solid; margin: 1em 0; padding: 1em;">
<p></p>
<p>For layout performance, you can now use CSS size containment with MathML elements via <code>contain-intrinsic-inline-size</code> and <code>contain-intrinsic-block-size</code>. This helps the browser optimize rendering of complex mathematical expressions, particularly when they’re off-screen or being dynamically loaded.</p>
<p>Finally, <code>math-style</code> and <code>math-shift</code> now animate as discrete values, allowing you to create transitions between different mathematical presentation styles.</p>
<p>These additions make MathML more powerful and performant, particularly for educational content, scientific publications, and any site that needs to display mathematical notation.</p>
<p>Along with these new features, a number of  MathML bugs were fixed:</p>
<ul>
<li>Fixed default MathML rule thickness to use the font’s <code>underlineThickness</code> metric with a zero fallback. (164693673)</li>
<li>Fixed <code>mpadded</code> elements in RTL (<code>dir="rtl"</code>) to respect <code>lspace</code>. (164740784)</li>
<li>Fixed an issue where empty <code>&lt;msqrt&gt;</code> radical operators in MathML were not painted correctly. (164776629)</li>
<li>Fixed MathML <code>&lt;mpadded&gt;</code>, <code>&lt;mfrac&gt;</code>, <code>&lt;munderover&gt;</code>, <code>&lt;mover&gt;</code> and <code>&lt;mspace&gt;</code> elements not updating layout when attributes like <code>width</code>, <code>height</code>, <code>depth</code>, <code>lspace</code>, and <code>voffset</code> etc. changed. (164797996)</li>
<li>Fixed MathML boolean attributes so they are now compared ASCII case-insensitively. (164819048)</li>
<li>Fixed incorrect positioning of <code>mpadded</code> content in right-to-left mode. (166045517)</li>
<li>Fixed an issue where <code>&lt;msqrt&gt;</code> or <code>&lt;mroot&gt;</code> elements did not update their radical operators when children were dynamically added or removed. (166556627)</li>
<li>Fixed <code>&lt;mpadded&gt;</code> so that percentage values for <code>width</code>, <code>height</code>, and <code>depth</code> attributes are treated as absent and use content dimensions as defaults, matching the MathML Core specification. (167350169)</li>
</ul>
<h3><a name="zoom"></a>Zoom</h3>
<p>Safari 26.4 includes a significant set of CSS Zoom fixes. The <code>zoom</code> property in CSS scales an element and its contents. While <code>transform: scale()</code> does something similar, <code>zoom</code> is handy because it affects layout, causing surrounding content to respond to the change in size.</p>
<p>CSS <code>zoom</code> is separate from browser zoom, (the kind triggered by ⌘+ and ⌘−), but the two can compound. An element with <code>zoom: 2</code> on a page that’s been zoomed in to 150% gets scaled by both factors. Getting everything to calculate correctly in that situation is genuinely tricky, and a lot of the fixes in this release are about getting that right. Properties like <code>width</code>, <code>height</code>, <code>margin</code>, and positional values now correctly apply zoom at used-value time. CSS <code>calc()</code> expressions correctly account for the zoom factor. And <code>getBoundingClientRect()</code> and <code>getClientRects()</code> in JavaScript now return properly scaled values.</p>
<p>Here’s the full list:</p>
<ul>
<li>Fixed <code>width</code>, <code>height</code>, <code>min-width</code>, <code>min-height</code>, <code>max-width</code> and <code>max-height</code> to apply CSS zoom at used-value time. (161848512)</li>
<li>Fixed CSS zoom to scale <code>&lt;iframe&gt;</code> element contents. (162314059)</li>
<li>Fixed <code>getBoundingClientRect</code> and <code>getClientRects</code> to return scaled lengths according to CSS zoom instead of unscaled values, aligning with the CSS Viewport specification. (162325730)</li>
<li>Fixed <code>top</code>, <code>left</code>, <code>right</code>, and <code>bottom</code> to apply CSS zoom at used-value time (162663056)</li>
<li>Fixed <code>margin</code> to apply CSS zoom at used-value time. (162907254)</li>
<li>Fixed evaluation of <code>calc()</code> expressions to correctly apply the used <code>zoom</code> factor to length values, ensuring properties like <code>line-height</code> and box dimensions scale properly. (163141549)</li>
<li>Fixed an issue where <code>calc(em)</code> values for unzoomed properties were incorrectly adjusted. (163267333)</li>
<li>Fixed an issue where <code>calc()</code> incorrectly treated margins as present. (163605539)</li>
<li>Fixed <code>devicePixelRatio</code> so that page zoom now affects the main frame consistently with iframes, keeping their values synchronized. (163857955)</li>
<li>Fixed <code>line-height</code> to correctly scale font-relative units when text zoom is applied. (165073337)</li>
<li>Fixed performance and correctness issues with inheritance in the modern CSS Zoom implementation. (167715972)</li>
<li>Fixed an issue where <code>&lt;video&gt;</code> poster images were incorrectly double-scaled when <code>zoom</code> was applied by using the cached intrinsic poster size without reapplying zoom. (150976146)</li>
</ul>
<h3><a name="threaded-scroll-driven-animations"></a>Threaded Scroll-driven Animations</h3>
<p>Safari 26.4 adds support for threaded Scroll-driven Animations. Now, the animations driven by scroll position run on the compositor thread, separate from the main thread. You don’t need do anything to get this benefit. When you use <code>animation-timeline: scroll()</code> or <code>animation-timeline: view()</code>, you automatically get the same kind of performance benefit that CSS transitions and keyframe animations have long enjoyed. Your scroll-driven animations will stay smooth even when the main thread is busy.</p>
<p>It also includes the following update:</p>
<ul>
<li>Fixed incorrect overlap calculations for transform animations including <code>translate</code>, <code>scale</code>, and <code>rotate</code> properties. (88383253)</li>
</ul>
<h3><a name="positioning"></a>Positioning</h3>
<p>Safari 26.4 includes many refinements for Anchor Positioning. It updates absolutely positioned boxes in scrollable containing blocks to allow alignment overflow in scrollable directions, in accordance with a recent CSS spec change. And it folds several more fixes to positioning:</p>
<ul>
<li>Fixed an infinite style resolution loop when a <code>position-try</code> box was inside a <code>display: none</code> subtree. (161570947)</li>
<li>Fixed <code>position-area</code> normal alignment to align toward the non-auto inset when only one inset is auto, in accordance with recent CSS spec changes. (163317238)</li>
<li>Fixed an issue where fixed-positioned boxes using <code>position-area</code> were incorrectly included in the root scrollable containing block, ensuring they position correctly while still allowing overflow when appropriate. (163955483)</li>
<li>Fixed an issue where <code>padding-inline-end</code> was not included in the scrollable overflow for block containers. (170503510)</li>
<li>Fixed an issue where <code>position-area</code> for elements in scrollable containers only used the initial scrollport bounds instead of the entire scrollable area. (170503694)</li>
<li>Fixed an issue where absolutely-positioned elements inside inline containers did not correctly account for the margin of a preceding block when determining their static position. (170934098)</li>
<li>Fixed incorrect width calculation for <code>positioned</code> elements using <code>box-sizing: border-box</code> with an <code>aspect-ratio</code>, ensuring borders and padding are not double-counted. (121500004)</li>
<li>Fixed <code>getComputedStyle("top")</code> to correctly resolve percentage values for absolutely positioned elements inside inline containers. (161390162)</li>
<li>Fixed an issue where CSS <code>@starting-style</code> entry animations were only applied on the first transition, especially when interacting with anchor positioning or position fallbacks. (163928932)</li>
</ul>
<h3><a name="layout-engine-improvements"></a>Layout Engine Improvements</h3>
<p>For several years, WebKit engineers have been working to rebuild each layout algorithm on a more modern foundation. Rather than waiting until a rewrite is complete before shipping its benefits, we’ve developed a mechanism so the new algorithm handles what it can as early as possible. Each algorithm starts with simpler use cases, then expands coverage over time as it becomes more capable — until it handles every situation.</p>
<p>Inline layout was completed <a href="https://webkit.org/blog/15063/webkit-features-in-safari-17-4/#css">in Safari 17.4</a> two years ago. Now, Safari 26.4 completes blocks-in-inline layout — fixing bugs and improving performance when block-level elements appear inside inline elements. Our work on the new Flexbox algorithm continues as well, covering increasingly complex cases over time.</p>
<p>Work on a new Grid layout engine is also now underway. When you use CSS Grid in a simple fashion, the new implementation in Safari 26.4 may be handling your layout. As the work progresses, support for more complex Grid layouts will follow.</p>
<p>Specific changes in Safari 26.4 include:</p>
<ul>
<li>Fixed incorrect min and max width calculations for block-level boxes inside inline content. (166157696)</li>
<li>Fixed an issue where <code>getClientRects</code> returned an incomplete list of rectangles for inline boxes containing block elements. (167209147)</li>
<li>Fixed baseline alignment for grid items by adding correct first baseline and last baseline row axis handling and properly accounting for baseline offsets. (155967278)</li>
</ul>
<h3><a name="table-layout"></a>Table Layout</h3>
<p>Table layout dates back to the early days of CSS, when the specification left a lot of behavior undefined. Browsers are still working through the consequences.</p>
<ul>
<li>Fixed an issue where <code>max-width</code> was not correctly applied to tables with fixed widths. (96554687)</li>
<li>Fixed table layout so that fixed horizontal margins on <code>&lt;caption&gt;</code> elements now contribute to the table’s minimum preferred logical width, preventing captions from causing narrower than expected tables. (120990942)</li>
<li>Fixed table column width distribution when a <code>colspan</code> spans mixed percentage and auto-width columns to properly respect percentage constraints. (165561401)</li>
<li>Fixed baseline handling for table cells when cell has no inflow children. (160774504)</li>
<li>Fixed <code>element.clientWidth</code> and <code>element.clientHeight</code> to correctly include padding for <code>content-box</code> tables. (165515755)</li>
<li>Fixed table height calculation to correctly account for captions with orthogonal <code>writing-mode</code>. (167220730)</li>
</ul>
<h3><a name="additional-changes-to-css"></a>Additional changes to CSS</h3>
<p>Safari 26.4 removes the deprecated <code>FontFaceSet</code> constructor from the CSS Font Loading API, aligning with a CSSWG resolution that deemed it unnecessary. The constructor was rarely used and its removal shouldn’t affect the web.</p>
<p>And this release includes even more improvements to CSS:</p>
<ul>
<li>Fixed an issue where <code>display: list-item</code> was incorrectly supported on <code>fieldset</code>. (95638460)</li>
<li>Fixed incorrect sizing and fragment URL handling for SVG images used in <code>-webkit-cross-fade()</code>. (106633417)</li>
<li>Fixed <code>text-combine-upright</code> to properly ignore <code>letter-spacing</code> when composing text horizontally, aligning with the CSS Writing Modes specification. (116562622)</li>
<li>Fixed an issue where <code>background-blend-mode</code> was not applied correctly when combined with <code>background-clip: text</code>. (120901898)</li>
<li>Fixed the UA style sheet to use <code>:focus-visible</code> instead of <code>:focus</code> for outline properties. (123155364)</li>
<li>Fixed <code>HighlightRegistry</code> to remove its non-standard <code>constructor</code> and updated tests to use <code>CSS.highlights</code> while ensuring <code>Map.prototype</code> is properly restored after tampering. (125529396)</li>
<li>Fixed handling of <code>@property</code> registration so that the <code>initial-value</code> descriptor can be optional. (131288198)</li>
<li>Fixed scrolling behavior so that <code>scrollRectToVisible()</code> can bring fixed anchor-positioned boxes outside the viewport into view, improving keyboard navigation. (162378346)</li>
<li>Fixed an issue where <code>@font-face</code> and <code>FontFace.family</code> failed when the font family name contained spaces, ensuring the family name is now treated as a plain string instead of being parsed. (162637501)</li>
<li>Fixed incorrect underline positioning for <code>text-decoration</code> when inline box sides are trimmed. (163858721)</li>
<li>Fixed <code>-webkit-line-clamp</code> so that it no longer propagates into <code>inline-block</code> children. (164488778)</li>
<li>Fixed an issue where nested identical CSS <code>filter</code> effects were not rendered. (165163823)</li>
<li>Fixed: Refactored the handling of block-level boxes inside inline boxes. (165523565)</li>
<li>Fixed an issue where <code>text-decoration: underline</code> appeared higher than expected when <code>text-box-trim</code> was applied to the root inline box. (165614136)</li>
<li>Fixed <code>::first-line</code> pseudo-element to always use <code>inline</code> display to match the CSS Display specification. (166068698)</li>
<li>Fixed an issue where <code>shape-outside</code> did not update correctly after web fonts loaded. (166336491)</li>
<li>Fixed incorrect text selection ranges for truncated right-to-left content. (166944754)</li>
<li>Fixed <code>counter-</code> properties serialization order. (167518994) </li>
<li>Fixed <code>outline-width</code> and <code>outline-offset</code> to follow updated computed style resolution rules. (167618367)</li>
<li>Fixed the computed style resolution for <code>border-width</code> properties. (167689519) </li>
<li>Fixed the computed style resolution for the <code>column-rule-width</code> property. (167725940)</li>
<li>Fixed <code>border-width</code>, <code>outline-width</code>, and <code>column-rule-width</code> so they now pixel snap correctly during CSS animations and transitions. (167763497) </li>
<li>Fixed the disclosure triangle in <code>&lt;details&gt;</code> elements to use the larger <code>system-ui</code> font variant, preventing it from rendering as an emoji and ensuring consistent display across writing directions. (168364553)</li>
<li>Fixed CSS rules within <code>@scope</code> not being applied to <code>&lt;input&gt;</code> and <code>&lt;textarea&gt;</code> elements. (169751338)</li>
<li>Fixed an issue where empty CSS rules sharing a selector with non-empty rules could prevent dynamic style updates from applying correctly. (170348749)</li>
<li>Fixed an issue where CSS transitions were incorrectly triggered when <code>border-width</code> computed values did not change, causing unexpected layout shifts. (170657059)</li>
<li>Fixed an issue where multi-column layout rendered columns at incorrect positions for some fonts. (171016194)</li>
</ul>
<h2><a name="webtransport"></a>WebTransport</h2>
<p>Safari 26.4 adds support for <a href="https://www.w3.org/TR/webtransport/">WebTransport</a>, a modern API for low-latency, bidirectional communication between clients and servers.</p>
<p>If you’ve been building real-time applications — like multiplayer games, live collaboration tools, or video conferencing — you’ve likely run into the limitations of existing technologies. WebSockets work well for many use cases, but they’re built on TCP, which means head-of-line blocking can cause delays when packets are lost. HTTP/3 and QUIC solve this problem, but don’t directly offer the same bidirectional streaming capabilities you might need.</p>
<p>WebTransport gives you the best of both worlds. It runs over HTTP/3 and QUIC, providing multiple streams that won’t block each other. You can send data reliably (like WebSockets) or unreliably (when you’d rather drop old data than wait for it), and you can mix both approaches in the same connection. This makes it particularly useful for applications where low latency matters most — think live audio, real-time sensor data, or fast-paced gaming. When the underlying network environment doesn&#8217;t support QUIC, WebTransport can run over HTTP/2 and TCP as a fallback with the same API.</p>
<p>The API is built around streams, similar to the Streams API you might already be using elsewhere. You can open bidirectional streams, send datagrams, and handle backpressure naturally. Here’s a basic example:</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">url</span> <span class="operator">=</span> <span class="char">'https://example.com:443/webtransport'</span>;
<span class="keyword type">const</span> <span class="identifier">transport</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">WebTransport</span>(<span class="identifier">url</span>);

<span class="identifier">await</span> <span class="identifier">transport</span>.<span class="identifier">ready</span>;

<span class="comment">// Send data via a unidirectional stream
</span><span class="keyword type">const</span> <span class="identifier">stream</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">transport</span>.<span class="identifier">createUnidirectionalStream</span>();
<span class="keyword type">const</span> <span class="identifier">writer</span> <span class="operator">=</span> <span class="identifier">stream</span>.<span class="identifier">getWriter</span>();
<span class="identifier">await</span> <span class="identifier">writer</span>.<span class="identifier">write</span>(<span class="keyword operator">new</span> <span class="identifier">Uint8Array</span>([<span class="number">1</span>, <span class="number">2</span>, <span class="number">3</span>]));
<span class="identifier">await</span> <span class="identifier">writer</span>.<span class="identifier">close</span>();
</code></pre>
<p>WebTransport opens up new possibilities for what you can build on the web, bringing performance characteristics that previously required native applications or complex workarounds.</p>
<p>A related fix also landed:</p>
<ul>
<li>Fixed <code>ReadableStream</code> and <code>WritableStream</code> to correctly pass abort and cancel reasons and improved <code>WebTransport</code> stream handling. (165474756)</li>
</ul>
<p>Also fixed in Networking:</p>
<ul>
<li>Fixed a regression where <code>fetch()</code> would throw a <code>TypeError</code> when using <code>targetAddressSpace: 'loopback'</code> for localhost requests. (166574523)</li>
</ul>
<h2><a name="web-api"></a>Web API</h2>
<h3><a name="keyboard-lock-api"></a>Keyboard Lock API</h3>
<p>Safari 26.4 adds support for the Fullscreen Keyboard Lock API, which allows web applications to capture keyboard input that would normally be handled by the browser.</p>
<p>If you’ve ever built a game, a remote desktop client, or a creative tool, you’ve probably encountered this frustration: certain keyboard shortcuts are off-limits. Press the Escape key and you are thrown out of fullscreen mode. There’s been no way to prevent this — until now.</p>
<p>The Keyboard Lock API lets you request access to specific keys when your application needs it. A game can now use the Escape key for its own menu system. To exit fullscreen mode then the user would need to hold down the escape key for 1.5 seconds. A remote desktop client can pass through all keyboard shortcuts to the remote machine.</p>
<pre><code class="js"><span class="identifier">element</span>.<span class="identifier">requestFullscreen</span>({ <span class="identifier">keyboardLock</span><span class="operator">:</span> <span class="string">"browser"</span> });
</code></pre>
<p>The browser automatically releases the lock when the user leaves fullscreen or switches tabs. And of course, this only works in secure contexts — sites served over HTTPS.</p>
<h3><a name="readablebytestream"></a>ReadableByteStream</h3>
<p>Safari 26.4 adds support for <code>ReadableByteStream</code>, completing the implementation of byte-oriented streams in the Streams API.</p>
<p>Until now, <code>ReadableStream</code> has primarily worked with chunks of any type — objects, strings, or arbitrary data. <code>ReadableByteStream</code> is specifically designed for efficiently handling binary data, like files, network responses, or media streams.</p>
<p>The key advantage is memory efficiency. With byte streams, you can use BYOB (Bring Your Own Buffer) readers, which let you provide your own <code>ArrayBuffer</code> for the stream to fill. This means you can reuse buffers and avoid unnecessary allocations.</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">reader</span> <span class="operator">=</span> <span class="identifier">stream</span>.<span class="identifier">getReader</span>({ <span class="identifier">mode</span><span class="operator">:</span> <span class="char">'byob'</span> });
<span class="keyword type">const</span> <span class="identifier">buffer</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">ArrayBuffer</span>(<span class="number">1024</span>);
<span class="keyword type">const</span> { <span class="identifier">value</span>, <span class="identifier">done</span> } <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">reader</span>.<span class="identifier">read</span>(<span class="keyword operator">new</span> <span class="identifier">Uint8Array</span>(<span class="identifier">buffer</span>));
</code></pre>
<p>Safari 26.4 also adds support for using byte streams as <code>fetch</code> request and response bodies, and for reading <code>Blob.stream()</code> with a BYOB reader. If you’re working with video, audio, large files, or any scenario where you’re moving significant amounts of binary data around, byte streams give you the tools to do it efficiently.</p>
<p>A related encoding fix also landed:</p>
<ul>
<li>Fixed incorrect handling of invalid UTF-8 sequences in the <code>TextDecoder</code> streaming decoder to properly manage partial sequence buffers. (166583808)</li>
</ul>
<h3><a name="readablestream-async-iteration"></a>ReadableStream Async Iteration</h3>
<p>Safari 26.4 adds support for <code>ReadableStream.getIterator()</code> and the <code>[@@asyncIterator]</code> method, making it much easier to work with streams using modern JavaScript syntax. Previously, reading from a stream required manually calling <code>getReader()</code> and repeatedly calling <code>read()</code> in a loop. Now you can use <code>for await...of</code> to iterate over stream chunks directly:</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">response</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">fetch</span>(<span class="char">'/data'</span>);
<span class="keyword type">const</span> <span class="identifier">stream</span> <span class="operator">=</span> <span class="identifier">response</span>.<span class="identifier">body</span>;

<span class="keyword control">for</span> <span class="identifier">await</span> (<span class="keyword type">const</span> <span class="identifier">chunk</span> <span class="keyword operator">of</span> <span class="identifier">stream</span>) {
  <span class="comment">// Process each chunk as it arrives
</span>  <span class="identifier">console</span>.<span class="identifier">log</span>(<span class="identifier">chunk</span>);
}
</code></pre>
<p>This is much cleaner than the previous approach and fits naturally with how you’re already using async iteration elsewhere in JavaScript. It’s particularly nice when you’re processing streaming data — like server-sent events, large file uploads, or any scenario where data arrives over time.</p>
<h3><a name="improvements-to-scoped-custom-element-registries"></a>Improvements to Scoped Custom Element Registries</h3>
<p>In September, Safari 26.0 was the first browser to ship support for the standardized version of Scoped Custom Element Registries. Before then, custom elements were always registered globally on a single registry shared across the entire document. This created problems when building component libraries or working with multiple frameworks. If two different parts of an application tried to register the same element name, one would fail.</p>
<p>Scoped registries solve this by letting you create separate registries for different parts of the same document:</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">starRegistry</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">CustomElementRegistry</span>();
<span class="identifier">starRegistry</span>.<span class="identifier">define</span>(<span class="char">'my-button'</span>, <span class="identifier">MyCustomButton</span>);
<span class="identifier">document</span>.<span class="identifier">createElement</span>(<span class="char">'my-button'</span>, { <span class="identifier">customElementRegistry</span><span class="operator">:</span> <span class="identifier">starRegistry</span> });

<span class="keyword type">const</span> <span class="identifier">bananaRegistry</span> <span class="operator">=</span> <span class="keyword operator">new</span> <span class="identifier">CustomElementRegistry</span>();
<span class="identifier">bananaRegistry</span>.<span class="identifier">define</span>(<span class="char">'my-button'</span>, <span class="identifier">MyFancyButton</span>);
<span class="identifier">document</span>.<span class="identifier">createElement</span>(<span class="char">'my-button'</span>, { <span class="identifier">customElementRegistry</span><span class="operator">:</span> <span class="identifier">bananaRegistry</span> });
</code></pre>
<p>Safari 26.4 now extends Scoped Custom Element Registries by:</p>
<ul>
<li>Upgrading elements in <code>CustomElementRegistry.prototype.initialize</code></li>
<li>Supporting the <code>customelementregistry</code> content attribute and handling of <code>nullcustomElementRegistry</code> values in <code>document.createElement</code>, <code>document.createElementNS</code>, and <code>element.attachShadow</code></li>
<li>Fixing <code>shadowrootcustomelementregistry</code> attribute serialization to correctly compare ShadowRoot and document registries. (165476421)</li>
</ul>
<h3><a name="auxiliary-mouse-button-support"></a>Auxiliary Mouse Button Support</h3>
<p>Safari 26.4 adds support for auxiliary mouse button values in <code>MouseEvent.button</code>, so you can now detect additional mouse buttons beyond the standard left, middle, and right clicks. If you’re building applications that take advantage of gaming mice or other input devices with extra buttons, you can now respond to those inputs.</p>
<pre><code class="js"><span class="identifier">element</span>.<span class="identifier">addEventListener</span>(<span class="char">'mousedown'</span>, (<span class="identifier">e</span>) <span class="operator">=</span><span class="operator">&gt;</span> {
  <span class="keyword control">if</span> (<span class="identifier">e</span>.<span class="identifier">button</span> <span class="operator">=</span><span class="operator">=</span><span class="operator">=</span> <span class="number">3</span>) { <span class="comment">/* back button */</span> }
  <span class="keyword control">if</span> (<span class="identifier">e</span>.<span class="identifier">button</span> <span class="operator">=</span><span class="operator">=</span><span class="operator">=</span> <span class="number">4</span>) { <span class="comment">/* forward button */</span> }
});
</code></pre>
<p>The <code>button</code> property will correctly report values for buttons 3, 4, and beyond, matching the behavior in other browsers.</p>
<h3><a name="resource-timing"></a>Resource Timing</h3>
<p>Safari 26.4 adds two new attributes from the Resource Timing Level 3 specification: <code>finalResponseHeadersStart</code> and <code>firstInterimResponseStart</code>. These give you more precise timing measurements for HTTP responses — particularly useful if you’re using 103 Early Hints.</p>
<p><code>firstInterimResponseStart</code> captures when the first interim response (like a 103 Early Hints response) was received, and <code>finalResponseHeadersStart</code> captures when the final response headers arrived. Together they let you measure exactly how much time your 103 Early Hints are saving.</p>
<pre><code class="js"><span class="keyword type">const</span> [<span class="identifier">entry</span>] <span class="operator">=</span> <span class="identifier">performance</span>.<span class="identifier">getEntriesByType</span>(<span class="char">'resource'</span>)
  .<span class="identifier">filter</span>(<span class="identifier">e</span> <span class="operator">=</span><span class="operator">&gt;</span> <span class="identifier">e</span>.<span class="identifier">name</span>.<span class="identifier">includes</span>(<span class="char">'example.com'</span>));

<span class="identifier">console</span>.<span class="identifier">log</span>(<span class="identifier">entry</span>.<span class="identifier">firstInterimResponseStart</span>);  <span class="comment">// when 103 arrived
</span><span class="identifier">console</span>.<span class="identifier">log</span>(<span class="identifier">entry</span>.<span class="identifier">finalResponseHeadersStart</span>);  <span class="comment">// when final headers arrived
</span></code></pre>
<p>If you’re not yet using 103 Early Hints, these attributes give you a reason to explore it — you can now actually measure the impact.</p>
<h3><a name="mediadeviceinfo-in-secure-contexts-only"></a>MediaDeviceInfo in Secure Contexts Only</h3>
<p>Safari 26.4 now exposes the <code>MediaDeviceInfo</code> interface only in secure contexts (HTTPS), aligning with the web specification. If you’re working with <code>navigator.mediaDevices.enumerateDevices()</code> to detect cameras and microphones, make sure your site is served over HTTPS.</p>
<p>Along the same lines:</p>
<ul>
<li>Fixed <code>DeviceMotionEvent</code> and <code>DeviceOrientationEvent</code> interfaces so that they only show up in secure contexts just like the corresponding events and made <code>ondevicemotion</code> and <code>ondeviceorientation</code> enumerable, aligning with the specification. (44804273)</li>
</ul>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Safari 26.4 also includes a number of other Web API fixes:</p>
<ul>
<li>Fixed an issue where <code>IntersectionObserver</code> computed the root rectangle incorrectly when overflow clipping was present. (117143395)</li>
<li>Fixed Trusted Types to correctly send CSP violation reports when a default policy returns an invalid <code>javascript:</code> URL or throws an exception. (160960418)</li>
<li>Fixed <code>Element.requestFullscreen</code> on iOS to correctly reflect hardware keyboard attachment state during fullscreen sessions and exit automatically when the keyboard is detached. (161429040)</li>
<li>Fixed event ordering and committed promise timing for intercepted <code>Navigation API</code> traverse navigations. (161445256)</li>
<li>Fixed the processing order of Trusted Types for DOM attribute setting. (162143148)</li>
<li>Fixed <code>NavigateEvent</code> to correctly fire an <code>AbortSignal</code> when a navigation is aborted. (163957784)</li>
<li>Fixed <code>NavigateEvent.sourceElement</code> to correctly reference elements from different browsing contexts. (163962362)</li>
<li>Fixed the Navigation API to prevent scripts from flooding the system with navigation requests. (164510890)</li>
<li>Fixed an issue where <code>scroll-margin</code> from <code>IntersectionObserver</code> incorrectly applied to scrollers inside cross-origin iframes. (164994009)</li>
<li>Fixed <code>DigitalCredential</code> behavior to make user mediation implicitly required. (165597827)</li>
<li>Fixed an issue where the Big5 <code>TextDecoder</code> failed to recover and emit ASCII characters after encountering an invalid leading byte. (166672674)</li>
<li>Fixed <code>MouseEvent.offsetX</code> and <code>MouseEvent.offsetY</code> so they are now calculated relative to the padding edge of the target element. (168015965)</li>
<li>Fixed an issue where pointer events would fail to dispatch after a parent view&#8217;s custom gesture recognizer blocked <code>touchesEnded:</code> or <code>touchesCancelled:</code>. (169109808)</li>
<li>Fixed an issue where JavaScript-to-native object serialization could fail entirely when any individual key-value pair could not be serialized, causing broken workflows in some apps. (171547386)</li>
</ul>
<h2><a name="javascript"></a>JavaScript</h2>
<p>Safari 26.4 adds support for iterator sequencing. It lets you chain multiple iterators together into a single sequence using <code>Iterator.concat()</code>.</p>
<pre><code class="js"><span class="keyword type">const</span> <span class="identifier">odds</span> <span class="operator">=</span> [<span class="number">1</span>, <span class="number">3</span>, <span class="number">5</span>].<span class="identifier">values</span>();
<span class="keyword type">const</span> <span class="identifier">evens</span> <span class="operator">=</span> [<span class="number">2</span>, <span class="number">4</span>, <span class="number">6</span>].<span class="identifier">values</span>();

<span class="keyword control">for</span> (<span class="keyword type">const</span> <span class="identifier">n</span> <span class="keyword operator">of</span> <span class="identifier">Iterator</span>.<span class="identifier">concat</span>(<span class="identifier">odds</span>, <span class="identifier">evens</span>)) {
<span class="identifier">console</span>.<span class="identifier">log</span>(<span class="identifier">n</span>); <span class="comment">// 1, 3, 5, 2, 4, 6
</span>}
</code></pre>
<p>This is a clean alternative to flattening arrays or writing manual chaining logic just to iterate over several collections in sequence.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Several JavaScript bugs were also fixed:</p>
<ul>
<li>Fixed <code>Date</code> constructor overflow handling so that invalid day values now return <code>NaN</code>. (155776209)</li>
<li>Fixed <code>Intl.DateTimeFormat</code> to throw a <code>RangeError</code> for legacy non-IANA timezones, aligning behavior with TC39 standards. (156857252)</li>
<li>Fixed <code>Intl.Locale.prototype.getWeekInfo()</code> to remove the <code>minimalDays</code> property for compliance with the specification. (165083619)</li>
<li>Fixed <code>Intl.NumberFormat</code> to properly apply <code>minimumFractionDigits</code> and <code>maximumFractionDigits</code> to ensure currency and compact notations behave correctly. (165875014)</li>
<li>Fixed <code>%TypedArray%.prototype.includes</code> to correctly check that the <code>index</code> is less than the array length, aligning its behavior with ECMA-262. (167183441)</li>
<li>Fixed async functions without any <code>await</code> to inline their bodies for performance and corrected async stack traces with a single function entry for exceptions thrown from or through async functions. (167254635)</li>
</ul>
<h2><a name="html"></a>HTML</h2>
<p>Safari 26.4 adds support for using the <code>min()</code>, <code>max()</code>, and <code>clamp()</code> math functions inside the <code>sizes</code> attribute of <code>&lt;img&gt;</code> elements.</p>
<p>The <code>sizes</code> attribute tells the browser how wide an image will be displayed at different viewport sizes, helping it choose the right image from your <code>srcset</code>. Until now, you were limited to media queries and length values. Now you can use CSS math functions for more precise control:</p>
<pre><code class="html"><span class="tag">&lt;<span class="keyword">img</span> 
  <span class="keyword attribute">srcset</span>=<span class="attribute value string">"small.jpg 400w, medium.jpg 800w, large.jpg 1200w"</span>
  <span class="keyword attribute">sizes</span>=<span class="attribute value string">"min(100vw, 1200px)"</span>
  <span class="keyword attribute">src</span>=<span class="attribute value string">"medium.jpg"</span>
  <span class="keyword attribute">alt</span>=<span class="attribute value string">"..."</span>&gt;</span>
</code></pre>
<p>This is particularly useful for responsive images that need to respect both viewport width and maximum content width. You can use <code>clamp()</code> to set minimum, ideal, and maximum sizes:</p>
<pre><code class="html">sizes="clamp(300px, 50vw, 800px)"
</code></pre>
<p>This gives you the same flexible sizing control in <code>sizes</code> that you already have in CSS, making responsive images easier to manage.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<ul>
<li>Fixed an issue where nested <code>about:blank</code> frames were incorrectly treated as self-referencing, preventing them from loading. (148373033)</li>
<li>Fixed <code>HTMLImageElement.currentSrc</code> to return an empty string for <code>&lt;img src=""&gt;</code> instead of resolving to the document base URL. (167229274)</li>
<li>Fixed image uploading to not transcode images when <code>accept="image/*"</code> is specified. (166124206)</li>
<li>Fixed an issue where input fields did not display user input while typing. (163613957)</li>
<li>Fixed an issue where <code>input[type="search"]</code> fields with <code>appearance: none</code> incorrectly reserved space for the datalist dropdown button. (166754216)</li>
<li>Fixed an incorrect fallback for the menu style for empty lists, improving readability and correctness. (167662316)</li>
</ul>
<h2><a name="svg"></a>SVG</h2>
<p>Safari 26.4 adds support for the <code>lighter</code> operator in <code>SVGFECompositeElement</code>, aligning with the Compositing and Blending specification. This gives you an additional blending mode when compositing SVG filter effects, useful for creating additive lighting and glow effects in your SVG graphics. This example shows it in action. With support, there’s a soft glow around each circle. Without it, the glow is just not there.</p>
<p class="codepen" style="height: 365px; display: flex; border: 2px solid; margin: 1em 0; padding: 1em;">
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Safari 26.4 also includes a large number of SVG bug fixes:</p>
<ul>
<li>Fixed an issue where <code>stroke-dasharray</code> incorrectly propagated to SVG markers when explicitly marked as &#8216;0&#8217;. (46607685)</li>
<li>Fixed an issue where <code>foreignObject</code> elements in SVG incorrectly allowed margin collapsing. (97208795)</li>
<li>Fixed SVG intrinsic sizing and <code>preferredAspectRatio()</code> to correctly transpose dimensions for vertical writing modes. (103262534)</li>
<li>Fixed animation of the <code>stop-color</code> attribute on <code>&lt;stop&gt;</code> elements. (109823555)</li>
<li>Fixed an issue where dynamically changing <code>marker-start</code>, <code>marker-mid</code>, or <code>marker-end</code> attributes on SVG elements did not trigger re-rendering. (130678384)</li>
<li>Fixed tiling gaps in CSS reference filters using <code>&lt;feDisplacementMap&gt;</code>. (135448018)</li>
<li>Fixed <code>SVGLength</code> parsing to correctly return the initial value when encountering parser errors or invalid values. (136102554)</li>
<li>Fixed an issue where <code>SVGImage</code> did not respect system dark mode changes. (140661763)</li>
<li>Fixed breaking SVG resource referencing when removing a resource which shares its <code>id</code> with other resources. (147015037)</li>
<li>Fixed behavior to avoid incorrect pruning of SVG mask subtrees based on visibility. (157729389)</li>
<li>Fixed an issue where SVG <code>animateTransform</code> animations on hidden elements were triggering full-page rendering updates each frame. (159647563)</li>
<li>Fixed <code>SVGLength.prototype.valueAsString</code> to throw a <code>SyntaxError</code> when assigned an empty string. (165429393)</li>
<li>Fixed <code>SVGLength</code> percentage resolution for elements inside non-instanced <code>&lt;symbol&gt;</code> elements. (165431008)</li>
<li>Fixed an issue where lengths with leading or trailing whitespace failed to be parsed. (165501190)</li>
<li>Fixed an issue where <code>SVGLength.value</code> did not update for font-relative units (e.g., <code>ch</code>, <code>em</code>) after changes to <code>writing-mode</code>. (166190252)</li>
<li>Fixed missing gradient fills when using paint-order <code>stroke fill</code>. (166997630)</li>
<li>Fixed embedded <code>&lt;svg&gt;</code> elements in <code>&lt;img&gt;</code> without an explicit <code>viewBox</code> to synthesize <code>preserveAspectRatio='none'</code> so the SVG stretches to fill the container. (167121931)</li>
<li>Fixed the <code>&lt;stop&gt;</code> element <code>offset</code> attribute in SVG to reject invalid values with trailing characters and correctly fall back to <code>0</code>. (167356988)</li>
<li>Fixed the transform order for <code>clipPath</code> elements so that the bounding box is scaled correctly before applying the local transform. (167417135)</li>
<li>Fixed <code>&lt;clipPath&gt;</code> to clip to its <code>&lt;use&gt;</code> child element based on the visibility of the <code>&lt;use&gt;</code> target element. (167491519)</li>
<li>Fixed incorrect rendering when combining <code>markerUnits=strokeWidth</code> with <code>vector-effect=non-scaling-stroke</code>. (167493417)</li>
<li>Fixed displaying an SVG filter referencing an element with a huge stroke. (167516452)</li>
<li>Fixed hit testing for overlapping <code>&lt;text&gt;</code> and <code>&lt;tspan&gt;</code> elements in SVG. (167691166)</li>
<li>Fixed rendering of dimensionless SVG images. (168176556)</li>
</ul>
<h2><a name="safari-compact-tabs"></a>Safari Compact tabs</h2>
<p>The Compact tabs option on macOS and iPadOS makes a return in Safari 26.4. If you preferred the more space-efficient tab design from earlier versions of Safari, you can now enable it again in Safari settings, under Tabs > Tab layout.</p>
<figure class=""><source media="(prefers-color-scheme: dark)" type="image/png" /><img alt="Safari settings panel, showing where to switch from Separate to Compact tabs." class="aligncenter size-full wp-image-17883" height="1154" src="https://webkit.org/wp-content/uploads/safari264-compacttabs-light.png" width="1896" /></figure>
<h2><a name="web-authentication"></a>Web Authentication</h2>
<p>Safari 26.4 adds two important WebAuthn improvements for advanced authentication scenarios.</p>
<p>The PRF (Pseudo-Random Function) extension enables credential-bound cryptographic secrets during both credential creation and authentication flows with security keys. This maps to the CTAP <code>hmac-secret</code> extension and allows you to derive cryptographic keys from WebAuthn credentials — useful for applications that need to encrypt user data with keys tied to their authentication credentials, such as password managers or encrypted storage systems.</p>
<p>Safari 26.4 also adds support for CTAP PIN/UV Auth Protocol 2, which uses HKDF-SHA-256 for key derivation. This enables proper support for newer FIPS-compliant authenticators, which is important for enterprise and government applications with strict security requirements.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<ul>
<li>Fixed an issue where the <code>excludeCredentials</code> list was not sent over CTAP when its size was 1. (164546088)</li>
</ul>
<h2><a name="web-inspector"></a>Web Inspector</h2>
<p>In addition to the new Grid Lanes tooling described above, Safari 26.4 includes numerous Web Inspector enhancements to help you debug and build websites more effectively.</p>
<h3><a name="layer-visualization"></a>Layer Visualization</h3>
<p>The Layers tab now shows actual composited layer snapshots instead of outline representations, giving you a more accurate picture of how your page is being rendered and composited.</p>
<figure class=""><source media="(prefers-color-scheme: dark)" type="image/png" /><img alt="The Web Inspector Layers tab, showing a webpage turned in #D space, with the separate layers of the site stacked translucently on top of each other" class="aligncenter size-full wp-image-17886" height="1592" src="https://webkit.org/wp-content/uploads/layervis-light.png" width="2550" /></figure>
<h3><a name="developer-experience"></a>Developer Experience</h3>
<p>A new context menu option lets you copy pretty-printed HTML from DOM nodes in the Elements tab — much easier to read than minified markup. In the settings tab, you can now toggle the visibility of User Agent stylesheet rules, reducing clutter when you’re focused on your own styles.</p>
<figure class=""><source media="(prefers-color-scheme: dark)" type="image/png" /><img alt="Web Inspector open on a website, with something in the DOM tree selected. The context menu is open, showing options, and Copy HTML (Formatted) is being chosen." class="aligncenter size-full wp-image-17889" height="1683" src="https://webkit.org/wp-content/uploads/webinspector-copyformatedHTML-light-scaled.png" width="2560" /></figure>
<p>The Timelines Heap view displays the dominator object when viewing the shortest GC path, making it easier to track down memory leaks. And Web Inspector now fetches CSS property keyword completions based on actual feature support, so auto-complete suggestions reflect what’s actually available.</p>
<h3><a name="worker-debugging"></a>Worker Debugging</h3>
<p>You can now capture <code>console.screenshot</code> images within a Worker, supporting <code>ImageData</code>, <code>ImageBitmap</code>, <code>OffscreenCanvas</code>, and various canvas rendering contexts. Canvas recordings can also be started and stopped from the console within a Worker using <code>console.record()</code> and <code>console.recordEnd()</code>.</p>
<h3><a name="additional-improvements"></a>Additional Improvements</h3>
<p>Auto-completion now includes <code>sideways-lr</code> and <code>sideways-rl</code> values for the <code>writing-mode</code> property, making it easier to work with vertical text layouts.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Safari 26.4 also includes a number of Web Inspector bug fixes:</p>
<ul>
<li>Fixed incorrect breakpoint and search result positions in the Web Inspector after pretty-printing inline scripts containing multi-line template literals. (29417859)</li>
<li>Fixed the Styles sidebar filter in Web Inspector to be case-insensitive. (36086981)</li>
<li>Fixed an issue where a large number of search results in the Search tab would freeze Web Inspector. (49234522)</li>
<li>Fixed an issue where the Console tab search bar in Web Inspector would disappear when the window was too narrow. (50922509)</li>
<li>Fixed an issue where CSS properties added to new rules were not applied and were marked as invalid. (103548968)</li>
<li>Fixed context menu items to rename <code>Copy HTTP Request</code> and <code>Copy HTTP Response</code> to <code>Copy HTTP Request Headers</code> and <code>Copy HTTP Response Headers</code> for clarity. (117708766)</li>
<li>Fixed incorrect grid track sizing display in the Web Inspector when using CSS custom properties. (141709306)</li>
<li>Fixed an issue in the Console where the count of identical consecutive messages could be wrong. (162612099)</li>
<li>Fixed an issue where breakpoints and search results in Web Inspector could point to the wrong location after a previously formatted source file was reopened in an unformatted state. (165059693)</li>
<li>Fixed an issue where the Sources navigation sidebar could be empty when reloading the page. (166141968)</li>
<li>Fixed timestamp formatting in the Web Inspector to remove unnecessary trailing <code>.0</code> values for readability. (166500013)</li>
<li>Fixed item order labels in the Web Inspector grid and flex overlays to remove the <code>#</code> symbol, changing from <code>Item #N</code> to <code>Item N</code>. (166767949)</li>
<li>Fixed an issue where the text filter in the Sources tab did not apply to the Local Overrides and Console Snippets sections. (169804196)</li>
<li>Fixed a performance issue in the Web Inspector search panel by limiting initial results to 100 per resource and adding UI controls to load more or all results, reducing unnecessary UI work for large queries. (169804865)</li>
<li>Fixed an issue where the search bar settings icon disappeared when the search field was focused. (169997100)</li>
</ul>
<h2><a name="media-captions"></a>Media Captions</h2>
<p>Safari 26.4 adds improved caption controls on macOS, including a pop-up menu that lets users select and manage caption style profiles and configure subtitle display settings.</p>
<p>These enhancements give users more control over how captions appear — adjusting text size, color, background, and other styling options to match their preferences. If you’re providing video content with captions, users will have a better experience customizing how those captions are displayed.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Quite a few media bugs were also fixed:</p>
<ul>
<li>Fixed dispatching of enter and exit events on <code>TextTrackCue</code> and <code>VTTCue</code> objects with no associated track, aligning with other browsers. (160195643)</li>
<li>Fixed an issue where changing an <code>HTMLMediaElement</code> volume from <code>0</code> to <code>0</code> did not activate the audio session or update the sleep disabler. (161691743)</li>
<li>Fixed an issue where videos would freeze on the first frame when transitioning from encrypted to clear content by ensuring the decoded buffer maintains at least 100ms of frames even when the next frame is far in the future. (162234566)</li>
<li>Fixed an issue where the mute button disappeared in macOS inline videos with adjustable sizes. (162897286)</li>
<li>Fixed playback of <code>application/ogg</code> blob media. (163119790)</li>
<li>Fixed an issue where Video Viewer UI elements overlapped or exited unexpectedly. (164051864)</li>
<li>Fixed an issue where empty <code>&lt;track&gt;</code> elements prevented media from advancing its readyState and blocked <code>play()</code> calls. (164125914)</li>
<li>Fixed an issue where <code>HTMLMediaElement</code> did not correctly detect new audio or video tracks causing Safari to pause video when leaving a tab. (164514685)</li>
<li>Fixed a crash in <code>AudioData.copyTo()</code> when copying the last channel of 3-channel audio. (164730320)</li>
<li>Fixed an issue where the <code>ended</code> event for Media Source Extensions might never fire by ensuring buffered ranges update correctly and playback gaps are observed even when the video does not start at time zero. (165430052)</li>
<li>Fixed an issue where caption previews were not shown in the default media controls. (165931046)</li>
<li>Fixed the caption menu&#8217;s <code>On</code> option to correctly enable the highest-scoring text track and mark the appropriate language as checked in the subtitle menu. (166158394)</li>
<li>Fixed <code>parseSequenceHeaderOBU</code> to return an <code>AV1CodecConfigurationRecord</code>, fully decode the Sequence Header OBU, and capture the complete color profile. (166439682)</li>
<li>Fixed an issue where the macOS inline media controls timeline scrubber overlapped the right container buttons. (167634241)</li>
<li>Fixed an issue where <code>WebCodecs VideoDecoder</code> could output H264 frames in the wrong order. (168046597)</li>
<li>Fixed an issue where the mute button and volume slider overlapped in the video player controls when using a right-to-left language. (170174446)</li>
</ul>
<h2><a name="webrtc"></a>WebRTC</h2>
<p>Safari 26.4 adds two significant WebRTC enhancements for audio and networking.</p>
<p>On macOS, <code>getUserMedia</code> now supports capturing audio from multiple microphones simultaneously while intelligently managing echo cancellation. The system dynamically migrates existing audio captures to appropriate processing units, making it easier to build applications like podcasting tools, multi-participant recording, or music collaboration apps that need multiple audio inputs.</p>
<p>On iOS, Safari 26.4 adds network slicing support for WebRTC. Network slicing allows different types of traffic to be prioritized differently on cellular networks, which can improve quality and reliability for real-time communication applications in challenging network conditions.</p>
<h3><a name="resolved-issues"></a>Resolved issues</h3>
<p>Several WebRTC bugs were also fixed:</p>
<ul>
<li>Fixed <code>RTCDataChannelInit</code> to support <code>[EnforceRange]</code> on the <code>maxPacketLifeTime</code> and <code>maxRetransmits</code> fields to align with the WebRTC specification. (133630397)</li>
<li>Fixed an issue on macOS where calling <code>getUserMedia</code> with echo cancellation disabled could unintentionally affect existing audio tracks. (151143554)</li>
<li>Fixed <code>MediaStreamTrackProcessor</code> to respect <code>track.enabled = false</code>. (165199900)</li>
<li>Fixed an issue where <code>RTCDataChannel</code> close events did not fire when <code>RTCPeerConnection</code> was closed. (165617848)</li>
<li>Fixed <code>RTCConfiguration.iceServers</code> to be a non-optional sequence with an empty array as the default, improving spec compliance and ensuring <code>RTCPeerConnection</code> behaves correctly when <code>iceServers</code> is undefined. (167607478)</li>
</ul>
<h2><a name="additional-resolved-issues"></a>Additional resolved issues</h2>
<p>There are even more issues that have been fixed in Safari 26.4.</p>
<h3><a name="accessibility"></a>Accessibility</h3>
<ul>
<li>Fixed an issue where Voice Control commands could cause Safari to hang. (168364189)</li>
<li>Fixed an issue where a button&#8217;s label would not update when a descendant&#8217;s <code>aria-hidden</code> attribute changed. (169012516)</li>
<li>Fixed elements with <code>aria-controls</code> or <code>aria-expanded</code> and the <code>hidden</code> attribute to no longer appear in VoiceOver&#8217;s Form Control menu. (169499630)</li>
<li>Fixed an issue where VoiceOver would announce with extra verbosity when moving onto the first item of a list on the webpage. (169982730)</li>
<li>Fixed an issue where controls with <code>aria-labelledby</code> pointing to visually-hidden elements could not obtain proper bounding box geometry through accessibility APIs. (170639492)</li>
</ul>
<h3><a name="browser"></a>Browser</h3>
<ul>
<li>Fixed Safari gesture support to prevent pages that should not be able to scroll, such as with explicit <code>overflow: hidden</code>, from unexpectedly scrolling. (163660111)</li>
</ul>
<h3><a name="canvas"></a>Canvas</h3>
<ul>
<li>Fixed <code>ImageBitmap</code> created from SVG image sources to correctly honor the <code>flipY</code> orientation. (83959718)</li>
</ul>
<h3><a name="clipboard"></a>Clipboard</h3>
<ul>
<li>Fixed an issue where using the &#8220;Copy Image&#8221; context menu in Safari would also copy the image URL, causing some sites to paste the URL instead of the image. (76598990)</li>
</ul>
<h3><a name="editing"></a>Editing</h3>
<ul>
<li>Fixed incorrect text selection when dragging across pseudo elements. (142905243)</li>
<li>Fixed an issue on iOS 26 where the edit menu would not appear when tapping inside an already-focused text field that had a looping <code>content</code> animation. (164290305)</li>
<li>Fixed an issue where focusing a hidden editable element would incorrectly display the text cursor and selection at full opacity. (165489471)</li>
<li>Fixed a regression where dragging to select text would stop scrolling when the cursor left the window. (169983104)</li>
</ul>
<h3><a name="events"></a>Events</h3>
<ul>
<li>Fixed an issue where <code>mouseleave</code> and <code>mouseout</code> events were not dispatched when a window moved out from under a stationary cursor. (161493924)</li>
</ul>
<h3><a name="privacy"></a>Privacy</h3>
<ul>
<li>Fixed an issue where cross-browser Private Click Measurement recorded attribution entries even when &#8220;Allow privacy-preserving measurement of ad effectiveness&#8221; was disabled. (170669444)</li>
</ul>
<h3><a name="rendering"></a>Rendering</h3>
<ul>
<li>Fixed over-aggressive clipping of child layers in multicolumn layouts to prevent visual overflow issues with <code>position: relative</code> elements and <code>transform:scale()</code> text. (126413036)</li>
<li>Fixed unreadable Scroll-to-Text-Fragment highlights on dark pages. (126539910)</li>
<li>Fixed an issue where auto-positioned absolutely positioned descendants were not always marked for layout when their parent’s border box moved. (131806062)</li>
<li>Fixed an issue where positioned, transformed, or opacity-altered <code>&lt;img&gt;</code> elements with HDR JPEG gainmaps would incorrectly render in SDR. (156858374)</li>
<li>Fixed an issue on iPadOS where closing the sidebar or resizing the window could cause the page to remain zoomed in by recalculating the target scale to automatically match the new minimum scale. (157676989)</li>
<li>Fixed an issue where fixed positioned elements were not rendered correctly in right-to-left pages using the <code>vertical-rl</code> writing mode. (161712734)</li>
<li>Fixed a performance issue in layouts with long <code>pre</code> blocks and <code>word-break: break-all</code> by including whitespace in overflow width calculations. (162695099)</li>
<li>Fixed an issue where overconstrained sticky elements were not properly adjusting their insets when the sticky box rectangle was larger than the viewport. (163654023)</li>
<li>Fixed an issue where applying <code>word-spacing</code> to <code>::first-line</code> could cause other lines to disappear. (163779992)</li>
<li>Fixed inconsistent text layout when using <code>list-style-type</code> by ensuring outside list markers do not affect intrinsic width calculations. (164650313)</li>
<li>Fixed an issue where color fonts could affect the color of other DOM elements. (166631312)</li>
<li>Fixed <code>&lt;col&gt;</code> elements with <code>span &gt; 1</code> not applying their width to all spanned columns during table layout, aligning behavior with other browsers. (167225435)</li>
<li>Fixed table layout <code>min-width</code> distribution for spanning cells with mixed <code>percent</code>, <code>fixed</code>, and <code>auto</code> columns. (167684748)</li>
<li>Fixed: Improved drop-shadow and blur effects rendering performance. (169472992)</li>
</ul>
<h3><a name="spatial-web"></a>Spatial Web</h3>
<ul>
<li>Fixed auto-dimming for playback sessions in visionOS. (163824973)</li>
</ul>
<h3><a name="storage"></a>Storage</h3>
<ul>
<li>Fixed an issue where IndexedDB databases might have mismatched metadata version and database name encoding format. (163219457)</li>
</ul>
<h3><a name="wkwebview"></a>WKWebView</h3>
<ul>
<li>Fixed an issue where <code>WKWebView</code> apps with a toolbar would fail to display a top scroll edge effect when relying on automatic content inset adjustments. (161370795)</li>
</ul>
<h3><a name="web-extensions"></a>Web Extensions</h3>
<ul>
<li>Fixed an issue where <code>window.open()</code> calls from web extensions would incorrectly open &#8220;about:blank&#8221; instead of the intended URL by ensuring each extension URL loads in a fresh tab configuration. (143901129)</li>
</ul>
<h3><a name="webassembly"></a>WebAssembly</h3>
<ul>
<li>Fixed <code>Error.isError(WebAssembly.Exception)</code> to correctly return <code>false</code> based on current WebAssembly spec semantics. (167110254)</li>
</ul>
<h3><a name="webgpu"></a>WebGPU</h3>
<ul>
<li>Fixed incorrect handling of some PNG pixel formats in WebGPU. (158797747)</li>
</ul>
<h2><a name="feedback"></a>Feedback</h2>
<p>We love hearing from you. To share your thoughts, find us online: Jen Simmons on <a href="https://bsky.app/profile/jensimmons.bsky.social">Bluesky</a> / <a href="https://front-end.social/@jensimmons">Mastodon</a>, Saron Yitbarek on <a href="https://bsky.app/profile/saron.bsky.social">BlueSky</a> / <a href="https://front-end.social/@saron">Mastodon</a>, and Jon Davis on <a href="https://bsky.app/profile/jondavis.bsky.social">Bluesky</a> / <a href="https://mastodon.social/@jondavis">Mastodon</a>. You can follow WebKit <a href="https://www.linkedin.com/in/apple-webkit/">on LinkedIn</a>.</p>
<p>If you run into any issues, we welcome your <a href="https://bugs.webkit.org/">bug report</a>. Filing issues really does make a difference.</p>
<p>You can also find this information in the <a href="https://developer.apple.com/documentation/safari-release-notes/">Safari release notes</a>.</p>
