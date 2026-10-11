# Add inline public results to experience search

[View pull request #335](https://github.com/NotValra/RoValra/pull/335)

The feature branch is published at `cc297291fb9c97eb6ce94c4356fff7076fa76b79`. The three feature test files have been removed from the pull request. Settings localization remains unchanged for Valra's review.

[Copy the updated PR description](https://github.com/mattstellar/RoValra/blob/screenshots/public-game-discovery/public-game-search/pr-body.md). The GitHub connector could not edit the upstream description because its token lacks permission; use this text to update the existing PR.

Adds an opt-in **Public Game Discovery** setting under Experiences. On `/discover/?keyword=...`, a **Public results** switch displays anonymous search results inline; switching it off restores Roblox's normal results. It uses the existing navbar search, filters the loaded games by content maturity, and supports pagination and retry.

Search requests omit account credentials and bound authentication. Cards link to ordinary Roblox game pages, where Roblox continues to enforce age and parental restrictions. The implementation reuses the shared observer, toggle, dropdown, cards, thumbnails, and localization. Query changes use the existing URL watcher; pending requests are cancelled during navigation or cleanup. Keyboard focus is preserved during loading and result updates.

The setting defaults to off. Contributor credit: `1955001309` (mattstellar). English UI strings were AI-assisted and reviewed for accuracy. No extension dependencies or permissions changed.

### Draft limitation

**This has not demonstrated a fix for the requested Kids/Select discovery restriction.** In the [recorded Everest check](https://github.com/mattstellar/RoValra/blob/screenshots/public-game-discovery/public-game-search/everest-check.json), the game displayed Minimal maturity with a 16+ audience but was absent from the bounded anonymous searches. Further pagination stopped after HTTP 429 responses. Authenticated age-checked 16+ versus Kids/Select visibility remains unverified. Public search is not equivalent to an adult account, and these results do not establish a moderation cause.

### Validation

- Before removal, local API credential-isolation, URL-change, and Chromium checks passed for mode switching, filtering, pagination/retry, cancellation, sanitization, thumbnails, cleanup, navigation, keyboard focus, and mobile layout. The three test files have been removed from this PR following review feedback.
- The previous live signed-out check returned 40 games and 40 correct thumbnails; switching off restored native results. No feature JavaScript errors, text overlaps, or horizontal overflow at 1440px and 390px.
- Chrome/Firefox builds passed after removing the test files. Targeted ESLint had zero errors and six existing API warnings. Firefox extension lint had zero errors/notices and 280 existing bundled warnings.

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
npm run lint:firefox
```

(not sure if this works,bare with me here)

