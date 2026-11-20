# Kkeep CDN launcher

A small, original SVG launcher that displays the live Kkeep website in a full-size iframe. It opens Kkeep automatically and provides a compact **•••** menu for reloading or opening Kkeep directly.

## What it runs

The launcher is served by jsDelivr; the embedded website continues to run at **https://kkeep.fun/**. This preserves Kkeep's existing frontend, server endpoints, updates, and browser origin. The launcher contains no analytics and stores no authentication tokens or other user data.

This implementation is a live-site iframe launcher. The reference website bundles its frontend inside SVG; this project embeds Kkeep's existing website instead.

This is an embedded live website, not an independent copy of Kkeep or a proxy server hosted by jsDelivr. Kkeep's hosting must remain available. If a network cannot reach Kkeep, the launcher cannot supply the missing website.

## Public URLs

Open the public launcher:

```text
https://cdn.jsdelivr.net/gh/KJah8273/kkeep-cdn@main/index.svg
```

For a fixed, reproducible launcher version, replace `COMMIT_SHA` with the full published commit hash:

```text
https://cdn.jsdelivr.net/gh/KJah8273/kkeep-cdn@COMMIT_SHA/index.svg
```

The `@main` version can be cached. A commit URL remains fixed; publish a new commit and use its URL when changing the launcher. Kkeep itself still loads live in either case.

Open the SVG URL as a webpage. Loading it as an image with an `<img>` element does not run this launcher.

## Sharing a Kkeep route

Use the optional, URL-encoded `path` parameter:

```text
https://cdn.jsdelivr.net/gh/KJah8273/kkeep-cdn@main/index.svg?path=%2Fplay%2Fblumgi-racers
```

Only paths on `https://kkeep.fun` are accepted. Schemes, protocol-relative addresses, backslashes, control characters, and malformed encoding are rejected and fall back to the homepage. The **Reload Kkeep** and **Open Kkeep directly** controls use the original requested route. Navigation inside the cross-origin frame is not mirrored into the launcher address.

## Browser behavior and limits

- An iframe `load` event hides the opening overlay; it does not prove that the app, login, or a game is healthy. The tools menu remains available. If no load event arrives within 15 seconds, the launcher shows retry and direct-opening options.
- Kkeep must permit embedding. `Content-Security-Policy: frame-ancestors` and `X-Frame-Options` headers can prevent the iframe from displaying.
- Kkeep cookies marked `SameSite=Strict` are not available to a cross-site embedded session. Safari and iPad browsers also restrict third-party cookies. Profile login or session persistence can therefore require **Open Kkeep directly**. This launcher does not bypass those protections or copy credentials into the shared jsDelivr origin.
- Fullscreen, autoplay, encrypted media, picture-in-picture, gamepad, and clipboard-write are delegated to the frame, subject to browser support, browser policy, and user gestures. Camera and microphone are not delegated. Existing game/device compatibility limits remain.
- The page uses its own SVG/XHTML markup and JavaScript. It does not include the reference website's code, branding, advertising, or tracking.

## Validation

The SVG must parse as XML, and its CDATA JavaScript must pass a syntax check. Deployment should additionally be checked in a browser, including opening Kkeep, in-frame navigation, the tools menu, a representative game, and the direct-opening fallback. XML and syntax checks alone do not verify login or game compatibility.
