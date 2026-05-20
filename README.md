# @bodnar-sh/configs

Shareable lint, format, and git-hook configs consumed across the `bodnar-sh` workspace.

## Install

```sh
bun add -D github:bodnar-sh/configs
```

GitHub-URL installs avoid an npm-publish loop. Pin to a tag if you want stability:

```sh
bun add -D github:bodnar-sh/configs#v0.0.0
```

## Consume

### oxlint

```ts
// oxlint.config.ts
import base from "@bodnar-sh/configs/oxlint";
import { defineConfig } from "oxlint";

export default defineConfig({ extends: [base] });
```

> Note: `extends` requires the TypeScript config file (`oxlint.config.ts`). The JSON variant (`.oxlintrc.json`) does **not** support package imports.

### oxfmt

```ts
// oxfmt.config.ts
import { extendOxfmt } from "@bodnar-sh/configs/oxfmt";

export default extendOxfmt({
  // overrides
});
```

oxfmt has no native `extends`; this helper merges the shared preset with your overrides.

### Git hooks

```sh
bun run @bodnar-sh/configs/git-hooks/install
```

This sets `core.hooksPath` in the current repo to point at the installed hooks. Hooks run scanners and fail loudly:

- `pre-commit`: trufflehog + nyx-scanner over staged files
- `pre-push`: full-repo trufflehog, socket scan against deps, full nyx scan

Required tools (install via mise): `trufflehog`, `nyx-scanner`, `socket` (`@socketsecurity/cli`).

## License

MIT
