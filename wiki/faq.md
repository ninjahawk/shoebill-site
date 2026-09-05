---
layout: default
title: FAQ
nav_order: 9
---

# Frequently asked questions

### 1. Do I need an account?

Not to read. The feed, threads, profiles, search, channels and the video feed
all work with no sign-in. There is no Shoebill account to create.

### 2. What does signing in change?

It lets you act: like, repost, reply, and on Mastodon also post, follow and
bookmark. It does not change the ranking, the sources, or what is stored.
See [accounts]({{ site.baseurl }}/wiki/accounts.html).

### 3. Is it free?

Yes. No advertising, no in-app purchases, no subscription, no promoted posts.
There are no advertisers, so there is nothing to promote.

### 4. Which networks does it read?

Mastodon, Bluesky, Hacker News, Lemmy, PieFed, Lobsters and seven worksafe
4chan boards, each through its own documented public API. Posts from Threads,
Pixelfed and Flipboard arrive as ordinary federated posts on the Mastodon
servers the app reads. Full detail on the
[sources page]({{ site.baseurl }}/wiki/sources.html).

### 5. Is this a Mastodon client?

No. Mastodon is one of several sources, and the app is not affiliated with
Mastodon or with any other network it reads. Every post is labelled with where
it came from and links back to the original.

### 6. Where does the ranking happen?

On the phone. There is no server, no proxy and no hosted timeline. The app
opens connections to each network's public API directly, merges what comes
back, and ranks it in memory.

### 7. How does it decide what to show?

Engagement the post actually earned, decayed by its age, multiplied by how many
independent servers surfaced it, then adjusted for subject, media, author
repetition and a handful of other factors, and finally interleaved between
networks at fixed proportions. The whole of it is written out on the
[feed page]({{ site.baseurl }}/wiki/feed.html), including the parts that do not
work.

### 8. Why is my feed not chronological?

Because a chronological view of the open social web is mostly noise. The
freshest posts have no engagement signal at all — measured on 2026-09-01, a
sweep of 320 posts from the federated firehose had a median of zero
favourites. A ranked feed is the point of the app. A reverse-chronological tab
is available beside it if you want one.

### 9. Why am I seeing a post from yesterday?

Most of the feed is from the last 24 hours, and the outer limit is 48 hours.
An older post appears only where the network it came from voted heavily for it.
One source, 4chan, has a longer window, because threads there live for days.

### 10. What is the number beside the reply, like and repost buttons?

Reach: the number of independent servers that surfaced that post. Other apps
show a view count in that position. Neither Mastodon nor Bluesky reports view
counts, so rather than show a number the app does not have, it shows one it
does.

### 11. Can I post from Shoebill?

Composing a new post works with a connected Mastodon account. Replies work on
Mastodon and Bluesky. Hacker News, Lemmy, Lobsters and 4chan are read-only in
the app.

### 12. Is anything collected about me?

No. There is no analytics, no advertising identifier, no tracking, and no
server to send anything to. What the ranker learns about your interests, your
blocks, your saved posts and your settings all stay on the phone and are
deleted with the app. See [privacy]({{ site.baseurl }}/wiki/privacy.html).

### 13. Does it work without a connection?

Yes, up to a point. The app keeps a rolling reserve of recent posts on the
phone — 200 by default, up to 5,000 — and shows them with a line saying it is
offline. Video is never saved. See
[offline]({{ site.baseurl }}/wiki/offline.html).

### 14. How do I stop seeing an account, a server, or a word?

Block the account or the whole server from the menu on any post, and mute words
in Settings. All three work signed out, are stored on the phone, and apply
everywhere in the app, including to posts already held offline.

### 15. How do I report something?

Report is in the menu on every post and every account. The post is hidden for
you immediately, your mail app opens with the report pre-filled and addressed
to the support address, and if you are signed in to Mastodon and it is a
Mastodon post, it is also sent to that account's own server. Reports are
answered within 24 hours.

### 16. A picture disappeared a moment after it loaded. Why?

Every picture is checked on the device by a classifier that ships inside the
app. Because it runs after the picture has been decoded, so that it never slows
the feed down, a picture it flags is withdrawn a moment after it appears rather
than never appearing. The thresholds are published on the
[moderation page]({{ site.baseurl }}/wiki/moderation.html).

### 17. Is the app moderated?

The app is not a moderator and does not claim to be. It applies the source
networks' own flags and labels, its own hate-speech and adult filters, and an
on-device picture check, then gives you blocks, mutes and reports for anything
else. Nothing is reviewed before it is published, on any network.

### 18. Why is 4chan one of the sources?

It supplies one kind of material the other sources do not, and seven worksafe
boards were measured before any of it was included. Every post from it passes
the same filters as every other post, is labelled 4chan, and links back to the
thread it came from. There is no 4chan tab and it is not presented as a
feature. The [sources page]({{ site.baseurl }}/wiki/sources.html) sets out what
is read, the rate rules that are followed, and why that source is filtered more
strictly than the others.

### 19. Why does Ask say it is search only?

Because on most iPhones it is. The full assistant runs a language model
entirely on the device, which requires iOS 26 and a device supporting Apple
Intelligence — in practice iPhone 15 Pro and later. Everywhere else, Ask
retrieves and lists what it found rather than writing an answer, and it says so
instead of pretending otherwise.

### 20. Which devices does it run on?

iPhone, iOS 17 or later. There is no iPad, Mac, Android or web version.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
