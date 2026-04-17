<p align="center">
  <img src="caveman-claude-code.png" alt="Caveman Claude Code Output Style" width="1280" />
</p>

<h1 align="center">Caveman Output Style for Claude Code</h1>

<p align="center">
  Claude Code caveman output style. Less fluff. Same technical signal. Can be always on by default. Better than CLAUDE.md or skills.
</p>

## quick start

One command. Done.

```bash
# macOS / Linux
mkdir -p ~/.claude/output-styles && cp ./.claude/output-styles/caveman.md ~/.claude/output-styles/caveman.md
```

```powershell
# Windows
New-Item -ItemType Directory $HOME\.claude\output-styles -Force | Out-Null; Copy-Item .\.claude\output-styles\caveman.md $HOME\.claude\output-styles\caveman.md -Force
```

Then: `/config` → `Output Style` → `Caveman`. Restart session.

<img width="891" height="268" alt="image" src="https://github.com/user-attachments/assets/8a04a7a0-f043-4ac0-a6d5-62f1cd83364b" />

Want it always on? Add to `~/.claude/settings.json`:

```json
{ "outputStyle": "caveman" }
```

## Why use caveman?

| prompt | normal answer | caveman answer | rough token cut |
| --- | --- | --- | --- |
| why build fail? | Build is failing because TypeScript cannot resolve the `@/auth` import after the alias change. Update the path mapping or import path. | Build fails: TypeScript cannot resolve `@/auth`. Fix alias or import path. | ~42% |
| what changed in auth? | I updated the middleware to reject missing bearer tokens before decoding the JWT, which prevents the null token crash. | Auth middleware now rejects missing bearer token before JWT decode. Crash gone. | ~45% |
| how set default style? | Open your Claude settings file and add the `outputStyle` field with the value `caveman`, then start a new session. | Add `"outputStyle": "caveman"` to settings. Start new session. | ~47% |

Real token count will vary. Table shows rough reduction only. Pattern is the same: less fluff out -> less output spend.

Same answer. Less bla. Shorter replies every turn. Lower token bill and less energy wasted on filler.

Use when:

- You keep typing "be concise"
- You want the same terse format on every turn
- You want less output spend without losing technical substance

Backed by research: [Brevity Constraints Reverse Performance Hierarchies in Language Models](https://arxiv.org/abs/2604.00025). Shorter answer keeps quality, and sometimes even improves it.

## why output style, not other things

[Claude Code official documentation](https://code.claude.com/docs/en/output-styles) show output styles change how Claude responds, not what Claude knows.

Output style is the perfect matching tool for achieving "talk short on every turn" goal:

| tool | good for | why worse? |
| --- | --- | --- |
| `CLAUDE.md` | project rules, conventions, codebase memory | adds user message after default prompt. not purpose-built for response style, directive lost on long threads |
| skills | reusable workflows, task prompts | skills load when invoked or relevant. Claude Code may decide against using it. Not always-on formatting layer |
| `--append-system-prompt` | one-off system prompt append | appended at end of system prompt. lower priority. busts cache if value changes |

All methods add roughly the same amount of input tokens. Output style wins on adherence and consistency, not input cost.

## how it works

Output styles inject a dedicated section into Claude Code's system prompt:

```
# Output Style: Caveman
[style text here]
```

This section is:
- **Dedicated** — purpose-built for response formatting
- **System prompt level** — not buried in user messages like CLAUDE.md
- **Always on** — no model discretion, no invocation needed
- **Survives long threads** — style persists without dilution

vs other methods:
- **CLAUDE.md**: User message after system prompt. Directive loses weight on long threads.
- **Skills**: Lazy-loaded. Model decides if relevant.
- **`--append-system-prompt`**: End of system prompt. Lower priority. Cache-busting if value changes.

## FAQ

**Does caveman make Claude dumber?**
Not at all. Same knowledge, same reasoning, just shorter output. Research shows output brevity can even improve answer quality.

**Will it break code generation?**
No. `keep-coding-instructions: true` keeps all coding behavior intact. Only the voice changes.

**Can I switch back?**
Sure! `/options` → pick different style. Or remove it from `settings.json`.

**Does it work with skills and agents?**
Yes. Output style is the base voice; skills and agents still work normally.

**Why not just tell Claude "be concise"?**
You can, but you have to say it every. single. turn. Output style is always on, set once and forget.

**Does it save money?**
Yes. Fewer output tokens = lower cost, especially on long sessions.

**Can I customize it?**
You are more than welcome. Edit `caveman.md` in your `~/.claude/output-styles/` folder and make it your own.

## license

MIT. Do what you want with it.

---

<p align="center">
  <strong>Like this? Star the repo. Share with your team.</strong>
</p>
