<h1 align="center">caveman</h1>

<p align="center">
  <strong>why use many word when few do trick</strong>
</p>

<p align="center">
  Claude output style. Less fluff. Same technical signal.
</p>

Grounding: [Claude Code output styles docs](https://code.claude.com/docs/en/output-styles)

## before / after

| normal Claude | caveman Claude |
| --- | --- |
| "The authentication middleware is failing because the token expiry check runs after decode and the missing token path is not guarded. Move validation earlier and reject empty bearer tokens." | "Auth middleware fails: missing token not guarded before decode. Reject empty bearer token first." |
| "To make this your default style, open your settings file, add the `outputStyle` field with the value `caveman`, then start a new session so the system prompt reloads." | "Add `\"outputStyle\": \"caveman\"` to settings. Start new session." |

Same answer. Less yak.

Less yak also mean lower cost and less wasted compute.

## why output style, not other thing

Docs say output styles change how Claude responds, not what Claude knows.

For goal "talk short every turn," output style fit exact job:

| tool | good for | why worse for this goal |
| --- | --- | --- |
| output style | tone, format, structure | always on once selected. direct fix for reply shape |
| `CLAUDE.md` | project rules, conventions, codebase memory | docs say it adds user message after default prompt. not purpose-built for response style |
| agents | delegated tasks with own tools, model, context | docs say agents solve specific jobs. not base voice for whole session |
| skills | reusable workflows, task prompts | docs say skills load when invoked or relevant. not always-on formatting layer |

Short version: want caveman every reply -> use output style.

## repo layout

```text
.
|-- .claude
|   `-- output-styles
|       `-- caveman.md
`-- README.md
```

Copy same path into local `~/.claude`.

## install

### 1. copy file

PowerShell:

```powershell
New-Item -ItemType Directory $HOME\.claude\output-styles -Force | Out-Null
Copy-Item .\.claude\output-styles\caveman.md $HOME\.claude\output-styles\caveman.md -Force
```

macOS / Linux:

```bash
mkdir -p ~/.claude/output-styles
cp ./.claude/output-styles/caveman.md ~/.claude/output-styles/caveman.md
```

### 2. enable style

1. Open Claude.
2. Run `/options`.
3. Pick `Output Style`.
4. Pick `Caveman`.

If build shows `/config` instead, use same picker there. Claude Code docs use `/config`.

Start new session after change. Docs say output style loads at session start.

## make default in Claude Code

Add this to `~/.claude/settings.json`:

```json
{
  "outputStyle": "caveman"
}
```

## why this save tokens

Docs say custom style text adds some input tokens up front. Docs also say prompt caching reduces repeat cost after first request in session.

Big win comes from shorter replies every turn.

Less unnecessary output means lower token bill and less energy burned on useless text.

Paper also interesting: [Brevity Constraints Reverse Performance Hierarchies in Language Models](https://arxiv.org/abs/2604.00025). Shorter answer can still keep quality, and sometimes improve it.

### rough savings

| prompt | normal answer | caveman answer | rough token cut |
| --- | --- | --- | --- |
| why build fail? | Build is failing because TypeScript cannot resolve the `@/auth` import after the alias change. Update the path mapping or import path. | Build fails: TypeScript cannot resolve `@/auth`. Fix alias or import path. | ~42% |
| what changed in auth? | I updated the middleware to reject missing bearer tokens before decoding the JWT, which prevents the null token crash. | Auth middleware now rejects missing bearer token before JWT decode. Crash gone. | ~45% |
| how set default style? | Open your Claude settings file and add the `outputStyle` field with the value `caveman`, then start a new session. | Add `"outputStyle": "caveman"` to settings. Start new session. | ~47% |

Real token count vary. Table shows rough reduction only. Pattern same: less fluff out -> less output spend.

## why `keep-coding-instructions: true`

Docs say custom output styles drop Claude Code coding instructions unless this field is true.

This file keeps caveman voice **and** keeps normal coding behavior.

## use when

- You keep typing "be concise"
- You want same terse format every turn
- You want less output spend without losing technical substance

## skip when

- Need project memory or repo rules -> use `CLAUDE.md`
- Need one reusable workflow -> use skill
- Need delegated sub-task with separate context/tools -> use agent
