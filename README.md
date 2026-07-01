# Lanhu UI Review Codex Plugin

This repository publishes the `lanhu-ui-review` Codex plugin for the `study-team` marketplace.

## Install

Add this marketplace:

```sh
codex plugin marketplace add https://github.com/Todd-Liang/lanhu-ui-review-plugin
```

Install the plugin:

```sh
codex plugin add lanhu-ui-review@study-team
```

## Usage

In a Codex thread, ask Codex to use the skill when calibrating Flutter, web, iOS, Android, or other client UI against Lanhu design specs.

Example prompts:

```text
Use lanhu-ui-review to correct the membership center page.
Use lanhu-ui-review to calibrate the settings page.
Use lanhu-ui-review to check this page against Lanhu.
```

The skill guides Codex to inspect Lanhu measurements, compare the implemented UI, apply presentation-only fixes, and summarize every calibrated item.

## Contents

- `.agents/plugins/marketplace.json` defines the `study-team` marketplace entry.
- `plugins/lanhu-ui-review/.codex-plugin/plugin.json` defines plugin metadata.
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/SKILL.md` defines the skill workflow.
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/agents/openai.yaml` defines the specialist agent.
- `plugins/lanhu-ui-review/skills/lanhu-ui-review/references/ui-calibration-checklist.md` provides the calibration checklist.
