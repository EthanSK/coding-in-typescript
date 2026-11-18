# Coding in TypeScript

This skill was made from the coding and TypeScript instructions for AI Music Video Studio (AIMVS). It brings the guidance that applies across projects into a standalone skill published for anyone to use.

Use it when writing, changing, or reviewing TypeScript. The skill follows your project's framework, tools, and conventions.

The skill covers:

- **Types and validators.** Derive fields from their owner, catch key typos at the point of use, preserve discriminated unions, and validate external data at runtime.
- **Ownership and structure.** Reuse the established implementation, keep feature code out of generic layers, and put related files and declarations where readers expect them.
- **Data, APIs, and operations.** Preserve schemas, queries, pagination, authorization, error semantics, and retry behavior.
- **Comments and JSDoc.** Explain decisions where they matter and document the caller's contract.
- **Frontend, tests, and review.** Verify real behavior, including form state and shared controls, and use the project's compiler, formatter, and test runner.

## Install in Codex

To install it in one project, run this from the root of your own repository:

```sh
git clone https://github.com/EthanSK/coding-in-typescript.git .agents/skills/coding-in-typescript
```

For all your projects, use `"$HOME/.agents/skills/coding-in-typescript"` as the destination. The [Codex skill install paths](https://developers.openai.com/api/reference/cli) also describe the project and user scopes. For another Agent Skills host, copy this folder to its documented skills directory, keeping the references and the update resources together.

Start a new session and try:

> Use $coding-in-typescript to update this request type and its validator. Show that the compiler rejects a misspelled field.

Read [SKILL.md](SKILL.md) for the operating instructions and links to the detailed guidance. The skill can check for public updates on first use once due, and it asks before installing an update. Python 3 is used only for the update check state.

## License

[MIT](LICENSE)
