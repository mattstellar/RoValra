# Add inline public results to experience search

[Open the prefilled pull request in the original repository](https://github.com/NotValra/RoValra/compare/main...mattstellar:RoValra:feature/browse-all-maturity?quick_pull=1&title=Add%20inline%20public%20results%20to%20experience%20search&body=Adds%20an%20opt-in%20**Public%20Game%20Discovery**%20setting%20under%20Experiences.%20On%20%60%2Fdiscover%2F%3Fkeyword%3D...%60%2C%20it%20adds%20a%20**Public%20results**%20switch.%20Turning%20it%20on%20displays%20public%20game%20search%20results%20inline%3B%20turning%20it%20off%20restores%20Roblox's%20normal%20results.%20It%20uses%20the%20existing%20navbar%20search%20term%2C%20with%20maturity%20filtering%20and%20pagination%20in%20the%20result%20area.%0A%0APublic%20search%20requests%20omit%20account%20credentials%20and%20bound%20authentication.%20Cards%20open%20ordinary%20Roblox%20game%20pages%2C%20where%20Roblox's%20age%20requirements%20and%20parental%20settings%20continue%20to%20apply.%20The%20API%20helper%20separates%20anonymous%20and%20authenticated%20requests%20during%20deduplication.%0A%0AThe%20feature%20uses%20the%20shared%20observer%2C%20toggle%2C%20dropdown%2C%20game%20card%2C%20thumbnail%20helper%2C%20and%20localization.%20Wide%20thumbnails%20use%20root-place%20IDs%20and%20match%20search's%2016%3A9%20card%20shape.%20The%20existing%20URL%20watcher%20now%20dispatches%20changes%20for%20new%20keywords%20without%20rerunning%20unrelated%20route%20features.%0A%0AThe%20setting%20defaults%20to%20off%2C%20and%20normal%20results%20remain%20selected%20until%20the%20user%20switches%20modes.%20Contributor%20credit%3A%20%601955001309%60%20(mattstellar).%20English%20UI%20strings%20were%20AI-assisted%20and%20reviewed%20for%20accuracy%3B%20no%20other%20translations%2C%20extension%20permissions%2C%20or%20dependencies%20changed.%0A%0A%23%23%23%20Validation%0A%0A-%20API%20credential-isolation%20regression%20tests%20and%20URL%20watcher%20tests%20passed.%0A-%20Chromium%20integration%20tests%20passed%20for%20opt-in%20behavior%2C%20localized%20search%2C%20mode%20switching%2C%20filtering%2C%20pagination%2Fdeduplication%2C%20retry%2C%20unknown%20maturity%20labels%2C%20input%20sanitization%2C%20correct%20thumbnail%20IDs%2C%20stale%20cancellation%2C%20root%20replacement%2C%20setting%20cleanup%2C%20Back%2FForward%2C%20keyboard%20focus%2C%20and%20mobile%20layout.%0A-%20Live%20signed-out%20search%20returned%20HTTP%20200%20with%20credentials%20omitted%20and%2040%20results.%20The%20actual%20shared%20thumbnail%20helper%20returned%2040%20correct%20wide%20thumbnails.%20Desktop%20(1440px)%20and%20mobile%20(390px)%20had%20no%20text%20overlap%20or%20horizontal%20overflow%2C%20and%20switching%20off%20restored%20native%20results.%20No%20JavaScript%20page%20errors.%0A-%20Chrome%20and%20Firefox%20builds%20passed.%20Changed%20search%2Fwatch%2Ftest%20JavaScript%20passed%20ESLint%20with%20no%20errors%20or%20warnings.%20Firefox%20extension%20lint%20had%20zero%20errors%2Fnotices%20and%20280%20existing%20bundled%20warnings.%0A%0A%23%23%23%20Testing%20limit%0A%0AThe%20exact%20younger-account%2013%2B%2F16%2B%20discovery%20case%20remains%20unverified%20because%20a%20suitable%20account%2Fgame%20example%20was%20unavailable.%20Roblox%20controls%20which%20results%20its%20public%20search%20API%20returns%2C%20so%20this%20does%20not%20promise%20a%20complete%20catalog.%20Maturity%20filters%20apply%20to%20loaded%20pages%20and%20display%20Roblox's%20actual%20maturity%20labels.%0A%0A%23%23%23%20Screenshots%0A%0ACaptured%20on%20the%20live%20signed-out%20search%20page%20with%20the%20actual%20feature%2Fshared%20components%20injected%20into%20an%20isolated%20verification%20browser.%20These%20demonstrate%20live%20results%20and%20UI%3B%20they%20are%20not%20a%20younger-account%20test.%0A%0A**Before**%0A%0A!%5BRoblox%20search%20before%20enabling%20the%20feature%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F51a26e7807f14fb574d5891785aa1b9c5037f156%2Fpublic-game-search%2Fbefore.svg)%0A%0A**Public%20results%20enabled**%0A%0A!%5BPublic%20search%20results%20integrated%20inline%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F51a26e7807f14fb574d5891785aa1b9c5037f156%2Fpublic-game-search%2Fpublic.svg)%0A%0A**Mobile**%0A%0A!%5BInline%20public%20search%20on%20mobile%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F51a26e7807f14fb574d5891785aa1b9c5037f156%2Fpublic-game-search%2Fmobile.svg)%0A%0A%23%23%23%20Reproducing%20the%20checks%0A%0A%60%60%60sh%0Anpm%20ci%0Anode%20scripts%2Ftests%2Fapi-credentials.test.cjs%0Anode%20scripts%2Ftests%2Furl-changes.test.cjs%0Anpm%20install%20--no-save%20--package-lock%3Dfalse%20playwright%0Anpx%20playwright%20install%20chromium%0Anode%20scripts%2Ftests%2Fpublic-game-discovery.test.cjs%0Anpm%20run%20build%0Anpm%20run%20lint%3Afirefox%0A%60%60%60%0A%0APlaywright%20is%20an%20optional%20local%20verification%20tool%2C%20not%20an%20extension%20dependency.%0A)

On GitHub, use the arrow beside **Create pull request** and choose **Create draft pull request**. The title, description, and screenshots are prefilled.

Adds an opt-in **Public Game Discovery** setting under Experiences. On `/discover/?keyword=...`, it adds a **Public results** switch. Turning it on displays public game search results inline; turning it off restores Roblox's normal results. It uses the existing navbar search term, with maturity filtering and pagination in the result area.

Public search requests omit account credentials and bound authentication. Cards open ordinary Roblox game pages, where Roblox's age requirements and parental settings continue to apply. The API helper separates anonymous and authenticated requests during deduplication.

The feature uses the shared observer, toggle, dropdown, game card, thumbnail helper, and localization. Wide thumbnails use root-place IDs and match search's 16:9 card shape. The existing URL watcher now dispatches changes for new keywords without rerunning unrelated route features.

The setting defaults to off, and normal results remain selected until the user switches modes. Contributor credit: `1955001309` (mattstellar). English UI strings were AI-assisted and reviewed for accuracy; no other translations, extension permissions, or dependencies changed.

### Validation

- API credential-isolation regression tests and URL watcher tests passed.
- Chromium integration tests passed for opt-in behavior, localized search, mode switching, filtering, pagination/deduplication, retry, unknown maturity labels, input sanitization, correct thumbnail IDs, stale cancellation, root replacement, setting cleanup, Back/Forward, keyboard focus, and mobile layout.
- Live signed-out search returned HTTP 200 with credentials omitted and 40 results. The actual shared thumbnail helper returned 40 correct wide thumbnails. Desktop (1440px) and mobile (390px) had no text overlap or horizontal overflow, and switching off restored native results. No JavaScript page errors.
- Chrome and Firefox builds passed. Changed search/watch/test JavaScript passed ESLint with no errors or warnings. Firefox extension lint had zero errors/notices and 280 existing bundled warnings.

### Testing limit

The exact younger-account 13+/16+ discovery case remains unverified because a suitable account/game example was unavailable. Roblox controls which results its public search API returns, so this does not promise a complete catalog. Maturity filters apply to loaded pages and display Roblox's actual maturity labels.

### Screenshots

Captured on the live signed-out search page with the actual feature/shared components injected into an isolated verification browser. These demonstrate live results and UI; they are not a younger-account test.

**Before**

![Roblox search before enabling the feature](https://raw.githubusercontent.com/mattstellar/RoValra/51a26e7807f14fb574d5891785aa1b9c5037f156/public-game-search/before.svg)

**Public results enabled**

![Public search results integrated inline](https://raw.githubusercontent.com/mattstellar/RoValra/51a26e7807f14fb574d5891785aa1b9c5037f156/public-game-search/public.svg)

**Mobile**

![Inline public search on mobile](https://raw.githubusercontent.com/mattstellar/RoValra/51a26e7807f14fb574d5891785aa1b9c5037f156/public-game-search/mobile.svg)

### Reproducing the checks

```sh
npm ci
node scripts/tests/api-credentials.test.cjs
node scripts/tests/url-changes.test.cjs
npm install --no-save --package-lock=false playwright
npx playwright install chromium
node scripts/tests/public-game-discovery.test.cjs
npm run build
npm run lint:firefox
```

Playwright is an optional local verification tool, not an extension dependency.
