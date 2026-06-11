# ARIAMiner — Pearl (PRL) GPU Miner

**A GPU miner for Pearl (PRL) — native support for RTX 30 (Ampere), RTX 40 (Ada) and RTX 50 (Blackwell), in a single binary.**

- ✅ One binary for RTX 30 / 40 / 50 — the optimal kernel path is selected at runtime, per card
- ✅ Zero-config: per-architecture tuning is applied automatically
- ✅ Efficiency-first: sustains high GPU clocks at the same power budget
- ✅ Operator-friendly: auto-reconnect, bounded RAM, versioned agent string, optional JSON stats endpoint
- ✅ CUDA runtime bundled — no install required
- ✅ Closed-source binary · transparent **1% announced dev-fee**

---

## Requirements

- **GPU:** NVIDIA **RTX 30 / 40 / 50 series**
- **Driver:** NVIDIA 570 or newer
- **OS:** Linux x86_64 (native Linux recommended — WSL2 is not officially supported)
- CUDA runtime is **bundled** — no CUDA install required.

## Download

Grab the latest archive from [**Releases**](../../releases/latest):
`ariaminer-v0.6.3-linux-x64.tar.gz` (binary + bundled runtime + `SHA256SUMS`).

Verify and extract:

```bash
sha256sum -c SHA256SUMS
tar xzf ariaminer-v0.6.3-linux-x64.tar.gz
cd ariaminer-v0.6.3
```

## Quick start (LuckyPool)

```bash
LD_LIBRARY_PATH=. ./ariaminer \
  --pool pearl-eu2.luckypool.io:3360 \
  --wallet YOUR_PRL_ADDRESS \
  --worker $(hostname)
```

The pool dialect is auto-detected from the pool host — no extra flags needed.

## HiveOS

ARIAMiner ships as a HiveOS **custom miner** (multi-GPU rigs supported — one worker per GPU, aggregated stats).

Flight sheet:

| Field | Value |
|-------|-------|
| Miner | `Custom` |
| Installation URL | `https://github.com/stefancrypto68/ariaminer-pearl/releases/download/v0.6.3/ariaminer-0.6.3-hiveos.tar.gz` |
| Miner name | `ariaminer` (auto-filled from the URL) |
| Wallet and worker template | `%WAL%` (your `prl1...` address) |
| Pool URL | `pearl-eu2.luckypool.io:3360` |

Requires a HiveOS image with NVIDIA driver 570+ (needed for RTX 50; RTX 30/40 work with the same image).

## Options

| Flag | Description |
|------|-------------|
| `--pool <host:port>` | Stratum endpoint |
| `--wallet <addr>` | Your Pearl (PRL) payout address |
| `--worker <name>` | Worker name (default: hostname) |
| `--threads <n>` | GPU feed threads (default: 1 — one is enough to saturate the GPU) |
| `--stats-port <port>` | Expose a JSON stats endpoint on `127.0.0.1:<port>` (HiveOS / monitoring) |
| `--dialect <pearl\|luckypool>` | Wire dialect (default: auto-detected from the pool host) |

## Dev-fee

A transparent **1% dev-fee**: for roughly one 60-second round every ~100 minutes the
miner authorizes to the developer wallet, then returns to yours. It's announced in the
startup log. If you already mine to the developer wallet, the fee is a no-op.

## License

Proprietary freeware. Free to use for mining. Redistribution, modification, and
reverse-engineering are not permitted. See [LICENSE](LICENSE).

## Disclaimer

Provided as-is, without warranty. Mining involves hardware wear and electricity costs;
run it at settings you're comfortable with. Not affiliated with the Pearl project or
any pool operator.
