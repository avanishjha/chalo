# Chalo!

An interactive trip album for Indian Dream Travel, showing India to travellers since 2009: cultural trips and Himalayan adventures told as comic pages, with 300-year-old Rajput paintings cut into moving paper puppets.

**Live:** https://avanishjha.dev/chalo/

![The Chalo! hero: a Mewar painting of a prince on a blue horse inside a cusped arch, with the Chalo! wordmark](preview.jpg)

![The puppet caravan walking across the desert on the About page, and the Pink City chapter with an elephant puppet stepping out of its panel](preview-2.jpg)

> **Work in progress.** This is a design prototype, not the client's live site. Nights, contact details and policies in brackets (`[n] nights`, `[WhatsApp number]`) are placeholders, there is no WhatsApp number wired in yet, and pricing is deliberately left as a surprise until the price list is ready. The page asks search engines not to index it.

## What happens on the page

- **Arrival.** An ink stamp flips through silhouettes of the puppets, then morphs into a cusped Mewar arch.
- **Puppet hero.** A Mewar painting (about 1700) is cut into five pieces. The horse rocks and swishes its tail, the attendant waves his fly whisk, and a camel from another painting photobombs from the edge. Each layer moves with the pointer at its own depth, and hovering a figure glitches it with a short red and blue split.
- **Painting to ink.** Scrolling turns the painting into its own ink drawing, then an iris of colour opens onto the trips.
- **Trip carousel.** Seven ways in, as perforated stamps in an endless 3D carousel you can grab and drag. Behind them, a small WebGL shader draws rings in the active trip's colours, and each trip repaints the screen.
- **Next stop is loading.** Opening a trip gives a short dark beat over a faint ink drawing of that place, then a wavy curtain lifts onto the chapter.
- **Comic chapters.** Native scroll drives a camera across tilted comic pages, panel by panel. Ek the one-humped camel travels north through every chapter and meets Do, the two-humped one, in Nubra (ek and do mean one and two in Hindi). Trip facts sit in captions, speech bubbles pop in when the camera arrives, sound words (THUD., CHHAPAK!, POM POM!) break past the panel borders, each panel has a small loop of its own (water, clouds, snow, stars, Holi colour), a brass lantern swings when the camera moves, kites fly over Jaipur, and an elephant puppet with two riders steps out of its panel.
- **Optional sound.** Off by default. A camel bell and the comic's sound words, synthesised in the browser with no audio files.
- **About us.** A scroll-driven caravan of puppets walks from the desert into the mountains while the story since 2009 plays out above it.
- **Your message.** Trips you add, plus a few quick questions, are written into a WhatsApp or email message you can edit before sending. There is no login, booking or payment.

## How it works

- Plain HTML, CSS and JavaScript, built with Vite. No framework.
- Native scroll is the source of truth, smoothed by Lenis on desktop and left to native momentum on touch. Each chapter is a tall section with a sticky stage; a damped camera eases between panel keyframes, then settles on the nearest panel when scrolling stops.
- One ticker drives everything, and motion is GPU-only (transform and opacity on promoted layers), so nothing repaints per frame.
- The puppets are transparent cut-outs made from the museum scans with Segment Anything, one click-prompted cut per coloured part, finished with hand-traced details. Each piece rotates around its own joint with the Web Animations API. Phones load smaller copies.
- The ink drawings are made with an extended difference-of-Gaussians filter.
- The rings are one fragment shader at half resolution, paused when off screen.

### Accessibility and fallbacks

- **Reduced motion:** with `prefers-reduced-motion`, the camera, loader and carousel switch off. The pages stack as plain readable comics, and the hero is a still painting.
- **Keyboard:** the arrow keys move panel by panel, and every control can be reached with Tab.
- **Without JavaScript:** the page still reads top to bottom.

## Run it locally

Any static server works. From this folder:

```bash
python -m http.server 8000
```

Then open http://localhost:8000/. Opening `index.html` straight from disk will not work, because the scripts are ES modules.

## What's in this repository

This repository holds the built site only, ready for GitHub Pages:

```text
index.html        the page
about/            the About us page
assets/           built JavaScript and CSS
img/art/          paintings (Cleveland Museum of Art, CC0)
img/puppets/      puppet pieces cut from those paintings (full and -sm phone sizes)
img/ink/          ink drawings of chapter photos
img/*.webp        photos (Wikimedia Commons)
```

Network: fonts load from Google Fonts. Everything else is in this folder.

## Credits and inspiration

- **Paintings:** Cleveland Museum of Art Open Access, CC0.
- **Photos:** Wikimedia Commons, under CC BY, CC BY-SA and FAL licences. Every photographer, licence and source link is listed under "Picture credits" at the bottom of the page.
- **Inspiration:** the comic-camera idea, puppet characters and loading beats are inspired by [Ponpon Mania](https://ponpon-mania.com/). This project is not affiliated with it, and it uses none of its art or code.

No licence is granted for reusing the code in this repository. The images keep their own licences, listed on the page.
