# Add opt-in public game discovery on Charts

[Open the prefilled pull request in the original repository](https://github.com/NotValra/RoValra/compare/main...mattstellar:RoValra:feature/browse-all-maturity?quick_pull=1&title=Add%20opt-in%20public%20game%20discovery%20on%20Charts&body=Adds%20an%20opt-in%20**Public%20Game%20Discovery**%20setting%20under%20Experiences.%20When%20enabled%2C%20Charts%20and%20Discover%20show%20**Browse%20public%20games**%2C%20with%20public%20popular%20games%2C%20title%20search%2C%20maturity%20filters%2C%20and%20search%20pagination.%20This%20gives%20users%20another%20way%20to%20discover%20games%20independently%20of%20their%20account's%20personalized%20results.%20Maturity%20filters%20apply%20to%20the%20loaded%20results.%0A%0ADiscovery%20and%20search%20requests%20omit%20account%20credentials%20and%20bound%20authentication.%20Cards%20open%20normal%20Roblox%20game%20pages%2C%20where%20Roblox's%20age%20requirements%20and%20parental%20settings%20continue%20to%20apply.%20The%20shared%20API%20helper%20also%20keeps%20public%20and%20authenticated%20requests%20separate%20when%20deduplicating%20requests.%0A%0AThe%20feature%20uses%20existing%20UI%20components%2C%20the%20shared%20observer%2C%20and%20localization%2C%20and%20defaults%20to%20off.%20No%20extension%20permissions%20or%20dependencies%20changed.%20Contributor%20credit%3A%20%601955001309%60%20(mattstellar).%20English%20UI%20strings%20were%20AI-assisted%20and%20reviewed%20for%20accuracy%3B%20no%20other%20language%20translations%20changed.%0A%0A%23%23%23%20Validation%0A%0A-%20API%20credential-isolation%20regression%20checks%20passed%2C%20and%20fail%20against%20the%20original%20API%20implementation.%0A-%20Chromium%20integration%20checks%20passed%20for%20opt-in%20behavior%2C%20localized%20routes%2C%20maturity%20filtering%2C%20search%2Fpagination%2C%20deduplication%2C%20sanitized%20titles%2C%20ordinary%20game%20links%2C%20empty%2Ferror%20recovery%2C%20cancellation%2C%20cleanup%2C%20and%20keyboard%2Ffocus%20behavior.%0A-%20A%20live%20signed-out%20Roblox%20smoke%20check%20returned%2098%20popular%20games%20and%2040%20cart-ride%20search%20results%2C%20with%20both%20endpoints%20returning%20HTTP%20200%2C%20all%2040%20search%20thumbnails%20loaded%2C%20no%20JavaScript%20errors%2C%20and%20no%20card%20text%20overlap.%0A-%20Chrome%20and%20Firefox%20builds%20passed.%20Changed-file%20ESLint%20had%20zero%20errors%20and%20six%20existing%20warnings%3B%20Firefox%20extension%20lint%20had%20zero%20errors%2Fnotices%20and%20280%20bundled%20warnings.%0A%0A%23%23%23%20Testing%20limit%0A%0AThe%20exact%20younger-account%2013%2B%2F16%2B%20discovery%20case%20in%20the%20suggestion%20remains%20unverified%20because%20a%20suitable%20account%2Fgame%20example%20was%20unavailable.%20This%20adds%20a%20separate%20public%20browser%3B%20Roblox%20controls%20which%20results%20its%20public%20APIs%20return.%20The%20native%20maturity%20menu%20retains%20Roblox's%20filters.%20A%2016%2B%20publishing%20audience%20is%20separate%20from%20a%20game's%20maturity%20label%2C%20so%20the%20browser%20displays%20the%20labels%20returned%20by%20Roblox.%0A%0A%23%23%23%20Screenshots%0A%0AThese%20show%20the%20actual%20signed-out%20Roblox%20Charts%20page%20with%20the%20feature%20and%20shared%20components%20injected%20into%20an%20isolated%20verification%20browser.%20They%20demonstrate%20the%20UI%20and%20live%20public%20results%2C%20and%20are%20not%20a%20younger-account%20test.%0A%0A**Before%20enabling**%0A%0A!%5BCharts%20before%20enabling%20Public%20Game%20Discovery%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F0e3762fe8c946eb5a12f6fe4791b825909033aaf%2Fpublic-game-discovery%2Flive-before.svg)%0A%0A**After%20enabling**%0A%0A!%5BCharts%20with%20Browse%20public%20games%20enabled%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F0e3762fe8c946eb5a12f6fe4791b825909033aaf%2Fpublic-game-discovery%2Flive-after.svg)%0A%0A**Public%20cart-ride%20search**%0A%0A!%5BPublic%20game%20discovery%20showing%20live%20cart-ride%20results%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F0e3762fe8c946eb5a12f6fe4791b825909033aaf%2Fpublic-game-discovery%2Flive.svg)%0A%0A%23%23%23%20Reproducing%20the%20checks%0A%0A%60%60%60sh%0Anpm%20ci%0Anode%20scripts%2Ftests%2Fapi-credentials.test.cjs%0Anpm%20install%20--no-save%20--package-lock%3Dfalse%20playwright%0Anpx%20playwright%20install%20chromium%0Anode%20scripts%2Ftests%2Fpublic-game-discovery.test.cjs%0Anpm%20run%20build%0Anpm%20run%20lint%3Afirefox%0A%60%60%60%0A%0APlaywright%20is%20an%20optional%20local%20verification%20tool%2C%20not%20an%20extension%20dependency.%0A)

On GitHub, use the arrow beside **Create pull request** and choose **Create draft pull request**. The title, description, and screenshots are prefilled.

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
