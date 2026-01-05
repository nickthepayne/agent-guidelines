# Thorough Analysis Mode

When this rule is referenced, perform a comprehensive analysis of the problem statement before proposing any implementation.

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

The analysis must produce the following sections:

### Problem & Solution Diagram

Provide a high-level flow diagram directly in markdown (no Mermaid). Use ASCII/text-based diagrams:

```
Example format:

[User] --> [API Gateway] --> [Service A]
                                  |
                                  v
                            [Service B] --> [Database]
```

### Risks & Uncertainties

- List all identified risks
- Note any assumptions made
- Highlight areas requiring clarification
- Identify potential failure modes
- Note any performance or scalability concerns

### Suggested Way Forward

- Recommended approach with rationale
- High-level implementation tasks (ordered)
- Dependencies between tasks
- Suggested validation/testing strategy
- Rollout considerations (if applicable)

## Process

1. **Gather context** — Read the problem statement carefully
2. **Identify scope** — Determine all services and systems involved
3. **Research dependencies** — Examine external service code on GitHub
4. **Check GraphQL layer** — Review graph-registry if user-facing
5. **Synthesize findings** — Produce the required output sections
6. **Validate completeness** — Ensure all risks and dependencies are documented

