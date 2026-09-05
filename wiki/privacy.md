---
layout: default
title: Privacy
nav_order: 8
---

# Privacy, in summary

This page is a summary. The full policy is the authoritative document and is
published at [/privacy.html](/privacy.html).

## The short version

There is no account, there is no Shoebill server, and there is no analytics.
The app runs entirely on the phone. It reads public posts by calling public
APIs directly from the device, ranks them on the device, and stores what it
remembers on the device.

## Nothing is collected

The app contains no analytics library, no advertising library, no attribution
or crash-reporting library, and no tracking of any kind. It does not use the
advertising identifier and does not ask for tracking permission, because it has
nothing to track with. There is no backend for data to be sent to.

It has exactly one third-party dependency: an open-source image-loading
library, which loads and caches pictures on the device and sends nothing
anywhere on its own.

## Services the phone contacts directly

Because the app talks to each network straight from the phone, each of those
networks receives the device's IP address and the requests it makes, exactly as
a web browser visiting the same site would. Their own privacy policies govern
what they do with that. Shoebill receives none of it, and adds no identifier of
its own to those requests.

The full list of hosts is in the [policy](/privacy.html); it covers the
Mastodon servers the app sweeps, Bluesky's public API, Hacker News, Lemmy and
PieFed instances, Lobsters, 4chan's JSON and image hosts, and the hosts behind
the link previews and media in the feed.

## What is stored, and where

On the device only, in the app's own storage:

- Which posts have already been shown, so the feed does not repeat itself.
- The interest profile: a set of weights the ranker learns from what is opened,
  lingered on, saved or skipped.
- Saved posts and bookmarks, and the posts kept for offline reading.
- The image cache.
- Mutes and blocks — accounts, domains and words. Stored locally on purpose, so
  they keep working while signed out.
- Reports that have been filed, listed in Settings.
- Settings, including appearance, notifications, sensitive-content options,
  pinned tabs and reserve size.
- Per-day counts of opens and refreshes, used by the app for its own decisions.
  They have nowhere to go and are not sent anywhere.

In the iOS Keychain: if an account is connected, that service's access token,
one entry per account, used only to talk to that service. Signing out deletes
it.

## Clearing it

Blocks, mutes and reports are managed in Settings. The interest profile has a
Reset button. The offline reserve is emptied by setting its size to Off.
Signing out removes the tokens, and access can also be revoked from the other
service's own settings. Deleting the app removes all of it, including the
Keychain entries, because none of it exists anywhere else.

## Notifications

Notifications, if they are turned on, are scheduled locally by the app from
content it has already fetched. There is no push server and no device token is
sent anywhere.

## Children

The app is not directed at children. It shows unmoderated public posts from
open social networks and is rated accordingly.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
