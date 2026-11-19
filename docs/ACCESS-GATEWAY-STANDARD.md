# RO’Lyfe shared front-door access standard

## Current preview phase

The following public media front doors use one common remembered-device key:

`rolyfe.shared.preview.access.v1`

- RO’Lyfe Entertainment Network
- RO’Lyfe Live Sports Center
- RO’Lyfe Gaming
- RO’Lyfe Vision Hub
- RO’Lyfe JUST LISTENING

These projects are hosted as paths on `https://rolrichman.github.io`, so browser localStorage is shared across the project paths. A visitor enters at one configured front door and the others skip the preview prompt on that same browser.

## What it does

- Presents a cinematic welcome / login-style background.
- Announces the planned first-three-months-free launch preview.
- Remembers preview entry on the current browser until the visitor signs out or clears browser storage.
- Provides a sign-out control.
- Allows navigation among configured same-origin projects without repeated prompts.
- Bypasses the gateway when a page is opened with an embed query parameter.

## Important boundary

This is **not authentication**. There is no email/password verification, identity, account recovery, protected server route, or access control. A visitor can bypass a static-site overlay. Do not put confidential information or privileged API actions behind it. API keys stay server-side.

The GoldenSteal DJ Studio performance workspace remains accessible without this front-door prompt so DJs are not blocked from using the pilot workstation.

When Supabase Auth or another identity provider is approved, replace the preview flag with a real shared authentication design (same trusted auth project, session refresh, callback/redirect allowlist, and consistent logout). Confirm the production domain and each project's allowed redirects before enabling it.

## Rollout standard

Every additional public RO’Lyfe front door should load the same gateway behavior and shared key. For projects hosted on a different domain, the browser key will not be shared; they must use the later secure sign-in flow rather than trying to copy localStorage across domains.
