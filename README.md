# MailerLiteTube

A video player that looks like YouTube and only has five videos on it, all of
them me answering the questions on a job application.

**Live:** https://badcristian.github.io/lite/watch/

MailerLite's PHP Engineer posting asks you to skip the CV and build a landing
page in their own page builder instead. This is what I embedded in mine. It was
built for fun, for one interview, and it has no purpose beyond that.

## What it does

It is a working single-page client, not a screenshot:

- **Home grid and watch view**, with routing — `?v=2` deep-links straight to the
  third video, back/forward work, and reloading keeps your place.
- **Light and dark themes.** Light is the default; the choice is remembered in
  `localStorage`.
- **Hover previews.** Point at a card for a moment and the thumbnail starts
  flipping through the video's own storyboard frames, then swaps to the muted
  player — the same two-stage trick the real site uses.
- **Collapsible rail** that folds itself away when a video opens, plus a proper
  slide-over drawer on narrow screens.
- **Search, filter chips, comments, subscribe, the notification bell with the
  little 9+ on it** — the furniture is all there because a half-drawn copy looks
  worse than no copy at all.

Some of that furniture is decorative. The channels down the left side are
invented, the counts on the buttons are not real analytics, and every video
honestly reports **one view**, because that is how many it has. Nothing on the
page claims a number it did not measure.

## How it works

One file. `watch/index.html` is around 630 lines of plain HTML, CSS and
JavaScript with **no framework, no dependencies and no build step** — open it in
a browser and it runs.

- **The videos** live in a `<script type="application/json">` block near the
  bottom of that file. Edit the array, reload, done. Leave an `id` empty and the
  card renders an explicit placeholder rather than a dead player.
- **The players** are ordinary `youtube-nocookie.com` iframes. Clicking a card
  passes `autoplay=1`, so it plays on the first click rather than the second.
- **Preview frames** come from `i.ytimg.com/vi/<id>/hq1|hq2|hq3.jpg`, the
  storyboard stills YouTube generates at the 25/50/75% marks. They are about
  13 KB each, so a hover costs almost nothing.
- **Icons** are inline SVG paths, drawn to match. No icon font, no sprite sheet.
- **The layout** is CSS Grid. The one genuinely fiddly part is that the whole
  thing is embedded in someone else's page builder, whose mobile preview fakes a
  phone by narrowing a column inside a window that is still 1600px wide. `100vw`
  lies in that situation, so the embed sizes itself with a **container query**
  against its actual column instead of the viewport.

`index.html` at the root is a six-line redirect to `watch/`.

## Running it

```
git clone https://github.com/badcristian/lite.git
open lite/watch/index.html
```

There is no install step, because there is nothing to install.

## Credit where it is due

The visual design is YouTube's, reproduced by hand as an exercise. I am not
affiliated with YouTube or with MailerLite, the logo is my own wordmark rather
than theirs, and the whole thing exists because writing a CV sounded less
interesting than writing this.
