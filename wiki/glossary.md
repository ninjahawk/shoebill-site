---
layout: default
title: Glossary
nav_order: 11
---

# Glossary

Terms that appear throughout this wiki and, in places, inside the app.

**ActivityPub**
: The protocol that connects Mastodon, Lemmy, PieFed, Pixelfed, Threads,
Flipboard and others. It defines how one server hands a post, a follow or a
reply to another server. A network that speaks it can exchange posts with any
other network that speaks it, without either side having an agreement with the
other.

**AT Protocol**
: The protocol Bluesky is built on. It differs from ActivityPub in that a
user's identity and their records are portable between hosts, and that
indexing, moderation and feed generation are separable services rather than
functions of the server holding the account.

**Boost**
: Mastodon's term for resharing someone else's post to one's own followers,
unchanged and without comment. The equivalent on Bluesky is a repost. The
ranker treats a boost as worth twice a favourite.

**Content warning**
: A short line of text a Mastodon author writes in place of their post, with the
post itself hidden behind it until a reader taps to reveal it. It is written by
the author, not applied by a moderator, and it is a normal part of the culture
on the network rather than a mark against a post. Shoebill keeps content
warnings intact and shows the author's own wording.

**Favourite**
: Mastodon's term for a like. The ranker counts a favourite as the smallest of
the three engagement signals it uses.

**Federation**
: The arrangement in which many independently operated servers exchange posts,
so that a person with an account on one server can follow and reply to a person
on another. There is no central server and no single operator. The practical
consequence for a reader is that where an account lives matters much less than
it would on a closed network.

**Feed generator**
: On Bluesky, a service that publishes a list of posts under a name, which
anyone can subscribe to. Some are algorithmic, some are curated, and anyone can
run one. They are public and readable without an account, which is how Shoebill
reads Bluesky.

**Fediverse**
: The collective name for the servers and networks that federate with one
another over ActivityPub. It is not a company, a product or a place; it is the
set of servers that have agreed to talk to each other.

**Hashtag timeline**
: A view of every public post carrying a given hashtag that a server has seen,
including posts that arrived from other servers. It is one of the endpoints
that stays open on servers that have closed their public timeline, and it is
one of the ways Shoebill reaches material held on those servers.

**Instance**
: One server in a federated network, run by one operator, with its own rules,
its own moderation and its own decisions about which other servers it will talk
to. Also called a server. An account lives on exactly one instance, and the
part of a handle after the second `@` names it.

**Label**
: On Bluesky, a machine-readable mark attached to a post or account by a
moderation service — for example marking a post as adult content. Labels are
composable: several services can label the same post, and clients decide what
to do about each label. Shoebill acts on them rather than displaying them.

**Trend**
: A post, hashtag or link that a server's own trend calculation has surfaced as
currently notable among the material that server can see. Because every server
computes its own, the number of independent servers that surfaced the same post
is itself a signal, and it is the one the ranker relies on most.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
