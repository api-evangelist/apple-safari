---
name: send-a-web-push
description: Send a Web Push notification to a Safari subscriber against Apple's push service, with the correct VAPID auth, headers, size limit and error handling.
api: Safari Web Push API
base_url: https://*.push.apple.com
generated: '2026-09-07'
method: generated
source: https://developer.apple.com/documentation/usernotifications/sending-web-push-notifications-in-web-apps-and-browsers
---

# Send a web push to Safari

This is a standards flow, not an Apple-proprietary one: Apple implements RFC 8030 Web
Push with VAPID. If your server already pushes to Chrome or Firefox, the same code
works — the checks below are the ones Safari is strict about.

## Preconditions

- A VAPID key pair for your application server.
- The subscription's endpoint URL and encryption keys, stored from
  `PushManager.subscribe` on the client and associated with the user's account.
- Network egress allowed to `https://*.push.apple.com`.
- TLS with SNI. APNs supports HTTP/1.1 (the default) and HTTP/2; negotiate with ALPN.
- No Apple Developer Program membership is required for web push.

## Steps

1. **Build and encrypt the payload.** It must be **4 KB or less** encrypted. Set
   `Content-Encoding` to the encryption method used; you may omit it only for an empty
   payload.
2. **Mint the VAPID JWT.** Subject must be a URL or a `mailto:` URI. Audience must be the
   origin of the push service you are posting to. Expiry must be **no more than one day**
   ahead. **Do not refresh more often than once per hour** — cache it.
3. **Set the headers.**
   - `Authorization` — the VAPID JWT and the public key. The public key must match the
     one passed to `PushManager.subscribe`.
   - `TTL` — seconds before the message expires. The service may store an undeliverable
     notification for up to 30 days depending on this value, then drops it permanently.
   - `Topic` (optional) — at most 32 URL/filename-safe Base64 characters; the service
     coalesces notifications sharing a topic.
   - `Urgency` (optional) — exactly one of `very-low`, `low`, `normal`, `high`. Use
     `high` to attempt immediate delivery.
4. **POST to the subscription endpoint.** Only `POST`; any other method returns 405.
   On HTTP/1.1 keep at most **100 unacknowledged** pipelined requests in flight; on
   HTTP/2 stay within the server's `SETTINGS_MAX_CONCURRENT_STREAMS`.
5. **Read the response.** `201` is success. Record the `apns-id` response header — it is
   the only correlation identifier this API gives you.
6. **Handle failures by `reason`, not just by status.** The body is a JSON dictionary
   with a `reason` key. See `errors/apple-safari-problem-types.yml` for all 16 codes.
   - `410` — the subscription is dead. **Delete it from your store.** Do not retry.
   - `413` / `PayloadTooLarge` — shrink to 4 KB. Do not retry unchanged.
   - `429` / `TooManyRequests` — too many consecutive sends to that one subscription.
     Back off. **No `Retry-After` header is sent**, so pick your own interval.
   - `403`, `BadJwtToken`, `BadVapidPublicKey`, `VapidPkHashMismatch` — an auth problem,
     not a transient one. Fix the key or the JWT; retrying is pointless.
   - `500`, `503`, `IdleTimeout`, `Shutdown` — retry with backoff, reconnecting if needed.

## Cautions

- **There is no idempotency key and no way to recall a sent notification.** A retry after
  an ambiguous failure can deliver twice. `Topic` coalesces *display*, not submission.
  The only lever you have before sending is `TTL`.
- **Safari does not support invisible push.** Your service worker must present a
  notification to the user immediately on receipt, or Safari revokes push permission for
  the site.
