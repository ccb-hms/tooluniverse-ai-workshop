# Follow along: two worked examples

CCB AI Workshop · ToolUniverse · 8 October 2026

**Before you start:** ToolUniverse must be installed and connected to your AI assistant (Claude Desktop, Claude Code, ChatGPT app, or Codex). Setup: paste `Read https://aiscientist.tools/setup.md and set up ToolUniverse for me.` into your assistant.

**How to use this page:** copy a query below, paste it into your assistant, and press enter. Every query starts with **"Using ToolUniverse,"**. Keep that part, or your assistant may use its own web search instead.

---

## 1. Clinical: does the evidence cover this patient?

**Background:** A patient with atrial fibrillation is being considered for a blood thinner to prevent stroke, but has severe kidney disease (stage 4, not on dialysis). The major trials of these drugs excluded patients with kidney function this low. So the real question is whether any published evidence is actually about this patient.

**Useful for:** clinicians, pharmacists, and anyone doing literature or evidence reviews.

**Paste this:**

```
Using ToolUniverse, a 66-year-old has atrial fibrillation and an eGFR of 22, which is chronic kidney disease stage 4 and not dialysis. Apixaban or warfarin? The pivotal trials excluded this degree of renal impairment, so the real question is whether the retrievable literature is about this patient at all.
```

**Watch for:** whether your agent checks *which patients* each paper studied. In our run, the first searches returned dialysis studies (the wrong patients), and the agent caught that and searched again.

---

## 2. Genetics: which gene does this variant control?

**Background:** rs12740374 is a common DNA variant strongly linked to LDL cholesterol and heart attack risk. It sits inside the gene CELSR2 but doesn't change any protein. The question is which nearby gene it actually controls, and in which tissue.

**Useful for:** geneticists, and anyone working with GWAS hits, eQTLs or regulatory variants.

**Paste this:**

```
Using ToolUniverse, rs12740374 is a common non-coding variant at the 1p13 locus, the strongest genome-wide association signal for LDL cholesterol and myocardial infarction. It sits inside the 3' untranslated region of CELSR2, but it changes no protein. Which gene does it actually regulate, in which tissue?
```

**Watch for:** whether your agent picks the right tissue. The strongest statistical signal is in muscle, but LDL cholesterol is set by the liver.

---

## Good to know

- **Your run may look different from ours.** The model plans its steps fresh each time, so it may call different tools or databases. Compare your final answer with ours.
- **It can take a few minutes.** The first call after install is slower.
- **Some databases need API keys.** Without them, your agent may skip a source or use another one.
- **Read the reasoning, not just the answer.** The tools return real data, but the model can still draw the wrong conclusion.

Each step of our 5 October 2026 runs (the reasoning, each ToolUniverse call, and what came back) is shown in the workshop slides in this repository.

Questions: ccb_help@hms.harvard.edu
