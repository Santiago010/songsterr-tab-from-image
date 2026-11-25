# songsterr-tab-from-image

A Claude skill that takes a guitar tab from an image and writes it into the Songsterr editor. You give Claude a screenshot of a tab, say "create this in Songsterr," and it enters the tab note by note in your Chrome tab, with the rhythm, the techniques, and the repeats.

It started as a practical problem. Copying exercises from a PDF or a photo into Songsterr by hand is slow, and the editor has a right-click menu with almost a hundred buttons. Claude could already use it, but it kept tripping over things like a triplet carrying over into the next note, or the menu opening on the left one time and on the right the next. The skill writes down what has worked and what hasn't.

## What you need

- Claude with the Claude in Chrome extension.
- A Songsterr account with the tab open in the editor (the pencil button on the right turns blue). It can be a new, empty tab or one you've already started.
- The screenshot of the tab. It works better when the rhythm stems, or standard notation above the tab, are visible.

## How to use it

Open the tab in the Songsterr editor, give Claude in Chrome the image, and ask something like:

> Create this tab in Songsterr.

You don't need to name the skill. Claude loads it on its own when it sees you want a tab moved from an image into Songsterr.

## What Claude does

First it reads the image and makes a plan, bar by bar: string, fret, note value, whether it's a triplet, and which technique each note has. Before touching the editor it checks that every bar adds up. If one doesn't, it reads it again. If the image is blurry or cropped, it asks for a better one.

Then it writes in two passes. The first pass is notes and rhythm. The second is everything else: hammer-ons, pull-offs, slides, bends, palm mutes, harmonics, accents, and dynamics. It works this way because a hammer-on or a slide needs the next note to already be there.

Last, it adds what applies to whole bars (repeats, first and second endings, chords, sections, tempo), checks each bar against the image, and tells you what it wrote, what it wasn't sure about, and what it left out.

The tab is never saved or published on its own. Claude leaves it in the editor and asks you first, because publishing on Songsterr makes it visible to everyone.

## What it covers

- Note values from whole notes to sixty-fourths, dotted and double-dotted.
- Rests, triplets, and other tuplets.
- Ties and fermatas.
- Hammer-ons, pull-offs, all six kinds of slide, bends, vibrato, and the whammy bar.
- Palm mute, let ring, dead notes, ghost notes, and harmonics.
- Accents, staccato, pick direction, trills, tapping, grace notes, and tremolo picking.
- Dynamics from ppp to fff, crescendo, and diminuendo.
- Repeats, alternate endings, swing, tempo, time signature, pickup bars, chords, sections, and annotations.

The skill includes a table that maps each symbol you might find in a tab (h, p, /, b, ~, P.M., x, <12>…) to the Songsterr button for it.

## What still needs testing

So far only a few buttons have actually been used in the editor: note values, triplets, repeats, the pin that keeps the menu open, and deleting notes. The rest are described by their Songsterr name and by what that mark means in any tab. For those, the skill tells Claude to zoom in and check what each one did the first time it uses it.

Three things are still open: how to pick a bend's amount, whether an empty beat already counts as a rest, and how Songsterr draws marks that span several notes, like palm mute or let ring. If one of them comes out wrong, it's worth updating the skill with what you saw.

It also doesn't touch tuning or capo. Those settings live in the track settings, not in the note menu. If the image says Drop D or shows a capo, Claude tells you.

## Language

This version of the skill is written in English, but the button names are the ones Songsterr shows when its interface is in Spanish, because that's how it was set up when the menu was read. Each button is listed with its English meaning and its exact Spanish label. If your Songsterr is in English, the labels will be different, so Claude reads the real labels from the menu and finds each button by what it does instead of guessing its name.
