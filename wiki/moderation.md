---
layout: default
title: Moderation
nav_order: 5
---

# Moderation

Shoebill shows public posts from networks it does not moderate. It cannot
review that material before it is published, and it does not claim to. What it
can do is decide what reaches the reader, give the reader controls that work
without an account, and answer reports. All of that runs on the device.

Nothing here should be read as a claim that the app is safe or curated. The
accurate statement is narrower: content flagged by the networks' own labelling
services is dropped before it reaches the reader, several further filters run
locally, and the reader can remove anything else.

## What runs before a post is shown

These checks run in order, on the phone, on every post from every source.

### 1. The source network's own verdict

- **Mastodon's sensitive flag.** A post an instance has flagged is dropped by
  default. This is a separate control from the sensitive-media setting,
  deliberately: a blurred adult post is still an adult post in a general feed.
  A reader who wants flagged posts can turn that off in Settings.
- **Mastodon content warnings.** A content warning is the author's own short
  line of text standing in front of their post. It is kept, shown in the
  author's wording, and the post opens on a tap. Content warnings are a normal
  part of the network's culture rather than a mark against a post, and they are
  never stripped.
- **Bluesky labels.** Labels attached by Bluesky's own moderation service are
  read and acted on. The ones treated as adult or otherwise disqualifying are
  `porn`, `sexual`, `sexual-figurative`, `nudity`, `nsfw`, `adult`,
  `graphic-media`, `gore`, `corpse`, `torture`, `nsfl`, `self-harm`,
  `extremist`, `intolerant`, `threat`, `illicit`, `csam`, `child-abuse`,
  `sensitive`, `!hide`, `!warn`, `!takedown` and `!no-unauthenticated`. Both
  post labels and account labels count: an account labelled at the account
  level is treated as adult in every post it makes. A labelled post is dropped
  while Hide flagged posts is on, which is the default, and blurred when it is
  off.
- **Sources with no verdict.** 4chan supplies none of the above — no sensitive
  flag, no content warning, no label, no vote. On that source the app's own
  filters remove a post where they would blur one from another network.

### 2. Hate speech

A lexicon of slurs is applied to every source, not only to the ones with no
moderation of their own, because there is no argument for holding one network
to a lower bar than another. It matches whole words after normalisation, and it
deliberately leaves out terms that are ordinary words far more often than they
are slurs — removing a post for one of those costs more than it buys.

### 3. Adult text

Separate word, phrase and hashtag lists catch adult and explicit material that
carries no label, in the post's text, its hashtags and the account's handle and
display name. A further list applies only in the video feed, where a small
vocabulary is adult in that context and harmless elsewhere; it fires on
combinations rather than on single words, because a single one of those words
is usually a dog's harness.

These lists are blunt instruments and they produce false positives. That is the
chosen trade: in a general feed, over-removal costs less than what gets through
without them.

### 4. The on-device picture check

Text filters cannot see a picture, so every image the feed loads is classified
on the device before it is shown, by a small image classifier that ships inside
the app. Nothing is uploaded, no picture leaves the phone, and the check works
with no network connection.

The classifier returns five categories. Two of them gate content, at these
thresholds:

| Category | Threshold | Effect |
|:--|:--|:--|
| Pornography | 0.90 or above | flagged |
| Pornographic drawing | 0.95 or above | flagged |
| Suggestive | never gates, at any value | none |
| Drawing | never gates | none |
| Neutral | never gates | none |

A flagged picture removes its post outright while Hide flagged posts is on,
which is the default. With that setting off, the picture is blurred behind a
tap instead.

The second threshold is set higher than the first because that category's
failure mode is systematic rather than random: it fires on ordinary
illustration, and the highest false positive observed while the thresholds were
being chosen reached 0.82. The rule that the suggestive category never gates
anything is written into the code even though it costs nothing today, so that a
later adjustment cannot quietly reintroduce over-removal.

Pictures below 120 pixels on the short side are not classified, because a
thumbnail that small carries too little to judge. The check runs after a
picture has been decoded, on its own background queue, so that it never holds
up the feed; a picture that turns out to be flagged is therefore withdrawn a
moment after it loads rather than never appearing at all. Verdicts are cached
on the device so that the same picture is not scored twice, and the cache also
covers pictures held in the offline reserve.

Measured on a sample of 298 pictures drawn from the sources in use, this policy
withheld one picture (0.34 per cent) and dropped no posts. There was no
pornography in that sample, so it produced no measurement of how much
pornography it catches. Both halves of that sentence belong together.

### 5. The reader's own lists

Blocks and mutes are applied last and override everything above.

## Controls

All of these work while signed out, and all of them are stored on the device
and applied by the device. They are not synchronised with a block list held on
Mastodon or Bluesky, in either direction: blocks made in another client do not
appear here, and blocks made here are not sent there. No blocklist of domains
ships with the app; the list starts empty and holds only what the reader put in
it.

- **Block an account.** The overflow menu on any post. Their posts stop
  appearing.
- **Block a whole server.** The same menu. Everything from that domain is
  dropped.
- **Mute a word or phrase.** Settings, Muted words. Any post whose text or
  content warning contains it, anywhere and in any case, is removed from the
  feed. The match is on the characters, not on whole words.
- **Sensitive media.** Off by default: the app never opens onto unblurred
  sensitive media from strangers.
- **Hide flagged posts.** On by default, and a separate control from the one
  above.

## Reporting

Every post and every account has a Report action in the overflow menu.

The categories match the ones Mastodon itself uses, so a report needs no
translation when it is forwarded: Spam, Illegal content, Breaks a server rule,
and Something else. A note can be added.

What happens when a report is filed:

1. The post is hidden immediately on the device, and the report is recorded
   under Settings, Your reports.
2. The mail app opens with a message addressed to the support address,
   pre-filled with the post's address, the account, the network, the chosen
   category, any note and the app version. It is sent by the reader, from the
   reader's own mail account. The app says which of these happened: that the
   report was forwarded to the server, that the mail is ready to send, or that
   the report was recorded when no mail app could be opened.
3. If a Mastodon account is connected and the post is a Mastodon post, the
   report is additionally sent to that account's own server through Mastodon's
   public reports API, so a moderator there can act on the account.
4. The same sheet offers to block the account at the same time.

**Reports are answered within 24 hours**, at icebreakermint10@gmail.com. The
address is published here, in the app under Settings, Support, and on the
[support page](/support.html).

## The rules this satisfies

**Apple's App Store guideline 1.2**, which governs apps showing user-generated
content, requires four things. Each is in place before submission rather than
after a rejection:

- **Filtering of objectionable material.** The sensitive flag, content
  warnings, Bluesky's labels, the hate and adult text lists and the on-device
  picture check, described above.
- **A mechanism to report offensive content, with timely responses.** The
  report flow above, and the 24-hour answer.
- **Blocking of abusive users.** Account blocks, domain blocks and muted words,
  all of which work with no account.
- **Published contact information**, reachable from inside the app.

**Bluesky's developer guidelines** require an app carrying user-generated
content to provide a way to report illegal content, a way to block forbidden
content, a way to block abusive users, deletion on request, a system for
responding to user reports, and a monitored public contact address. The same
mechanisms cover all six.

## What this does not do

- It does not review anything before publication, on any network.
- It cannot read a picture for meaning beyond the categories above and the
  object labels the phone's own vision framework produces.
- It cannot tell satire from sincerity.
- The word lists are word lists: material that avoids those words passes
  through.
- Blocks and mutes made in another client are not imported; the device's lists
  are the ones the app applies.
- The hate-speech list drops a post outright on every source. The adult text
  list flags rather than drops, which means it removes the post while Hide
  flagged posts is on and blurs it when that setting is off.

---

Contact: [icebreakermint10@gmail.com](mailto:icebreakermint10@gmail.com) — reports are answered within 24 hours. Not affiliated with any network shown.
