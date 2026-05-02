# Post Fiat Evidence Manifest Guide

> A reusable proof packet that makes human work reviewable, comparable, privacy-safe, and reusable across the network.

## Purpose

The Post Fiat Evidence Manifest is a reusable proof structure for Task Node submissions.

Its purpose is to make completed work easier to review, compare, verify, and reuse across the network.

The manifest does not replace judgment. It provides consistency.

- What the contributor claims they did
- What evidence supports the claim
- Where the artifact can be inspected
- How the work can be reproduced or reviewed
- What was redacted for privacy or safety
- How the contribution may create downstream value for the network

The goal is to reduce reviewer ambiguity, not to create new governance policy.

<details>
<summary><strong>1. Evidence Manifest Field Set</strong></summary>

| Field | Required | Description |
|---|---|---|
| `task_objective` | Yes | The task the contributor was attempting to complete. |
| `contributor_claim` | Yes | A concise statement of what the contributor claims they completed. |
| `source_signals` | Yes | The inputs, references, prompts, briefs, market signals, documents, or context used to produce the work. |
| `artifact_links` | Yes | Links to the completed output or deliverable. |
| `review_steps` | Yes | Plain-English steps a reviewer can follow to inspect, test, or evaluate the work. |
| `proof_media` | Yes | Screenshots, videos, logs, commits, exports, documents, or other proof that supports the claim. |
| `redactions` | Yes | Any removed, blurred, summarized, or anonymized information. |
| `downstream_reuse_potential` | Yes | How the work may be reused by Post Fiat, future contributors, reviewers, onboarding flows, content systems, market intelligence processes, tooling, or sales assets. |
| `token_value_rationale` | Yes | Why the contribution deserves value recognition inside the network. |
| `reviewer_status` | Yes | The current review state of the submission. |
| `reviewer_notes` | No | Optional reviewer comments, concerns, or requests. |
| `submission_timestamp` | No | Date and time the manifest was submitted. |
| `contributor_id` | No | Contributor name, handle, wallet, or other identifier. Use only what is appropriate to share. |

</details>

<details>
<summary><strong>2. Copyable JSON Schema-Style Template</strong></summary>

```json
{
  "task_objective": {
    "type": "string",
    "required": true,
    "description": "The specific task or outcome the contributor was asked to complete."
  },
  "contributor_claim": {
    "type": "string",
    "required": true,
    "description": "A concise claim describing what the contributor completed."
  },
  "source_signals": {
    "type": "array",
    "required": true,
    "items": {
      "type": "object",
      "properties": {
        "signal_type": {
          "type": "string",
          "description": "Examples: task brief, market signal, user feedback, source document, code issue, screenshot, research note."
        },
        "description": {
          "type": "string",
          "description": "Short explanation of the source signal and why it mattered."
        },
        "link_or_reference": {
          "type": "string",
          "description": "URL, file reference, internal reference, or short citation. Use 'redacted' if private."
        }
      }
    },
    "description": "The inputs or context used to produce the work."
  },
  "artifact_links": {
    "type": "array",
    "required": true,
    "items": {
      "type": "object",
      "properties": {
        "artifact_type": {
          "type": "string",
          "description": "Examples: Markdown guide, code repository, dashboard, spreadsheet, video, memo, thread, landing page."
        },
        "description": {
          "type": "string",
          "description": "What the artifact is and what it contains."
        },
        "url": {
          "type": "string",
          "description": "Public or reviewer-accessible link to the artifact."
        }
      }
    },
    "description": "Links to completed work products."
  },
  "review_steps": {
    "type": "array",
    "required": true,
    "items": {
      "type": "string"
    },
    "description": "Steps a reviewer can follow to inspect, reproduce, or evaluate the submission."
  },
  "proof_media": {
    "type": "array",
    "required": true,
    "items": {
      "type": "object",
      "properties": {
        "media_type": {
          "type": "string",
          "description": "Examples: screenshot, screen recording, commit log, terminal output, export, dataset sample, before/after comparison."
        },
        "description": {
          "type": "string",
          "description": "What the proof shows."
        },
        "url_or_reference": {
          "type": "string",
          "description": "Link or reference to the proof media."
        }
      }
    },
    "description": "Evidence that supports the contributor claim."
  },
  "redactions": {
    "type": "array",
    "required": true,
    "items": {
      "type": "object",
      "properties": {
        "redacted_item": {
          "type": "string",
          "description": "What was removed, blurred, anonymized, or summarized."
        },
        "reason": {
          "type": "string",
          "description": "Why the information was redacted."
        },
        "reviewable_alternative": {
          "type": "string",
          "description": "How the reviewer can still evaluate the work without seeing private information."
        }
      }
    },
    "description": "Privacy-preserving changes made to the evidence."
  },
  "downstream_reuse_potential": {
    "type": "string",
    "required": true,
    "description": "How the artifact, method, data, or insight can be reused by the network."
  },
  "token_value_rationale": {
    "type": "string",
    "required": true,
    "description": "Why this contribution may merit token-value recognition based on usefulness, difficulty, originality, or network leverage."
  },
  "reviewer_status": {
    "type": "string",
    "required": true,
    "allowed_values": [
      "submitted",
      "needs_clarification",
      "accepted",
      "accepted_with_notes",
      "rejected",
      "duplicate",
      "out_of_scope"
    ],
    "description": "Current review state of the evidence manifest."
  },
  "reviewer_notes": {
    "type": "string",
    "required": false,
    "description": "Optional reviewer comments, concerns, or requests."
  },
  "submission_timestamp": {
    "type": "string",
    "required": false,
    "description": "Date and time the manifest was submitted."
  },
  "contributor_id": {
    "type": "string",
    "required": false,
    "description": "Contributor name, handle, wallet, or other identifier. Use only what is appropriate to share."
  }
}
```

</details>

<details>
<summary><strong>3. Contributor Guidance: Code and Engineering Tasks</strong></summary>

### Acceptable evidence may include

- Repository links
- Pull request links
- Commit hashes or commit ranges
- Issue references
- Before/after screenshots
- Terminal output
- Test results
- Deployment links
- Linked routes where the feature or fix can be inspected
- Short screen recordings
- Setup or reproduction instructions
- Notes on known limitations, edge cases, or incomplete work

### Good review steps might include

1. Open the linked repository, pull request, or deployment.
2. Review the commit range from `[start commit]` to `[end commit]`.
3. Check the issue reference or task brief that the work responded to.
4. Run the setup instructions in the README or submission notes.
5. Run the relevant test command, build command, or local preview if applicable.
6. Confirm the feature, fix, or output appears at the linked route.
7. Compare before/after screenshots, logs, or screen recordings.
8. Review any disclosed limitations, edge cases, or incomplete areas.

### Privacy-safe guidance

- Do not expose API keys, passwords, tokens, seed phrases, or private credentials.
- Do not include private environment variables such as `.env` files.
- Redact user data, customer data, private logs, internal URLs, private repo details, and sensitive system information when needed.
- If a full repository cannot be public, provide screenshots, commit summaries, test output, a short screen recording, or a limited reviewer-access link.
- Use fake or sample data when showing features publicly.
- If screenshots include sensitive information, blur the sensitive parts while keeping the relevant feature visible.

</details>

<details>
<summary><strong>4. Contributor Guidance: Research Tasks</strong></summary>

### Acceptable evidence may include

- Source links
- Research notes
- Annotated documents
- Datasets
- Screenshots of relevant claims
- Comparison tables
- Methodology notes
- Summary memos
- Reasoning trail at a high level

### Good review steps might include

1. Review the source list.
2. Check whether the cited sources support the claims.
3. Compare the summary against the original task objective.
4. Inspect the methodology notes for obvious gaps.
5. Confirm whether the output can be reused in future briefs or reviews.

### Privacy-safe guidance

- Do not include private conversations without consent.
- Summarize sensitive sources instead of exposing them directly.
- Redact names, handles, emails, wallet addresses, or private group content where appropriate.
- Keep enough source context for the reviewer to understand why the claim is credible.

</details>

<details>
<summary><strong>5. Contributor Guidance: Content and Narrative Tasks</strong></summary>

### Acceptable evidence may include

- Final copy
- Drafts
- Source material
- Screenshots
- Published links
- Before/after comparisons
- Editorial rationale
- Distribution links
- Performance snapshots, when relevant

### Good review steps might include

1. Open the final artifact.
2. Compare it against the task objective.
3. Review the source signals used to shape the content.
4. Check whether the piece is clear, reusable, and aligned with Post Fiat language.
5. Confirm whether the artifact can become a future onboarding, sales, or educational asset.

### Privacy-safe guidance

- Do not expose private client information.
- Redact unpublished strategy details if needed.
- If using screenshots of messages, blur names and unrelated content.
- Preserve enough context to show why the content was created.

</details>

<details>
<summary><strong>6. Contributor Guidance: Market-Intelligence Tasks</strong></summary>

### Acceptable evidence may include

- Watchlists
- Screenshots
- Source links
- Market structure notes
- Wallet or protocol observations
- Public data dashboards
- Comparison tables
- Thesis memos
- Risk notes

### Good review steps might include

1. Review the stated market question.
2. Inspect the source signals.
3. Check whether the conclusion follows from the evidence.
4. Confirm whether uncertainty and risk were clearly stated.
5. Determine whether the intelligence can inform future Post Fiat decisions.

### Privacy-safe guidance

- Avoid exposing private financial information.
- Do not include sensitive personal trading data unless intentionally shared.
- Redact private wallet addresses if needed.
- Separate observation from recommendation.
- Make uncertainty visible.

</details>

<details>
<summary><strong>7. Filled Examples</strong></summary>

<details>
<summary><strong>Example 1: Engineering / Tooling Submission</strong></summary>

```json
{
  "task_objective": "Create a lightweight internal tool that converts completed task submissions into a standardized evidence manifest format.",
  "contributor_claim": "I built a working form-to-JSON prototype that lets contributors enter task proof and export a structured evidence manifest.",
  "source_signals": [
    {
      "signal_type": "task brief",
      "description": "The task requested a reusable evidence manifest format for future Task Node reviews.",
      "link_or_reference": "Task Node proposal reference"
    },
    {
      "signal_type": "reviewer pain point",
      "description": "Reviewers need a consistent way to compare task proof across different types of work.",
      "link_or_reference": "summarized from reviewer feedback"
    }
  ],
  "artifact_links": [
    {
      "artifact_type": "prototype",
      "description": "A simple web form that outputs a copyable JSON evidence manifest.",
      "url": "https://example.com/evidence-manifest-tool"
    },
    {
      "artifact_type": "repository",
      "description": "Source code for the prototype.",
      "url": "https://github.com/example/evidence-manifest-tool"
    }
  ],
  "review_steps": [
    "Open the prototype link.",
    "Fill in each required field with sample task data.",
    "Click export JSON.",
    "Confirm the output matches the evidence manifest field set.",
    "Review the repository README for setup instructions."
  ],
  "proof_media": [
    {
      "media_type": "screen recording",
      "description": "Shows the contributor filling out the form and exporting valid JSON.",
      "url_or_reference": "https://example.com/demo-video"
    },
    {
      "media_type": "commit log",
      "description": "Shows implementation history for the form, validation, and export function.",
      "url_or_reference": "https://github.com/example/evidence-manifest-tool/commits/main"
    }
  ],
  "redactions": [
    {
      "redacted_item": "Local environment variables",
      "reason": "They may expose private development configuration.",
      "reviewable_alternative": "The README includes safe setup instructions using placeholder values."
    }
  ],
  "downstream_reuse_potential": "The tool can become a contributor-facing submission helper for future Task Node reviews, reducing formatting inconsistency and reviewer ambiguity.",
  "token_value_rationale": "The contribution improves review throughput, standardizes proof collection, and creates reusable infrastructure for future network submissions.",
  "reviewer_status": "submitted",
  "reviewer_notes": "",
  "submission_timestamp": "2026-05-02",
  "contributor_id": "contributor_handle"
}
```

</details>

<details>
<summary><strong>Example 2: Capital-Intelligence Submission</strong></summary>

```json
{
  "task_objective": "Produce a capital-intelligence brief identifying three AI/crypto projects where narrative clarity may affect market positioning.",
  "contributor_claim": "I created a comparative brief covering three AI/crypto projects, their public positioning, narrative gaps, and possible Post Fiat relevance.",
  "source_signals": [
    {
      "signal_type": "project website",
      "description": "Public homepage and documentation were reviewed to understand each project's stated positioning.",
      "link_or_reference": "public project URLs listed in the brief"
    },
    {
      "signal_type": "market signal",
      "description": "Public social posts, ecosystem discussions, and recent updates were reviewed for narrative momentum.",
      "link_or_reference": "source links included in research appendix"
    },
    {
      "signal_type": "category comparison",
      "description": "Projects were compared across AI utility, crypto rails, contributor networks, and reputation relevance.",
      "link_or_reference": "comparison table in final brief"
    }
  ],
  "artifact_links": [
    {
      "artifact_type": "research memo",
      "description": "Final capital-intelligence brief with project summaries, narrative gaps, and opportunity notes.",
      "url": "https://example.com/capital-intelligence-brief"
    },
    {
      "artifact_type": "spreadsheet",
      "description": "Comparison table used to evaluate the three projects.",
      "url": "https://example.com/comparison-table"
    }
  ],
  "review_steps": [
    "Open the research memo.",
    "Check whether each project summary is supported by the listed public sources.",
    "Review the comparison table.",
    "Confirm that claims are separated from speculation.",
    "Evaluate whether the brief could inform future outreach, content, or contributor strategy."
  ],
  "proof_media": [
    {
      "media_type": "source appendix",
      "description": "List of public URLs used in the research process.",
      "url_or_reference": "included at bottom of research memo"
    },
    {
      "media_type": "screenshot set",
      "description": "Screenshots of public positioning and relevant market signals.",
      "url_or_reference": "https://example.com/source-screenshots"
    }
  ],
  "redactions": [
    {
      "redacted_item": "Private notes about possible trades",
      "reason": "Personal financial strategy is not necessary for task review.",
      "reviewable_alternative": "The public market observations and project analysis remain included."
    }
  ],
  "downstream_reuse_potential": "The brief can support future outreach targeting, narrative compression offers, ecosystem mapping, and Post Fiat positioning research.",
  "token_value_rationale": "The submission creates reusable intelligence that helps the network identify where narrative, reputation, and contribution systems may matter commercially.",
  "reviewer_status": "submitted",
  "reviewer_notes": "",
  "submission_timestamp": "2026-05-02",
  "contributor_id": "contributor_handle"
}
```

</details>

<details>
<summary><strong>Example 3: Retail / Content Submission</strong></summary>

```json
{
  "task_objective": "Create a reusable content asset explaining portable reputation to non-technical contributors.",
  "contributor_claim": "I created a five-slide carousel that explains portable reputation as the byproduct of verified work, using Post Fiat language and a simple visual sequence.",
  "source_signals": [
    {
      "signal_type": "source essay",
      "description": "The carousel was adapted from an existing portable reputation essay.",
      "link_or_reference": "https://example.com/portable-reputation-essay"
    },
    {
      "signal_type": "message architecture",
      "description": "The content follows the sequence: Context -> Tasks -> Proof -> Reputation -> Rewards.",
      "link_or_reference": "Post Fiat narrative module"
    },
    {
      "signal_type": "audience need",
      "description": "The asset was designed to make the concept easier for new contributors to understand quickly.",
      "link_or_reference": "summarized onboarding need"
    }
  ],
  "artifact_links": [
    {
      "artifact_type": "carousel",
      "description": "Five-slide visual explainer for portable reputation.",
      "url": "https://example.com/portable-reputation-carousel"
    },
    {
      "artifact_type": "caption draft",
      "description": "Suggested post copy for publishing the carousel.",
      "url": "https://example.com/carousel-caption"
    }
  ],
  "review_steps": [
    "Open the carousel.",
    "Read the slides in order.",
    "Compare the language against the source essay.",
    "Check whether the concept is understandable without the original essay.",
    "Determine whether the asset can be reused in onboarding, social distribution, or outreach."
  ],
  "proof_media": [
    {
      "media_type": "before/after comparison",
      "description": "Shows how the long essay was compressed into a shorter visual asset.",
      "url_or_reference": "https://example.com/before-after"
    },
    {
      "media_type": "export file",
      "description": "Final PNG or PDF export of the carousel.",
      "url_or_reference": "https://example.com/carousel-export"
    }
  ],
  "redactions": [
    {
      "redacted_item": "Private editorial comments",
      "reason": "They included unrelated conversation context.",
      "reviewable_alternative": "The final carousel, source essay, and before/after comparison are sufficient for review."
    }
  ],
  "downstream_reuse_potential": "The asset can be reused as onboarding material, social content, sales proof, or a visual explanation of the Post Fiat reputation model.",
  "token_value_rationale": "The contribution turns dense source material into a reusable education asset that can improve understanding, distribution, and contributor onboarding.",
  "reviewer_status": "submitted",
  "reviewer_notes": "",
  "submission_timestamp": "2026-05-02",
  "contributor_id": "contributor_handle"
}
```

</details>

</details>

<details open>
<summary><strong>8. Reviewer Checklist</strong></summary>

Use this checklist when reviewing an Evidence Manifest.

| Review Area | Questions |
|---|---|
| Completeness | Does the manifest include all required fields? Is the contributor claim clear? Are artifact links included? Are review steps specific enough to follow? |
| Relevance | Does the submitted work match the original task objective? Is the evidence directly connected to the claim? Are irrelevant links, screenshots, or claims avoided? |
| Authenticity | Does the proof support that the contributor actually performed the work? Are there timestamps, commits, exports, screenshots, or other signals of authorship? Does anything appear copied, unverifiable, or inflated? |
| Reproducibility / Reviewability | Can a reviewer inspect the artifact without needing private context? For code, can the reviewer run, test, or inspect the implementation? For research, can the reviewer trace claims back to sources? For content, can the reviewer compare the final artifact to the source material or objective? |
| Privacy Safety | Are private keys, credentials, personal data, private messages, or sensitive financial details removed? Are redactions clearly explained? Does the manifest preserve enough evidence to remain reviewable after redaction? |
| Network Reuse | Can this work be reused by other contributors, reviewers, onboarding flows, tools, content systems, or market-intelligence processes? Does the submission create value beyond a one-time task? Is the downstream reuse potential realistic and clearly stated? |
| Token-Value Rationale | Does the contributor explain why the work may deserve value recognition? Is the rationale based on usefulness, difficulty, originality, leverage, or reuse? Does the rationale avoid exaggerated claims? |

</details>

## Simple Contributor Submission Format

For easier use, contributors can copy this shorter version into future task submissions:

```markdown
# Evidence Manifest

## Task Objective
[What task were you completing?]

## Contributor Claim
[What do you claim you completed?]

## Source Signals
- [Input, source, brief, market signal, or context used]
- [Input, source, brief, market signal, or context used]

## Artifact Links
- [Final artifact link]
- [Supporting artifact link]

## Review Steps
1. [Step one]
2. [Step two]
3. [Step three]

## Proof Media
- [Screenshot, video, commit, export, source appendix, or other proof]
- [Screenshot, video, commit, export, source appendix, or other proof]

## Redactions
- [What was removed or blurred? Why? How can it still be reviewed?]

## Downstream Reuse Potential
[How can this work be reused by the network?]

## Token-Value Rationale
[Why might this contribution deserve value recognition?]

## Reviewer Status
submitted
```

## One-Line Definition

A Post Fiat Evidence Manifest is a structured proof packet that makes human work reviewable, comparable, privacy-safe, and reusable across the network.
