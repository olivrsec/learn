# learn

[![video](assets/thumbnail.png)](https://www.youtube.com/watch?v=kzcI5F4tGiU)

Forked from [amosblomqvist/learn](https://github.com/amosblomqvist/learn), an AI learning system featured in [How I Use AI to Learn Things](https://www.youtube.com/watch?v=kzcI5F4tGiU).

Built as a pi configuration: the teaching philosophy encoded in a skill, a few small extensions, and agent definitions.

## What's different in this fork

The original skill was rigid: mandatory quiz after every node, no error correction when you disputed wrong grading, and heavy subagent overhead even for simple questions. This fork makes teaching adaptive and practical:

- **Adaptive quizzing** replaces quiz-every-node with smart filtering: only quiz foundations, non-obvious steps, and misconceptions. Skip trivial/repetitive patterns. Adds a "quiz filter" principle and light-check alternatives.
- **Dispute protocol** fixes false negatives. When you challenge a quiz result, the AI stops and re-evaluates instead of defending. It admits mistakes plainly and never doubles down when uncertain.
- **Conditional verification** makes the researcher subagent optional (complex topics only). Web search handles quick checks. The AI states confidence levels when teaching from memory.
- **Scaled ceremony** collapses phases for simple topics. Quick clarifications don't need full probe-plan-approval cycles. Rigor preserved for complex material.
- **Mission-driven goals** push for concrete endpoints (Why/Success/Out-of-scope) instead of vague "understand X" goals.
- **Storage strength thinking** designs quizzes for long-term retention via retrieval practice, spacing, and interleaving - not just in-the-moment checks.
- **Tighter quiz construction** adds character-count parity to catch length tells, and emphasizes high-trust resources for complex topics.

Net result: same core philosophy (unconditional truths + motivated discovery), but the skill now scales from quick questions to deep learning sessions without quiz fatigue or trust-breaking errors.

## What's in it

- `skills/teach/` — the philosophy and the process
- `skills/visualize/` — adds a correct, minimal diagram to a lesson when an idea is clearer as a picture
- `extensions/ask-user-question/` — the agent asks you questions through a UI popup
- `extensions/quiz/` — graded questions with instant feedback (✓/✗, correct answer, explanation)
- `extensions/md-log/` — link a markdown file to the session
- `extensions/visual-tools/` — tools for visualization subagents
- `agents/` — `researcher`, `svg-maker`, `mermaid-maker`: the subagents the system delegates to

## Install

This repo **is** a `.pi` directory. From your learning project's root:

```bash
git clone https://github.com/olivrsec/learn .pi
```

Then open pi in that directory. (Or copy the pieces you want into your existing project config.)

## Requirements

- [pi](https://github.com/earendil-works/pi)
- **Optional:** A subagent implementation for the researcher (complex topic verification) and visual makers (diagrams). Recommended: [pi-interactive-subagents](https://github.com/amosblomqvist/pi-interactive-subagents) (tmux only). The system works without subagents - you just lose automated research verification and generated visuals. For simple topics, the main session handles everything via inline web search.
- `ask-user-question` — use the copy bundled here. If your setup already has an `ask-user-question` extension, use **this** one in its place. Popups from different extensions serialize through a shared UI lock, which only works when it's the same implementation.

## Notes

Subagents are now conditional: the researcher fires only for complex/unfamiliar topics where you need field mapping. Simple questions use inline verification. You can run entirely without subagents - the main session does all teaching.

The teaching skill adapts to your needs. Edit `skills/teach/SKILL.md` to fit how you learn best.
