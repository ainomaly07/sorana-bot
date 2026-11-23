# The lead - character bible

The lead is **Sorana** by default, the open character from sorana.gallery (the source of truth: re-read her canon
with the MCP tool `sorana_canon` at the start of the project; docs/05-sorana-gallery.md). Replace her with a new
character only when the owner asks for one, and record that with `slop decide`.

The lead's identity is TEXT, pinned in every prompt with the lead. Never use a face image as the identity reference:
image references of a face over-condition the model and drift. Test it on 4 plates and get the face approved (gate G3)
before any batch. Then store the prompt text in project.json:

    slop --project {{NAME}} lead --canon "..." --far "..." --possessive "..."

## Canon (every prompt and edit keeps these)
- Face / age / ethnicity / skin (pin them in the prompt - Midjourney drifts otherwise): a Latina woman, 27; a
  grown-up face with high cheekbones; warm tan skin, hazel-green eyes, full lips, a small beauty mark under her left
  eye. She rests in a half-smile. Never the word "young".
- Hair / marks: very long, glossy, straight violet hair (#9945FF) with a centre part and soft curtain bangs; ONE
  mint-green streak (#14F195) down the front lock on her left side (the viewer's right in a front view); a sharp
  mint-green eyeliner wing on each eye; a small flat mint-green lightning-bolt earring on her left ear.
- Outfit (base look): changes with every world (each look's wardrobe text is in the canon); her head never changes.
- Colour rules: violet and mint are hers. Each look brings its own colours; on her head, mint is the one accent.
- Medium: photographic film stills with grain and stage light, never illustrated.

## Prompt text
- `lead.canon` (close and medium framings; the framing words come FIRST in the prompt, then this text):
  a 27-year-old Latina woman with a grown-up face, high cheekbones, warm tan skin, hazel-green eyes, full lips and a small beauty mark under her left eye, very long glossy straight violet-purple hair with a centre part and soft curtain bangs, exactly one mint-green streak down the front lock on her left side, a sharp mint-green eyeliner wing on each eye, a small flat mint-green lightning-bolt earring on her left ear
- `lead.far` (full-length and wide shots: a SHORT variant - face details pull the model into a close-up):
  a 27-year-old woman with very long straight violet hair, one mint-green streak, mint eyeliner wings and a mint lightning-bolt earring
- `lead.possessive` (e.g. "the singer's"): a Latina woman's

## Never
- two streaks, or any other green in her hair
- the Solana logo, or any brand mark, on her; a real person's face
- logos or text on her clothes
- an influencer smile for the camera
- anything that reads under-age; explicit or sexualised posing
- the word "young" in her prompts
- designer or celebrity names in prompts (describe the piece instead)
- generic mall Y2K (velour tracksuits, plain tees and jeans) when she goes Y2K
- Midjourney lettering, logos or UI: all type is drawn in code on top
