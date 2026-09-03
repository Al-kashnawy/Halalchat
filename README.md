# Halal Chat — Production MVP

Halal Chat is a privacy-first Muslim community platform built around trusted communities, messaging, events and Muslim-first utilities.

## Included
- Firebase Authentication: anonymous, email/password and optional Google sign-in
- UID-based profiles
- Public and private communities
- Community membership and owner/admin/moderator foundations
- Invite-code flow for private communities
- Real-time community channels and messages
- Message deletion and reporting
- One-to-one DM threads with member-scoped Firestore rules
- User blocking foundation
- Events + RSVP storage
- Prayer times + Qibla via Aladhan
- Responsive web UI for desktop/mobile
- Firestore security rules

## Before public launch
1. In Firebase Authentication, enable Anonymous and Email/Password. Enable Google only if you want it.
2. Deploy `firestore.rules`.
3. Create the Firestore composite indexes requested by Firebase when queries first run.
4. Add App Check before opening the service broadly.
5. Connect payments through a server-side Stripe/Paystack integration. Never trust client-only subscription state.
6. Add a real admin console and server-side moderation workflows.
7. Add rate limiting / abuse protection, email verification, password reset UX, account deletion, privacy policy and terms.
8. Replace UID-only DM discovery with an approved directory/invite system.
9. Add Cloud Functions/Cloud Run for counters, notifications, moderation queues and billing webhooks.

## Deploy with Firebase CLI
```bash
firebase login
firebase use halalchat-edece
firebase deploy --only firestore:rules
firebase deploy --only hosting
```

## Deploy with Vercel
Keep `index.html` at the repository root. Vercel can serve the static site directly. Firestore rules are deployed separately with the Firebase CLI.

## Important
The frontend Firebase configuration is not a server secret. Security comes from Authentication, Firestore Security Rules, App Check and server-side controls. Do not commit Firebase service-account JSON files, private keys, payment secrets or API secrets.


## Account onboarding
The site now includes a polished Sign in / Create account flow with email/password, Google sign-in, password reset, and profile onboarding. New email accounts are asked for a display name and optional bio, location, and interests. Email verification is requested after email/password registration.

In Firebase Console, enable **Anonymous**, **Email/Password**, and optionally **Google** under Authentication → Sign-in method. Configure the authorized domain for your deployed Vercel site if Firebase asks for it.

Multilingual repair note:
- English, Arabic (RTL), French, and Hausa language selector restored safely.
- Translation is applied at runtime to static and modal UI text without altering Firebase logic.
- Existing Firestore rules are retained; no rules change is required for language support.
