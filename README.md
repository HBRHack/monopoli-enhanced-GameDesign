# 🎲 Monopoli Enhanced Rule — Game System & Design

<p align="center">
  <b>Modern Digital Property-Trading Board Game System Design</b><br>
  <i>Hostile Takeover 2× • Matras 2 Mode • Berita Ekonomi RNG Dinamis • Multiplatform Architecture</i>
</p>

---

## 🌐 Pilih Bahasa / Select Language

<details open>
<summary><b>🇮🇩 Bahasa Indonesia (Klik untuk tutup/buka)</b></summary>

### 📌 Ringkasan Game

**Monopoli Enhanced Rule** adalah pembaruan mekanik modern dari permainan papan perdagangan properti klasik yang dirancang khusus untuk platform digital (Mobile, Roblox, PC Steam). Proyek ini membuang kelemahan klasik seperti *board lock* (papan macet karena pemain menolak barter) dan eliminasi pasif dini yang membosankan.

#### 🌟 6 Fitur Kunci:
1. **Akuisisi Paksa (Hostile Takeover 2x Lipat):** Lawan dapat mencaplok properti komplek secara paksa dengan membayar 2x lipat total valuasi aset tunai. Korban menerima 100% uang kompensasi ini, sehingga tidak ada eliminasi sia-sia dan korban langsung memiliki amunisi kas untuk membalas.
2. **Kontrol Dadu Lingkaran Presisi (Circular Gauge Roll):** Pemain tidak lagi pasrah pada dadu hoki-hokian (*no blind RNG*). Menggunakan meteran lingkaran *Hold & Release* dengan 3 zona bidik: **Kecil (2–5)**, **Sedang (6–8)**, dan **Besar (9–12)** dengan akurasi berbasis refleks 75%–80%.
3. **Matras 2 Mode Pacing:**
   - **Mode Cepat (15 Menit):** Modal awal besar (Rp 7.500 jt + 2 petak acak), tanpa syarat komplek, tangga bangun bertahap (2 rumah $\rightarrow$ 4 rumah $\rightarrow$ hotel), dan penentuan pemenang di menit 15 berbasis *Net Worth*.
   - **Mode Lama (45 Menit):** Modal pas-pasan (Rp 2.000 jt), wajib satu komplek utuh untuk membangun, barter P2P, fitur Caplok 2x aktif, dan target kemenangan *Net Worth Rp 8.000 jt* atau timer 45 menit.
4. **Sistem Berita Ekonomi Dinamis (Global RNG):** Setiap pemain melewati petak Start, selain mengambil gaji Rp 400 jt, 1 berita ekonomi global disiarkan ke seluruh papan (Krisis Properti -50%, Booming Sewa 2x, Pajak Likuiditas Sultan 30%, Moratorium Izin Bangun).
5. **Penyelamat Likuiditas (Jual Darurat ke Bank 50%):** Sebelum dinyatakan bangkrut saat kas kurang membayar sewa, pemain berhak menjual rumah atau melepas tanah kosong ke Bank seharga 50% harga beli.
6. **Lapisan Kompleksitas Mode Lama:** **Landmark** (upgrade pamungkas di atas Hotel, kebal caplok), **Obligasi Kawasan** (ikut dapat 20% sewa komplek lawan tanpa harus mencaploknya), berita **Skandal AMDAL** (komplek termahal disegel — penyeimbang pemain yang memimpin jauh), serta **Perfect Bullseye + Express Pass** pada dadu lingkaran. *Status: desain awal, angka belum disimulasikan.*

---

### 🗺️ Panduan Membaca Dokumen (Reading Roadmap)

Untuk memahami proyek ini secara bertahap, disarankan membaca berkas dokumen di folder `docs/` dengan urutan berikut:

```
[1] Question Framework (MDA) ──▶ [2] Master GDD (10 Seksi) ──▶ [3] Economy Sheet & Board Sheet
                                                                         │
                                                                         ▼
[5] Development Guidelines   ◀─────────────────────────────── [4] Kartu Bilingual (49 Kartu)
```

1. **Langkah 1 — Pahami Visi & Kerangka Rasa Pemain:**  
   📄 [docs/game-design/question-framework.md](docs/game-design/question-framework.md)  
   *Membahas fondasi MDA (Mechanics, Dynamics, Aesthetics), riset pembanding industri (Fortune Street, Let's Get Rich, Business Tour), dan 100% keputusan desain yang terkunci.*

2. **Langkah 2 — Pelajari Dokumen Desain Utama (GDD Master):**  
   📄 [docs/game-design/GDD.md](docs/game-design/GDD.md)  
   *Living Document 10 seksi lengkap dengan diagram interaktif Mermaid (alur giliran, sirkuit uang tertutup, State Machine petak, UX flows) serta §10 Roadmap Modular Masa Depan (Mode Pro Opsional: Saham Distrik, Pinjaman Bank, Spesialisasi Hotel, Upkeep, Dewan Kota, Asuransi).*

3. **Langkah 3 — Cek Formula Matematika & Layout Papan:**  
   📄 [docs/game-design/economy-sheet.md](docs/game-design/economy-sheet.md) — *Tabel harga tanah, tangga rumah A–H (50..225), sewa hotel, dan daftar lengkap denda/punish.*  
   📄 [docs/game-design/board-sheet.md](docs/game-design/board-sheet.md) — *Pemetaan 40 petak dwibahasa (Mode Indonesia vs Mode Internasional).*

4. **Langkah 4 — Baca Konten Narasi & Kartu Permainan:**  
   📄 [docs/game-design/kartu-draft.md](docs/game-design/kartu-draft.md)  
   *49 kartu bilingual lengkap dengan identifier teknis engine: 9 Berita Ekonomi RNG, 20 Dana Umum (Community Chest), dan 20 Kesempatan (Chance).*

5. **Langkah 5 — Aturan Eksekusi untuk Tim Pengembang & Bisnis:**  
   📄 [docs/ATURAN-PENGEMBANGAN.md](docs/ATURAN-PENGEMBANGAN.md)  
   *Panduan arsitektur modular untuk Developer (Unity/Roblox/Qt), kontrol data & telemetri untuk Analyst, dan strategi peluncuran serta viralitas untuk Marketing.*

</details>

---

<details open>
<summary><b>🇬🇧 English (Click to expand/collapse)</b></summary>

### 📌 Game Overview

**Monopoli Enhanced Rule** is a modern game system overhaul of the classic property-trading board game specifically designed for digital gaming ecosystems (Mobile, Roblox, PC Steam). It eliminates traditional tabletop pain points such as stagnant board locks and boring early-game player eliminations.

#### 🌟 6 Key Innovations:
1. **Hostile Takeover (2× Valuation):** Players can forcibly acquire an opponent's developed complex property by paying double its total asset valuation. The defender receives 100% of this compensation in liquid cash, providing them immediate counter-attack capital and preventing premature elimination.
2. **Circular Gauge Precision Dice (Semi-Deterministic Roll):** Eliminates blind dice frustration (*no pure RNG reliance*). Utilizes a circular *Hold & Release* radial gauge with 3 targeted sectors: **Small (2–5)**, **Medium (6–8)**, and **Large (9–12)** with a 75%–80% reflex-based timing accuracy.
3. **Dual-Pacing Game Modes:**
   - **Fast-Elimination Mode (15 Minutes):** High starting cash (8,000 equivalent / 7,500 + 2 random tiles), no color-group requirement to build, tiered lap build limits (2 houses $\rightarrow$ 4 houses $\rightarrow$ hotel), and Net Worth evaluation at minute 15.
   - **Long-Term Strategy Mode (45 Minutes):** Lean starting capital (2,000), full complex set required to construct houses, active P2P trading, Hostile Takeover enabled, and win condition set to *Net Worth 8,000* or 45-minute timeout.
4. **Dynamic Economy RNG (Global News Events):** Passing the GO/Start tile grants 400 salary and automatically broadcasts 1 global macroeconomic event across the board (Property Crisis -50%, Regional Rent Boom 2×, 30% Liquidity Tax on the wealthiest player, Zoning Permit Freezes).
5. **Emergency Bank Liquidation (50% Cash-out):** When cash is insufficient to pay incoming rent, players can sell houses and liquidate unbuilt properties back to the Bank at 50% face value before facing bankruptcy.
6. **Long-Term Mode Depth Layer:** **Landmark** (final upgrade above Hotel, immune to takeover), **District Bonds** (earn 20% of rivals' rent without needing to take over), the **Environmental Scandal** news event (seals the most valuable complex — a catch-up valve against runaway leaders), plus **Perfect Bullseye + Express Pass** on the circular dice gauge. *Status: early design, numbers not yet simulated.*

---

### 🗺️ Documentation Reading Guide

To explore the architecture and game design logically, navigate through the `docs/` directory in this recommended order:

```
[1] Question Framework (MDA) ──▶ [2] Master GDD (10 Sections) ──▶ [3] Economy & Board Sheets
                                                                         │
                                                                         ▼
[5] Development Guidelines   ◀─────────────────────────────── [4] Bilingual Cards (49 Deck)
```

1. **Step 1 — Understand Core Philosophy & Player Aesthetics:**  
   📄 [docs/game-design/question-framework.md](docs/game-design/question-framework.md)  
   *Covers the MDA framework (Mechanics, Dynamics, Aesthetics), competitive industry benchmarks (Fortune Street, Let's Get Rich, Business Tour), and 100% locked design decisions.*

2. **Step 2 — Study the Master Game Design Document (GDD):**  
   📄 [docs/game-design/GDD.md](docs/game-design/GDD.md)  
   *A formal 10-section living document featuring interactive Mermaid diagrams (turn loops, closed-loop financial flows, tile state machines, UX flows) and Section 10: Modular Future Roadmap (Pro Mode Options: District Stock Market, Bank Credit, Hotel Branching, Property Upkeep, City Council, Insurance).*

3. **Step 3 — Inspect Financial Balancing & Board Geometry:**  
   📄 [docs/game-design/economy-sheet.md](docs/game-design/economy-sheet.md) — *Deed prices, tiered house cost ladders A–H (50 to 225), rent scaling, and complete penalty schedules.*  
   📄 [docs/game-design/board-sheet.md](docs/game-design/board-sheet.md) — *40-tile board layout supporting localized Indonesian and International themes.*

4. **Step 4 — Review Card Mechanics & Narrative Flavor:**  
   📄 [docs/game-design/kartu-draft.md](docs/game-design/kartu-draft.md)  
   *Complete 49 bilingual card deck with technical logic identifiers: 9 World News Events, 20 Community Chest cards, and 20 Chance cards.*

5. **Step 5 — Engineering, Analytics & Go-To-Market Standards:**  
   📄 [docs/ATURAN-PENGEMBANGAN.md](docs/ATURAN-PENGEMBANGAN.md)  
   *Modular engine guidelines for Developers (Unity/Roblox/Qt), telemetry telemetry gates for Analysts, and viral clipping / zero pay-to-win strategies for Marketing.*

</details>

---

## 🛠️ Multiplatform Compatibility (Ready for Engine Implementation)

The system is architected to be completely engine-agnostic:
- **Unity (C#)** — Pure transaction command patterns & state machines.
- **Roblox (Lua)** — Fast-paced multiplayer networking with server authority.
- **Qt / Desktop (C++)** — Lightweight tabletop logic and local match simulation.
