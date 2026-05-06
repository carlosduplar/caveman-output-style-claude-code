<p align="center">
  <img src="caveman-claude-code.png" alt="Caveman Output Style for Claude Code - less fluff, token savings, always-on formatting" width="1280" />
</p>

<h1 align="center">Caveman Output Style for Claude Code</h1>

<p align="center">Better consistency and adherence than CLAUDE.md or skills. Always-on formatting. Less fluff, same technical signal.</p>

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

Then: `/config` → `Output Style` → `Caveman`. 

<img width="891" height="268" alt="image" src="https://github.com/user-attachments/assets/8a04a7a0-f043-4ac0-a6d5-62f1cd83364b" />

Want it always on? Add this to `~/.claude/settings.json`:

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

Same answer, less bla. Shorter replies every turn, lower token bill and less energy wasted on filler.

Use when:

- You keep typing "be concise"
- You want the same terse format on every turn
- You want less output spend without losing technical substance

Backed by research: [Brevity Constraints Reverse Performance Hierarchies in Language Models](https://arxiv.org/abs/2604.00025). Shorter answer keeps quality, and sometimes even improves it.

## why output style, not other things

[Claude Code official documentation](https://code.claude.com/docs/en/output-styles) show output styles change how Claude responds, not what Claude knows.

Output styles are the perfect matching tool for achieving "talk short on every turn" goal:

| tool | good for | why worse? |
| --- | --- | --- |
| `CLAUDE.md` | project rules, conventions, codebase memory | adds user message after default prompt. not purpose-built for response style, directive lost on long threads |
| skills | reusable workflows, task prompts | skills load when invoked or relevant. Claude Code may decide against using it. Not always-on formatting layer |
| `--append-system-prompt` | one-off system prompt append | appended at end of system prompt. lower priority. busts cache if value changes |

All methods add roughly the same amount of input tokens. Output styles win on adherence and consistency, not input cost.

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

## available styles

### Caveman (default)

Standard terse mode. Drop articles, filler, pleasantries, hedging. Fragments OK.

### Caveman Ultra

Maximum terseness. Telegraphic fragments. Symbols over words. Abbreviated prose.
Use when you want the most aggressive compression.

```bash
# macOS / Linux
cp ./.claude/output-styles/caveman-ultra.md ~/.claude/output-styles/caveman-ultra.md
```

```powershell
# Windows
Copy-Item .\.claude\output-styles\caveman-ultra.md $HOME\.claude\output-styles\caveman-ultra.md -Force
```

Then: `/config` → `Output Style` → `Caveman Ultra`.

### Tokenizer-safe terseness

Caveman (default) avoids aggressive abbreviations that may hurt clarity or tokenization on non-Anthropic models. Caveman Ultra goes further with symbols and prose abbreviations — use it when you trust your model's tokenizer.

## FAQ

<details>
<summary><strong>Does caveman make Claude dumber?</strong></summary>
<p>Not at all. Same knowledge, same reasoning, just shorter output. Research shows output brevity can even improve answer quality.</p>
</details>

<details>
<summary><strong>Will it break code generation?</strong></summary>
<p>No. <code>keep-coding-instructions: true</code> keeps all coding behavior intact. Only the voice changes.</p>
</details>

<details>
<summary><strong>Can I switch back?</strong></summary>
<p>Sure! <code>/options</code> → pick different style. Or remove it from <code>settings.json</code>.</p>
</details>

<details>
<summary><strong>Does it work with skills and agents?</strong></summary>
<p>Yes. Output style is the base voice; skills and agents still work normally.</p>
</details>

<details>
<summary><strong>Why not just tell Claude "be concise"?</strong></summary>
<p>You can, but you have to say it every. single. turn. Output style is always on, set once and forget.</p>
</details>

<details>
<summary><strong>Does it save money?</strong></summary>
<p>Yes. Fewer output tokens = lower cost, especially on long sessions.</p>
</details>

<details>
<summary><strong>Can I customize it?</strong></summary>
<p>You are more than welcome. Edit <code>caveman.md</code> in your <code>~/.claude/output-styles/</code> folder and make it your own.</p>
</details>

## license

MIT. Do what you wish with it.

---

<p align="center">
  <strong>Like this? Star the repo. Share with your team.</strong>
</p>
