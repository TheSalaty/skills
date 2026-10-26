# skills

## Install

Add this repo's skills to your coding agent:

```sh
npx skills@latest add falcondev-oss/skills -g
```

## Skills

| Skill | What it does |
|---|---|
| [`conventional-commits`](skills/conventional-commits/SKILL.md) | Formats commit messages, branch names, PR titles, and issue titles to the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) spec. Splits oversized diffs into atomic commits and verifies every message against the spec before it lands. |
| [`implement-pr`](skills/implement-pr/SKILL.md) | Implements a change, reviews and verifies it, opens a pull request, then monitors CI and review feedback until the PR is merge-ready. |
| [`review-local-changes`](skills/review-local-changes/SKILL.md) | Cold-reviews the local changes with `code-review`, `simplicity-review` and `bug-review`, fixes valid findings, and reports the summary and every finding to the user. |
| [`falcondev-form`](skills/falcondev-form/SKILL.md) | Building or editing forms with [`@falcondev-oss/form`](https://github.com/falcondev-oss/form) — the type-safe, reactive, schema-driven form library (`form-core`, `form-react`, `form-vue`) built on `@vue/reactivity`. Covers `useForm`/`useFormCore`, `form.fields` accessors, `$use()`, `field.value`/`handleChange`/`model`, and Standard Schema (zod v4 / arktype) forms in React or Vue. |
| [`trpc-typed-form-data`](skills/trpc-typed-form-data/SKILL.md) | Type-safe file uploads through tRPC with [`@falcondev-oss/trpc-typed-form-data`](https://github.com/falcondev-oss/trpc-typed-form-data). Covers the three touch points (`typedFormDataLink`, `createTypedFormDataPlugin`, `typedFormData()`), `createTypedFormData`, the `file()` validator / `FileValue` type as a stable alternative to `z.file()`, and `ReactNativeFile` / Expo uploads. |
| [`workflow`](skills/workflow/SKILL.md) | Durable, type-safe queue workers with [`@falcondev-oss/workflow`](https://github.com/falcondev-oss/workflow) on Redis. Covers `WorkflowNamespace`/`createWorkflow`, `defineWorkflow`/`handle()` to enqueue without loading handlers, `step.do`/`wait`/`waitUntil` and replay semantics, `run`/`runIn`/`runAt`/`work()`, `job.wait()` and its errors, `upsertSchedule` cron schedules, group ordering and the four concurrency caps, plus a full option reference. |
| [`shareflare`](skills/shareflare/SKILL.md) | Shares any local file through a public URL using `SHAREFLARE_URL` and `SHAREFLARE_TOKEN`, including artifacts for GitHub issues and pull requests. |
| [`file-pr`](skills/file-pr/SKILL.md) | File a PR from the current branch |
| [`babysit-pr`](skills/babysit-pr/SKILL.md) | Monitor a pull request through review and CI |
| [`simplicity-review`](skills/simplicity-review/SKILL.md) | Reviews a diff for complexity it can shed: dead code, duplicated repo helpers, reinvented stdlib, speculative abstractions, derivable stored state. One numbered line per finding naming what to cut and what replaces it, each checked against lint, types and the contract. |
| [`bug-review`](skills/bug-review/SKILL.md) | Reviews a diff for merge-blocking bugs only. Each finding carries `file:line`, why it is wrong, and how to demonstrate the failure; unconfirmed suspicions are marked with where it looked. |
| [`spec-review`](skills/spec-review/SKILL.md) | Reviews a diff against its ticket or contract only: missing, unrequested and wrongly implemented requirements. Each finding carries `file:line`, the quoted requirement, and what the diff does instead. |
| [`show-me`](skills/show-me/SKILL.md) | Shows a change, flow or structure with the smallest fitting view: pseudocode, call tree, component or file tree, Mermaid, `diff`, or a focused HTML file. Adapted from [`humanlayer/skills`](https://github.com/humanlayer/skills/tree/main/plugins/show-me) (MIT) to be model-invocable. |
| [`quick-iteration`](skills/quick-iteration/SKILL.md) | Enter a quick iteration session |
