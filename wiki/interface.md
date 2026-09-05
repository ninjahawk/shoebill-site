---
layout: default
title: Interface
nav_order: 4
---

# The interface

## The five tabs

The tab bar carries five tabs, shown as icons.

1. **Home** — the timeline.
2. **Explore** — search, and what is happening now.
3. **Ask** — the assistant.
4. **Shorts** — a full-screen vertical video feed.
5. **Notifications** — local alerts about posts worth returning for.

Tapping the tab that is already selected scrolls to the top; it does not
refresh. Which tab the app opens on is a setting: the last one used, the
timeline, or the video feed.

## Home, and its tab strip

Above the timeline is a horizontally scrolling strip of tabs. The first two are
always present:

- **For you** — the ranked feed, described on the
  [feed page]({{ site.baseurl }}/wiki/feed.html).
- **Latest**, which becomes **Following** when a Mastodon account is connected.
  The label changes because the feed changes: signed out it is the federated
  firehose from the servers that serve it publicly, in the order it arrived;
  signed in it is the Mastodon home timeline of the accounts that account
  follows. Bluesky is not merged into this tab.

Any number of further tabs can be pinned to the strip, from the button at its
right-hand end. Three kinds can be pinned: a **hashtag**, including any hashtag
typed in by hand; a whole **network**, so that a tab shows only Mastodon, only
Bluesky, only Hacker News, only Lemmy, only Lobsters or only 4chan; or a
**channel**.

## Channels

A channel is a named bundle of communities, feeds and searches drawn from more
than one network, with a quality floor applied before ranking: a post has to
beat the median score of its own pool to be included, no account may appear
more than three times, and some channels require a picture.

Five channels ship: **Shitposting**, **Science**, **Comics**, **Animals** and
**Funny**. A channel is a virtual place assembled inside the app from measured
public feeds. It does not correspond to an account anywhere, nothing is posted
to any network to create one, and every post inside it shows the counts its own
network reported.

## Explore

A search field, and six sections: **For you**, **Trending**, **News**,
**Sports**, **Markets** and **Tags**. Search runs as text is typed and covers
posts, accounts and hashtags across the networks at once.

Sports and Markets are live public data rather than posts: scores, event odds
and coin prices, shown as cards. They are not ranked and are not mixed into the
timeline.

## Posts

A post shows its author, its network, its text with content warnings intact,
its media, and a row of actions: reply, like, repost, and a fourth slot showing
**reach** — the number of independent servers that surfaced the post. That slot
holds a view count in other apps. Neither Mastodon nor Bluesky reports view
counts, so rather than showing a number the app does not have, it shows one it
does, and one nothing else shows.

The overflow menu on a post offers Not interested, Report post, Block the
account, and Block everything from that domain.

## Shorts

A full-screen vertical video feed with its own sources and its own ranker. The
videos come from Bluesky's public video feeds, which supply the large majority,
and from video attachments on Mastodon's trending posts.

Gestures: swipe up and down to page, double-tap to like, single tap to pause
and resume, press and hold for a menu of Not interested, Report and Open
original, and swipe left for the creator's page.

The ranker is separate from the timeline's. In outline: adult material is
dropped on labels and word lists rather than blurred; anything over 48 hours,
over three minutes or under three seconds goes; a video needs roughly three
reactions an hour since it was posted and ten in total, so that a clip nobody
reacted to does not ride recency to the top; and a source under 720 pixels on
its short side is dropped. What survives is scored on reactions per hour, then
adjusted by age, by subject read from the caption and hashtags, by aspect ratio
— a wide clip scores lower because the player is vertical and a letterboxed
video fills half the screen — and by what the phone's own vision framework can
see in the still frame. From slot fifteen, one in eight is drawn from the
lower-traction pool, so the feed does not close in on itself.

What the video ranker cannot do is the important part: **it has never watched a
video.** It reads the poster frame, not the footage, so editing, camera work,
a burned-in watermark and stolen audio are all invisible to it. It does not
know whether a video is funny; it knows that the caption used a word from a
list. And the counts it ranks on are the counts of the network the video was
posted to, which for a clip reposted from elsewhere may bear no relation to how
widely it was actually seen.

## Ask

Ask answers questions from live retrieval across the networks. It has two
modes, and which one is used depends on the phone.

**Search, the common case.** The question is routed to one of three retrieval
paths — what is trending, what links are being shared, or a summary of the last
few hours — and the result is shown as a structured list of what was found,
with its sources. There is no language model involved, and the app says so: the
composer is labelled Search, and the empty state reads "Questions typed here
use search only on this iPhone. The on-device assistant needs Apple
Intelligence."

**On-device, where Apple Intelligence is available.** The same retrieval runs,
and a model running entirely on the phone classifies the question and then
writes the answer from the numbered results it was handed, citing them. Nothing
is sent to any server, and the answer carries the line "Answered on this phone
from what the tools above found. Check the sources."

This second mode requires iOS 26 and a device that supports Apple Intelligence,
which in practice means iPhone 15 Pro and later. On every other iPhone, Ask is
the search mode, and it is labelled as such rather than degraded silently.

Three starting questions are offered: what is trending right now, what links
people are sharing, and a catch-up on today.

## The drawer

Swiping in from the left edge, or tapping the avatar, opens a drawer holding
Profile, Bookmarks and Settings. Signed out, it says so plainly: "Browsing
signed out. Everything here works without an account."

## Swipe back

Settings, Bookmarks, threads and profiles are dismissed by swiping from the
left edge, in the way system screens are. The gesture requires horizontal
movement to clearly exceed vertical movement, so that it does not fire while
scrolling.

## Settings

In order:

- **Accounts** — one row per connected account, or the options to add a
  Mastodon account and connect Bluesky.
- **Appearance** — Light, Dim, or Lights out. Lights out is the default.
- **Open to** — Last used, Timeline, or Videos.
- **Notifications** — Best posts, a few times a day. They are scheduled by the
  phone from content already fetched: at most four a day, and none between
  10 pm and 8:30 am. There is no push server.
- **Content** — Show sensitive media, off by default. Hide flagged posts,
  which removes adult posts, on by default.
- **Saved posts** — the size of the offline reserve. See
  [offline]({{ site.baseurl }}/wiki/offline.html).
- **Muted words** — the list, and a field to add one.
- **Your interests** — what the ranker has learned, with a button to forget it.
  It stays on the phone.
- **Blocked accounts** and **Blocked servers** — each with an unblock control.
- **Your reports** — shown once a report has been filed.
- **Support** — contact support, and the privacy policy.
- **About** — the version.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
