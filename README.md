# tenhkspark

Self-hosted AI infrastructure, written down while it runs: a four-node DGX Spark cluster serving
one 1M-token model, the fan curve that keeps it quiet, the watchdogs that keep it alive, and the
controls that keep an agent from doing something expensive.

Everything here is measured on the machines, not copied from a datasheet. Where a number is a
guess or a single run, the page says so.

## The stack, in the order I would rebuild it

1. **[dgx-spark-tuning](https://github.com/tenhkspark/dgx-spark-tuning)** — the cluster itself:
   clock floor, serving recipe, patching while the kernel and driver stay frozen, watchdogs.
   Start here; it is the operating picture.
2. **[dgx-spark-fan-tuning](https://github.com/tenhkspark/dgx-spark-fan-tuning)** — the fan curve
   and the one-patch controller change. Separate repository because it patches a GPL-2.0 driver.
3. **[cluster-recipe](https://github.com/tenhkspark/cluster-recipe)** — *retired 2026-10-28*,
   superseded by the Spark work above. Kept for the measurements.
4. **[agent-blast-radius](https://github.com/tenhkspark/agent-blast-radius)** — what to do when you
   run an agent on top: egress allow-list, tool-call audit, ingest quarantine, weights ledger, and
   an honest list of what each one does not cover.
5. **[secbrief](https://github.com/tenhkspark/secbrief)** — a daily vulnerability briefing for
   machines that agents manage.

## Serving notes (the model side)

- **[spark-ds41f](https://github.com/tenhkspark/spark-ds41f)** — a fork of the upstream serving
  project, kept for my branches and upstream PRs. Production runs `spark-ds41f-1030`.
- **[gemma4-spark](https://github.com/tenhkspark/gemma4-spark)** — Gemma 4 26B on a single Spark,
  NVFP4, serving notes.
- **[glm53-flash-nvfp4-2node](https://github.com/tenhkspark/glm53-flash-nvfp4-2node)** — two-node
  GLM serving.
- **[glm53-flash-nvfp4-dgx-spark](https://github.com/tenhkspark/glm53-flash-nvfp4-dgx-spark)** —
  *archived*: earlier stage of the same work.

## Around the cluster

- **[elementx-local-recipe](https://github.com/tenhkspark/elementx-local-recipe)** — self-hosted
  Matrix chat (Element X + Tuwunel + Tailscale), no cloud in the message path.
- **[dsh-phone-ui](https://github.com/tenhkspark/dsh-phone-ui)** — a phone-only layer for a
  browser-based agent UI: bigger tap targets, slide-over sidebar.
- **[voice-recipe](https://github.com/tenhkspark/voice-recipe)** — a voice layer for coding agents
  on a Mac.
- **[dgx-spark-fan-control](https://github.com/tenhkspark/dgx-spark-fan-control)** — a fork of the
  upstream fan controller, kept for a performance PR.

## Reading the repos

- Repositories that say *retired* or *archived* are kept for their measurements, not maintained.
- Repositories that carry a fork badge are forks: the value is in the branches and PRs, not in the
  default branch.
- Licenses differ on purpose: MIT for the recipes, GPL-2.0 where a GPL driver is patched,
  Apache-2.0 where the upstream work is Apache.
