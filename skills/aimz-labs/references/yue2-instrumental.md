# Separate local YuE2 instrumental track

Read the current [official instrumental skill](https://github.com/multimodal-art-projection/YuE/blob/main/skills/yue2-music/instrumental/SKILL.md) and [generation guide](https://github.com/multimodal-art-projection/YuE/blob/main/docs/generation.md).

Prefer local YuE2 when it is actually installed and the selected workflow exposes the required score inputs. The official instrumental method uses score-level vocal-to-instrument conversion before rendering; a style request saying “no vocals” is not equivalent. Preserve the original score, converted score and conversion limits. Use a fresh score submission rather than unrelated cached tokens. Lyrics must not introduce sung words.

Keep music in a separate file and timeline track. Inspect actual duration, channels and synchronization, and retain foreground Foley. Silence/no vocal leakage and musical quality require listening; a successful generation or signal measurement cannot establish them.

Hosted MCP cannot access an unrelated local installation. If the actual route lacks score injection or a local bridge, report that limitation before choosing a supported separate audio route. Do not invent a tool, workflow input or local capability.
