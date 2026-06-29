# DSober invite web (source of truth)

These files are deployed to the **`yousifabuhaija.github.io`** user-root GitHub
Pages site. They power invite links (Track C, Phase 2):

| Path served at the domain root | File | Purpose |
|---|---|---|
| `/.well-known/apple-app-site-association` | `.well-known/apple-app-site-association` | Apple App Site Association — tells iOS that `https://yousifabuhaija.github.io/i/*` Universal Links belong to the DSober app (`FRKF7H5XZ5.com.yousifabuhaija.DSober`). **Must** live at the domain root, which is why this needs the user-root repo (not the `/DSober/` project pages). |
| `/i/` | `i/index.html` | Invite landing page. Installed users open the app directly via the Universal Link; everyone else gets "Get DSober" → copies the invite URL to the clipboard → App Store, so the freshly-installed app can read the clipboard and auto-join the right chapter. |
| `/` | `index.html` | Redirects to `/i/` (a generic install page when there's no `?t=` token). |

## Deploy

The user-root repo serves GitHub Pages from `main` / root. To publish, copy the
contents of this `web/` folder to the root of the `yousifabuhaija.github.io` repo
and push. (The first Phase-2 setup created that repo from these files.)

## Notes
- Invite link format: `https://yousifabuhaija.github.io/i/?t=<token>`.
- Universal Links also require `ios.associatedDomains: ["applinks:yousifabuhaija.github.io"]`
  in `app.json` + the **Associated Domains** capability on the App ID, then a
  native rebuild + a new TestFlight/App Store build (they can't be shipped OTA).
- Universal Links only activate on a real device (not the simulator), after Apple's
  CDN has fetched the AASA.
