# cazz

A Claude Code skill that explains a code change, or a part of your code, so that it is easy
to read.

It gives the parts of good user documentation (what it does, how it works, how to use it,
what can go wrong) in short, plain sentences, with small ASCII diagrams. The parts follow
ISO/IEC/IEEE 26514. The sentences follow the writing rules of ASD-STE100 Simplified Technical
English. It is not a conformance claim to either standard.

## What you get

```text
In short.  Two or three sentences with the whole answer.

What it does          plain prose: the problem, the change, what stays the same
Before and after      a small table (for a change)
How it works          plain prose and diagrams
How to use it         numbered steps, real commands, real output
Options               what you can type or set
If something goes wrong   what you see, the cause, the action
Be careful            cautions
Results               measured numbers
Words                 a maximum of five special words
More information      commit, paths, limits
```

The skill reads the code before it writes. It runs the read-only commands that it shows, and
it tells you which ones it could not run.

## Install

```bash
git clone https://github.com/pratyaydeep/cazz ~/.claude/skills/cazz
```

Start a new Claude Code session. The skill is then available in all your projects.

To use it in one project only, clone it into `.claude/skills/cazz` in that project.

## Use

| You type | It explains |
|---|---|
| `/cazz` | The changes of this session, or the uncommitted diff, or the last commit. |
| `/cazz 25da8ea` | One commit. A range, a PR or a path also works. |
| `/cazz how does the cache work` | An idea or a part of the code. |
| `/cazz --short` | Only the answer, the idea, one procedure and the cautions. |
| `/cazz --full` | All the parts, all the options and all the problems. |
| `/cazz --file NAME.md` | The same text, in a file. |

## Update

```bash
git -C ~/.claude/skills/cazz pull
```

## Claude apps

For the claude.ai and desktop apps, make a zip that contains the folder `cazz` with `SKILL.md`
in it. Upload the zip in Settings > Customize > Skills. The options `--short`, `--full` and
`--file` are for Claude Code; in the apps, say what you want in words.
