# AX — Agent eXperience

A portable skill for reviewing how tools behave toward the agents that use them. AX examines scripts, CLIs, hooks, error paths, configuration, and skills against a source-backed catalog of **26 criteria across five principles**: visibility, actionability, honesty, load and handoff, and drift and portability.

An AX review reports findings, applicability, suggested fixes, and what the review could not see. It never certifies a tool as “AX-compliant” and never automatically applies its suggested fixes.

## Install

### Claude Code marketplace

```text
/plugin marketplace add michaelstingl/ax-skill
/plugin install ax@ax-skill
```

Then ask for an AX review or invoke `/ax:ax` with the artifact to review. Plugin skills use the plugin name as a namespace; a bare installation uses `/ax`.

If AX is already installed through another marketplace, use one installation to avoid duplicate skills. The `claude-skills` marketplace remains a separate distribution entry; this repository is the maintenance home.

### Any agent that supports Agent Skills

Clone this repository and copy or symlink the **whole** `skills/ax/` directory into your agent's skill directory. Include `catalog/`: the review criteria and their sources travel with the skill. Follow your agent's instructions for its skill directory and discovery behavior.

The skill follows the [Agent Skills format](https://agentskills.io). The [Claude Code marketplace](https://code.claude.com/docs/en/plugin-marketplaces) is an installation adapter over the same files.

## Use

Ask the agent to review a concrete artifact and describe its consumer:

> Review this CLI's Agent eXperience. An agent runs it through a shell tool and parses its stdout. Read the code, identify applicable criteria, suggest fixes, and state what you could not verify.

“Quick AX look” focuses on the most applicable criteria. A thorough review considers all 26. For prose-only skills, the review focuses on honesty and cognitive load.

Read the [skill instructions](skills/ax/SKILL.md) for the report format, or the [catalog](skills/ax/catalog/AX-CATALOG.md) to inspect the criteria and evidence directly. Each criterion carries its applicability conditions and an evidence tier: external, measured, or consensus.

## Maintain

The skill and catalog are under `skills/ax/`. Update `catalog/VERSION` when the catalog changes, and keep the skill's descriptions consistent with it. Repository documentation and skill content are in English.

Run the same checks locally as in CI (Bash, `jq`, and standard Unix tools required):

```sh
bash scripts/validate.sh
```

With Claude Code installed, also validate the marketplace:

```sh
claude plugin validate .
```

The repository checks cover marketplace structure, skill paths, frontmatter, a heuristic English-language check, and structural internal-reference patterns. Copy `.scrub-deny.example` to the ignored `.scrub-deny` to check additional private names locally. CI also scans for secrets. These checks do not establish the completeness of the criteria, the accuracy of their sources, or the usability of the prose; changes still need review.

## Provenance

AX was first published in [michaelstingl/claude-skills](https://github.com/michaelstingl/claude-skills). This repository extracts the history of `skills/ax/`, retaining the original authorship, dates, and commit message. The extraction changes commit identifiers: publication commit [`bed8173`](https://github.com/michaelstingl/claude-skills/commit/bed81730dc94cb113626bc7d77ff9f901c788bad) becomes `75846e955ce013907710aa6ea7c44e2c3bc8fcf8` here. The initial extraction preserves all three published AX files byte-for-byte, including catalog version 2.

## License

No license has been declared for AX. This extraction does not add a license grant.
