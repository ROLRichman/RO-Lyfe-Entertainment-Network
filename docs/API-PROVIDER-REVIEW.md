# API Provider Review — RO'Lyfe Entertainment Network

**Reviewed:** 2026-11-04  
**Purpose:** Select a rights-aware, budget-conscious movie/TV discovery and trailer stack. This is a technical screening, not legal advice. Re-check each provider's current terms before launch.

## Recommended direction

Use **Trakt Standard as the first candidate for in-app movie/TV discovery**, subject to creating the app registration and testing required endpoints/rate limits. Use **KinoCheck as a trailer source candidate** after confirming commercial deployment expectations with the provider. Keep Watch Hub availability links as official outbound links until a commercial streaming-availability license makes financial sense.

Do not use any API key in browser JavaScript. Provider calls should go through a secured backend function. The Entertainment Network needs its own backend project; do not reuse the Sports or Trading Intelligence Supabase projects without an explicit project decision.

## Provider findings

### Trakt — first catalog candidate
- Standard API tier is currently listed at $0.
- Current API policy permits qualifying free or paid apps, including ad-supported apps, and says permitted use does not require a separate commercial agreement.
- Public discovery results, title/person details, images, ratings and lists may be displayed in the app.
- Do not bulk-harvest, mirror the catalog, resell API data, or supply the data as a feed to another service.
- Cache images; direct hotlinking to the Trakt image CDN is prohibited.
- Add this statement to an About/Credits area: **“RO'Lyfe Entertainment Network uses Trakt but is not endorsed or certified by Trakt.”**
- Standard access uses public endpoints and standard rate limits. Premium is optional for higher limits and restricted endpoints; do not purchase it until actual usage requires it.
- **Status:** User has verified the developer portal identity, but the app registration and API credentials have not yet been confirmed.

Official references:
- https://developer.trakt.tv/docs/api-use-policy
- https://developer.trakt.tv/docs/images
- https://developer.trakt.tv/premium

### KinoCheck — trailer candidate
- Public API documentation currently describes 1,000 requests per day per client; an API key can be requested for higher limits.
- Movie/show lookup accepts a KinoCheck ID, TMDB ID, or IMDb ID. This means an IMDb/TMDB identifier returned by the catalog can be used without making TMDB the primary catalog provider.
- Trailer, teaser, clip and featurette metadata are available.
- KinoCheck's FAQ says to embed the YouTube player rather than upload the video yourself and to link KinoCheck as the source.
- The API Terms discuss app use, credentials and quotas, but do not clearly state a broad commercial reuse license for every data field or asset. Obtain written clarification for the commercial RO'Lyfe use case before production.
- **Status:** No API key confirmed yet; 1,000/day public limit documented.

Official references:
- https://api.kinocheck.com/
- https://kinocheck.com/api-terms-of-use
- https://www.kinocheck.com/contact

### TVmaze — optional TV metadata source
- Public REST API is free and supports show search, show details, cast, crew, episodes and schedules.
- Current documentation states data is licensed under CC BY-SA; use requires attribution and compliance with ShareAlike.
- Published rate guidance is at least 20 calls per 10 seconds per IP, with 429/backoff handling recommended.
- Because ShareAlike can affect downstream use of modified/combined data, keep TVmaze-derived data clearly attributed and review whether its license fits the planned catalog before mixing it into other sources.
- The public API documentation does not require an API key for the documented public endpoints; do not rely on a stored TVMAZE_API_KEY unless the chosen feature specifically needs it.
- **Status:** Key is not assumed necessary; no integration test recorded.

Official reference:
- https://www.tvmaze.com/api

### Watchmode — defer commercial subscription
- Current Developer tier: free, 2,500 credits/month, up to 3 countries, non-commercial only with attribution.
- Current Startup tier: $349/month, 40,000 credits/month, commercial use.
- Current Business tier: $599/month, 100,000 credits/month, commercial use and additional US TV-guide features.
- The API supplies availability data and provider links; it is not a video playback service.
- **Decision:** Do not use the free tier for the commercial Root Of Lyfe platform. Defer a paid plan until user demand and revenue justify it. For now, use carefully curated official provider links and clearly label availability as not verified per title.

Official references:
- https://api.watchmode.com/pricing
- https://api.watchmode.com/tc

### OMDb — hold pending written rights clarification
- An API key being activated does not, by itself, establish a commercial content license.
- OMDb's currently posted Terms of Use include broad restrictions on indexing contributions and on commercial use of contributions.
- **Decision:** Do not use OMDb-sourced metadata, images or stills in a commercial public catalog until OMDb confirms in writing which API fields and uses are licensed for this product.
- **Status:** User previously activated a key; no verified application integration. Keep the key out of front-end code and do not delete the stored secret until its location/name is reconciled.

Official reference:
- https://www.omdbapi.com/legal.htm

### TMDB — commercial terms require direct confirmation
- Current official developer FAQ says free API use is for non-commercial projects with attribution; commercial API/data use requires contacting TMDB sales for a license.
- The user's prior signup flow displayed a $149/month commercial checkout. The current public FAQ does not publish a universal price, so treat the displayed price as the offer presented to that account and verify its scope directly with TMDB before paying.
- **Decision:** Do not subscribe yet. Trakt + KinoCheck may support the first discovery/trailer prototype without TMDB as the primary source.

Official reference:
- https://developer.themoviedb.org/docs/faq

## First implementation plan

1. Register the Trakt developer app under the RO'Lyfe Entertainment Network identity. Do not create extra apps to work around limits.
2. Confirm the exact Entertainment Supabase project before storing credentials or deploying Edge Functions. Existing Sports and Trading projects remain untouched.
3. Build a server-side catalog endpoint for public Trakt discovery, using documented public endpoints only, with rate-limit handling and source/attribution metadata.
4. Add trailer lookup through KinoCheck by IMDb ID or TMDB ID when available; embed only the official YouTube player and link to KinoCheck. Confirm the commercial permission question first.
5. Keep Watch Hub as official external-provider links until an appropriate commercial availability-data license is justified.
6. Add a visible About/Credits page with required source attributions and a separate privacy notice before accounts or personalization launch.

## Non-negotiable security and rights checks
- Never commit API keys, tokens, client secrets or service-role keys to GitHub.
- Never expose secret credentials in browser JavaScript.
- Do not claim an API is connected until a real backend request has been tested successfully.
- Do not host, scrape, rebroadcast, frame or stream content without the required rights and provider permission.
- Do not mirror a third-party catalog or image library.
- Label unavailable integrations and non-live sample content honestly.
