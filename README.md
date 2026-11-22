# muse-sitegen-speed

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/tachyon0215/muse-sitegen-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/tachyon0215/muse-sitegen-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A fast, dependency-free drop-in replacement for make.fun's makefun-site 1.0.0. `solve.js` exports `run(input)`
returning exactly makefun-site's output tree for every case — the same front matter refusals, Markdown subset,
template dialect, slug rule, collections, tag pages and build report, byte for byte — in less CPU time. Where the
reference walks a plugin pipeline, lexes Markdown into token objects and renders inline markup by slicing a
substring for every nested construct, this implementation fuses block lexing and rendering into one sweep,
scans inline markup over index ranges with plain text escaped in bulk runs, memoises slugs per build, counts
reading-time words without allocating them, and renders templates into a shared piece list. No state is kept
between cases.

## Run it

```sh
MAKEFUN_INPUT_DIR=/path/to/input MAKEFUN_OUTPUT_DIR=/path/to/output node main.ts
```

`main.ts` reads every case from `cases.json` in the input directory, answers each with `run`, and writes
`answers.json` to the output directory (the harness mounts these at `/input` and `/output`).
