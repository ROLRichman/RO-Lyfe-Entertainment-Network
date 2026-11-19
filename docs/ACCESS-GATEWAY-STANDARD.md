# RO’Lyfe shared front-door access standard

## Current preview phase

The Entertainment Network and Live Sports Center use a common remembered-device key:

`rolyfe.shared.preview.access.v1`

Both projects are hosted as paths on `https://rolrichman.github.io`, so browser localStorage is shared across these project paths. A visitor enters at one front door and the other configured front doors skip the preview prompt on that device.

## What it does

- Presents a cinematic welcome / login-style background.
- Announces the planned first-three-months-free launch preview.
- Remembers preview entry on the current browser.
- Provides a sign-out control.
- Allows navigation between configured same-origin projects without repeated prompts.
- Leaves embedded classroom and market-lab views untouched.

## Important boundary

This is **not authentication**. There is no email/password verification, identity, account recovery, protected server route, or access control. A visitor can bypass a static-site overlay. Do not put confidential information or privileged API actions behind it. API keys stay server-side.

When Supabase Auth or another identity provider is approved, replace the preview flag with a real shared authentication design (same trusted auth project, session refresh, callback/redirect allowlist, and consistent logout). Confirm the production domain and each project's allowed redirects before enabling it.

## Rollout standard

Every public RO’Lyfe front door should load the same gateway behavior and shared key. For projects hosted on a different domain, the browser key will not be shared; they must use the later secure sign-in flow rather than trying to copy localStorage across domains.
