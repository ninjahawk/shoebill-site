---
layout: default
title: Roadmap
nav_order: 10
---

# Roadmap

Nothing on this page is a promise or a schedule. It is a record of stated
intentions, published so that the direction is checkable against what actually
ships. Items are listed in the order they are currently intended to be
attempted. Anything measured and abandoned is recorded on the pages it belongs
to rather than quietly dropped.

## The ranking, first

The ranker is the acknowledged weak point, and the complaint about it is
specific: the feed reads as assorted rather than curated. The cause is
understood. Author damping, per-server damping, the run-length limit and the
weighted round robin were each ported from a system that needed them to stop
one loud account owning a screen in a feed that was already coherent. Applied
to a pool drawn from unrelated networks, they enforce variety in a feed that
has no coherence to protect, and variety of that kind reads as noise.

Directions under consideration, cheapest first, none committed:

- **Topic runs.** Group two or three related posts together rather than
  strictly interleaving by network. Coherence is a property of what sits next
  to what, and that is free to change.
- **Weaker diversity brakes**, now that their cost is understood.
- **Session continuity.** Weight the last handful of posts opened far more
  heavily than the slowly decaying interest profile, so the feed leans into
  what is being read now rather than what was read last week.
- **A real cold start.** A first session that leans hard on cross-server spread,
  or a first-launch topic choice, so a new reader opens on the network's best
  rather than its most average.
- **An ordered record of recent actions** in place of the current unordered set
  of interests.

The rule that governs any change here does not change: measure against one
cached pool of posts before and after, and do not ship a ranker that cannot be
explained in three sentences.

## Live video and chat

The intention is a surface for what is broadcasting now, with the chat
alongside it, readable without an account. Nothing about this has been measured
yet, and nothing will be claimed until it has. The piece most likely to prove
impossible is video playback; the piece most likely to work is anonymous
read-only chat. The measurement comes before the design.

## Connected accounts

The intention is that linking accounts makes Shoebill a front end for all of
them: one post published to every linked network at once, one timeline of
everything a person has written wherever they wrote it, likes and replies from
every linked account in one place, and a follower count that is the sum across
every network they are on. That last figure is only meaningful to an app
standing in all of those places at once.

The known cost is that every network added here is a separate authentication
integration, a separate write API and a separate set of failure modes, any of
which can be revoked. A cross-post that silently fails on one network is worse
than not offering the feature, so it will be measured before it is offered.

## A comment layer

The intention is a conversation among Shoebill's own readers, sitting over
content from networks that know nothing about it — reading a Hacker News story
in the app and replying to it in the app, where other Shoebill readers see the
reply.

This is the one part of the product that would need a server, and it is
deliberately not at launch. It would also change what the app is: a host of
other people's comments is a publisher rather than only a reader, with a
moderation burden that cannot be forwarded to anyone else. If it is built,
signing in would be required to comment and would remain optional for
everything else, because reading without an account is the point of the app.

## Ask, with tools and an in-app browser

The assistant currently answers by retrieval: it queries the same public
endpoints the feed uses and reports what it found. The intention is that it
should be able to fetch things during an answer rather than working from a
template, and that reading a linked page should be one of the things it can
fetch. An in-app browser is worth having on its own, since a large share of the
feed is links to articles.

The constraint is hardware: the on-device model this depends on requires a
recent iPhone and a recent version of iOS, so the feature will never be
available to every reader. The tool layer is kept free of anything specific to
one model provider so that it can be pointed elsewhere later.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
