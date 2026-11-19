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

- **Terakhir diperbarui (WIB):** 19 Nov 2026, 12:51
- **Bounty aktif saat ini:** `github-core-clone-01` — $500, deadline 21 Nov 2026, 13:30 WIB
- **Status build / check:** `SUBMITTED + ACCEPTED (HTTP 202)` — 19 Nov 2026, ~12:51 WIB. Standalone GitHub-compatible git forge, one Node process, ~3,511 lines TypeScript, stdlib only (REST v3, git smart HTTP, GraphQL v4, MCP). Repo: https://github.com/satriax30-commits/makefun-github-core-clone, final commit `61919565556421988afb0136e6fcb213b372bfa8` (push `e5f98154` + README badges fix `6191956`). About set (website https://make.fun/bounty/github-core-clone-01, topics makefun, ai-agents, bounties, code).
- **Submission ID:** `01a1f25c-1502-7340-a190-f27b11163600` — title "GitHub-compatible git forge". (Claim code kept private in STATE.md, not on this board.)
- **Practice / local grade score:** `~963/1000` estimated — kit's own `program/env/server.mjs` suite: **120/120 conformance** (git 30/30, GraphQL 20/20, issues 15/15, MCP 15/15, protocol 5/5, pulls 20/20, repos 15/15) + **163/200 perf** (push 43, clone 35, read 43, write 42). Kit `check --kit .` v2: **15 passed, 0 failed** (transcripts reproduce 87.4%, 109 turns, 2 usage records priced). Submit attempt 1 was refused 422 (README badges) — does not count; badges added + resubmitted.
- **Status check after submit:** ALL intake checks pass (wallet, competition_open, quota, form, repo_owner, repo_public, license_osi, repo_created_after_open, commit_in_repo, repo_readme, repo_about). Round 1 in progress; outcome not decided yet; result due not set. Prizes NOT escrowed, so the entry went unsigned.
- **Kendala / Blocker:** None — submitted. Next: wait for result; check status again after the Nov 21 deadline.
- **Bounty baru terdeteksi watcher:** tidak ada bounty baru (watcher `--once` run 19 Nov 2026 ~12:39 WIB and ~12:31 WIB; seen tetap `github-core-clone-01`, `tiny-chess-01`, `token-radar-01`). Watcher runs every 15 min; this board updates when a new bounty appears or a milestone completes.
- **NEXT — `tiny-chess-01` dimulai 19 Nov 2026 ~12:51 WIB** (Dani's word): $500, ends 25 Nov 2026, 00:00 WIB. Kit download + builder starting now; repo target to confirm from the kit (`makefun-tiny-chess` expected pattern — do NOT use the §1 table's `makefun-tiny-chess-01-entry` name until Muse confirms it in this log).
- **Queued (Dani's word only):** `token-radar-01` ($1,325, ends 14 Dec 2026, 17:00 WIB).
