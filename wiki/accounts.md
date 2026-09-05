---
layout: default
title: Accounts
nav_order: 6
---

# Accounts

## Reading needs no account

There is no Shoebill account. The feed, threads, replies, profiles, search, the
video feed, channels, blocking, muting and reporting all work with no sign-in
of any kind, because everything the app reads is public data served by APIs
that do not ask for one.

Signing in is optional, and it connects an account the reader already holds
somewhere else. It exists for one reason: some actions belong to a person, and
the networks require a person's own credentials to perform them.

## Connecting a Mastodon account

Mastodon sign-in uses OAuth in the system's browser view. The app registers
itself with the chosen server, opens that server's own authorization page in
the browser, and receives a token back when the reader approves it. The
password is typed into the server's page in the browser, never into the app.
The browser session is ephemeral, so it does not share cookies with Safari.

The sign-in screen asks where the account lives, offers a list of servers to
choose from, and accepts any other server typed in.

## Connecting a Bluesky account

Bluesky sign-in uses an app password. An app password is created in Bluesky's
own settings, under App passwords, and is entered in Shoebill in place of the
account password. It can be revoked from the same screen at any time without
affecting the main account password. This is the only way the app signs in to
Bluesky.

If a Bluesky session expires, the app says so and asks for the account to be
connected again in Settings.

## What signing in enables

| Action | Mastodon | Bluesky |
|:--|:--|:--|
| Favourite or like a post | yes | yes |
| Boost or repost | yes | yes |
| Reply | yes | yes |
| Follow an account | yes | no |
| Write a new post | yes | no |
| Bookmark | yes | no |
| A Following timeline of the accounts you follow | yes | no |

Composing a new post is Mastodon-only. Following is Mastodon-only. Bookmarks
are stored on the device and also pushed to Mastodon when a Mastodon account is
connected; bookmarks made in another Mastodon client are not read back into
Shoebill, so the device's list is the one the app shows.

The Following timeline appears only when a Mastodon account is connected. With
only a Bluesky account connected, the feed's second tab remains the public
Latest timeline.

Nothing else changes when signed in. The ranking is the same, the sources are
the same, and no data is sent anywhere it would not otherwise go.

## Networks the app cannot post to

Hacker News, Lemmy, Lobsters and 4chan are read-only in Shoebill. Liking or
resharing a post from one of them records the action on the device and sends
nothing anywhere. A reply typed on one of those posts is kept on the device, is
visible only on that device, and is removed after 48 hours. It is never sent
anywhere.

Likes and reposts reach the network only on Mastodon and Bluesky, and only when
an account for that network is connected.

Voting in a poll is not implemented on any network.

## Where the token is kept

An access token is stored in the iOS Keychain, one entry per connected account,
and is used only to talk to the service it belongs to. It is never sent
anywhere else, and there is no Shoebill server for it to be sent to.

## Signing out, and revoking access

Signing out of an account in Settings deletes that account's token from the
phone. Deleting the app deletes every token with it.

Removing the token from the phone stops the app using it, but it does not by
itself withdraw the permission on the other service. To revoke the app's access
at the service:

- **Mastodon:** Preferences, then Account, then Authorized apps, and revoke the
  entry there.
- **Bluesky:** Settings, then App passwords, and delete the app password that
  was used.

Doing both is the complete removal.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
