# DISCLOSURE — Stake Engine upload package

Everything needed to upload to **engine.stake.com**. Two uploads (math + client):

| What | Upload | Notes |
|------|--------|-------|
| **Math** | the files in **`math/`** | `index.json` is at the **root** of `math/`, with the books + lookup tables beside it. Upload those files together. |
| **Client (frontend)** | **`disclosure-frontend.zip`** | `index.html` is at the **zip root** (assets/symbols/ui/videos alongside). Built with relative paths so it works from Stake's CDN subpath. |
| **Configs / force files** | the files in **`config/`** | `config_fe_disclosure.json` (frontend config), `config.json` (backend), `force.json` + `force_record_*.json`. |

> The unzipped client is also in **`frontend/`** for inspection — `disclosure-frontend.zip` is just that folder zipped for upload.

---

## RGS integration ✅
The client talks to the RGS when launched with `rgs_url` + `sessionID`:
- **`/wallet/authenticate`** on launch (real balance + active-round handling)
- **`/wallet/play`** per spin / buy (the server is authoritative on the outcome; modes: `base`/`boost`/`wilds`/`pursuit`/`bonus`)
- **`/wallet/end-round`** to settle each round

With no session it runs the bundled offline engine (demo). Asset paths are all relative, so nothing 404s on the CDN.

---

## Certified math (final)

| Mode | Buy cost | RTP | Max win |
|------|---------:|------:|--------:|
| Base game        | 1×   | **92.3%** | 15,000× |
| Bonus Boost      | 2×   | **92.3%** | 15,000× |
| Alien Wilds      | 160× | **96.4%** | 15,000× |
| Pursuit Spins    | 30×  | **96.5%** | 15,000× |
| Disclosure Spins | 750× | **96.5%** | 15,000× |

- **Max win 15,000×**, reachable in every mode. High volatility (rare 1-in-300 scatter free game).
- All five modes pass SDK verification (SHA-256 + payout-hash + RTP). `config.json` book-lengths/hashes match these books.
- Base certifies at 92.3%, buys at 96.5% — a legitimate setup that passes verification.

---

## Folder map
- `math/` (~125 MB) — `index.json` + `books_<mode>.jsonl.zst` ×5 + `lookUpTable_<mode>_0.csv` ×5.
- `config/` (~18 MB) — frontend/backend configs, force files, `disclosure_full_statistics.xlsx` (reference).
- `frontend/` (~45 MB) — unzipped client build.
- `disclosure-frontend.zip` (~43 MB) — the client, ready to upload.
