# RO'Lyfe Entertainment Network™

**Live website:** https://rolrichman.github.io/RO-Lyfe-Entertainment-Network/

RO'Lyfe Entertainment Network is the discovery front door for movies and television, sports, music, watch destinations, and games.

## Project boundaries
- This repository owns the Entertainment Network website.
- RO'Lyfe Live Sports Center remains a separate project and backend.
- RO'Lyfe Gaming remains a separate gaming project. The Games Arcade section links to it; it does not merge or duplicate its code.
- Collectibles / comics / baseball cards remain a separate future-project idea and are not part of this repository.

## Movies & TV app foundation
- `movies.html` is the dedicated, mobile-first Movies & TV experience.
- Full-width responsive app layout; mobile slide-out navigation supports edge-swipe right to open, left to close, tap-outside, and Escape.
- Dedicated sections for Discover, Movies, TV Shows, Anime, Release Calendar, Continue Watching, Watch History, Watchlist, Collections, and Settings.
- Catalog filters include title/keyword search, genre (including Horror, Crime, Romance, Family, Western and War), release year, year range, decade, minimum rating, original language, country, content type, and sort order.
- Discover includes a dedicated Horror After Dark shelf and one-tap Horror genre filtering.
- Includes trending/recent/series shelves, title details, local watchlist and local history.
- Current entries are clearly labeled preview/sample data; this is not a live provider catalog.
- Trailer lookup and title-specific watch availability remain pending secured backend/provider integrations.

## Current website foundation
- Responsive, full-screen mobile-first Movies & TV app with cinematic dark styling and green/orange accents.
- Navigation for Home, Movies & TV, Sports, Music, Videos, Watch Hub, and Games.
- The Games Arcade doorway links to the separate RO’Lyfe Gaming hub; the Video doorway links to the separate RO’Lyfe Vision Hub.
- Official external links to selected streaming services.
- One central Jamal launcher links to the RO’Lyfe assistant; duplicate local assistant UI was removed.
- Mobile menu opens as a floating panel, closes after selection, and supports Escape / outside-click dismissal.
- Clear status labels where data providers and playback are not connected.

## Provider review
See [docs/API-PROVIDER-REVIEW.md](docs/API-PROVIDER-REVIEW.md) for the current API rights, costs, attribution requirements, and recommended integration sequence. Provider terms must be re-checked before commercial launch.

## Last.fm Music integration
- A dedicated `music.html` discovery page is now in the site, linked from the main Music navigation and tile.
- Music views include global artists/tracks/tags, Hip-Hop and R&B artist/track/album shelves, tagged trending albums, and the `RichROLyfe` personal profile (scrobbles, top artists and top albums when listening data exists).
- Last.fm does not expose one universal global top-albums chart; the current album shelves use genre-tag rankings, and personal/artist top albums use their respective documented endpoints.
- RO’Lyfe Radio is a coming-soon concept, not a live station. Last.fm's former Radio API is deprecated and its data API does not grant music-streaming rights.
- A separate `entertainment-lastfm` Supabase Edge Function is deployed in the selected `ROLyfe-Live-Sports-Center` project. It is isolated from the Sports functions and proxies a limited set of read-only Last.fm discovery methods.
- The function reads `LASTFM_API_KEY` from Supabase Edge Function secrets; the key is never placed in GitHub or browser code.
- **Runtime verification is pending:** the connected tools confirmed function version 2 is deployed, but did not provide a successful live Last.fm response. Confirm that `LASTFM_API_KEY` exists in this specific Supabase project's Edge Function Secrets, then test the page.
- Last.fm's API introduction asks developers planning commercial use to contact `partners@last.fm`; obtain confirmation before commercial launch. The page provides discovery metadata only and does not stream music.

## Integration status
The site currently does **not** have verified live catalog search, scores, trailer API calls, music API calls, personal accounts, watchlists, or in-site streaming playback. Do not present demo placeholders as live data.

API credentials must never be committed to this repository. Provider integrations should call secured server-side endpoints (for example, a dedicated Supabase Edge Function) rather than exposing keys in browser code. Confirm the target Supabase project before making backend changes.

## Content and provider rules
- Use official provider links and approved playback methods.
- Do not rebroadcast, scrape, frame, or play third-party streams without the relevant permission.
- Only host or play content for which Root Of Lyfe has the necessary rights.
- Verify each API's current terms, attribution requirements, rate limits, storage/caching rules, and commercial-use requirements before launch.

## Planned build sequence
1. Verify the Pages deployment and polish responsive layouts.
2. Replace the Movies & TV preview data with a secured live catalog endpoint; test search, discovery, details and rate-limit handling.
3. Add authorized trailer metadata and official YouTube embeds after commercial-use permission is confirmed.
4. Add region-aware Watch Hub availability and official provider links.
5. Connect sports data through the separate sports backend after its health is confirmed.
6. Add music metadata and authorized listening destinations.
7. Connect Jamal through the central secure assistant service.
8. Add cloud accounts and cross-device watchlists; the current watchlist is device-local only.
9. Add licensed playback only after product, security, and rights review.

## GitHub Pages
The site is configured to publish from the `main` branch. The expected project URL is:
https://rolrichman.github.io/RO-Lyfe-Entertainment-Network/
