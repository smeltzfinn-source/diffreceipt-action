# DiffReceipt GitHub Action

**Capability-change control for pull requests.** DiffReceipt shows what new powers a PR gives an application—outbound hosts, likely-secret names, routes, database operations, dependencies, scheduled jobs, process execution, and GitHub Actions permissions—without installing dependencies or executing analyzed repository code.

[Explore the demo](https://diffreceipt.coachdaveswim.com/demo) · [Five-minute quickstart](https://diffreceipt.coachdaveswim.com/quickstart.md) · [Detector support](https://diffreceipt.coachdaveswim.com/detector-support.md) · [Policy cookbook](https://diffreceipt.coachdaveswim.com/policy-cookbook.md)

## Use

```yaml
name: DiffReceipt
on: pull_request
permissions:
  contents: read
jobs:
  receipt:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@11d5960a326750d5838078e36cf38b85af677262
        with:
          fetch-depth: 0
      - uses: smeltzfinn-source/diffreceipt-action@v0
```

For immutable supply-chain pinning, use a full accepted runtime commit SHA. `v0` moves only after an immutable beta tag passes an unrelated-repository acceptance run.

| Input | Default | Purpose |
|---|---|---|
| `policy` | `.diffreceipt/policy.yml` | Reviewed repository policy path |
| `json-output` | `diffreceipt-receipt.json` | Machine-readable receipt output path |

The `conclusion` output is `allowed`, `attention-required`, or `error`. Approval-required and blocked decisions fail the step by design. Start with informational/warn policy rules while learning normal repository behavior.

## Real synthetic PRs

The public [`diffreceipt-examples`](https://github.com/smeltzfinn-source/diffreceipt-examples/pulls) repository contains credential-free PRs for eight detector categories. Every example is analyzed by this Action and never represents customer source.

## Trust boundary

- Deterministic, non-LLM analysis.
- Never installs target dependencies, imports target modules, or executes target scripts.
- Reads the checked-out base/head as untrusted text.
- Requires only `contents: read`; broad write permissions are unnecessary.
- Does not upload repository source to the hosted service.
- Is capability-diff review, not SAST, CVE scanning, secret-value scanning, malware detection, or runtime monitoring.

See the public [trust model](https://diffreceipt.coachdaveswim.com/trust), [compatibility contract](https://diffreceipt.coachdaveswim.com/compatibility.json), and [security policy](SECURITY.md).

## Support and license

Use [public issues](https://github.com/smeltzfinn-source/diffreceipt-action/issues) for reproducible non-sensitive bugs. Follow [SECURITY.md](SECURITY.md) for vulnerabilities; never post credentials, private source, webhook payloads, private receipt URLs, or production environment contents.

Apache-2.0 covers this public Action runtime. The hosted service and private operational source are outside this repository's license scope.
