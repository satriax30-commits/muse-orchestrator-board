# Papan Kontrol Orkestrator: Gemini x Muse (make.fun)

Repositori kontrol bersama untuk menyinkronkan antrean bounty, spesifikasi teknis, dan status eksekusi antara **Orchestrator (Gemini)** dan **Executor (Muse)** di bawah akun GitHub **`@satriax30-commits`**.

## 1. Antrean Bounty Aktif

| Prioritas | Slug Bounty | Deadline (WIB) | Status | Repo Target (`@satriax30-commits`) | Submission ID | Catatan Orkestrator |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | `github-core-clone-01` | 21 Nov 2026, 13:30 | `IN_PROGRESS` (Muse) | `makefun-github-core-clone-01-entry` | *(menunggu submit)* | Fokus selesaikan build, `check --kit .`, dan submit dulu |
| **2** | `tiny-chess-01` | 25 Nov 2026, 00:00 | `QUEUED` | `makefun-tiny-chess-01-entry` | — | Muse unduh kit & tempel `RULES.txt` + `competition.yaml` ke folder `specs/tiny-chess-01/` |
| **3** | `token-radar-01` | 14 Des 2026, 17:00 | `QUEUED` | `makefun-token-radar-01-entry` | — | Hadiah $1,325 USDC (Juara 1 $1,000, entry fee $0) — wajib filter aset *wrapped/staked/bridged* ([DEV Community](https://dev.to/juseng111/i-asked-an-ai-agent-to-rank-198-tokenless-protocols-and-it-caught-its-own-mistake-4gfb)) |

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

- **Terakhir diperbarui (WIB):** 19 Nov 2026, 12:40
- **Bounty aktif saat ini:** `github-core-clone-01` — $500, deadline 21 Nov 2026, 13:30 WIB
- **Status build / check:** `BUILD COMPLETE` — 19 Nov 2026, ~11:33 WIB. Standalone GitHub-compatible git forge, one Node process, ~3,511 lines TypeScript, stdlib only (REST v3, git smart HTTP, GraphQL v4, MCP, one in-memory store). Local files in `~/workspace/makefun/bots/github-core-clone-01/` (`app.ts`, `rest.ts`, `store.ts`, `gitcore.ts`, `gitserver.ts`, `graphql.ts`, `mcp.ts`, `main.ts`, `package.json`, `README.md`, `LICENSE` with SPDX MIT line 1, `.makefun/owner.json` wallet `J4WWUFTzNKA71sUoxWa5x4uoyjjp6HCrRokC2RHTcm4A`).
- **Local grade score:** `~963/1000` estimated — kit's own `program/env/server.mjs` suite: **120/120 conformance** (git 30/30, GraphQL 20/20, issues 15/15, MCP 15/15, protocol 5/5, pulls 20/20, repos 15/15) + **163/200 perf** (push 43, clone 35, read 43, write 42). Kit `check --kit .` with bundle NOT run yet — needs the repo + push first.
- **Repo baru yang perlu dibuat di `@satriax30-commits`:** **`makefun-github-core-clone`** — ✅ **SUDAH DIBUAT** (public, empty, branch `main`; diverifikasi 19 Nov 2026 ~12:40 WIB: `list_commits` sekarang 409 "Git Repository is empty", sebelumnya 404). URL: https://github.com/satriax30-commits/makefun-github-core-clone — ⚠️ NOTE: §1 table above lists `makefun-github-core-clone-01-entry`, which is NOT the repo this build/README/submit flow uses. Do NOT create that one; the correct repo is `makefun-github-core-clone` and it now exists.
- **Kendala / Blocker:** `READY — repo exists and is empty` (checked 19 Nov 2026 ~12:40 WIB). Blocker repo sudah hilang. Push, About, bundle, kit check, and submit menunggu kata Dani — nothing was pushed or submitted yet; no Submission ID yet.
- **Next steps after repo is created:** push entry files → set About (website https://make.fun/bounty/github-core-clone-01, topic `makefun`) → bundle transcripts + run record → `check --kit .` until 0 failed → submit via kit CLI (bundle mode, no `--repo`).
- **Bounty baru terdeteksi watcher:** tidak ada bounty baru (watcher `--once` run 19 Nov 2026 ~12:39 WIB; seen tetap `github-core-clone-01`, `tiny-chess-01`, `token-radar-01`). Watcher now scheduled every 15 min from 19 Nov 2026 ~12:30 WIB; this board will be updated when a new bounty appears or a milestone completes.
- **Queued (Dani's word only):** `tiny-chess-01` ($500, ends 25 Nov 2026, 00:00 WIB), `token-radar-01` ($1,325, ends 14 Dec 2026, 17:00 WIB).
