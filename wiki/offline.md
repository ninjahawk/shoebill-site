---
layout: default
title: Offline
nav_order: 7
---

# The offline reserve

The app keeps a rolling store of recent posts on the phone so that opening it
with no signal shows a feed rather than an error. This is called the reserve.

## What is saved

**Posts.** The text of a post, its author, its counts and the network it came
from, written as a file in the app's own Application Support directory. Nothing
about the reserve leaves the phone.

**Pictures, when they survive.** Images are held in the app's image cache on
disk, which is shared with normal scrolling and is transient: iOS may clear it
when the device is short of storage. A reserve entry is therefore guaranteed
its text and not its picture, and a text-only entry is still kept, because text
is what stops the reserve reaching zero.

**Never video.** Video files are large and a reserve of text and pictures is
what fits in a phone's spare space. Video is never cached.

**Never adult material.** The same check that keeps adult content out of the
feed runs before an entry is written to disk, and runs again over anything an
earlier version of the app left in the file, so an update scrubs the store
rather than trusting it.

## The size setting

Settings, Saved posts, offers four values:

| Setting | Posts held |
|:--|:--|
| Off | none |
| 200 | 200 |
| 1,000 | 1,000 |
| 5,000 | 5,000 |

The default is 200. The setting screen shows how many posts are currently held
and how much space the reserve and its pictures are using.

## How it fills and empties

The reserve is filled on every successful load of the main feed, including a
refresh the system runs in the background: posts that pass every filter are
appended as they are ranked. There is no separate download step and no
wi-fi-only restriction. Reading from the reserve never removes anything from it
— entries are rotated, so a post that has never been served is offered before
one that has, and the least recently served comes next.

Entries leave the store in three ways only: they expire after a week, they are
pushed out when the store is at its size limit, or they are removed because a
moderation setting, a block or a mute now excludes them.

The moderation rules are re-applied to the stored entries every time the feed
loads, so a block, a mute or a change of setting takes effect on the reserve as
well as on the live feed.

There is no separate clear button: setting the size to Off empties the reserve
and deletes the file. Deleting the app removes it along with everything else.

## What it looks like in use

When the app is showing reserve content rather than a live fetch, it says so on
the screen: a line reading that it is offline and showing saved posts, and,
once the reserve has been read through, that there is nothing further. A post
from earlier in the day behind a line that admits it is offline is more useful
than an empty screen, and the app does not pretend the content is live.

The Saved posts screen shows how many posts are held and how much space they
and their pictures are using.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
