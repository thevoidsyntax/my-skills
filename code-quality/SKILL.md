---
name: code-review
description: "Review the changes since a fixed point (commit, branch, tag, or merge-base) along two axes: Standards (does the code follow this repo's documented coding standards?) and Spec (does the code match what the originating issue/spec asked for?). Runs both reviews in parallel sub-agents and reports them side by side. Use when the user wants to review a branch, a PR, work-in-progress changes, or asks to \"review since X\"."
---

Two-axis review of the diff between `HEAD` and a fixed point the user supplies:

- **Standards**: does the code conform to this repo's documented coding standards?
- **Spec**: does the code faithfully implement the originating issue / spec?

Both axes run as **parallel sub-agents** so they don't pollute each other's context, then this skill aggregates their findings.

## Process

### 1. Pin the fixed point

Whatever the user said is the fixed point (a commit SHA, branch name, tag, `main`, `HEAD~5`, etc.). If they didn't specify one, ask for it.

Capture the diff command once: `git diff <fixed-point>...HEAD` (three-dot, so the comparison is against the merge-base). Also note the list of commits via `git log <fixed-point>..HEAD --oneline`.

Before going further, confirm the fixed point resolves (`git rev-parse <fixed-point>`) and the diff is non-empty.

### 2. Identify the spec source

Look for the originating spec, in this order:
1. Issue references in the commit messages (`#123`, `Closes #45`, etc.)
2. A path the user passed as an argument
3. A spec file under `docs/`, `specs/`, or `.scratch/`
4. If nothing is found, ask the user

### 3. Identify the standards sources

Anything in the repo that documents how code should be written (`CODING_STANDARDS.md`, `CONTRIBUTING.md`, etc.).

**Fowler Code Smells baseline** (always applies unless repo documents otherwise):

- **Mysterious Name**: function/variable/type name doesn't reveal what it does
- **Duplicated Code**: same logic shape in more than one place
- **Feature Envy**: method reaches into another object's data more than its own
- **Data Clumps**: same few fields/params keep travelling together
- **Primitive Obsession**: primitive/string standing in for domain concept
- **Repeated Switches**: same switch/if-cascade recurs
- **Shotgun Surgery**: one change forces scattered edits
- **Divergent Change**: one module edited for unrelated reasons
- **Speculative Generality**: abstraction added for needs the spec doesn't have
- **Message Chains**: long `a.b().c().d()` navigation
- **Middle Man**: class/function that mostly just delegates
- **Refused Bequest**: subclass ignores most of what it inherits

### 4. Spawn both sub-agents in parallel

**Standards sub-agent** → Check diff against standards + smell baseline

**Spec sub-agent** → Check diff against spec requirements

### 5. Aggregate

Present findings under `## Standards` and `## Spec` headings.

End with a one-line summary: total findings per axis, worst issue per axis.

## Why Two Axes

A change can pass one axis and fail the other:
- **Standards pass, Spec fail**: Implements wrong thing correctly
- **Spec pass, Standards fail**: Implements right thing incorrectly

Reporting separately prevents one axis from masking the other.

---

**Invoke:** `/code-review` | **Priority:** HIGH
