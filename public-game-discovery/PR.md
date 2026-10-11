# Add opt-in public game discovery on Charts

Adds an opt-in **Public Game Discovery** setting under Experiences. When enabled, Charts and Discover show **Browse public games**, with public popular games, title search, maturity filters, and search pagination. This gives users another way to discover games independently of their account's personalized results. Maturity filters apply to the loaded results.

Discovery and search requests omit account credentials and bound authentication. Cards open normal Roblox game pages, where Roblox's age requirements and parental settings continue to apply. The shared API helper also keeps public and authenticated requests separate when deduplicating requests.

The feature uses existing UI components, the shared observer, and localization, and defaults to off. No extension permissions or dependencies changed. Contributor credit: `1955001309` (mattstellar). English UI strings were AI-assisted and reviewed for accuracy; no other language translations changed.

### Validation

- API credential-isolation regression checks passed, and fail against the original API implementation.
- Chromium integration checks passed for opt-in behavior, localized routes, maturity filtering, search/pagination, deduplication, sanitized titles, ordinary game links, empty/error recovery, cancellation, cleanup, and keyboard/focus behavior.
- A live signed-out Roblox smoke check returned 98 popular games and 40 cart-ride search results, with both endpoints returning HTTP 200, all 40 search thumbnails loaded, no JavaScript errors, and no card text overlap.
- Chrome and Firefox builds passed. Changed-file ESLint had zero errors and six existing warnings; Firefox extension lint had zero errors/notices and 280 bundled warnings.

### Testing limit

The exact younger-account 13+/16+ discovery case in the suggestion remains unverified because a suitable account/game example was unavailable. This adds a separate public browser; Roblox controls which results its public APIs return. The native maturity menu retains Roblox's filters. A 16+ publishing audience is separate from a game's maturity label, so the browser displays the labels returned by Roblox.

### Screenshots

These show the actual signed-out Roblox Charts page with the feature and shared components injected into an isolated verification browser. They demonstrate the UI and live public results, and are not a younger-account test.

**Before enabling**

![Charts before enabling Public Game Discovery](https://raw.githubusercontent.com/mattstellar/RoValra/0e3762fe8c946eb5a12f6fe4791b825909033aaf/public-game-discovery/live-before.svg)

**After enabling**

![Charts with Browse public games enabled](https://raw.githubusercontent.com/mattstellar/RoValra/0e3762fe8c946eb5a12f6fe4791b825909033aaf/public-game-discovery/live-after.svg)

**Public cart-ride search**

![Public game discovery showing live cart-ride results](https://raw.githubusercontent.com/mattstellar/RoValra/0e3762fe8c946eb5a12f6fe4791b825909033aaf/public-game-discovery/live.svg)

### Reproducing the checks

```sh
npm ci
node scripts/tests/api-credentials.test.cjs
npm install --no-save --package-lock=false playwright
npx playwright install chromium
node scripts/tests/public-game-discovery.test.cjs
npm run build
npm run lint:firefox
```

Playwright is an optional local verification tool, not an extension dependency.
