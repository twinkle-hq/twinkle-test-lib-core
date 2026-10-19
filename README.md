# twinkle-test-lib-core

QA fixture: the **core library** for the system-test harness. Published to
`twinkle-hq/twinkle-test-lib-core`.

Exercises MVS resolution + capabilities + the parallel phase type:

- Depends on the leaf library `twinkle-hq/twinkle-test-valid-lib` (`v0.1.0`),
  so the resolved catalog served to a `qa` worker must contain BOTH this
  library's `qa-capability` plugin AND the leaf's transitive `test-plugin`.
- `plugins/qa-capability/plugin.yaml` — a passive capability plugin. It declares
  `session.capabilities: [qa-parallel-review]`, which the session compiler folds
  into SKILL.md so the harness can assert the capability surfaced.
- `tasks/qa-parallel-review.yaml` — a `type: parallel` task. Fan-out review the
  harness uses to assert the parallel phase compiles and dispatches.

## Manifest (`flows.toml`)

Schema per `packages/flows-core/src/manifest-schema.js`:

- `[package].version` is a tagged version (`MAJOR.MINOR.PATCH`, **no** leading `v`).
- `[exports]` entries are `pattern -> bool` maps (not bare strings); patterns are
  lowercase alphanumerics + hyphens + a single `*`.
- `[dependencies]` values are version literals (`vMAJOR.MINOR.PATCH`, **with** the
  leading `v`).

Validate locally with flows-core:

```bash
node --input-type=module -e '
import { readFileSync } from "node:fs";
import { parseManifest, validateManifest } from "./packages/flows-core/src/manifest.js";
validateManifest(parseManifest(readFileSync("tests/fixtures/lib-core/flows.toml","utf8")));
console.log("VALID");
'
```
