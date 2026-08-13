# DiffReceipt Action

Deterministically identify new application capabilities introduced by a pull request without installing dependencies or executing repository code.

This repository is the public, runtime-only distribution of the DiffReceipt GitHub Action. Hosted-service source and private operational configuration are not included.

## Usage

```yaml
name: DiffReceipt
on:
  pull_request:
permissions:
  contents: read
  pull-requests: read
jobs:
  capability-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@11d5960a326750d5838078e36cf38b85af677262
        with:
          fetch-depth: 0
      - uses: smeltzfinn-source/diffreceipt-action@v0
```

For security-sensitive repositories, pin DiffReceipt to the full commit SHA corresponding to the accepted immutable release rather than a moving major tag.

## Output

- `conclusion`: `allowed`, `attention-required`, or `error`

The Action writes `diffreceipt-receipt.json` by default, adds a job summary, and fails for `block` or unresolved `require_approval` findings. A nonzero policy verdict is expected enforcement behavior, not an Action runtime crash.

## Trust boundary

DiffReceipt parses supported repository files as untrusted text. It does not install the target repository's dependencies, run package scripts, import application modules, or execute discovered commands.

## License

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE). The hosted DiffReceipt service and private operational source are outside this runtime distribution's license scope.

## Security

Do not open a public issue containing credentials or private source. Report vulnerabilities through the security contact configured at https://diffreceipt.coachdaveswim.com.
