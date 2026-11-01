# fmani.github.io

GitHub Pages user site serving the Bookflow Android app's eBay OAuth App Link
infrastructure (no other content is published).

## Why this exists

eBay's developer portal only accepts `https` Auth accepted/declined URLs, so the
Bookflow app receives the OAuth consent redirect via an Android **App Link** on
this domain instead of a custom-scheme deep link. This is the pattern recommended
by eBay's own Android OAuth library and RFC 8252 (OAuth 2.0 for Native Apps).

## Files

- `.well-known/assetlinks.json` — Android App Links statement: declares that the
  `com.fmani.bookflow` app (debug signing cert SHA-256 `97:7E:0B:4F:…:2F:F4`) may
  handle `https://fmani.github.io/bookflow/auth/ebay/` URLs. Android fetches this
  file to auto-verify the App Link. If the release signing key changes, append its
  fingerprint to the list (do not remove the debug one while debug builds are used).
- `.nojekyll` — disables Jekyll so the dot-directory `.well-known/` is published.
- `bookflow/auth/ebay/index.html` — the page users land on after eBay consent.
  Shows an "Open Bookflow" button carrying the OAuth query parameters into the
  `bookflow://auth/ebay` deep link (fallback if the App Link is not verified or
  the page is opened on a desktop browser).

## Related

- App repo (private): `fmani/bookflow`
- eBay portal: Auth accepted/declined URL must be
  `https://fmani.github.io/bookflow/auth/ebay/`
