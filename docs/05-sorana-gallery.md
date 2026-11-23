# 05 · sorana.gallery: the source of truth

Read this before anything else in a session. Sorana is an original AI pop singer about Solana, an open fan character:
anyone may make work with her. The gallery at sorana.gallery holds her canon, her recipe, her songs and her
videoclips. **It is the #1 source of truth.** When a doc in this toolkit disagrees with it, the gallery wins: follow
it, and tell the owner which doc to fix.

**What the bot makes:** Sorana content, sized to the ask: a still, a clip, a song, a music video or a post. Sorana is
the lead by default. Make a new character only when the person asks for one.

---

## 1. Connect it

The MCP server is `https://www.sorana.gallery/sorana/mcp` (Streamable HTTP). It is public and read-only: no account, no
key, no state. It writes prompts and plans; it never generates media and never spends. On the bot, Claude Code on the
box does the production and holds this connection; Grok relays (`96-relay.md`).

Claude Code:

```sh
claude mcp add --transport http sorana https://www.sorana.gallery/sorana/mcp
```

Codex CLI (`~/.codex/config.toml`):

```toml
[mcp_servers.sorana]
url = "https://www.sorana.gallery/sorana/mcp"
```

Claude (web and desktop): Settings → Connectors → Add custom connector, and paste the URL. Clients that only speak
stdio: `npx mcp-remote https://www.sorana.gallery/sorana/mcp`.

**The skill** (her canon, the recipe and BLINK as files, for agents that load skills) ships in this repository:

```sh
curl -sL https://raw.githubusercontent.com/ainomaly07/sorana-bot/main/skill/sorana-skill.zip -o sorana-skill.zip
unzip -o sorana-skill.zip -d ~/.claude/skills/
```

`slop relay setup` installs it by itself. Without either, read the gallery page itself: `https://www.sorana.gallery`.

---

## 2. Which tool answers which question

| Question | Tool |
|---|---|
| How is a song or a film made? | `get_recipe` (the method on one page, with the six checkpoints: call it first for a film) |
| Who is she? Her constants, the identity text (full and short), every look's wardrobe, her voice, the never-list | `sorana_canon` (call it first, every project) |
| The fields for a song model and a structure in bars at 150 BPM | `song_brief` |
| Is this lyric ready? Hooks, syllables, numbers spelled as sung, no price talk | `check_lyric` |
| Her first single | `get_song` (BLINK: the audio, the style and the lyric) |
| A prompt for a new still of her, from her face sheet | `build_prompt` |
| A video take, with the sung words in quotes | `write_shot` |
| Is this prompt safe to spend on? | `check_prompt` (a video, image or song-style prompt) |
| What will a music video take, and what will it cost? | `plan_film` (shots, takes and a dollar estimate) |
| Where do the cuts fall? | `beat_grid` (a bar every 1.6 s at 150 BPM) |

Prompts on the server: `make_clip` (a music video or a clip), `make_song` (a song about a theme), `make_still` (a new
still). Resources: `sorana://recipe`, `sorana://canon`, `sorana://songs/blink`.

---

## 3. The canon in short (re-read `sorana_canon` for the exact words)

- **Photographic, never illustrated.** Production images are film stills with grain and stage light. No anime or drawn
  version is her canon.
- **Her identity text goes into every image prompt, verbatim.** The full form for close and medium shots, the short
  form for full length and wider. Framing first, then the identity text, then the look's wardrobe, then the scene.
- **A grown woman of 27,** with an adult face and high cheekbones. Never the word "young". Nothing that reads
  under-age, nothing explicit or sexualised.
- **Violet and mint are hers.** Hair violet (#9945FF), one mint-green streak (#14F195). Each look brings its own
  colours; on her head, mint is the one accent.
- **Her clothes change with every world; her head never does.** Five looks so far: Mainnet, Validator, Solana Summer,
  400 ms, Afterparty (`sorana_canon` has each wardrobe, place and light).
- **The never-list:** two streaks or any other green in her hair; the Solana logo or any brand mark on her; logos or
  text on her clothes; a real person's face; designer or celebrity names in prompts; price talk or promises in her
  lyrics; image-model lettering (all type is drawn in code).
- **Face filters.** A decline is free, and final for that image on that service. Never alter an image to get it
  through. The same unaltered image may go to another service (`62-moderation.md`).

Close and medium shots:

```
a 27-year-old Latina woman with a grown-up face, high cheekbones, warm tan skin, hazel-green eyes, full lips and a small beauty mark under her left eye, very long glossy straight violet-purple hair with a centre part and soft curtain bangs, exactly one mint-green streak down the front lock on her left side, a sharp mint-green eyeliner wing on each eye, a small flat mint-green lightning-bolt earring on her left ear
```

Full length and wider:

```
a 27-year-old woman with very long straight violet hair, one mint-green streak, mint eyeliner wings and a mint lightning-bolt earring
```

Set them once per project: `slop lead --canon "<the close form>" --far "<the short form>"`, after the four test
plates pass checkpoint 3.

**Her voice.** A smoky low alto, close to the mic, with breath in every line. Half-spoken verses that ride the kick,
then sung hooks stacked with whispered doubles. 150 BPM, always: one beat every 400 ms, the length of a Solana slot.
English, with Spanish ad-libs: dale, uno, dos, sol. Never a high squeaky vocal, a slow ballad, or a song about price.

---

## 4. Grok's jobs

- **Suno.** Opus writes the lyric and style fields (`10-song.md` §4.6, with `song_brief` and `check_lyric`); Grok
  creates the song through Suno's own connector (Suno's MCP; its browser only while that is not set up), on the
  person's account, and downloads both takes. Downloading on a paid plan is what allows commercial use.
- **Midjourney.** Opus writes the prompt blocks (`slop plates book`); Grok runs them in its browser and downloads every
  image. A personal style profile code is never published.
- **Grok Imagine** is Grok's own tool (no browser; up to 720p clips on the bot's Grok Bot usage); a 1080p clip runs on
  grok.com in Grok's browser with the person's X plan. Opus asks with `slop relay job --kind grok-imagine`
  (`96-relay.md`).
- Sign-ins go through the person's saved login (Vault) or the Secure Form, which Grok fills in without seeing it;
  single sign-on, passkeys, captchas and two-factor prompts are always the person's.

---

## 5. Checkpoints, spending and release

The six checkpoints and the spending rules are in `00-overview.md` §4 and §5.3, and in `get_recipe`: silence never
approves spending; estimate = planned clip seconds × price × 2; quote real spend only from the provider; a quality
complaint stops all spending, in every workflow that can spend; declines are free and final on that service. A small
ask uses only the checkpoints it reaches (a still: her face and the prompts before spend).

Releasing and posting (`90-master-publish.md` §5–6): release songs under your own artist name; no "feat. Sorana" in
the artist field; credit her in the description and on the cover: "Sorana is an original fan character about Solana
(sorana.gallery)"; an AI label if AI made any of it. Posts get the platform's AI label and name the tools. Sorana is
fan work about Solana, not affiliated with or endorsed by the Solana Foundation or Solana Labs.

---

## 6. The toolkit, stage by stage

Most stages exist as `slop` commands. "Missing" means the toolkit has no command for it.

| Stage | Toolkit |
|---|---|
| The project folder and its logs | `slop new`, `slop decide`, `slop runs add`, `slop status` (`DECISIONS.md`, `NOTES.md`, `RUNS.md`, `ledger.jsonl`) |
| The lyric scorer: scansion and assonance | `$SLOP_HOME/venv/bin/python /workspace/sorana/tools/scansion.py lyric LYRICS.md --brief`; `slop lyrics lint` for Suno spelling; `check_lyric` for her rules |
| The Suno pack | no command: written by the bot from `10-song.md` §4 and `song_brief` into `suno/` |
| Stems, timed words, the ear check | `slop analyze`, `slop lyrics fix`, `slop lyrics check` |
| The beat map, sections and hits | `slop analyze`, `slop song bars`, `slop song sections`; `beat_grid` for her 150 BPM grid |
| Display tokens | `slop lyrics display` |
| The board file, its audit and its sheet | `slop board draft`, `slop board set`, `slop board fill`, `slop board audit`, `slop board sheet` |
| The plate book, contact sheets and picks | `slop plates book`, `slop plates ingest`, `slop plates sheet`, `slop plates pick`, `slop plates vary` |
| Clip files and the spend gate | `slop clip new`, `slop clip lock`, `slop clip submit`, `slop gate prompts`, `slop spend` |
| The clean vocal window and the sync check | `slop audio window --mode clean`, `slop clip sync`, `slop sync check`, `slop sync review` |
| Covers and coverage | `slop clip cover`, `slop clip coverage`, `slop clip frame` |
| The edit list and the renderer | `slop edit edl`, `slop edit export`, `slop render frames` (the engine in `engine/`) |
| The lyric gate, the history and flash checks | `slop render lyrics`, `slop render check` |
| Contact sheets and the reviewer | `slop render sheet`; the reviewer runs delegated (`95-delegation.md`, `80-review-qa.md`) |
| The safety and canon scan | `slop review scan-sheets`, `slop review record`, `slop review status` |
| Encode and deliver | `slop render encode`, `slop render vertical`, `slop render encode --share` |
| Workflows, run records and the stop switch | `slop job`, `slop runs`, `slop spend --freeze`; workflows in `templates/workflows/` (`95-delegation.md`) |
| Pace against the music | missing (`board.pace` sets the cut pace at the draft; nothing measures the review copy) |
