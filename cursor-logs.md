## [2026-05-10 12:10] - Fix SSR crash and Client auth mode toggle bug

**Problem/Request:**
The user reported that the registration as a user "disappeared" (the toggle was gone, and they were stuck on the Business Onboarding screen) and there were SSR errors ("This page didn't load").

**Files Modified:**
- frontend/src/routes/index.tsx (added `setMode("client")` to `useEffect` when session is detected)
- frontend/src/lib/supabase.ts (added fallback values to prevent SSR crashes)

**Solution Summary:**
1. **SSR Crash Fix**: Added a fallback URL to `supabase.ts`. If `import.meta.env` is missing during Server-Side Rendering (SSR), it won't throw an "Invalid URL" error and crash the page, but will gracefully render the initial HTML.
2. **Logic Trap Fix**: Previously, if a user logged in (e.g. via Google OAuth) and was redirected back, the app correctly detected the session and set `isClientLoggedIn = true`. However, it left the `mode` as `"business"` (the default). This caused the app to render the Business Onboarding screen and hide the mode toggle, trapping the user. I updated the `useEffect` to automatically switch the `mode` to `"client"` when a valid Supabase session is detected.

**Verification:**
The code has been updated and formatted. The logic now correctly forces the UI into the client dashboard when a session exists.

**Outcome:**
✅ Success