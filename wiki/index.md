---
layout: default
title: Overview
nav_order: 1
---

# Shoebill

Shoebill is an iPhone app that reads public posts from several open social
networks and presents them as one ranked feed. It compiles material that is
already published in the open — Mastodon, Bluesky, Hacker News, Lemmy, PieFed,
Lobsters and a set of worksafe 4chan boards — deduplicates it, ranks it on the
device, and labels every post with the network it came from. It is not a client
for any one of those networks, and it is not affiliated with any of them.

The app has no server. Every refresh opens connections straight from the phone
to those networks' own public APIs, and the merging, filtering and ranking all
happen in memory on the handset. Nothing is proxied, nothing is cached off the
device, and no record of what anyone reads exists anywhere else. That is the
reason the app can be used without an account: reading public data does not
require one, so the app does not ask. Signing in is optional and exists only so
that a reader can post, reply, like, repost, bookmark or follow using an
account they already hold on Mastodon or Bluesky.

This wiki documents how the app works in detail: where the posts come from,
what the ranker does and does not do, which filters run before a post is shown,
what is stored on the device, and what the app cannot do. It is written to be
checkable. Where a figure appears it is a measurement, and the date it was
measured on is given with it. Where something is a limit rather than a feature,
it is stated as a limit.

## Pages

| Page | What it covers |
|:--|:--|
| [The feed]({{ site.baseurl }}/wiki/feed.html) | Sources, filters, scoring, ordering, and what having no server rules out |
| [Sources]({{ site.baseurl }}/wiki/sources.html) | Each network, the API used, the rules honoured, and what is never done |
| [Interface]({{ site.baseurl }}/wiki/interface.html) | Tabs, channels, Shorts, Ask, settings |
| [Moderation]({{ site.baseurl }}/wiki/moderation.html) | Filters on the device, reporting, blocking, muting, response times |
| [Accounts]({{ site.baseurl }}/wiki/accounts.html) | Signing in, what it unlocks, signing out and revoking access |
| [Offline]({{ site.baseurl }}/wiki/offline.html) | The reserve of posts kept on the phone |
| [Privacy]({{ site.baseurl }}/wiki/privacy.html) | Summary of the privacy policy |
| [FAQ]({{ site.baseurl }}/wiki/faq.html) | Twenty short answers |
| [Roadmap]({{ site.baseurl }}/wiki/roadmap.html) | Stated intentions, not commitments |
| [Glossary]({{ site.baseurl }}/wiki/glossary.html) | Fediverse terms used throughout |

## Requirements

The app runs on iPhone with iOS 17 or later. It is free, contains no
advertising and no in-app purchases, and is distributed through TestFlight
during the beta.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
