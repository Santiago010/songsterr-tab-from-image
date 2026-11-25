---
name: songsterr-tab-from-image
description: Transcribe a guitar tab from a screenshot into the Songsterr editor with Claude in Chrome (notes, rhythm, rests, triplets, techniques, dynamics, repeats). Use whenever the user asks to create a tab in Songsterr from an image.
---

# Tab from an image into the Songsterr editor

The user gives you a screenshot of a guitar tab (sometimes with standard notation above it) and wants it written in the Songsterr editor, in the tab they already have open in Chrome. The job has three parts, and each one prevents a different kind of mistake:

1. **Read the image and write a plan**, bar by bar. Most transcription errors are reading errors, not clicking errors, and they are much cheaper to fix in the plan than in the editor.
2. **Write in the editor in two passes**: notes and rhythm first, then techniques and expression marks.
3. **Check every bar** against the image before moving on.

## About button names

Songsterr labels its buttons in the UI language (the label lives in each button's `aria-label`). The labels below were read from a Songsterr editor set to **Spanish**, so each button is listed as *English meaning* followed by the exact Spanish label in «quotes». If the editor is in Spanish, match those labels exactly. If it is in English or another language, the labels will differ: list the real labels with the snippet in section 7 and match them by meaning. Don't guess an English label and click it blind.

Buttons marked *(tested)* were used in the real editor and behaved as described. The rest are known by their name only: the first time you use one, zoom in and check what it did.

## 0. Set up the browser

- If the `chrome-browser` skill is listed, load it. Load the Chrome tools in a single ToolSearch: `tabs_context_mcp`, `navigate`, `computer`, `find`, `read_page`, `javascript_tool`, `browser_batch`.
- Use `tabs_context_mcp` to find the Songsterr tab that already has the editor open. Working in the user's own tab is right here, because that is where their tab lives. If there is none, ask them to open the tab (new or existing) in the editor and tell you when it's ready. Don't create accounts or publish tabs on your own.
- The editor is active when the pencil button on the right is blue. The cursor is an amber box over the tab.

## 1. Read the image and write the plan

Before touching the browser, write down:

- **General info**: time signature (4/4, 3/4, 6/8…), tempo (♩ = 90), tuning and capo if shown, swing («♫ = ♪³», "Shuffle"), section names, and chord names written above the staff.
- **One table per bar**, one row per beat. A *beat* here means one column: everything that sounds together (a chord, a note with its bass) is a single beat.

```
Bar 1 (4/4). Sum: ⅓+⅓+⅓ (1) + ¼×4 (1) + 1 + 1 = 4 ✓
beat | string/fret | value | group   | techniques and marks
1    | 6/5         | 1/8   | triplet | —
2    | 6/8         | 1/8   | triplet | pull-off to next
3    | 5/5         | 1/8   | triplet | —
4    | 5/7         | 1/16  | —       | accent
…
```

**Check that every bar adds up.** In 4/4 you need 4 quarter-note beats: quarter 1, eighth ½, sixteenth ¼, thirty-second ⅛, half 2, whole 4. A dot adds half the value. Three triplet eighths equal 1 beat; three triplet quarters equal 2. If a bar doesn't add up, you misread something, so look at the image again before going on. Songsterr shows a **red «!»** under any bar that doesn't add up, so a misread bar turns into a broken bar.

### Reading rhythm from a tab

- If there is standard notation above the tab, take the rhythm from it. It's the most reliable source.
- If there's only tab, rhythm is in the stems under the fret numbers: stem with no beam = quarter; one beam or flag = eighth; two = sixteenth; three = thirty-second; a short stem or a circled number (depends on the engraver) = half; no stem = whole. A dot next to the stem = dotted. A bracket with "3" = triplet; with "5", "6"… = other tuplets.
- If the image has no rhythm at all, ask the user, or assume even eighths and say so at the end.
- A fret number in parentheses is usually the **continuation of a tied note** (same fret on the same string as the note before, often with an arc). If the fret doesn't match the previous note, it's a **ghost note**.

### When something is unreadable

If it's one or two notes, write your best reading and mention them at the end. If the image is cropped, blurry, or missing half a bar, ask for a better screenshot before you start. Half a tab built on guesses costs the user more than the wait.

## 2. From the image to the button

Which button to use for each thing you can see in a tab. The full menu reference is at the end.

| In the image | What it is | Songsterr button (Spanish label) |
|---|---|---|
| Rest symbols | Rest | Rest «Silencio» + the right duration |
| Bracket with 3 | Triplet | Triplet «Tríada» *(tested)*, on all three notes |
| Bracket with 5, 6, 7… | Tuplet | ⋮ next to Tuplets «Grupos irregulares» → «Quíntuple», «Séxtuple»… |
| Dot after a note | Dotted | Dot «Puntillo» (or Double dot «Doble puntillo») |
| Arc between equal frets, or (5) | Tie | Tie «Ligadura a la nota anterior o siguiente» |
| 𝄐 | Fermata | Fermata «Calderón» |
| h, H, arc up to a higher fret | Hammer-on | «Hammer-On / Pull-Off» |
| p, P, arc down to a lower fret | Pull-off | «Hammer-On / Pull-Off» |
| / or \ between two frets, "sl." | Slide | «Legato slide» (2nd note not picked) or «Shift Slide» (2nd note picked) |
| / or \ before a fret, no note before | Slide in | Slide in from below «Slide desde abajo» / from above «Slide desde arriba» |
| / or \ after a fret, going nowhere | Slide out | Slide out downward «Slide hacia abajo» / upward «Slide hacia arriba» |
| b, ↗ with "full", "½", "¼" | Bend | «Bend» (choose the amount) |
| r, pb, ↘ after a bend | Release | «Bend», if its options include release (untested) |
| ~~~, "vib." | Vibrato | «Vibrato» (⋮ for slight or wide) |
| "w/bar", "dive" | Whammy bar | Tremolo bar «Palanca de Trémolo» |
| P.M. with a dashed line | Palm mute | «Palm mute», on every note under the line |
| x instead of a fret | Dead note | Dead note «Nota muerta» |
| (5) with no tie | Ghost note | Ghost note «Nota fantasma» |
| <12>, "N.H.", "Harm." | Natural harmonic | «Armónico natural» |
| "A.H.", "P.H.", [12] | Artificial harmonic | «Armónico artificial» |
| "let ring" with a line | Let ring | «Sonido largo» |
| > | Accent | «Nota acentuada» |
| ^ | Heavy accent | «Nota fuertemente acentuada» |
| Dot above or below the note | Staccato | «Staccato» |
| ⊓ / V | Downstroke / upstroke | «Golpe hacia abajo» / «Golpe hacia arriba» |
| "tr" | Trill | «Trino» |
| T, "tap" | Tapping | «Tapping» |
| Small fret number before a note | Grace note | Grace note before the beat «Nota de gracia antes del pulso» (or on the beat «Nota de gracia en el pulso») |
| Slashes through the stem | Tremolo picking | «Trémolo 1/8» (⋮ for 1/16, 1/32) |
| ppp, pp, p, mp, mf, f, ff, fff | Dynamics | Dynamics «Dinámicas» |
| "cresc.", opening hairpin | Crescendo | «Crescendo» |
| "dim.", "decresc.", closing hairpin | Diminuendo | «Diminuendo (Decrescendo)» |
| Wavy arrow next to a chord | Arpeggio / rake | Arpeggio up «Arpegio ascendente» / down «Arpegio descendente» |
| ‖: and :‖ | Repeat | Repeat start «Inicio de repetición» / repeat end «Fin de repetición» *(tested)* |
| "x3", "x4" above :‖ | Repeat count | The number in the repeat-end dialog |
| Boxes 1. and 2. | Alternate endings | «1ª vez y finales alternativos» |
| ‖ double bar | Section end | Double bar line «Doble barra de compás» |
| Am7, G… above the bar | Chord | Chord «Acorde» |
| "Intro", "Verse", boxed "A" | Section | Section «Sección» |
| Free text ("slow", "finger 4") | Annotation | «Anotación» |
| ♩ = 100 | Tempo | «Tempo» |
| 3/4, 6/8 | Time signature | Time signature «Compás» |
| Deliberately short first bar | Pickup | Toggle pickup «Alternar anacrusa» |

If the image has something that isn't in this table or in the menu, don't fake it with a different mark. Leave it out and say so at the end.

## 3. Prepare the editor

- **Time signature and tempo**: if the image isn't in 4/4 or shows a tempo, set them on the first bar with «Compás» and «Tempo». Songsterr's default tempo is 120.
- **Tuning and capo** aren't in this menu; they belong to the track settings. If the image says Drop D, half step down, or capo, take a screenshot to see whether the track settings are visible. If they aren't, tell the user instead of guessing.
- **Pin the menu** with «Fijar la barra de herramientas abajo» (pin the toolbar to the bottom) *(tested)*. Without the pin, every click on a menu button closes the menu, and you have to right-click the note again for each change. Pinned, the menu stays open in a fixed spot and you move the cursor with the arrow keys. It's much faster.

## 4. First pass: notes and rhythm

### Keyboard *(tested)*

- **↑** moves to the higher-pitched string (toward string 1); **↓** to the lower one (toward string 6).
- **→** goes to the next beat; **←** to the previous one.
- Type the fret number. Two-digit frets are typed straight through: `12`.
- **Backspace** deletes the note under the cursor (same as «Eliminar nota»).
- **Escape** closes the menu when it isn't pinned.

### Rhythm carries over *(tested)*

Every new beat starts with the duration of the one before it, triplet included. Use this: set the duration only on the first note of each group, and the rest come out right. The flip side: right after a triplet, the next new note is also born as a triplet. If it shouldn't be, press «Tríada» again to remove it (it's a toggle) and set its duration.

### Order for each beat

1. Type the fret. If the beat has several strings, move with ↑/↓ and type each one **without** pressing → in between.
2. If the duration differs from the previous beat: «Establecer duración 1/…» (set duration) and, if needed, «Puntillo» or «Tríada».
3. Press → to go to the next beat.

Until a triplet is complete you'll see the red «!», and that's normal. When you finish a bar, the «!» has to be gone. If it's still there, fix it **before** moving on: in an incomplete bar, → adds more beats to the same bar and the following notes land in the wrong bar.

### Rests

With the cursor on a beat, «Silencio» turns it into a rest of that beat's duration. For a rest in the middle of a phrase: → to the beat, set its duration, press «Silencio». It hasn't been tested whether an empty beat already counts as a rest; check whether the «!» goes away.

### Going fast

Group predictable sequences (keys, numbers, arrows) into a single `browser_batch`, and end each batch with a zoom on the bar. You don't need a screenshot after every note.

## 5. Second pass: techniques, expression marks, dynamics

This is a separate pass for two reasons. Hammer-ons, slides, and ties need the next note to already exist on the same string. And once the rhythm is right, a misplaced technique can't break the bar's count.

- Put the cursor on the note (click its number or use the arrows) and press the button.
- **Hammer-ons/pull-offs, slides between two notes, and ties** go on the **first** note of the pair, and both notes must be on the same string.
- **A greyed-out button** doesn't apply where the cursor is. Usually the cursor is on a rest or on an empty string of the beat: move it onto the note.
- **The ⋮** next to a button opens its variants (vibrato types, tremolo picking speeds, tuplets, swing types, alternate endings).
- **Bend**: probably opens options for how far it goes. Take a screenshot when it opens and pick according to the image: "full" = whole step, "½" = half step, "¼" = quarter step.
- **Marks that span several notes** (palm mute, let ring, long vibrato, crescendo): apply them to every note under the line. After the first two, check how Songsterr draws them, in case it joins them on its own.
- **Dynamics**: only where the image shows a change. Everything defaults to mf, and each dynamic lasts until the next one.
- **Pick direction (⊓ V)**: only if the image marks it. Don't add it yourself.

## 6. Bar-level elements

These act on the bar where the cursor is, not on a single note.

- **Repeats** *(tested)*: «Inicio de repetición» on the first bar of the block and «Fin de repetición» on the last. Repeat end opens a dialog with the number of times: enter what the image says (2 if it says nothing) and press «Aplicar» (Apply). If Songsterr warns «La repetición no está abierta» (the repeat isn't open), the block is missing its start. A block that repeats from the very beginning of the song can go without a start.
- **Alternate endings**: «1ª vez y finales alternativos» on the bar under box 1, and its ⋮ for the 2nd ending.
- **Section, chord, double bar line, annotation**: with the cursor on the bar or beat where they appear in the image.
- **Swing**: «1/8 con swing» (or a variant from its ⋮) on the first bar, if the image calls for it. Keep writing the eighths straight.
- **Tempo or time-signature changes** mid-song: «Tempo» or «Compás» on the bar where they change.
- **Identical bars with no repeat sign**: «Duplicar compás en todas las pistas» (duplicate bar) or «Copiar pulsos» + «Paste» save you from typing them again.

## 7. Clicking menu buttons reliably

- **The menu doesn't always open in the same place.** Unpinned, it shows up on the left or right depending on where you right-click. Don't reuse coordinates from another opening. Take a screenshot, or find the button by name.
- **By name, with `javascript_tool`.** This snippet lists the buttons of the open menu (disabled ones are marked `[off]`):

```js
(() => {
  const root = document.querySelector('[role="dialog"]') || document;
  return [...root.querySelectorAll('button')]
    .map(b => (b.getAttribute('aria-label') || b.title || b.textContent.trim()).slice(0, 50) + (b.disabled ? ' [off]' : ''))
    .join(' | ');
})()
```

And this one returns the center of a button by its label, so you can `left_click` those coordinates:

```js
(() => {
  const name = 'Establecer duración 1/8';
  const root = document.querySelector('[role="dialog"]') || document;
  const bs = [...root.querySelectorAll('button')];
  const label = x => (x.getAttribute('aria-label') || x.title || '').trim();
  const b = bs.find(x => label(x) === name) || bs.find(x => label(x).includes(name));
  if (!b) return 'not found: ' + name;
  const r = b.getBoundingClientRect();
  return JSON.stringify({ x: Math.round(r.x + r.width / 2), y: Math.round(r.y + r.height / 2), disabled: b.disabled });
})()
```

  The first time, zoom in to confirm the click landed on the button. If the coordinates don't match the screenshot, trust the screenshot. With the menu pinned the buttons don't move, so locating them once is enough.
- **`find` also works** with the button's exact label; it gives you a reference to click.

## 8. Check and hand over

- After each bar, zoom in and compare it with the image: string, fret, duration, groups, techniques. At the end, go over the whole thing again and make sure no red «!» is left.
- **Don't save, publish, or submit the tab without asking.** Publishing on Songsterr makes it visible to everyone. Leave it in the editor and tell the user.
- Reply in the user's language, briefly:
  - what was written (bars, time signature, tempo, repeats);
  - what you read with doubt or assumed (rhythm with no stems, a blurry note);
  - what you left out and why (tuning, something the menu doesn't have).

  No need to read the tab back note by note: it's on their screen.

## Reference: the note menu, row by row

The menu opens when you right-click a note. An amber button is active on the note under the cursor. A grey one doesn't apply there. ⋮ opens variants. English meaning first, exact Spanish label in «quotes».

**Row 1. Duration.** Set duration «Establecer duración 1/64» · «1/32» · «1/16» *(tested)* · «1/8» *(tested)* · «1/4» *(tested)* · «1/2» · «1/1» — Dot «Puntillo» — Double dot «Doble puntillo» — Pin toolbar to bottom «Fijar la barra de herramientas abajo» *(tested)*. Duration applies to the whole beat, not to a single string. A new note with nothing before it starts as a quarter.

**Row 2. Rests, tuplets, ties, volume.** Rest «Silencio» — Triplet «Tríada» *(tested; toggle; goes on all three notes)* — ⋮ Tuplets «Grupos irregulares»: «Doble», «Tríada», «Cuádruple», «Quíntuple», «Séxtuple», «Séptuple», «Óctuple», «Nónuple», remove «Eliminar tuplet» — Tie «Ligadura a la nota anterior o siguiente» (the label changes depending on whether there's a note before or after; the second note isn't picked again) — Tie whole beat «Ligadura del pulso» (ties every note in the beat, for a chord that keeps ringing) — Fermata «Calderón» — Dynamics «Dinámicas» (ppp, pp, p, mp, mf, f, ff, fff; default mf) — «Crescendo» — «Diminuendo (Decrescendo)» — green magnifier button (by its icon it looks like an action search; untested).

**Row 3. Attack.** Ghost note «Nota fantasma» — Accent «Nota acentuada» — Heavy accent «Nota fuertemente acentuada» — «Staccato» — Let ring «Sonido largo» — «Palm mute» — Dead note «Nota muerta» — ⋮ Pick scrape «Raspado con púa» (down, up, remove) — Natural harmonic «Armónico natural» — Artificial harmonic «Armónico artificial».

**Row 4. Legato and slides** (most need a next note on the same string). «Hammer-On / Pull-Off» (going up = hammer-on, going down = pull-off) — «Legato slide» — «Shift Slide» — Slide in from below «Slide desde abajo» — Slide in from above «Slide desde arriba» — Slide out downward «Slide hacia abajo» — Slide out upward «Slide hacia arriba».

**Row 5. Bends and picking hand.** «Bend» — Tremolo bar «Palanca de Trémolo» — Auto brush strum «Rasgueo suave automático» (⋮ for up or down) — Arpeggio down «Arpegio descendente» — Arpeggio up «Arpegio ascendente» — Rasgueado «Rasgueado» — Downstroke «Golpe hacia abajo» — Upstroke «Golpe hacia arriba» — Trill «Trino».

**Rows 6 and 7. Special techniques and pedals** (some are for bass or other instruments). «Tapping» (⋮ Percussion «Percusión»: Tapping, Slap, Popping, remove «Eliminar percusión») — Grace note before the beat «Nota de gracia antes del pulso» — Grace note on the beat «Nota de gracia en el pulso» — Tremolo picking «Trémolo 1/8» (⋮ 1/16, 1/32, remove) — «Vibrato» (⋮ slight or wide by hand, slight or wide with the bar, remove all «Eliminar todos los vibratos») — Finger hit «Golpe con dedo» (⋮ finger, thumb, remove) — Wah open «Wah-Wah abierto» — Wah closed «Wah-Wah cerrado» — «Dead slap» — Sustain pedal «Pedal de resonancia» (piano).

**Row 8. Bar.** Repeat start «Inicio de repetición» *(tested)* — Repeat end «Fin de repetición» *(tested; dialog with repeat count and «Aplicar»)* — Alternate endings «1ª vez y finales alternativos» (⋮ up to the 8th, and remove) — Swing eighths «1/8 con swing» (⋮ Straight «Recta», swing 1/8 or 1/16, dotted 1/8 or 1/16, Scotch Snap) — «Tempo» — Time signature «Compás» — Toggle pickup «Alternar anacrusa» — Change instrument «Cambiar instrumento».

**Rows 9 and 10. Insert and text.** Double bar line «Doble barra de compás» — Insert beat before «Insertar pulso antes» — Insert beat after «Insertar pulso después» — Insert bar before «Insertar compás antes» — Insert bar after «Insertar compás después» — AI autocomplete «Autocompletar con IA» (needs the audio of a published song; useless on your own tab) — Chord «Acorde» — Detect and place chord «Detectar y colocar acorde» — Scale diagram «Diagrama de escala» — «Slash» — Section «Sección» — Annotation «Anotación».

**Rows 11 and 12. Move and transpose.** Move note up / down «Mover nota hacia arriba» / «hacia abajo» (changes string, keeps the pitch) — Move note up / down keeping the fret «… manteniendo el traste» (changes string, same fret number) — Move one fret up / down «Mover un traste hacia arriba» / «hacia abajo» — Octave up / down «Octava arriba» / «Octava abajo» — Move note left / right «Mover nota a la izquierda» / «a la derecha» (to the previous or next beat) — Transpose notes «Transponer notas» (shifts everything selected) — Voices «Voces» (up to four rhythm lines in one bar; useful for fingerstyle melody plus bass).

**Last row. Edit.** Cut beats «Cortar pulsos» — Cut bar in all tracks «Cortar compás de todas las pistas» — Copy beats «Copiar pulsos» — Copy bar in all tracks «Copiar compás de todas las pistas» — «Paste» (disabled until you copy something) — Clone beat(s) to end of bar «Clonar pulso(s) al final del compás» — Duplicate bar in all tracks «Duplicar compás en todas las pistas» — Delete note «Eliminar nota» *(tested; same as Backspace)* — Delete beat «Eliminar pulso» (removes the column and shortens the bar) — Delete bar «Eliminar compás».
