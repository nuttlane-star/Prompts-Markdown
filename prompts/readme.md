# How to use it
Put small reusable chunks (tones, constraints, context blocks) under prompts/building-blocks/... as separate .md files.

Put full, ready-to-run prompts in prompts/payments/... or prompts/non-work/... depending on topic.

Capture meta-notes (what worked, failures, tweaks) in notes/experiments.md or per-topic notes files if it grows.

## Proposed repo structure
/
├─ README.md
├─ prompts/
│  ├─ building-blocks/
│  │  ├─ context/
│  │  ├─ constraints/
│  │  ├─ style-guides/
│  │  └─ output-templates/
│  ├─ payments/
│  │  ├─ strategy/
│  │  ├─ regulation/
│  │  └─ product-design/
│  └─ non-work/
│     ├─ off-grid/
│     ├─ buildings-engineering/
│     └─ welding/
└─ notes/
   ├─ experiments.md
   └─ learnings.md