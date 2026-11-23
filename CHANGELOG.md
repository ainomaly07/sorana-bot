# Changelog

Each release is a tag `vX.Y.Z`. A bot on an older release reminds its person once ("say update"); `slop update apply`
installs it and prints the newest entries below.

## 0.3.7
- Sorana bot: the first release for SORANA, the AI pop singer about Solana. Song idea to finished lyric music video,
  plus stills, clips, songs and posts, with Sorana as the lead.
- Her source of truth is sorana.gallery and its MCP server (https://www.sorana.gallery/sorana/mcp): `sorana_canon`,
  `get_recipe`, `song_brief`, `check_lyric`, `get_song`, `build_prompt`, `write_shot`, `check_prompt`, `plan_film`,
  `beat_grid`. `slop relay setup` registers it and installs the Sorana skill from this repository.
- Her canon in the project template and the production brief: her identity text, her voice (a smoky low alto at
  150 BPM), her looks and her never-list.
