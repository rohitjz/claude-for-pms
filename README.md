# claude-for-pms

Claude skills built for product managers. Drop-in frameworks you can invoke from [Claude Code](https://claude.com/claude-code), Claude Desktop, or anywhere skills run, so Claude applies the right PM craft without you rewriting the prompt every time.

## Skills

### [patrick-winston-presentation](patrick-winston-presentation/)

Coach a presentation using Patrick Winston's MIT "How to Speak" framework. Five modes plus a Full Suite orchestrator:

1. **Opening**: Empowerment promise and first 60 seconds.
2. **Slide Audit**: The 10 Winston slide crimes, each with a specific fix.
3. **Memorability**: Winston Star (Symbol, Slogan, Surprise, Salient idea, Story).
4. **Talk Structure**: Vision, Proof of Work, Contributions with a minute-by-minute outline.
5. **Teaching**: Physical prop or vivid verbal equivalent, with story arc and script.

Use for keynotes, job talks, board presentations, investor pitches, all-hands, sales demos, technical teachings. Triggers on "Winston," "fix my talk," "audit my slides," "make this memorable," or any generic presentation prep request.

## Install

### Global (available in every Claude Code session)

```bash
git clone https://github.com/rohitjz/claude-for-pms.git
cp -r claude-for-pms/patrick-winston-presentation ~/.claude/skills/
```

After copying, the skill registers automatically. Trigger it in any Claude Code session.

### Per-project (scoped to one repo)

```bash
git clone https://github.com/rohitjz/claude-for-pms.git
mkdir -p .claude/skills
cp -r claude-for-pms/patrick-winston-presentation .claude/skills/
```

### Verify

In a Claude Code session, type `/skills` or ask Claude to list available skills. `patrick-winston-presentation` should appear.

## What makes a skill PM-grade

Every skill in this repo follows four rules:

1. **Opinionated over neutral.** Skills enforce specific rules (Winston's "no jokes at the opening," font minimum 40pt, final slide is contributions). PMs get craft, not options.
2. **Frameworks over freestyle.** Each skill packages a named framework from someone who has earned the right to be opinionated (Winston, Teresa Torres, Mike Cohn, etc).
3. **Interactive intake.** The skill asks for context before producing output, so the framework lands on your actual situation, not a generic template.
4. **Verification built in.** Each skill closes with a checklist the output must pass before the coaching session ends.

## Why Claude, why skills

Claude Code's skill system turns a good prompt into a reusable capability. Instead of pasting the same "act as a presentation coach applying Winston's framework" prompt every time, the skill lives in your `~/.claude/skills/` folder and Claude picks it up automatically when the conversation matches.

Skills are markdown. No build step, no runtime. If you can edit a file, you can modify the skill.

## Contributing

Feedback, issues, and PRs welcome. If you're a PM who finds a bug in how a skill coaches you, file an issue with the specific exchange where it went wrong.

## License

MIT. See [LICENSE](LICENSE).
