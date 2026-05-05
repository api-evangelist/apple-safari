---
title: "WebKit features for Safari 26.3"
url: "https://webkit.org/blog/17798/webkit-features-for-safari-26-3/"
date: "Wed, 11 Feb 2026 18:00:49 +0000"
author: ""
feed_url: "https://webkit.org/feed/"
---
<p>Safari 26.3 is here, with practical improvements for performance and user experience. This release gives you new tools for optimizing how your content is delivered and better control over navigation in single-page applications. We’ve also fixed issues developers have run into with anchor positioning, multi-column layouts, and other features — making them more robust and reliable. Plus, we’ve refined the everyday browsing experience by fixing issues we found while testing real websites.</p>
<h3>Video in visionOS</h3>
<p>Now in Safari 26.3 in visionOS, fullscreen video playback automatically dims the user’s surroundings to help put the focus on content.</p>
<figure><img alt="A floating rectangular image of a dog running at a dog show, covered by the site &quot;The Ultimate Spectacular&quot;. This rectangle is floating in a world covered by sandy hills, with mountains in the background, and a big cloudy sky above. This is a 3D environment in visionOS. The image is a video that&#039;s full brightness, while the environment around it is not as bright as normal. It&#039;s dimmed." class="aligncenter size-full wp-image-17799 preserve-color" height="1080" src="https://webkit.org/wp-content/uploads/world_around_video_dimmed_Safari263_visionOS.png" width="1920" /><figcaption>Now when a user plays a video in Safari (like <a href="https://www.youtube.com/watch?v=Z6wnDWzhaDA">this trailer</a> on YouTube for <a href="https://tv.apple.com/us/show/top-dogs/umc.cmc.6snqtei46tkkch7odsnoq9nac"><i>Top Dogs</i></a>) and enters fullscreen, the world around the video is dimmed in visionOS 26.3.</figcaption></figure>
<h2>Zstandard</h2>
<p>Safari 26.3 supports Zstandard (Zstd), a compression algorithm you can use to make your website’s files smaller before sending them to browsers. Like gzip and Brotli, it compresses text-based assets — HTML, CSS, JavaScript, JSON, and SVG — so less data travels over the network.</p>
<p>Zstandard decompresses quickly, reducing the workload on users’ devices. It also compresses fast enough to do on-the-fly, whereas Brotli is typically pre-compressed during your build process.</p>
<p>To use it, configure your server to compress responses with Zstandard and send the <code>Content-Encoding: zstd</code> header. Servers will automatically fall back to other compression methods for browsers that don’t have support yet.</p>
<p>Zstandard support is available in Safari 26.3 on iOS 26.3, iPadOS 26.3, visionOS 26.3, and macOS Tahoe 26.3 — and not in Safari 26.3 on earlier versions of macOS. This is because support comes from the system networking stack used by Safari.</p>
<h2>Navigation API</h2>
<p>When building single-page applications with the Navigation API, you might need a reliable way to cancel ongoing work when a navigation gets interrupted. Maybe the user clicked another link before the previous navigation finished, they hit the back button, or your code called <code>navigation.navigate()</code> again. Whatever the reason, you don’t want to keep processing a navigation that&#8217;s no longer relevant.</p>
<p>In Safari 26.3, the Navigation API exposes a <code>AbortSignal</code> on <code>NavigateEvent</code> which triggers when the navigation is aborted, giving you a standard way to clean up and cancel work:</p>
<pre><code class="js"><span class="identifier">navigation</span>.<span class="identifier">addEventListener</span>(<span class="char">'navigate'</span>, (<span class="identifier">event</span>) <span class="operator">=</span><span class="operator">&gt;</span> {
  <span class="identifier">event</span>.<span class="identifier">intercept</span>({
    <span class="identifier">async</span> <span class="identifier">handler</span>() {
      <span class="keyword type">const</span> <span class="identifier">response</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">fetch</span>(<span class="char">'/api/data'</span>, {
        <span class="identifier">signal</span><span class="operator">:</span> <span class="identifier">event</span>.<span class="identifier">signal</span>  <span class="comment">// Automatically cancels if navigation is aborted
</span>      });

      <span class="keyword type">const</span> <span class="identifier">data</span> <span class="operator">=</span> <span class="identifier">await</span> <span class="identifier">response</span>.<span class="identifier">json</span>();
      <span class="identifier">renderContent</span>(<span class="identifier">data</span>);
    }
  });
});
</code></pre>
<p>If the user navigates away before the fetch completes, the request automatically cancels. You can also listen to the signal’s <code>abort</code> event to clean up other resources like timers or animations.</p>
<p>This gives you fine-grained control over what happens when navigations don’t complete, helping you avoid memory leaks and unnecessary work.</p>
<h2>Bug fixes and more</h2>
<p>Along with the new features, WebKit for Safari 26.3 includes additional improvements to existing features.</p>
<h3>CSS</h3>
<ul>
<li>Fixed a style resolution loop that occurred when a <code>position-try</code> box was inside a <code>display: none</code> ancestor. (163691885)</li>
<li>Fixed an issue where anchor-positioned elements repeatedly transitioning from <code>display: block</code> to <code>display: none</code> cause position jumps during animation. (163862003)</li>
<li>Fixed an issue where <code>fixed</code>-positioned boxes using <code>position-area</code> were incorrectly included in the scrollable containing block calculation. (164017310)</li>
<li>Fixed an issue where <code>text-decoration: underline</code> was rendered too high when <code>text-box-trim</code> was applied to the root inline box. (165945326)</li>
<li>Fixed a multi-column layout issue where the <code>widows</code> and <code>text-indent</code> properties are applied cause an incorrect indent on the portion of the paragraph that flows into the next column. (165945497)</li>
<li>Fixed an issue where CSS cursors like <code>move</code>, <code>all-scroll</code>, <code>ew-resize</code>, and <code>ns-resize</code> did not display correctly. (166731882)</li>
</ul>
<h3>DOM</h3>
<ul>
<li>Fixed incorrect timestamp handling and switched to use the raw touch timestamp. (164262652)</li>
</ul>
<h3>Media</h3>
<ul>
<li>Fixed an issue where the fullscreen button in visionOS inline video controls did not visually indicate interactivity by extending the glow effect to all <code>button.circular</code> elements. (164259201)</li>
<li>Fixed Video Viewer mode for <code>iframe</code> videos on macOS. (164484608)</li>
<li>Fixed an issue where Safari could not play live videos when the <code>sourceBuffer</code> content is removed and re-added causing the seek to not complete. (165628836)</li>
</ul>
<h3>Rendering</h3>
<ul>
<li>Fixed an issue where positioned or transformed <code>&lt;img&gt;</code> elements containing HDR JPEGs with gain maps would incorrectly render as SDR. (163517157)</li>
</ul>
<h3>Safe Browsing</h3>
<ul>
<li>Fixed a bug where if Safe Browsing queried for an entry on the Public Suffix List, and a Safe Browsing vendor responded that the whole effective TLD was unsafe, the whole site would be marked as unsafe. (168155375)</li>
</ul>
<h2>Feedback</h2>
<p>We love hearing from you. To share your thoughts, find us online: Jen Simmons on <a href="https://bsky.app/profile/jensimmons.bsky.social">Bluesky</a> / <a href="https://front-end.social/@jensimmons">Mastodon</a>, Saron Yitbarek on <a href="https://bsky.app/profile/saron.bsky.social">BlueSky</a> / <a href="https://front-end.social/@saron">Mastodon</a>, and Jon Davis on <a href="https://bsky.app/profile/jondavis.bsky.social">Bluesky</a> / <a href="https://mastodon.social/@jondavis">Mastodon</a>. You can follow WebKit <a href="https://www.linkedin.com/in/apple-webkit/">on LinkedIn</a>.</p>
<p>If you run into any issues, we welcome your <a href="https://bugs.webkit.org/">bug report</a>. Filing issues really does make a difference.</p>
<p>You can also find this information in the <a href="https://developer.apple.com/documentation/safari-release-notes/">Safari release notes</a>.</p>
