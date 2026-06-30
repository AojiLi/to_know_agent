# How to Use AI Models Better

Language: English | [中文](./README.zh-CN.md)

Using AI well is not just about writing better prompts. It is about shaping the work environment so an AI agent can understand context, use tools, repeat known workflows, and verify its own results.

The operating model can be summarized in four layers:

```text
Context  decides what the AI understands
Tools    decide what the AI can do
CLI      decides what the AI can repeat reliably
Verify   decides how the AI knows whether it is correct
```

Or, more practically:

```text
.md / skills  provide knowledge
tools / API   provide capability
CLI           turns workflows into reusable operations
tests/checks  close the feedback loop
```

## 1. Context: Tell The AI What Matters

Context is not just background material. It is the decision environment. The AI needs to know what it is doing, why it matters, what state the project is in, what must not change, and what counts as success.

Good context usually includes:

- project goal: what problem the project is solving
- current state: what already exists and what should not be touched
- constraints: tech stack, coding style, permissions, and business rules
- success criteria: what counts as done and what counts as failure
- decision history: why previous choices were made

Useful context files include:

- `README.md`
- `AGENTS.md`
- `CLAUDE.md` / `CODEX.md`
- `docs/architecture.md`
- `docs/workflows/*.md`
- skill files

The key point is that context should be maintainable, searchable, and compressible. Do not put everything into one prompt. Let the AI read what it needs when it needs it.

## 2. Tools: Give The AI Ways To Act

An AI agent cannot complete real work with language alone. It needs tools.

Common tool categories include:

- file tools: read, search, edit, and test code
- browser tools: operate logged-in web pages, click, screenshot, and extract information
- API tools: GitHub, Linear, Slack, Gmail, databases, and cloud services
- local CLI tools: project scripts, deployment commands, and data-processing commands
- MCP / plugin tools: dedicated integrations that connect external systems to the agent

The goal is not to give the AI as many tools as possible. The useful tools are the ones with:

- clear permissions
- stable inputs and outputs
- readable error messages
- repeatable execution
- minimal dependence on manual visual judgment

For example, instead of asking an AI to manually click through a web page every time, it is usually better to give it an API or CLI when one exists.

## 3. CLI: Turn Successful Workflows Into Deterministic Operations

AI agents have limited context, and their reasoning can vary from run to run. Repeated workflows should not depend on prompt quality forever.

Any workflow that has succeeded several times is a candidate for CLI automation:

- creating projects
- generating reports
- syncing data
- batch-editing files
- publishing releases
- running a specific test suite
- checking project conventions
- generating documentation

A good CLI should have:

- explicit parameters
- `--dry-run`
- repeatable execution
- idempotency where possible
- structured output such as JSON
- clear exit codes
- traceable logs
- tests or fixtures

Then the AI does not need to rediscover the whole workflow. It only needs to call a stable command:

```bash
project-cli generate-report --date 2026-06-30 --format markdown
```

This greatly improves the accuracy and reliability of AI instructions.

## 4. Verify: Help The AI Know Whether It Is Right

The hardest problem is often not that the AI cannot do the task. It is that the AI may not know whether the result is correct.

Every task should have a verification path:

- unit tests
- type checks
- lint
- snapshots
- screenshot comparison
- data validation
- schema validation
- human acceptance criteria
- CI checks

The ideal workflow looks like this:

```bash
make test
make lint
make verify
```

Then the AI can read the results, fix failures, and iterate.

## Summary

People who use AI well are not just better prompt writers. They build environments where AI can understand the work, use the right tools, reuse proven workflows, and verify outcomes.

