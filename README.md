# DISCLOSURE — Stake Engine upload package

Three folders:

- **`math/`** — upload as the **math** (the "bookshelf"). `index.json` is at the **root** of this folder, with the books and lookup tables beside it — that's the layout the Stake dashboard expects. Upload the *contents* of `math/` (or the folder itself), not a parent folder.
- **`config/`** — the config + force files Stake uses alongside the math: frontend config, backend config, and force files (uploaded in their respective sections / used for verification).
- **`frontend/`** — the built PixiJS game client.

> ⚠️ Earlier "err_missing_file index.json" was because `index.json` was nested in a subfolder. It now sits at the root of `math/`.

---

## Certified math (final)

| Mode | Buy cost | RTP | Max win |
|------|---------:|------:|--------:|
| Base game        | 1×   | **92.3%** | 15,000× |
| Bonus Boost      | 2×   | **92.3%** | 15,000× |
| Alien Wilds      | 160× | **96.4%** | 15,000× |
| Pursuit Spins    | 30×  | **96.5%** | 15,000× |
| Disclosure Spins | 750× | **96.5%** | 15,000× |

- **Max win: 15,000× the bet**, reachable in every mode. High volatility (rare 1-in-300 scatter free game).
- All five modes passed SDK verification (SHA-256 + payout-hash + RTP).
- Base certifies at 92.3%, buys at 96.5% — a legitimate setup that passes verification. A true 96.5% base would need a reel-strip redesign (separate effort), not tuning.

---

## `math/` (≈125 MB) — flat
- `index.json` — manifest (modes + costs), **at the root**.
- `books_<mode>.jsonl.zst` ×5 — round events.
- `lookUpTable_<mode>_0.csv` ×5 — optimized weights.

Round counts were slimmed for a smaller upload (base/boost 15k, wilds 8k, pursuit 6k, bonus 5k) — RTP is unchanged.

## `config/` (≈18 MB)
- `config_fe_disclosure.json` — frontend config.
- `config.json` — backend config (book lengths + SHA-256 hashes that match these books).
- `force.json`, `force_record_<mode>.json` ×5 — force files.
- `disclosure_full_statistics.xlsx` — RTP / hit-rate / volatility stat sheet (reference).

## `frontend/` (≈45 MB)
Production build of the disclosure4 client. Buy prices (Disclosure 750× · Alien Wilds 160× · Pursuit 30× · Boost 2×) and the 6-spin signal meter bonus are synced to the math.

---

**Total ≈ 188 MB** (was 513 MB before slimming).
