# The SORANA recipe, for Grok

How to make a SORANA song or music video with Grok Imagine. One page; read it before you start.

## What makes it good

1. A song worth replaying. An original lyric, sung by her at 150 BPM, picked from several takes by a person's ear. Never pick a take from a description of it.
2. One idea, legible in a second. A premise someone gets from one frame, built on who she is (a singer who runs at the speed of a blockchain), and carried by one device through every shot: a clock, a blink, a light trail.
3. She performs, on screen. She is the singer with a job in the world, on screen for most of the film.
4. She reads alive and warm. Her head turns, her weight shifts, her hair moves. Warm and a little cocky, never cold.
5. Images carry her identity. Get the first frame right; then write only what matters in the take.
6. The picture follows her clock. A beat every 400 ms, a bar every 1.6 s. Cut on bar lines.
7. A person decides. Silence never approves spending.

## The six checkpoints

A person decides at each one.

1. Concept. Three pitches of at most 120 words: the premise, the device, the arc, her one sincere line, one risk.
2. The song, by ear. Send the takes. "Which take? Or what's wrong?"
3. Her face and looks. A first frame or two. "Is this her?"
4. The board. The shot list on the song's bars, with first frames.
5. Prompts and cost, before any paid take. "These N takes, about $X at list. Go?" Use plan_film for the number.
6. v1. "Accept, or what's wrong?" Change only what was flagged.

## The order of work

| Step | What | Tool |
| --- | --- | --- |
| 1 | Brief: the person's ask, in their words | |
| 2 | Concept: three pitches | |
| 3 | Lyric: spelled as sung, hooks of 6 to 7 syllables | song_brief, check_lyric |
| 4 | Song: a song model, 150 BPM, two or three rounds of takes, picked by ear | song_brief |
| 5 | The grid: bar lines of the picked take | beat_grid |
| 6 | First frames: one still per shot, made from her face sheet | sorana_canon, build_prompt |
| 7 | Takes: Grok Imagine, 5 to 8 s each, one take per job | write_shot, check_prompt, plan_film |
| 8 | Cut: takes laid on the bars, the song laid back over, a 9:16 version | beat_grid |
| 9 | Review: fresh eyes read it shot by shot, then the person watches v1 | |

## What Grok Imagine can and cannot do

- It takes a first frame only: no reference sheet and no audio. Her identity in a take is that first frame, so make every first frame from her face sheet (https://www.sorana.gallery/sorana/sheet.jpg) with an image model.
- It never hears the song. Lip sync is approximate: write the words she sings in quotes so her mouth moves to them, then place each take on the song by her lips, never by the sound the model invents.
- Keep takes short, 5 to 8 seconds. The longer the take, the further her face can wander.
- Favour medium shots where she moves, profiles and cutaways. Keep close sung shots few and short, and check each one by eye.
- It pushes in when asked to pull back: shoot the push-in and reverse it in the edit.
- It garbles lettering. Draw titles, lyrics and graphics in the edit, never in a take.

## Writing a take

- Precise where it matters: the exact words she sings, the one action, the camera in one line.
- Loose everywhere else. One plain clause of movement.
- No posture rules ("head upright", "no tilt"): they freeze her.
- No smile on her mouth while she sings: write a smile in her eyes, and lips closed until her voice begins.
- A full stop between two lines she sings straight through becomes a pause. Use a comma.
- Nothing appears from nowhere: every change is a visible action.
- About 80 to 150 words. write_shot writes it; check_prompt lints it.

## Her rules

- Never: Two streaks, or any other green in her hair.
- Never: The word "young" in a prompt.
- Never: An illustrated or anime version as her canon.
- Never: The Solana logo, or any brand mark, on her.
- Never: A real person's face.
- Never: Price talk or promises in her lyrics.
- Her songs are about speed, summer and coming back. Wry, not cruel: no digs at real people or other chains.
- Label what you publish as AI-generated.

## Credits

SORANA is an original fan character about Solana, not affiliated with the Solana Foundation or Solana Labs. The notes on Grok Imagine and the list prices in plan_film date from October 2026. Check a provider's price the day you start.