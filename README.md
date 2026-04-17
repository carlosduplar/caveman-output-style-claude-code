<h1 align="center">Caveman Output Style for Claude Code</h1>

<p align="center">
  <strong>why waste words when few work?</strong>
</p>

<p align="center">
  Claude Code caveman output style. Less fluff. Same technical signal. Can be set as always on by default. Better support than CLAUDE.md or skills.
</p>

## Why use caveman?

| prompt | normal answer | caveman answer | rough token cut |
| --- | --- | --- | --- |
| why build fail? | Build is failing because TypeScript cannot resolve the `@/auth` import after the alias change. Update the path mapping or import path. | Build fails: TypeScript cannot resolve `@/auth`. Fix alias or import path. | ~42% |
| what changed in auth? | I updated the middleware to reject missing bearer tokens before decoding the JWT, which prevents the null token crash. | Auth middleware now rejects missing bearer token before JWT decode. Crash gone. | ~45% |
| how set default style? | Open your Claude settings file and add the `outputStyle` field with the value `caveman`, then start a new session. | Add `"outputStyle": "caveman"` to settings. Start new session. | ~47% |

Real token count vary. Table shows rough reduction only. Pattern same: less fluff out -> less output spend.

Same answer. Less bla. Also mean lower cost and less wasted compute.

## why output style, not other things

Official docs show output styles change how Claude responds, not what Claude knows.

For goal "talk short every turn," output style fit exact job:

| tool | good for | why worse for this? |
| --- | --- | --- |
| output style | tone, format, structure | always on once selected. direct fix for reply shape |
| `CLAUDE.md` | project rules, conventions, codebase memory | adds user message after default prompt. not purpose-built for response style, directive lost on long threads |
| agents | delegated tasks with own tools, model, context | agents solve specific jobs. not base voice for whole session |
| skills | reusable workflows, task prompts | skills load when invoked or relevant. Claude Code may decide against using it. Not always-on formatting layer |

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

Custom style text adds some input tokens up front. Prompt caching reduces repeat cost after first request in session.

Big win comes from shorter replies every turn.

Less unnecessary output: lower token bill, less energy wasted on filler.

Backed by research: [Brevity Constraints Reverse Performance Hierarchies in Language Models](https://arxiv.org/abs/2604.00025). Shorter answer can still keep quality, and sometimes improve it.

## why `keep-coding-instructions: true`

Custom output styles drop Claude Code coding instructions unless keep-coding-instructions is true.

This setting keeps caveman voice **and** normal coding behavior.

## use when

- You keep typing "be concise"
- You want same terse format every turn
- You want less output spend without losing technical substance

Grounding: [Claude Code output styles docs](https://code.claude.com/docs/en/output-styles)
