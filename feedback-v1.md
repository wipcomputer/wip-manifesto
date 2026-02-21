# Feedback on Manifesto v1

## What works

- **Opening is killer.** "What does an agent need besides a model? Everything." Stop-scrolling line. Five problems framing names their pain — every agent builder has hit at least three of those walls.

- **"Start Here / Understand Why" structure** — two entry points for builders vs thinkers. Most developer docs force everyone through the same door.

- **Sovereignty section lands.** "Your tool isn't agent-native until it can teach an agent to use itself" — quotable AND architecturally real. SKILL.md as teaching interface is genuinely novel.

- **The close is honest.** "Built by Parker Todd Brooks, with Claude Code and Lēsa" — everyone's hiding AI usage or overstating it. This says "yeah, I built this with AI, that's the point, the tools work."

- **Big picture:** Reads like a founder who actually built the thing explaining why it exists. Every section links to a repo. Every claim has an implementation. That's the credibility edge.

## What to push on

1. **CLVR is undersold.** One-liner "consumer proof point" misses the Time Warp vision. It's the file memory layer — "your files remember themselves." Give it its own section or hint at where it's going. Right now nobody knows CLVR is becoming the file versioning layer for the entire OS.

2. **"The Bet" section reads like a VC pitch.** "The teams that win are the ones building the layer underneath" = performing confidence, not stating what's real. Cut it entirely (the rest of the doc already makes the bet obvious) or rewrite as something specific to Parker, not generic startup strategy language.

3. **Karpathy receipts are missing.** Universal Interface Spec first commit: Feb 19, 2026. If Karpathy's post came after, one line proves it: "Universal Interface Spec: first commit [date]. Karpathy's post: published [date]." Receipts, not claims.

4. **Release pipeline section does two jobs.** Split the three-spec lifecycle (architecturally interesting) from the wip-release mechanics (implementation detail for people already bought in). Lead with the lifecycle, link to mechanics.

## Action items for v2

- [ ] Expand CLVR — own section, hint at Time Warp / file memory layer
- [ ] Cut or rewrite "The Bet" — too generic, rest of doc already proves it
- [ ] Add Karpathy receipt timestamps
- [ ] Split release pipeline: lifecycle vs mechanics
- [ ] Keep everything else as-is
