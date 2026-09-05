---
layout: default
title: The feed
nav_order: 2
---

# How the feed is built

The main feed, called For You, is assembled from scratch on the phone every
time it is refreshed. There is no server in the middle, so there is no
pre-computed timeline waiting to be downloaded: the app fetches, filters,
scores and orders the posts itself, in memory, in the time it takes the network
calls to return.

## 1. Where the posts come from

A refresh opens roughly thirty connections in parallel to the public APIs of
the networks listed on the [sources page]({{ site.baseurl }}/wiki/sources.html)
and pulls in the region of 850 posts. The fan-out is concurrent and does not
wait for the slowest server: what has arrived by the deadline is used, and the
rest fills in as it lands.

Duplicates are collapsed by each post's permanent address. The same post found
on nine different Mastodon servers becomes one post that remembers it was found
nine times. That count matters later.

### The two Mastodon pools

Mastodon is read twice, through two different endpoints, because they do
different jobs and neither is sufficient alone.

- **Trends** is the quality pool. Each server publishes the posts its own trend
  algorithm has surfaced. Measured on 2026-09-01 across sixteen servers, this
  pool returned 222 unique posts with a median engagement of 56, a mean of 153
  and a maximum of 2,758. Paging deeper by raising the offset produced 508
  unique posts across the same sixteen servers without the quality falling off
  a cliff.
- **The public timeline** is the freshness pool. It is the federated firehose:
  posts that arrived seconds ago. Measured on the same date, 320 posts pulled
  from eight servers had a mean of 0.1 favourites, a median of 0 and a maximum
  of 2.

The consequence is a rule the ranker is built around: the firehose has no
usable engagement signal and must never be sorted by favourite count. It
supplies recency. Trends supplies evidence that something was worth reading.
The feed needs both, because trends alone is stale by design — the same posts
sit there for hours — and the firehose alone is noise.

## 2. The ranker in three sentences

This is the explanation the ranking code itself carries, and it is the whole
description:

> Grade every post on the phone first — drop what the reader cannot read, has
> blocked, has seen, or that says nothing, and mark what is political — then
> score each post by the engagement it earned decayed by its age the way Hacker
> News and Lemmy decay theirs, divided by (hours + 2) to the power 1.8,
> counting a reply as ten likes and a repost as two, multiplied by how many
> independent servers surfaced it. Damp each author's second and third post,
> lift the posts a mainstream reader stops for — pets, food, nature, the
> absurd, the screenshot-worthy, a face, news breaking now — but only where
> they already beat their own network's median, hold political posts and posts
> about the fediverse itself to one per screen and none on the first, and lift
> one overlooked small account into the middle of the page. Then merge the
> networks in a fixed ratio, break up any run that would put one author or one
> network on screen twice, and open the page with the best picture and the
> biggest story.

## 3. The stages, in order

### Filters, before anything is scored

A post is discarded before it reaches the scorer if it has already been shown,
if it comes from an account, domain or word the reader has blocked or muted, if
it is older than 48 hours, if there is nothing to render, if it is under three
words with no picture, link or poll, or if it is not in the reader's language.
The language check reads the text on the device rather than trusting the
server's language tag, because servers commonly leave that field at a default.

### Scoring

Each post gets one number, built from five things.

**Engagement**, using the action weights that X published with its own ranking
code: a favourite counts 0.5, a repost 1.0 and a reply 5.0. A reply is
therefore worth ten favourites. One deliberate divergence: a post is credited
with at most as many replies as it has favourites, or five, whichever is
larger. Without that cap, a network where replies vastly outnumber favourites
becomes a comment-count sort.

**Age.** The score is divided by (hours old + 2) raised to the power 1.8. This
is the same gravity formula Hacker News and Lemmy use. The +2 is what stops a
five-minute-old post with two votes outranking an established one.

**Spread.** How many independent servers surfaced the same post. The measured
range on 2026-09-01 was 1 to 13. This signal exists only because the fediverse
is decentralised: a post that thirteen separate servers' trend algorithms
picked up independently is evidence of reach that cannot be manufactured from a
single server the way a favourite count can.

**Multipliers up:** a picture 1.25, an account that has verified a link on its
profile 1.15, a subject trending across more than one network that day 1.6, a
post that arrived through a curated topic feed 1.25.

**Multipliers down:** a reply 0.35, an account flagged as a bot 0.5, a post
behind a content warning 0.5, a bare link with no words of its own 0.8, a
paywalled link 0.7, an angry post 0.6, a political post 0.4, a post about
Mastodon, Bluesky or federation itself 0.5.

**Subject lifts.** Seven categories are lifted: pets 1.5, food 1.4, nature and
space 1.35, the absurd 1.4, a screenshot of text 1.35, a person-forward picture
1.3, and news that broke in the last three hours 1.5. These stack but are
capped at 1.8 in total, and each applies only to a post that already beat the
median engagement of its own network. A cat photograph with no reactions cannot
ride a category to the top.

### Adjustments

An author's second post in one refresh is worth 63 per cent of their first,
their third 44 per cent, with a floor of 25 per cent. The same curve, gentler,
is applied per server. One small, overlooked Mastodon account — fewer than a
thousand followers, posted in the last day — is lifted into the middle of the
first page, so that the feed is not only the accounts that are already large.

### Blending

Each network is sorted on its own terms, and the sorted lists are then merged
by a weighted round robin at fixed shares: Bluesky 37 per cent, Mastodon 27 per
cent, Lemmy 18 per cent, Hacker News 8 per cent, 4chan 8 per cent, Lobsters 2
per cent.

### Why cross-network scores are never compared

A Hacker News point, a Bluesky like and a Mastodon favourite are not the same
unit, and normalising them does not fix it, because the distributions are
different shapes rather than different scales. Measured on 2026-09-01,
Mastodon's best post was roughly eighteen times its median while Bluesky's was
roughly six times its median. Dividing each post by its source's median
therefore hands one network's long tail an unearned multiplier: in that test,
exactly one Bluesky post reached the top twenty despite having 8,198 likes.
Comparing two posts from the same network is valid. Comparing across networks
is not. So each network is ranked internally and the lists are interleaved at a
fixed ratio instead.

### Final ordering

One post per conversation. Never the same author twice on a screen. Never more
than three in a row from one network, measured over a sliding window of twelve
posts, which is roughly two screens. No political posts and no posts about the
fediverse itself in the first twelve slots. The page opens with the best
picture, then the biggest story.

## 4. Recency

Most of the feed is from the last 24 hours. Retrieval asks each source for the
last day by default and widens to three days only for material the source has
already voted for heavily. The age filter is the outer wall at 48 hours.

There is one deliberate exception. On 4chan a thread lives for days and is
bumped rather than reposted, and there is no equivalent of a fresh-post
firehose to draw from, so that source is given a longer window. A channel a
reader has pinned may also set its own window, because a channel is something
opted into rather than served by default.

There is no hall-of-fame content in For You. A source with no time window of
its own does not go into the main feed at all.

## 5. Diversity, and what it costs

Author damping, per-server damping, the run-length limit and the weighted round
robin all push against a single account, server or network dominating the
screen. They also push against topical coherence, which is the honest trade:
a feed assembled from unrelated networks and forced to alternate between them
reads as variety rather than as a subject. Reducing that effect is the main
open piece of work on the ranker and is described on the
[roadmap]({{ site.baseurl }}/wiki/roadmap.html).

## 6. Two things that were measured and are not built

Both looked obviously right before they were measured against a live pool of
posts, and neither survived.

- **Cross-network link deduplication.** The theory was that several
  aggregators carry the same article, so the same story appears repeatedly, and
  the number of networks carrying it would be a signal. Measured: of 741 posts
  carrying an outbound link, 648 links were distinct and exactly one appeared
  on more than one network. The overlap does not exist at this scale.
- **A similarity reranker** of the kind that pushes near-identical posts apart.
  Measured over the 150 highest-engagement posts: zero pairs above 0.5
  similarity on content words, and zero above 0.35. There was nothing for it to
  fix, because a pool drawn from unrelated networks is diverse already.

## 7. What the feed cannot do

These are consequences of having no server, and they are permanent unless that
changes.

- **No follow graph.** Signed out, the app does not know who anyone follows, so
  it cannot use the strongest signal a conventional feed has.
- **No impression log.** The app records which posts it has shown so it does
  not repeat them, but it keeps no history of what was shown and skipped, so it
  cannot learn from skipping.
- **No trained ranking model.** A model of the kind large networks use requires
  a corpus of labelled engagements from millions of users. The app has explicit,
  published weights instead.
- **It cannot read a picture for meaning.** It can read the object labels the
  phone's own vision framework produces, and nothing beyond that.
- **It cannot tell satire from sincerity**, and the political and
  fediverse-meta rules are word lists, so material that avoids those words
  passes through untouched.

## 8. Whether it works

The ranking is checked against what the source networks went on to do. In an
evaluation over 90 hourly snapshots of the ranked feed, each scored against the
engagement its posts actually gained three hours later, the correlation between
the app's score and the observed gain was +0.855, and on average 16.7 of the
app's top 20 posts were in the true top 20 by gain (measured 2026-09-04).

That measure answers one question only — whether the source network agreed —
and not whether the result was a good feed to read. The second question does
not have a number.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
