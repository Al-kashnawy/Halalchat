# Halal Chat — production package

This package contains the Halal Chat single-page app, Firestore rules, and Firebase Hosting configuration.

## Deploy

1. Put the contents of `halalchat-multilang-fixed/` in your Firebase project directory.
2. Make sure Firebase Authentication has Anonymous and Email/Password enabled; Google is optional.
3. Deploy Hosting and Firestore rules together:

```bash
firebase deploy
```

## Private community invitations

Private communities now support **shareable invite links**. A community admin can open **Info → Invite members**, then use **Copy link** or the device **Share** button.

The generated link has this form:

`https://halalchat.vercel.app/?invite=XXXXXXXX`

When another member opens the link, Halal Chat validates the invitation, shows the community name, and lets the recipient tap **Join community**. The 8-character code remains available as a fallback.

The invite is stored in `inviteCodes/{code}` and the Firestore rules verify that the invite is active and belongs to the target community before a member record can be created.

## Important production hardening

Before a large public launch, add Firebase App Check, server-side moderation/rate limiting, account deletion/privacy controls, payment webhooks, notification infrastructure, and server-side cascade cleanup for deleted communities.
