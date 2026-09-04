# Halal Chat — multilingual production candidate

Languages: English, Arabic (RTL), French, Hausa.

## Before deployment
1. Deploy Hosting and Firestore rules together: `firebase deploy`.
2. In Firebase Authentication, enable Anonymous, Email/Password, and optionally Google sign-in.
3. Confirm Firestore is enabled for the `halalchat-edece` project.
4. Test on a phone and desktop after deployment.

## Feature audit completed
- Firebase initialization and auth flows: source/syntax checked.
- Profile onboarding/edit/sign-out/password reset: source checked.
- Community discovery/listeners: fixed a realtime bug that could remove private member communities when the public-community listener updated.
- Public community joining: retained transactional membership/count update.
- Private invite joining: fixed security gap so direct membership creation cannot bypass the invite requirement; invite redemption records the invite code.
- Community chat: query/rules reviewed; message length and membership checks retained.
- Message delete/report: source/rules checked.
- Community leave: fixed to use a Firestore transaction and matching decrement rule.
- Owner member removal: fixed to use a transaction and avoid attempting to delete another user's private membership document, which the client rules correctly prohibit.
- Community deletion: owner-only confirmation retained. Note: deleting the parent community document does not cascade-delete Firestore subcollections; server-side cleanup is still recommended for true permanent deletion.
- Direct messages: list query no longer depends on the problematic composite `updatedAt` index. Block enforcement was added to thread creation/message creation rules.
- Events/RSVP: source/rules checked. Event creation remains available to signed-in users; consider community-admin-only events before public launch if desired.
- Prayer times/Qibla: source checked; depends on browser geolocation permission and the AlAdhan API.
- Quran/Hadith cards: currently roadmap placeholders, not implemented modules.
- Multilingual UI: English, Arabic/RTL, French, Hausa translations retained. Some dynamic/long-form copy remains English where no translation key exists.
- Responsive layout: CSS includes mobile navigation and small-screen layouts.

## Known production hardening still recommended
- Firebase App Check.
- Server-side rate limiting and abuse controls.
- Cloud Functions/Cloud Run for trusted moderation and cascade deletion.
- Privacy Policy / Terms / account deletion flow.
- Payment webhooks before accepting Pro payments.
- Server-side notification delivery.
- Full automated browser/E2E tests against a staging Firebase project.
