# respond-clearly

A skill for Claude Code and Codex that shapes replies for readers with ADHD, autism, or both.

Most "ADHD mode" skills make answers shorter. This one also covers what many autistic readers want: literal wording, exact numbers and state, no surprises, and the same shape every time. A profile file lets you add your own preferences on top.

## What it does

| For | What changes |
|---|---|
| ADHD | The answer is on line 1. Short sections and bullets. Status goes in three buckets (✅ Done, 🔜 In progress, 👉 Needs you), with anything you need to decide last. Your to-dos are batched into one list. No time estimates unless you ask. |
| Autism | Literal words, no idioms or analogies. Exact numbers, names, and dates, and never invented ones. One name per thing, no made-up labels. It says exactly what changed after any action. Anything unexpected comes first. |
| Both | Facts and offers instead of orders ("ready to merge" instead of "merge it"). No urgency words. Direct, never hinting. No jokes or performed enthusiasm by default. |

Needs vary from person to person. Every rule is a default your profile can change.

A reply shaped by the skill:

```
1 of 17 bug reports needs you. 14 are closed and 2 are still being checked.
State: bug tracker page updated. Nothing posted anywhere.

✅ Done
1. 17 reports filed since Monday → 17 rows on the tracker page.
2. 14 closed as duplicates or setup questions, each with a one-line reason.

🔜 In progress
3. Checking whether the 2 checkout-timeout reports are the same bug.

👉 Needs you
4. The login crash report has no owner. Assign it to the mobile team (recommended), or leave it for you?
```

## Install

**Claude Code**

```bash
claude plugin marketplace add joshdholtz/respond-clearly
claude plugin install respond-clearly@respond-clearly
```

**Codex**

```bash
codex plugin marketplace add joshdholtz/respond-clearly
codex plugin add respond-clearly@respond-clearly
```

**Other agents that read skill folders**

```bash
npx skills add joshdholtz/respond-clearly
```

**Manual:** copy `skills/respond-clearly/` into your agent's skills folder, for example `~/.claude/skills/` or `~/.agents/skills/`.

Restart your agent after installing.

## Make it yours

The rules in the skill are defaults. Your profile overrides them.

1. Create your profile from the template:

   ```bash
   mkdir -p ~/.config/respond-clearly
   curl -o ~/.config/respond-clearly/profile.md https://raw.githubusercontent.com/joshdholtz/respond-clearly/main/skills/respond-clearly/profile.example.md
   ```

2. Fill it in: what you like, what trips you up, and any hard rules ("no emoji", "never send messages as me"). Real examples help most, like a phrase that confused you or a reply you loved or hated. The guidance inside `<!-- -->` comments is ignored, so you can leave it in.

3. Claude Code only: to skip the permission prompt when the skill reads your profile, add this to `~/.claude/settings.json`:

   ```json
   { "permissions": { "allow": ["Read(~/.config/respond-clearly/**)"] } }
   ```

The profile lives outside the skill folder, so updating the skill never overwrites it.

## Use it on every reply (optional)

A skill loads when the model decides it's relevant. To use it for every conversation, add this line to `~/.claude/CLAUDE.md` (Claude Code) or `~/.codex/AGENTS.md` (Codex):

```markdown
Load the respond-clearly skill once per conversation and follow it for every reply.
```

## Credits

The ADHD side builds on ideas from [i-have-adhd](https://github.com/ayghri/i-have-adhd).

## License

[MIT](LICENSE)
