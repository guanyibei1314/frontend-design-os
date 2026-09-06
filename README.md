# Frontend Design OS

A portable, auto-routable frontend design workflow for agent harnesses that support `SKILL.md` discovery.

Frontend Design OS prevents visually significant frontend work from jumping directly from a vague prompt to code. It routes the task by scope, establishes product truth and a design contract, implements against that contract, then requires browser evidence and independent visual, UX, and engineering review before completion.

## Core capabilities

- automatic `FULL / STANDARD / LIGHT / PATCH` routing;
- reference website, screenshot, Figma, and existing-repository modes;
- product-truth gate before visual invention;
- explicit `DESIGN.md` contract and reusable templates;
- anti-AI-slop gate;
- independent Visual / UX / Engineering review gates;
- desktop and mobile browser verification before claiming completion.

## Automatic routing examples

| Request | Route |
| --- | --- |
| “做一个无人机地面站管理网页” | `FULL` |
| “重做这个 AI 求职项目的整个 UI” | `FULL + Existing Project Mode` |
| “按这个网站的感觉重新设计首页” | `FULL + Website Reference Mode` |
| “给当前产品加一个复杂的职位详情页” | `STANDARD` |
| “做一个新的数据表格组件” | `LIGHT` |
| “把按钮颜色改黑、修掉手机端溢出” | `PATCH` |

The detailed routing rules live in [`references/ROUTER.md`](references/ROUTER.md).

## Repository structure

```text
frontend-design-os/
├── SKILL.md
├── skill.json
├── references/
│   ├── ROUTER.md
│   ├── ANTI_SLOP.md
│   └── REVIEW_GATES.md
├── templates/
│   ├── PRODUCT.md
│   ├── DESIGN.md
│   └── REVIEW.md
└── scripts/
    └── validate.py
```

## Installation

This repository is intentionally self-contained. Install or reference the repository using the skill mechanism supported by your agent harness.

For filesystem-based `SKILL.md` discovery, clone or copy this repository into the harness's user-level or project-level skills directory. Project-local installation is recommended when the design rules should travel with one codebase.

Example generic layout:

```text
<skills-directory>/frontend-design-os/SKILL.md
```

Then start a new session so the host can discover the skill if it does not support hot reload.

## Validation

Run:

```bash
python scripts/validate.py
```

The validator checks the required files, metadata, routing modes, reference modes, anti-slop gate, and reviewer definitions.

## How it behaves

For a substantial new frontend, the default flow is:

```text
Request
  ↓
Route scope
  ↓
Product truth
  ↓
Design research when useful
  ↓
DESIGN.md contract
  ↓
Wireframe / visual direction
  ↓
Implementation
  ↓
Browser render
  ↓
Visual + UX + Engineering review
  ↓
Fix and re-render until pass
```

Small visual bugs do **not** run the full process. They route to `PATCH`, make the smallest safe change, and verify the result.

## Important limitation

A GitHub repository cannot force itself into every ChatGPT conversation. Automatic invocation depends on the host product or agent harness actually installing, indexing, or surfacing this skill. `whenToUse` in `SKILL.md` defines when the host/model should select it once the skill is available.

## Version

Current skill version: **2.0.0**.
