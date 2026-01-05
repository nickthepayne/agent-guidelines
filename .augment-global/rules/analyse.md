---
type: "always"
---

# Thorough Analysis Mode

> ⛔ **STOP — CONFIRMATION REQUIRED BEFORE PROCEEDING**
>
> If the user's request contains "analyse", "analyze", or asks for an in-depth review:
>
> **ASK THIS EXACT QUESTION FIRST:**
> "Would you like me to perform a thorough analysis? This includes researching cross-service dependencies, checking the GraphQL layer, and searching for prior art."
>
> - If confirmed → Follow the full analysis process below
> - If declined → Proceed with a standard response
>
> **DO NOT take any other action until the user responds.**

---

When confirmed, perform a comprehensive analysis of the problem statement before proposing any implementation.

> ⚠️ **Do NOT provide time estimates for any tasks or steps.**

> ⚠️ **Do NOT write or modify any code during the analysis phase.** Only create documentation artifacts. Code examples in the analysis are acceptable only as illustrative snippets to support the documentation, not as implementation.

## Analysis Requirements

### 1. Cross-Service Behavior Analysis

If the implementation is likely to require service calls to other services:

- Identify all external service dependencies
- Go to GitHub and examine the code of the other service(s)
- Understand the complete end-to-end dependencies
- Document API contracts, request/response formats, and error handling
- Note any authentication, rate limiting, or retry requirements

**GitHub Access:** Prefer the GitHub MCP server (`github-api` tool) when available. If no MCP server is available (e.g., CLI environment), use the GitHub CLI (`gh`) directly via `launch-process`.

### 2. User Interaction & GraphQL Analysis

If there is any user-facing interaction:

- Examine the `graph-registry` repository (federated graph)
- Understand how the feature fits into the existing GraphQL schema
- Identify which subgraphs are involved
- Document any schema changes required
- Note federation directives and entity relationships

### 3. External Research & Prior Art

If the problem involves common patterns, third-party integrations, or well-known domains:

- Search the web for existing solutions, best practices, and documentation
- Look for official API documentation, SDKs, and integration guides
- Find community discussions, blog posts, or case studies addressing similar problems
- Identify common pitfalls and lessons learned from others
- Let high-quality external resources influence the analysis and recommendations

**When to apply:** Third-party service integrations (e.g., Workday, Salesforce, payment providers), common architectural patterns (e.g., event sourcing, CQRS), or domain-specific problems with established solutions.

## Required Output

Create the following structure in the repository:

```
docs/analysis/<feature-name>/
├── README.md              # Summary document (for stakeholders/leads)
├── implementation.md      # Implementation guide (for engineers)
└── <supporting-files>     # Any additional artifacts at agent's discretion
```

### README.md — Summary Document

**Audience:** Stakeholders, tech leads, anyone needing context without deep code knowledge.

Contents:
- **Executive Summary** — Clear, concise overview of the problem and proposed solution. Should be understandable without full codebase knowledge.
- **Open Questions** — Unresolved questions that need input from stakeholders, domain experts, or further investigation. These should be prominent and actionable.
- **Risks & Uncertainties** — All identified risks, assumptions made, potential failure modes, performance/scalability concerns.
- **Research Summary** — What resources were consulted during the analysis: services examined, repositories reviewed, external documentation referenced, web searches performed. Provides transparency into the analysis process.
- **Link to Implementation Guide** — Reference to `implementation.md` for technical details.

### implementation.md — Implementation Guide

**Audience:** Engineers who will implement the solution.

Contents:
- **High-Level Flow Diagram(s)** — ASCII/text-based diagrams (no Mermaid). Example:
  ```
  [User] --> [API Gateway] --> [Service A]
                                    |
                                    v
                              [Service B] --> [Database]
  ```
- **Suggested Implementation Steps** — Ordered tasks with dependencies. Do NOT include time estimates.
- **Validation/Testing Strategy** — How to verify the implementation.
- **Rollout Considerations** — If applicable.

### Supporting Files

At the agent's discretion, include additional artifacts that support the analysis:
- API specifications or contracts
- Data flow diagrams
- Schema definitions
- Reference documentation excerpts

## Process

1. **Create isolated workspace** — Use `git worktree` to create an isolated working directory for the analysis
2. **Gather context** — Read the problem statement carefully
3. **Identify scope** — Determine all services and systems involved
4. **Research dependencies** — Examine external service code on GitHub
5. **Check GraphQL layer** — Review graph-registry if user-facing
6. **Synthesize findings** — Produce the required output sections
7. **Validate completeness** — Ensure all risks and dependencies are documented
8. **Open PR** — Commit the analysis, open a pull request, and reference the PR link when done

### Git Worktree Setup

Before starting the analysis, create an isolated branch and worktree:

```bash
# Create a new branch and worktree
git worktree add ../analysis-<feature-name> -b analysis/<feature-name>
cd ../analysis-<feature-name>
```

After completing the analysis:

```bash
# Commit and push
git add .
git commit -m "docs: analysis for <feature-name>"
git push -u origin analysis/<feature-name>

# Open PR using GitHub CLI
gh pr create --title "Analysis: <feature-name>" --body "Thorough analysis for <feature-name>"
```

Provide the PR link in the final output. Ensure the link is a full URL (e.g., `https://github.com/org/repo/pull/123`) so it is clickable in CLI environments.

### Continuing to Implementation

If the user asks to continue with implementation after the analysis:

- **Stay in the same worktree** — Do not create a new branch or worktree
- **Continue committing to the same branch** — Add implementation commits on top of the analysis
- **Update the existing PR** — Push additional commits to the same PR

