---
name: debug-page-in-safari
description: Reproduce and diagnose a rendering or JavaScript bug in real Safari by driving the Safari MCP server — load the page, read the console, inspect the failing network request and capture a screenshot.
api: Safari MCP server
transport: local-stdio (safaridriver --mcp)
operations:
  - create_tab
  - navigate_to_url
  - wait_for_navigation
  - browser_console_messages
  - list_network_requests
  - get_network_request
  - get_page_content
  - screenshot
generated: '2026-09-07'
method: generated
source: https://webkit.org/blog/18136/introducing-the-safari-mcp-server-for-web-developers/
---

# Debug a page in Safari

Every tool named here is a real tool published in WebKit's Safari MCP server
announcement. None are invented. Full input schemas are not published in the
announcement — call `tools/list` against your own install to get them.

## Before you start

The Safari MCP server is local-only. There is no endpoint to call. The user must have
Safari 27 beta or Safari Technology Preview 247+ installed, with:

- `Safari > Settings > Advanced > Show features for web developers`
- `Safari > Settings > Developer > Allow remote automation and external agents`

and the server registered, e.g. `claude mcp add safari-mcp -- "/usr/bin/safaridriver" --mcp`.

Only one Safari instance and one automation session can be active at a time
(`developer.apple.com/documentation/webkit/about-webdriver-for-safari`). If a session is
already attached, do not start a second one.

## Steps

1. **Open a clean tab.** `create_tab` — optionally passing the URL. Automation windows
   start from a clean slate, like a private session; they cannot see the user's history,
   AutoFill or logged-in state, so do not expect a page behind a login to render.
2. **Load the page.** `navigate_to_url`, then `wait_for_navigation` to confirm the load
   finished and to read back the final URL and title. Compare the final URL to the one
   requested — a redirect is often the bug.
3. **Read the console before touching anything.** `browser_console_messages` returns the
   buffered logs for the tab. Do this first; an interaction can flush or add noise.
4. **Look at the network.** `list_network_requests` gives URL, method, status and timing
   for the tab. Pick the failing or slow one, then `get_network_request` for its full
   headers, body and timing.
5. **Read the rendered content.** `get_page_content` extracts the page text in markdown,
   HTML or JSON. Prefer this over a screenshot when you need to reason about structure.
6. **Capture evidence.** `screenshot` returns a PNG of the current page. Attach it to the
   diagnosis; a visual bug is much cheaper to confirm than to describe.
7. **Report before you fix.** State the failing request or console error, the final URL,
   and what you saw rendered. Then change code.

## Notes

- `evaluate_javascript` runs arbitrary script in the page. Use it for measurement
  (`performance.getEntriesByType('navigation')`, computed styles, ARIA checks), not to
  patch the page — a patched page no longer reproduces the bug.
- This surface has no idempotency key and no rate-limit headers; it is a local browser,
  not a metered API. See `conventions/apple-safari-conventions.yml`.
