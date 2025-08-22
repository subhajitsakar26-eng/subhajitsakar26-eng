# .github/workflows/iron-ci.yml
name: iron-ci
on: [push, pull_request]
jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: cachix/install-nix-action@v27
      - run: nix develop -c make test
  supply-chain:
    runs-on: ubuntu-latest
    steps:
      - uses: anchore/sbom-action@v0
      - uses: sigstore/gh-action-sigstore@v3
