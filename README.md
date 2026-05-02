# Monorepo Management Tool

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> An AI-native, polyglot monorepo platform with intelligent build orchestration, affected-package detection, and first-class SBOM support — without locking you into a single language ecosystem or a commercial cloud.

Monorepo Management Tool is an open-source build orchestration and dependency management platform for engineering teams running multiple services, libraries, or applications in a single repository. It is designed for platform and DevEx engineers who need reproducible incremental builds, accurate affected-package scoping, and AI-assisted CI across JavaScript, Python, Go, Rust, and JVM codebases — in one tool, not five.

---

## Why Monorepo Management Tool?

- **JS/TS lock-in is the norm, not the exception.** Turborepo and Nx — the two most widely adopted tools (combined ~7M weekly downloads) — provide minimal or no support for Go, Python, or Rust. Teams with mixed-language repositories are forced to assemble Bazel, Changesets, and custom CI scripts manually.
- **Bazel scales, but at significant cost.** Bazel delivers unmatched build hermeticity and polyglot support, but the documentation gap (the top community complaint at BazelCon 2025) and 6–24 month migration timelines make it inaccessible for most organisations.
- **Commercial ceilings arrive quickly.** Nx Cloud caps the free tier at 300 CI pipeline executions per month before billing starts at $249/month. Develocity's advanced caching and analytics are enterprise-only with no published pricing. Open-source alternatives lack distributed execution entirely.
- **SBOM compliance is universally bolted on.** No mainstream monorepo tool generates per-package Software Bills of Materials as a first-class build output. EU CRA Article 20 requires 10-year SBOM retention; every team integrates Syft or cdxgen externally, with no awareness of the monorepo's package graph.
- **AI integration is shallow or absent.** Nx's MCP server (2025) is the only production implementation that exposes workspace graph data to AI assistants. Turborepo and Bazel are completely AI-blind. Self-healing CI remains rudimentary across all tools.

---

## Key Features

### Dependency Graph & Affected Detection

- Accurate DAG construction across all supported languages from source imports
- Affected-package detection scoping builds and tests to transitively impacted projects only
- AI-assisted prediction layer trained on historical CI outcomes to prune false positives from static graph traversal
- Natural language workspace queries via MCP server ("which packages are affected by this change?")

### Task Orchestration & Caching

- Topological task scheduling with configurable parallelism
- Content-addressed local build cache with deterministic input hashing
- Remote cache sharing across CI agents and developer machines (self-hosted and managed options)
- Distributed task execution across dynamic CI agent pools

### Polyglot Support

- First-class support for JavaScript/TypeScript, Python, Go, and Rust; extensible rule system for additional languages
- Unified versioning and publishing pipeline spanning multiple language registries (npm, PyPI, Go module proxy, crates.io)
- Toolchain version pinning per workspace, eliminating drift between developer machines and CI

### AI-Native Capabilities

- MCP server exposing workspace graph, project metadata, and task configuration to AI assistants
- Autonomous CI failure triage: correlates failures across the distributed task graph and identifies root-cause packages
- AI-generated dependency upgrade PRs with per-package impact forecasting
- Workspace topology recommendations derived from import graphs, team ownership, and change frequency

### Security & Compliance

- Native per-package SBOM generation in SPDX and CycloneDX formats as a first-class build output
- Security-aware dependency graph: CVE and licence findings scoped to the specific packages affected, not the entire repository
- Architectural constraint enforcement preventing invalid cross-package imports

---

## AI-Native Advantage

Current tools detect affected packages via deterministic static graph traversal — if file A imports B, every dependent of B is marked affected, regardless of whether the change is a comment edit or a behavioural regression. By training on historical CI pass/fail data, this project can learn which changes *actually* cause downstream failures and prune unnecessary test runs, reducing CI time without sacrificing coverage. Beyond build scoping, an AI agent can autonomously triage failures, correlate patterns across the distributed task graph, and generate targeted patch PRs — closing the loop that today requires human intervention after every flaky pipeline.

---

## Tech Stack & Deployment

The tool targets self-hosted deployment as a first-class mode; a managed cloud option is planned for teams without dedicated platform infrastructure. The remote cache and task execution APIs are designed to be compatible with the [Remote Execution API (REAPI)](https://github.com/bazelbuild/remote-apis) so that existing Bazel-compatible cache backends (BuildBuddy, EngFlow, NativeLink) can be reused. Build observability is exported via OpenTelemetry (OTLP) for compatibility with existing monitoring stacks. SBOM outputs conform to SPDX and CycloneDX standards. The AI layer exposes workspace data via the Model Context Protocol (MCP).

---

## Market Context

The broader software development tools market was valued at $7.47 billion in 2025 and is projected to reach $8.78 billion in 2026 at ~16% CAGR (Mordor Intelligence and others). Approximately 63% of companies with 50 or more developers have adopted monorepos (2026 industry survey). Primary buyers are platform and DevEx engineers at 50–500 person engineering organisations, staff engineers tasked with reducing CI cost, and engineering managers consolidating polyrepo estates. Existing commercial tools price from $249/month (Nx Cloud) to undisclosed enterprise contracts (Develocity), leaving a clear open-source gap for teams that need distributed caching and polyglot support without a SaaS dependency.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed open-source material with a compatible licence. Copyright infringement and licence violations will not be tolerated and will result in immediate removal of the offending contribution. If you are unsure whether a piece of code, text, or other material is safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. See [discussion](#) for context.
