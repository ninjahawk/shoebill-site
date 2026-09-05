---
layout: default
title: Sources
nav_order: 3
---

# Sources

Every source is read through a documented, publicly available API that requires
no key and no account. Nothing is scraped out of a web page, no undocumented
endpoint is called, and no server's stated access policy is worked around. The
rules below are what each operator has published; where an operator has
published nothing, that is said rather than assumed.

Three things are never done, on any network:

- **No accounts are operated.** Shoebill does not run bot accounts anywhere. It
  never reposts anyone's content to another network, and it never mirrors like
  counts onto an account it controls.
- **No HTML is scraped.** Only the JSON APIs the operators document.
- **No counts are invented.** Every number shown beside a post is the number
  the source network reported.

Every post is labelled with the network it came from and links back to the
original on that network.

---

## Mastodon

**What is read.** Trending statuses, trending tags and trending links; hashtag
timelines; the federated public timeline where a server serves it; threads and
replies; profiles and their posts; account and hashtag search. The app sweeps
roughly sixteen public servers in parallel.

**API.** The documented Mastodon REST API, anonymously. Nothing behind a token
is touched unless the reader has signed in.

**Rate limits.** Mastodon documents 300 requests per five minutes, per IP and
per account, for all endpoints. Because each phone talks to each server
directly, that budget belongs to the reader's own connection. Most servers do
not return rate-limit headers on anonymous reads, so the app tracks its own
request count per host rather than relying on the headers.

**Access is a per-server setting, and it is honoured.** A Mastodon
administrator can switch off anonymous API access. Measured on 2026-09-01
against 40 servers, 33 served their federated public timeline anonymously and 7
returned HTTP 422 with the message that the method requires an authenticated
user. Those seven included the largest server on the network. Two things follow.

First, that response is the server's own configuration, not bot protection.
Requests identifying as several different clients received the identical 422,
and registering an application and taking an application-level token opened
none of the closed endpoints. Skipping a server that says no is the correct
behaviour, and it is what the app does.

Second, it does not cost much, because the closed servers leave everything else
open. Trends, hashtag timelines, search, threads and profiles all return
normally without a token, and hashtag timelines carry federated posts from
across the network rather than only local ones: a 40-post pull of one hashtag
returned 26 posts from 12 other domains.

**Ownership.** Mastodon publishes no API terms of use, and there is no
network-wide operator to license content. Authors own their posts and each
server sets its own rules, which is why the app links back to the post on its
home server rather than presenting itself as the source.

---

## Bluesky

**What is read.** Public feed generators, trending topics, individual posts and
their replies, author feeds and people search.

**API.** The AT Protocol Lexicon endpoints that Bluesky documents as public and
serves without authentication, primarily through `public.api.bsky.app`, which
is the host Bluesky asks public web clients to use.

**Rate limits.** Bluesky documents these public endpoints as generously
limited and asks developers to make contact if they encounter limiting. The
published limit for traffic routed through a personal data server is 3,000
requests per five minutes per IP.

**Depth.** Measured on 2026-09-01, 42 popular feed generators were available,
each independently pageable; one feed alone yielded 299 unique posts over six
pages with the cursor not exhausted. Median engagement in that sample was 1,765
likes.

**The network's own rules.** Bluesky's developer guidelines require any app
with user-generated content to provide a way to report illegal content, a way
to block forbidden content from being shared in the app, and a way to block
abusive users; to delete content on request; to respond appropriately to all
user reports; and to keep a monitored public contact address. Shoebill provides
all of these — see [moderation]({{ site.baseurl }}/wiki/moderation.html) — and
publishes the contact address in the app, on this site and in the footer of
every page here.

**Labels.** Bluesky operates a labelling system in which moderation services
attach labels to posts. Shoebill reads those labels and acts on them.

---

## Hacker News

**What is read.** The top stories list and the story items behind it — title,
score, comment count and outbound link — plus comments.

**API.** The official Firebase API published by Hacker News, and the Algolia
Hacker News Search API for search and comments. Both are public and keyless.
The HTML site is never parsed, which matters: Y Combinator's site terms forbid
scraping the site, while the Firebase API was published deliberately for
exactly this use.

**Rate limits.** The Firebase API states that there is currently no rate limit.
Algolia's search API states a limit of 10,000 requests per hour from one IP,
which the app stays well under.

**What it supplies.** A title, a score, a comment count and a link. Article
bodies are never fetched from Hacker News. Measured 2026-09-01, the top 500
stories had a median of 228 points.

---

## Lemmy and PieFed

**What is read.** Community feeds sorted by Hot, from roughly ten instances,
and the comments on those posts.

**API.** The same documented public API that each project's own web interface
uses. Both are AGPL-licensed server software rather than a service, published
with a public API and an ecosystem of third-party clients as the intended
state. Neither project publishes API terms of use or a rate limit.

Because there is no central operator, there is no central licensor either.
Each instance sets its own rules and its own content policy, and posts belong
to their authors. The mitigation for the absence of a written limit is
politeness: an honest User-Agent, modest concurrency, and backing off on any
rate-limit response.

Measured 2026-09-01, 17 of 20 posts from the Lemmy sweep carried an image,
which is why this source is weighted for pictures rather than links.

---

## Lobsters

**What is read.** The hottest and newest lists, through the public JSON the
site serves alongside its HTML pages.

**API.** The `.json` endpoints the site advertises publicly. Lobsters publishes
no API terms page, no rate limit, no attribution requirement and no statement
of content ownership. Absence of a rule is not written permission, and it is
also the smallest source in the list and the one most easily hurt by impolite
polling, so it is polled rarely and holds the smallest share of the feed.

Measured 2026-09-01, a sweep produced about 32 unique stories with a median
score of 19, and only 1 of 23 links overlapped with the Hacker News top 60 —
so it adds material rather than repeating it.

---

## 4chan

4chan is one of the sources, and the site's API terms require that this be
disclosed. It is documented here for that reason.

**Source disclosure.** Material shown in Shoebill that comes from 4chan is
labelled 4chan on the post, and every such post links back to the thread it
came from on 4chan.

**What is read.** The public catalogue and thread JSON for seven worksafe
boards: Animals & Nature, Food & Cooking, Worksafe GIF, Photography, Papercraft
& Origami, Television & Film, and Video Games. Thumbnails are loaded from
4chan's own image host at the documented paths, which is the intended access
route; images are never re-hosted and are cached only on the device.

**API and its rules.** The read-only JSON API documented in 4chan's own API
repository. Its published terms are followed: no more than one request per
second, thread updates no more often than every ten seconds, and
`If-Modified-Since` on every request. The terms also state that an application
may not use "4chan" in its title, may not use the 4chan name or logo to promote
itself, may not present itself as official, and may not re-host the JSON. None
of those is done.

**What is different about this source.** Every other network hands the app at
least one upstream verdict to stand behind — a sensitive flag, a content
warning, a moderation label, or a vote. This one supplies none of those: there
is no sensitive flag, no content warning, no adult field and no vote, and a
catalogue is every live thread on the board rather than a curated selection.
Because of that, the app's own filters remove posts from this source where they
would blur a post from another source, and the boards it reads were chosen on
measured post-level pass rates. Measured 2026-09-04, each of the seven boards
sat at or below 6 per cent toxic content before the app's own filters ran.
Every post from this source passes the same hate-speech and adult text filters,
the same on-device picture check and the same block, mute and report controls
as every other source, which are described under
[moderation]({{ site.baseurl }}/wiki/moderation.html).

It holds 8 per cent of the For You blend and is not presented as a feature or a
destination: there is no 4chan tab, and material from it is labelled and mixed
into the feed on the same terms as everything else.

---

## Networks that arrive through Mastodon

Several other networks speak ActivityPub, the protocol Mastodon speaks. When
one of their users posts publicly and a Mastodon server the app reads has
federated that post, it arrives in the ordinary timeline like any other post,
carrying the author's real handle and domain.

- **Threads.** Meta's Threads federates public posts from accounts whose owners
  have turned fediverse sharing on. Those posts arrive through Mastodon. The
  app makes no call to Threads and has no relationship with it.
- **Pixelfed.** A photo-sharing network on the same protocol; its posts appear
  through Mastodon hashtag and public timelines, and a hashtag sample on
  2026-09-01 returned posts from several Pixelfed domains. Pixelfed's own API
  was probed and is not open to anonymous reads, so it is not called directly.
- **Flipboard.** Flipboard federates selected accounts and magazines, which
  arrive the same way.

The app does not call these networks' APIs, does not have accounts on them, and
does not present itself as a client for any of them. It shows what a Mastodon
server already received.

---

## Sources that are not in the main feed

- **Scores, odds and prices.** Public endpoints from ESPN, Kalshi and CoinGecko
  supply the live cards on the Explore screen. They are informational cards,
  not posts, and are not ranked.
- **Link previews.** When a post links out, the app fetches that page's own
  metadata and preview image to draw the card. That is a request to the linked
  site, made by the phone, in the same way a browser visiting the page would
  make it.

## Sources that were tried and are not used

Recording these is part of the method: a source that was measured and did not
work is worth as much as one that did.

- **Reddit.** Its data terms forbid redistribution and its keyless JSON returns
  an error to anonymous clients. It is not used.
- **Pixelfed's own API.** Closed to anonymous access when probed.
- **Nostr.** Requires websocket relays and has not been verified, so no claim
  is made about it.
- **Twitch clips.** The API requires a client secret, which cannot be shipped
  inside an app, so this source is not used.
- **Several video hosts** that work but publish no documentation for the
  endpoints involved. An undocumented endpoint is not a documented one, so they
  are not used.
- **Steam store reviews.** A channel built on publicly voted store reviews was
  written and then withdrawn, because Valve's terms grant no licence for a
  third party to redisplay that material. It contributes nothing to the app.
- **Imgur.** Wired but inert. It requires a client identifier whose daily
  budget would be shared by every install rather than belonging to each
  reader's own connection, which is the opposite of how every other source
  here works. It contributes nothing to the app.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
