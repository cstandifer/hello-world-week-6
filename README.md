# hello-world-week-6
Playing with pixels, mirrors, and sound

Two p5.js webcam sketches for Logic of Interaction, week 6. Both start from the
`p5-custom-pixel-class` example in
[areaofeffect/hello-world-week6-assignment](https://github.com/areaofeffect/hello-world-week6-assignment).
The webcam becomes a mirrored grid of colored squares, and your movement plays music.

## The sketches

### `theremin/`
A theremin you play by waving.
- **How much** you move sets the volume. It's silent when you're still and swells when you wave.
- **Where** you move sets the pitch. Waving high on screen plays a high note, and waving low plays a low one.

### `starlight/`
Motion wind chimes.
- Any square that changes a lot is a "splash." Each frame, one splash is picked at random.
- Its height chooses a note from a pentatonic scale, so random notes always sound good together.
- Six chime voices take turns playing. Each has a main tone plus a quieter shimmer overtone, a random volume, a soft attack and a long ring. The voices overlap and go through a reverb.

## How to run

1. In Terminal, from this folder, run `python3 -m http.server 8000`.
2. Open `http://localhost:8000/theremin/` or `http://localhost:8000/starlight/` in Chrome.
3. Allow the camera, then **click the page once** to turn on sound. Browsers block audio until you click.

## How it hears movement

A webcam doesn't know what movement is. Each square remembers its brightness from
the last frame and compares it with the brightness now. A big difference means something
moved there. Adding up those differences tells the sketch how much motion there is, and
where it happens on screen tells the sketch where you are.

## From raindrops to wind chimes

My original idea was **raindrops**: light "plink" sounds falling wherever I moved in the mirror.

- I built the **theremin** first, as a simpler way to learn p5.sound with one continuous tone. I liked it enough to keep it as its own piece.
- The first drops all played **one note at a steady tick**, so I made the timing random and had the height on screen pick the note.
- They kept landing on **low notes**. The loop let the lowest moving square always win, so I switched to giving every splash an equal chance.
- Then it sounded like a **robot bee**. Reverb and a quick upward pitch slide made it more watery, but tuning the length swung between **"bloop"** and **"popcorn."**
- What I really wanted was something more like a **chime**. I dropped the pitch slide and let each note ring with a natural fade.
- Slowing the notes down let them ring but felt **unresponsive**, so I made a `ChimeVoice` class and gave the sketch six voices that overlap.
- I finished by tuning by ear: random volumes, a shimmer overtone at 2.76× the note (like a metal tube), a higher note range, a softer attack (0.03), and a reverb size in between (4, 2).

## How I made this

I built this with Claude (Claude Code) as my tutor. Claude guided me through my idea
step by step, one small change at a time, explaining each concept as we went:
motion detection, `map()`, `lerp()` smoothing, oscillators and envelopes, MIDI
notes, arrays, classes and modulo. I typed the code and made the sound choices by ear.
Claude also checked my work after each step and handled the git and folder setup.
