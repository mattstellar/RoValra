# Add inline public results to experience search

[Open the prefilled pull request in the original repository](https://github.com/NotValra/RoValra/compare/main...mattstellar:RoValra:feature/browse-all-maturity?quick_pull=1&title=Add%20inline%20public%20results%20to%20experience%20search&body=Adds%20an%20opt-in%20**Public%20Game%20Discovery**%20setting%20under%20Experiences.%20On%20%60%2Fdiscover%2F%3Fkeyword%3D...%60%2C%20a%20**Public%20results**%20switch%20displays%20anonymous%20search%20results%20inline%3B%20switching%20it%20off%20restores%20Roblox's%20normal%20results.%20It%20uses%20the%20existing%20navbar%20search%2C%20filters%20the%20loaded%20games%20by%20content%20maturity%2C%20and%20supports%20pagination%20and%20retry.%0A%0ASearch%20requests%20omit%20account%20credentials%20and%20bound%20authentication.%20Cards%20link%20to%20ordinary%20Roblox%20game%20pages%2C%20where%20Roblox%20continues%20to%20enforce%20age%20and%20parental%20restrictions.%20The%20implementation%20reuses%20the%20shared%20observer%2C%20toggle%2C%20dropdown%2C%20cards%2C%20thumbnails%2C%20and%20localization.%20Query%20changes%20use%20the%20existing%20URL%20watcher%3B%20pending%20requests%20are%20cancelled%20during%20navigation%20or%20cleanup.%20Keyboard%20focus%20is%20preserved%20during%20loading%20and%20result%20updates.%0A%0AThe%20setting%20defaults%20to%20off.%20Contributor%20credit%3A%20%601955001309%60%20(mattstellar).%20English%20UI%20strings%20were%20AI-assisted%20and%20reviewed%20for%20accuracy.%20No%20extension%20dependencies%20or%20permissions%20changed.%0A%0A%23%23%23%20Draft%20limitation%0A%0A**This%20has%20not%20demonstrated%20a%20fix%20for%20the%20requested%20Kids%2FSelect%20discovery%20restriction.**%20In%20the%20%5Brecorded%20Everest%20check%5D(https%3A%2F%2Fgithub.com%2Fmattstellar%2FRoValra%2Fblob%2Fscreenshots%2Fpublic-game-discovery%2Fpublic-game-search%2Feverest-check.json)%2C%20the%20game%20displayed%20Minimal%20maturity%20with%20a%2016%2B%20audience%20but%20was%20absent%20from%20the%20bounded%20anonymous%20searches.%20Further%20pagination%20stopped%20after%20HTTP%20429%20responses.%20Authenticated%20age-checked%2016%2B%20versus%20Kids%2FSelect%20visibility%20remains%20unverified.%20Public%20search%20is%20not%20equivalent%20to%20an%20adult%20account%2C%20and%20these%20results%20do%20not%20establish%20a%20moderation%20cause.%0A%0A%23%23%23%20Validation%0A%0A-%20API%20credential%20isolation%20and%20URL-change%20regression%20checks%20passed.%0A-%20Chromium%20integration%20checks%20passed%20for%20mode%20switching%2C%20filtering%2C%20pagination%2Fretry%2C%20cancellation%2C%20sanitization%2C%20thumbnails%2C%20cleanup%2C%20navigation%2C%20keyboard%20focus%2C%20and%20mobile%20layout.%20The%20new%20keyboard%20regressions%20fail%20the%20old%20implementation.%0A-%20Final%20live%20signed-out%20check%20returned%2040%20games%20and%2040%20correct%20thumbnails%3B%20switching%20off%20restored%20native%20results.%20No%20feature%20JavaScript%20errors%2C%20text%20overlaps%2C%20or%20horizontal%20overflow%20at%201440px%20and%20390px.%0A-%20Chrome%2FFirefox%20builds%20passed.%20Targeted%20ESLint%20had%20zero%20errors%20and%20six%20existing%20API%20warnings.%20Feature%2Ftest%20formatting%20checks%20passed%3B%20existing%20shared-file%20formatting%20differences%20were%20confirmed%20against%20the%20base.%20Firefox%20extension%20lint%20had%20zero%20errors%2Fnotices%20and%20280%20existing%20bundled%20warnings.%0A%0A%23%23%23%20Screenshots%0A%0ACaptured%20using%20the%20actual%20feature%20and%20shared%20components%20injected%20into%20an%20isolated%20signed-out%20browser.%20These%20show%20the%20UI%20and%20live%20results%2C%20not%20an%20authenticated%20younger-account%20test.%0A%0A**Before**%0A%0A!%5BNormal%20Roblox%20search%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F3c5075d73e82a7d7908243141bfdc4532eeda702%2Fpublic-game-search%2Fbefore.svg)%0A%0A**Public%20results%20enabled**%0A%0A!%5BPublic%20results%20inline%20on%20search%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F3c5075d73e82a7d7908243141bfdc4532eeda702%2Fpublic-game-search%2Fpublic.svg)%0A%0A**Mobile**%0A%0A!%5BPublic%20search%20on%20mobile%5D(https%3A%2F%2Fraw.githubusercontent.com%2Fmattstellar%2FRoValra%2F3c5075d73e82a7d7908243141bfdc4532eeda702%2Fpublic-game-search%2Fmobile.svg)%0A%0A%23%23%23%20Reproduce%20checks%0A%0A%60%60%60sh%0Anpm%20ci%0Anpm%20run%20build%0Anode%20scripts%2Ftests%2Fapi-credentials.test.cjs%0Anode%20scripts%2Ftests%2Furl-changes.test.cjs%0Anpm%20install%20--no-save%20--package-lock%3Dfalse%20playwright%0Anpx%20playwright%20install%20chromium%0Anode%20scripts%2Ftests%2Fpublic-game-discovery.test.cjs%0Anpm%20run%20lint%3Afirefox%0A%60%60%60%0A%0APlaywright%20is%20an%20optional%20local%20verification%20tool%2C%20not%20an%20extension%20dependency.%0A)

Use the arrow beside **Create pull request** and choose **Create draft pull request**. The title, description, and screenshots are prefilled. The code branch is published at `d76c0c53b40e6970fd548638155fb3aa2ce7a081`; no upstream PR has been created by the connector.

Adds an opt-in **Public Game Discovery** setting under Experiences. On `/discover/?keyword=...`, a **Public results** switch displays anonymous search results inline; switching it off restores Roblox's normal results. It uses the existing navbar search, filters the loaded games by content maturity, and supports pagination and retry.

Search requests omit account credentials and bound authentication. Cards link to ordinary Roblox game pages, where Roblox continues to enforce age and parental restrictions. The implementation reuses the shared observer, toggle, dropdown, cards, thumbnails, and localization. Query changes use the existing URL watcher; pending requests are cancelled during navigation or cleanup. Keyboard focus is preserved during loading and result updates.

The setting defaults to off. Contributor credit: `1955001309` (mattstellar). English UI strings were AI-assisted and reviewed for accuracy. No extension dependencies or permissions changed.

### Draft limitation

**This has not demonstrated a fix for the requested Kids/Select discovery restriction.** In the [recorded Everest check](https://github.com/mattstellar/RoValra/blob/screenshots/public-game-discovery/public-game-search/everest-check.json), the game displayed Minimal maturity with a 16+ audience but was absent from the bounded anonymous searches. Further pagination stopped after HTTP 429 responses. Authenticated age-checked 16+ versus Kids/Select visibility remains unverified. Public search is not equivalent to an adult account, and these results do not establish a moderation cause.

### Validation

- API credential isolation and URL-change regression checks passed.
- Chromium integration checks passed for mode switching, filtering, pagination/retry, cancellation, sanitization, thumbnails, cleanup, navigation, keyboard focus, and mobile layout. The new keyboard regressions fail the old implementation.
- Final live signed-out check returned 40 games and 40 correct thumbnails; switching off restored native results. No feature JavaScript errors, text overlaps, or horizontal overflow at 1440px and 390px.
- Chrome/Firefox builds passed. Targeted ESLint had zero errors and six existing API warnings. Feature/test formatting checks passed; existing shared-file formatting differences were confirmed against the base. Firefox extension lint had zero errors/notices and 280 existing bundled warnings.

### Screenshots

Captured using the actual feature and shared components injected into an isolated signed-out browser. These show the UI and live results, not an authenticated younger-account test.

**Before**

![Normal Roblox search](https://raw.githubusercontent.com/mattstellar/RoValra/3c5075d73e82a7d7908243141bfdc4532eeda702/public-game-search/before.svg)

**Public results enabled**

![Public results inline on search](https://raw.githubusercontent.com/mattstellar/RoValra/3c5075d73e82a7d7908243141bfdc4532eeda702/public-game-search/public.svg)

**Mobile**

![Public search on mobile](https://raw.githubusercontent.com/mattstellar/RoValra/3c5075d73e82a7d7908243141bfdc4532eeda702/public-game-search/mobile.svg)

### Reproduce checks

```sh
npm ci
npm run build
node scripts/tests/api-credentials.test.cjs
node scripts/tests/url-changes.test.cjs
npm install --no-save --package-lock=false playwright
npx playwright install chromium
node scripts/tests/public-game-discovery.test.cjs
npm run lint:firefox
```

Playwright is an optional local verification tool, not an extension dependency.
