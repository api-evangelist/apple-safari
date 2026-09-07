---
name: check-responsive-and-media
description: Verify how a page behaves at a specific viewport size and under an emulated CSS media type in real Safari, using the Safari MCP server.
api: Safari MCP server
transport: local-stdio (safaridriver --mcp)
operations:
  - create_tab
  - navigate_to_url
  - wait_for_navigation
  - set_viewport_size
  - set_emulated_media
  - screenshot
  - get_page_content
  - evaluate_javascript
generated: '2026-09-07'
method: generated
source: https://webkit.org/blog/18136/introducing-the-safari-mcp-server-for-web-developers/
---

# Check responsive layout and print styles in Safari

WebKit names "improve compatibility with Safari" as a primary use case for this server:
testing in one engine misses bugs in another. This flow checks a page across viewports
and media types in the real engine rather than in a Chromium approximation.

## Steps

1. `create_tab`, then `navigate_to_url` and `wait_for_navigation`.
2. **Set the viewport.** `set_viewport_size` takes the size in CSS pixels. Step through
   the breakpoints the stylesheet actually declares — read them out of the CSS rather
   than guessing device widths.
3. **Screenshot each breakpoint.** `screenshot` after each `set_viewport_size`. Diff the
   images or describe what moved.
4. **Emulate print.** `set_emulated_media` with `"print"` to check print styles without
   opening a print dialog. Screenshot again.
5. **Measure rather than eyeball where you can.** `evaluate_javascript` with
   `getComputedStyle` or `getBoundingClientRect` on the element in question gives a
   number you can assert on; a screenshot gives an impression.
6. **Reset.** Restore the emulated media and viewport before handing the session back, or
   close the tab with `close_tab`.

## Notes

- Emulating a media type changes what CSS applies; it does not change the actual output
  device. Layout that depends on real print pagination still needs a real print.
- If several pages need checking, reuse one tab (`navigate_to_url`) rather than opening
  many — only one Safari automation session exists at a time.
