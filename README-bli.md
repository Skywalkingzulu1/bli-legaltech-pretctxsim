# PreTxSim — BLI Legal Tech Hackathon 2 Submission

## Pitch

PreTxSim is a local, air-gapped EVM simulation proxy that acts as a **pre-execution compliance gate**: every smart-contract call is simulated and checked against policy *before* signing, so non-compliant transactions never reach the network.

## Track Alignment: RegTech & Compliance

- **Policy-as-rules pre-check**: `RiskInspector` flags delegatecalls, selfdestructs, unlimited allowance grants, storage writes, and EIP-7702 delegations — the exact patterns compliance policies care about.
- **Audit trail by default**: every simulation emits a structured JSON report (`--ci` mode) suitable for compliance records.
- **Local-first**: keys, intents, and reports never leave the machine — no third-party data exposure.
- **CI-enforceable**: `--ci` exits non-zero on BLOCK findings, so compliance becomes a pipeline gate, not a checklist.

## Quick Start

```bash
docker compose up -d
```

See [demo_runbook.md](demo_runbook.md) for evaluator instructions.

## Key Features

- Air-gapped `revm` simulation — no keys broadcast until accepted
- RiskInspector: delegatecalls, selfdestructs, storage writes, allowances, EIP-7702
- Local LLM advisory (Ollama `smollm2`), zero telemetry
- Drop-in RPC proxy on `http://127.0.0.1:8545`
- `--ci` mode: structured JSON + exit codes for automated policy enforcement

## Demo

- [docs/assets/demo.mp4](docs/assets/demo.mp4)
- Payloads: [examples/demo_txs.json](examples/demo_txs.json)
