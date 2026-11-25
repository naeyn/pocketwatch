# Privacy Policy — Pocketwatch

_Last updated: 2026-11-23_

Pocketwatch is a browser extension that shows CS2 map play and win rates for
both teams in a Faceit match room. It is unofficial and not affiliated with
FACEIT.

## What the extension accesses

- **Your Faceit session token.** While you are logged in to faceit.com, the
  extension reads the session token from the Faceit page (cookie or local
  storage) so it can request match and player statistics on your behalf — the
  same data the Faceit website itself shows you. The token is used solely as
  the `Authorization` header on requests to Faceit and is never stored
  persistently or sent anywhere other than `faceit.com` / `api.faceit.com`.
- **Match and player statistics.** Match rosters, map veto state, and each
  player's recent match statistics and lifetime per-map record (games and wins)
  are fetched from Faceit's servers to build the overlay.
- **The enemy captain's past vetoes.** For "Their captain's drops", the
  extension reads the veto of each of the last few matches the other team's
  captain led, and that match's public page, to see which maps they dropped.
  These reads go to Faceit without your session token or cookies, as an
  anonymous visitor would make them.
- **Leetify public statistics.** For the role pendants and the Leetify
  ratings on the roster hover card, the extension queries the Leetify public API (`api-public.cs-prod.leetify.com`) with the
  public Steam64 game identifiers of the players in the match room to fetch
  their public career statistics. These identifiers are public gaming ids
  exposed by Faceit, not personal data collected from you. Leetify responses
  are cached only in session storage for up to 15 minutes and are never stored
  persistently, per Leetify's developer guidelines. Career-based badges and
  the ratings card carry Leetify's "Data Provided by Leetify" logo and a "View
  on Leetify" link. The
  logo is bundled with the extension, and the links make no request unless you
  click them.
- **Your own Leetify aim, for the session overview.** If you have a Leetify
  account, the session overview shows Leetify's aim numbers for each of your
  session's games. For that the extension asks Leetify for your own public
  profile (`/v3/profile`, by your public Steam64 id) at most once each time the
  overview is built, and not again while that answer is fresh. The answer is
  kept in memory and session storage only, never persisted, and the numbers
  carry the same Leetify logo and "View on Leetify" link. Without a Leetify
  account, Leetify answers that it does not know you and nothing is shown.
- **Your recent games, for the session overview.** When you open the session
  drawer on faceit.com, and every few minutes while a Faceit tab is in view,
  the extension fetches your own recent match history (including the
  Elo Faceit records after each game), the rosters of your latest games, and
  the recent history of the teammates who played them with you. To tell who
  is logged in without a match room, it looks for an open faceit.com tab and
  asks that page, the same check the match room uses. It does not read other
  tabs.
- **Players' countries, for the roster flags.** In a match room, the
  extension shows each player's Faceit profile country as a flag. When the
  match data does not include it, it fetches that player's public Faceit user
  record, once per player per day at most. It can be switched off in the
  settings. The flag images are bundled with the extension (Twemoji, CC-BY
  4.0), so no third-party image service is contacted.
- **Which match events Faceit's page receives.** On faceit.com pages, the
  extension watches the page's own realtime connection to Faceit
  (`edge.faceit.com`) for the names of a few match events — a check-in
  starting, a veto step, a status change — and the match id they belong to.
  It uses them only to know when to read the match again, and at check-in
  to start loading the lobby's statistics before the room opens. The
  messages' contents are not read further, stored, or sent anywhere.
- **Your match's game server address, for "Auto-copy server IP".** When
  Faceit assigns your match a server, it sends you its details over the same
  connection. With the setting on, the extension takes only the server's
  address and port from that message, puts `connect <address>:<port>` on
  your clipboard, and shows it in a short notice. The address is not
  stored, logged, or sent anywhere (the tab keeps only a hash of it, to
  avoid copying the same server twice); the rest of the message, including
  any password, is not read out.
- **A match's demo, sent to Leetify when you click "Send to Leetify".** In a
  finished match room, the panel has a "Send to Leetify" button. Nothing
  happens until you click it. Then the extension asks Faceit for a download
  link to that match's demo, the same request Faceit's own "Download demo"
  button makes. Faceit requires its usual Cloudflare Turnstile check for it.
  The extension runs that check with the Turnstile widget Faceit's match room
  page has already loaded, in that tab, and requests the link from that tab
  with your Faceit session; it adds no script of its own to the page. If you
  click on one of the room's Stats pages, where Faceit doesn't load that
  widget, the tab shows the room's Overview for the check and then goes back.
  The extension then sends that one link to Leetify
  (`api.cs-prod.leetify.com`) so Leetify can download the demo and build its
  match report. The link is a short-lived download address for the match
  recording. Your Faceit session token, cookies and account details are not
  sent to Leetify, and the link is not stored or logged. Leetify answers with
  a report id, which is kept in session storage only, for the "View on
  Leetify" link. A match's demo shows every player in it, as it does on Faceit
  and Leetify; what Leetify does with a submitted demo is covered by
  Leetify's own privacy policy. The button can be switched off in the
  settings.
- **Your current Elo, for the Elo bar.** On faceit.com pages, the extension
  fetches your own Faceit user record about once a minute to show your CS2
  Elo and progress toward the next level under your avatar. It can be
  switched off in the settings.

## What the extension stores

All storage is local to your browser (`chrome.storage`):

- Your feature settings (which extras are enabled, team colors, overlay
  position).
- Your own Faceit nickname and player id, so that a match room opened while
  Faceit is slow to say who is logged in still puts you on the right team.
- A short-lived (15 minute) in-session cache of fetched player statistics, so
  reopening a lobby does not refetch everything. Lifetime per-map records are
  kept in the same session storage for up to six hours; it is cleared when the
  browser closes.
- An optional Leetify API key, if you choose to enter your own on the options
  page instead of using the key built into the extension. It is stored only in
  your browser and sent only to Leetify.
- The last session overview and your teammates' recent games, in session
  storage, which the browser clears when it closes. The popup also remembers
  which of its tabs you had open.
- Your last fetched Elo, in session storage, which the browser clears when it
  closes.
- Players' countries, in session storage for up to a day; it is cleared when
  the browser closes.
- The past vetoes read for "Their captain's drops" (which side dropped which
  map, in order), in session storage, which the browser clears when it closes.
- For "Send to Leetify": the Leetify report id of each match you sent, the
  time until which Leetify asked to be left alone after a "too many
  requests" answer (five minutes), and Faceit's public captcha site key, all
  in session storage, which the browser clears when it closes.
- How many statistics requests Faceit accepted in a ten-second window before
  answering "too many requests", if it ever did, for up to a day, so the
  extension paces itself below that.

Nothing is synced to any server operated by the developer.

## What the extension sends

Network requests go exclusively to `www.faceit.com`, `api.faceit.com`, and —
for the role pendants and your aim in the session overview only —
`api-public.cs-prod.leetify.com`. When you click "Send to Leetify" in a
finished match room, it also sends one request to `api.cs-prod.leetify.com`
carrying that match's demo download link, and Faceit's captcha check, which
Faceit's page loads from Cloudflare (`challenges.cloudflare.com`) for its own
download button, runs in the match room's tab. The
extension carries no developer API key for FACEIT and never calls the FACEIT
Open Data API (`open.faceit.com`); that API is used only by the developer's
offline research scripts, which are not part of the extension. Requests
to Leetify carry only public Steam64 identifiers (those of the players in the
match room and, for the session overview, your own) or, on your click, one
match's demo link; nothing else about you is sent with them. Leetify is a statistics
provider, not an analytics or advertising service: there is no analytics,
telemetry, or advertising in this extension, and no data is sold or shared
with anyone.

## Removal

Uninstalling the extension removes all locally stored data. You can also clear
it at any time via the browser's extension storage controls.

## Contact

Questions or concerns: open an issue at
https://github.com/naeyn/pocketwatch/issues.
