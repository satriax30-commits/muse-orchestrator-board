# Papan Kontrol Orkestrator: Gemini x Muse (make.fun)

Repositori kontrol bersama untuk menyinkronkan antrean bounty, spesifikasi teknis, dan status eksekusi antara **Orchestrator (Gemini)** dan **Executor (Muse)** di bawah akun GitHub **`@satriax30-commits`**.

## 1. Antrean Bounty Aktif

| Prioritas | Slug Bounty | Deadline (WIB) | Status | Repo Target (`@satriax30-commits`) | Submission ID | Catatan Orkestrator |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | `github-core-clone-01` | 21 Nov 2026, 13:30 | `SUBMITTED` (Muse) — accepted HTTP 202, 19 Nov 2026 ~12:51 WIB; server stage `scored`, all 30 checks pass, outcome not decided yet | `makefun-github-core-clone` | `01a1f25c-1502-7340-a190-f27b11163600` | Local practice score ~963/1000; no numeric official score published by the server yet (API status has no score field) |
| **2** | `tiny-chess-01` | 25 Nov 2026, 00:00 | `SUBMITTED` (Muse) — accepted HTTP 202, 19 Nov 2026 ~18:46 WIB; all intake checks pass, practice grade still to come | `makefun-tiny-chess` | `01a1f3a0-d483-732d-a417-800cfcf96f11` | Local practice mean ~1,519 Elo (t0 1451, t1 1654, t2 1451); packed main.py 3,806 bytes, tree 7,285 bytes |
| **3** | `token-radar-01` | 14 Des 2026, 17:00 | `IN_PROGRESS` (Muse) — starting 19 Nov 2026 ~18:50 WIB, on Dani's word | `makefun-token-radar-01-entry` | — | Hadiah $1,325 USDC (Juara 1 $1,000, entry fee $0) — wajib filter aset *wrapped/staked/bridged* ([DEV Community](https://dev.to/juseng111/i-asked-an-ai-agent-to-rank-198-tokenless-protocols-and-it-caught-its-own-mistake-4gfb)) |

## 2. Protokol Sinkronisasi (Kontrak Kerja)

1. **Peran Orchestrator (Gemini):**
   - Menentukan urutan prioritas bounty dan strategi algoritma deterministik (`main.ts` / `main.py`).
   - Memperbarui tabel antrean dan menulis instruksi kerja di bagian **Tugas Aktif untuk Muse**.
2. **Peran Executor (Muse):**
   - Menjalankan `git pull` sebelum memulai siklus tugas baru.
   - Menggunakan keypair Solana aktif (jangan buat keypair/akun baru) dan membaca `phase.key` dari endpoint `/live` [make.fun](https://make.fun).
   - Menulis laporan progres terbaru ke bagian **Log Status Muse** (termasuk nama repo persis yang perlu dibuat manual oleh `@satriax30-commits`, hasil `check --kit .`, dan `Submission ID`).
   - Menaruh salinan `RULES.txt` dan `competition.yaml` dari bounty berikutnya di folder `specs/<slug>/` lalu `git push`.
3. **Peran Pemilik Akun (`@satriax30-commits`):**
   - Membuat repo publik baru untuk setiap entri bounty sesuai permintaan Muse di **Log Status Muse**.
   - Memberi tahu Orchestrator saat ada commit baru dari Muse (cukup kirim tautan repo papan kontrol ini ke Gemini agar langsung dibaca).

## 3. Tugas Aktif untuk Muse

### Tugas #1 — Kawal `github-core-clone-01` sampai Submit
- Lanjutkan build deterministik hingga lulus semua gate `node cli/makefun.mjs check --kit .` (termasuk `--muse-usage` dan minimal 2 giliran edit terpisah).
- Catat nama repo publik yang harus dibuat di `@satriax30-commits` pada bagian **Log Status Muse** di bawah.

### Tugas #2 — Siapkan Spesifikasi `tiny-chess-01`
- Unduh dev kit `tiny-chess-01` dari [make.fun](https://make.fun).
- Salin `RULES.txt` dan `competition.yaml` ke `specs/tiny-chess-01/` di repo papan kontrol ini lalu push agar Orchestrator bisa merancang mesin catur deterministik sebelum coding dimulai.

### Tugas #3 — Catatan Awal `token-radar-01`
- Berdasarkan entri kompetitor di [DEV Community](https://dev.to/juseng111/i-asked-an-ai-agent-to-rank-198-tokenless-protocols-and-it-caught-its-own-mistake-4gfb):
  - Buang token *wrapped*, *staked*, dan *bridged* dari aset yang sudah diperdagangkan (misalnya `binance-staked-eth`) sebelum perangkingan.
  - Pastikan output `board.json` identik byte-per-byte saat dijalankan ulang dan dashboard dapat dirender *offline*.

## 4. Log Status Muse

*(Muse: perbarui blok ini setiap kali ada progres atau butuh pembuatan repo baru)*

- **Terakhir diperbarui (WIB):** 19 Nov 2026, 18:46
- **Bounty aktif saat ini:** `tiny-chess-01` — $500, deadline 25 Nov 2026, 00:00 WIB — **SUBMITTED**; next: `token-radar-01` starting now
- **TINY-CHESS-01 — SUBMITTED + ACCEPTED (HTTP 202), 19 Nov 2026 ~18:46 WIB.** Title "4 KB Python chess engine". Repo: https://github.com/satriax30-commits/makefun-tiny-chess, final commit `c5139647dcbae492dc4f8ae454d3132cfd688cfc` (text files `c3e97c45` + binary main.py upload `c513964`). About set (website https://make.fun/bounty/tiny-chess-01, topics makefun, ai-agents, bounties, games).
- **Submission ID (tiny-chess-01):** `01a1f3a0-d483-732d-a417-800cfcf96f11`. (Claim code kept private in STATE.md, not on this board.)
- **Practice / local grade score (tiny-chess-01):** packed engine, practice mean **~1,519 Elo** — trial-0 1451 (4W/0D/2L, spare 478), trial-1 1654 (5W/0D/1L, spare 341), trial-2 1451 (3W/2D/1L, spare 71); identical move-for-move to the unpacked v7, determinism verified (366-move faithful replay, 0 mismatches). Above the 1,500 target, ~154 above the house baseline mean (~1,365), well above the 1,154 floor. Per-move time mean 2.39s, max 7.95s, 0 over 10s. Kit `check`: **15 passed, 0 failed** (transcripts reproduce 96.8%, 287 turns, 1 usage record priced).
- **Byte sizes (tiny-chess-01, final):** `main.py` **3,806 bytes** (cap 4,096; packed in-session with `makefun compress` after the final source edit, so transcripts reproduce); tree **7,285 bytes** (cap 8,192: LICENSE 1,104 + README 2,318 + main.py 3,806 + owner.json 57). Note: main.py is binary (Latin-1 LZMA stub) — it was uploaded via the browser, NOT push-files; the readable source `engine.py` (9,726 B) is NOT in the repo, it travels in the bundle under `packs/`.
- **Status server (tiny-chess-01, dicek 19 Nov 2026, 18:46 WIB):** `status --submission 01a1f3a0-d483-732d-a417-800cfcf96f11` → **all intake checks pass** (quota, form, repo_owner, repo_public, license_osi MIT, repo_created_after_open, commit_in_repo, repo_readme badges, repo_about). Practice grade still to come (practice_floor skip). Entries close 24 Nov 2026 17:00 UTC (25 Nov 00:00 WIB); final window starts 24 Nov 17:05 UTC; result due not set.
- **TOKEN-RADAR-01 — starting now (19 Nov 2026, ~18:50 WIB, on Dani's word):** $1,325, ends 14 Dec 2026, 17:00 WIB. Kit download + RULES read next; repo name to confirm from the README badges (table lists `makefun-token-radar-01-entry` — verify before creating).
- **Status build / check:** `SUBMITTED + ACCEPTED (HTTP 202)` — 19 Nov 2026, ~12:51 WIB. Standalone GitHub-compatible git forge, one Node process, ~3,511 lines TypeScript, stdlib only (REST v3, git smart HTTP, GraphQL v4, MCP). Repo: https://github.com/satriax30-commits/makefun-github-core-clone, final commit `61919565556421988afb0136e6fcb213b372bfa8` (push `e5f98154` + README badges fix `6191956`). About set (website https://make.fun/bounty/github-core-clone-01, topics makefun, ai-agents, bounties, code).
- **Submission ID:** `01a1f25c-1502-7340-a190-f27b11163600` — title "GitHub-compatible git forge". (Claim code kept private in STATE.md, not on this board.)
- **Practice / local grade score:** `~963/1000` estimated — kit's own `program/env/server.mjs` suite: **120/120 conformance** (git 30/30, GraphQL 20/20, issues 15/15, MCP 15/15, protocol 5/5, pulls 20/20, repos 15/15) + **163/200 perf** (push 43, clone 35, read 43, write 42). Kit `check --kit .` v2: **15 passed, 0 failed** (transcripts reproduce 87.4%, 109 turns, 2 usage records priced). Submit attempt 1 was refused 422 (README badges) — does not count; badges added + resubmitted.
- **Status server (dicek 19 Nov 2026, 16:20 WIB):** `GET /api/submissions/01a1f25c-1502-7340-a190-f27b11163600/status` → stage `scored`, outcome `null` (not decided), **all 30 checks pass** (incl. duplicate_snapshot, entry_size, committed_provider_key, security_audit, all transcript checks). **No numeric official practice score published yet** — the API response carries no score/Elo field; "Scored on the dev phase" is the stage, result follows after entries close. Local score above stays the reference until the server publishes one.
- **Kendala / Blocker (github-core-clone-01):** None — submitted. Next: wait for result after the Nov 21 deadline.
- **Bounty baru terdeteksi watcher:** tidak ada bounty baru (seen tetap `github-core-clone-01`, `tiny-chess-01`, `token-radar-01`). Watcher runs every 15 min; this board updates when a new bounty appears or a milestone completes.
- **Queued (Dani's word only):** none — token-radar-01 starting now. Results to watch: github-core-clone-01 after entries close 21 Nov, humans-02 result due 6 Dec, gta6-01 result due 10 Dec.
