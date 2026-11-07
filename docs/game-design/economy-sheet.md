# Economy Sheet — Tabel Sewa, Formula & Log Balance

> **Status:** DRAFT v1 — **semua angka `[asumsi — perlu playtest]`**
> Sumber rumus: proporsi Monopoli klasik ×1 juta (lihat GDD §3.4 & Research Notes). Halaman ini tempat angka berganti tiap iterasi playtest — **GDD §3 cukup merujuk ke sini**.

---

## 1. Formula Utama

| Besaran | Rumus |
| :--- | :--- |
| **Sewa dasar** (tanah kosong) | ≈ 5–8% harga beli tanah |
| **Sewa n rumah** (1–4) | Klasik-proporsional (tabel §2) — pola ~×10, ×30, ×90, ×160 dari dasar |
| **Sewa hotel** | ≈ 4–5× rumah keempat |
| **Komplek utuh** | Menggandakan semua tarif sewa warna itu (×2, klasik) |
| **Stasiun** | 25 / 50 / 100 / 200 per jumlah stasiun dimiliki |
| **Utilitas** | 4× dadu (1 utilitas) atau 10× dadu (keduanya) |
| **Harga rumah & hotel** *(skala Kompleks A–H)* | **A (Cokelat)=50 · B (Biru Muda)=75 · C (Merah Muda)=100 · D (Oranye)=125 · E (Merah)=150 · F (Kuning)=175 · G (Hijau)=200 · H (Biru Tua)=225** per rumah; upgrade ke **Hotel = 4 rumah + 1× harga rumah kompleks** (total investasi 5× harga rumah kompleks) |
| **Jual Darurat ke Bank** *(Emergency Liquidation)* | **50% dari harga beli asli** (baik jual rumah maupun lepas tanah kosong balik ke Bank saat kas kurang bayar sewa/denda) |
| **Hostile Takeover** (Mode Lama) | `[Harga Tanah + (n Rumah × Harga Rumah Kompleks)] × 2` — 100% tunai ke pemilik lama. Saat Krisis Properti aktif: valuasi ×0.5 dulu. **Landmark kebal total.** |
| **Landmark** *(Mode Lama · v0.6 `[asumsi — belum disimulasikan]`)* | Biaya = **7,5× harga rumah komplek** (= 1,5× total investasi hotel; dibulatkan ke atas kelipatan 5) · Sewa = **sewa hotel × 1,25** (dibulatkan ke atas kelipatan 5) · maks 1 per komplek, 2 per pemain · Jual Darurat: turun ke Hotel, dapat 50% biaya Landmark · tabel di §2c |
| **Obligasi Kawasan** *(Mode Lama · v0.6 `[asumsi]`)* | Harga = **25% × valuasi** petak (valuasi = `Harga Tanah + n Rumah × Harga Rumah`, hotel/Landmark dihitung 4 rumah; Krisis E01 ×0.5), dibayar ke Bank · Bagi hasil = **20% dari tiap sewa** di petak itu (pemilik 80%) · maks 3 obligasi aktif/pemain, 1 per petak · Tebus oleh pemilik = **1,5× harga obligasi** ke pemegang |
| **Denda AMDAL** *(berita E09, Mode Lama · v0.6 `[asumsi]`)* | **20% × valuasi komplek** ke Bank untuk membatalkan penyegelan (sewa 0 selama 2 putaran jika tidak dibayar) |
| **Net Worth** *(penentu pemenang)* | `Kas + Σ Harga Tanah + Σ (rumah × harga rumah komplek; hotel = 5×) + biaya Landmark` — Obligasi dihitung **harga beli** sebagai aset pemegang |
| **Gaji Start** | **Rp 400 jt** (saat berita Inflasi Liar E08 aktif: ×2 → **Rp 800 jt**) |
| **Denda & Pajak Papan** | **Pajak Penghasilan (#4) = Rp 200 jt** · **Pajak Mewah (#37) = Rp 100 jt** · **Denda Bebas Penjara (#10) = Rp 50 jt** (maks tahanan 2 giliran lalu bebas otomatis) |
| **Modal awal** *(keputusan 2026-10-24, OQ#5)* | Mode Cepat **Rp 7.500 jt** + 2 petak properti acak · Mode Lama **Rp 2.000 jt** papan kosong |
| **Limit waktu** *(keputusan 2026-10-24)* | Mode Cepat **15 menit seragam** (semua jumlah pemain) · Mode Lama **45 menit** |
| **Kontrol Dadu Lingkaran** *(Precision Gauge)* | **3 Zona Bidik:** Kecil (2–5, busur 0°–120°) · Sedang (6–8, busur 120°–240°) · Besar (9–12, busur 240°–360°). Akurasi timing 75%–80%, dispersi meleset 20%–25% (±1 angka) |
| **End condition** *(keputusan 2026-10-24)* | Cepat: timer → **pemenang = Net Worth tertinggi** (3 hotel = milestone; LMS shortcut). Lama: **Net Worth ≥ 8.000** ATAU LMS ATAU timer 45 mnt. Tie: NW → kas → adu dadu |
| **Target Net Worth Lama** *(terkalibrasi sim)* | **Rp 8.000 jt** — median NW pemenang menit 45 = 5.126 · 8.000 ≈ p80 · crossing median menit 35 |

## 2. Tabel Harga Tanah, Harga Rumah & Sewa per Komplek (skala juta — sinkron [`board-sheet.md`](./board-sheet.md))

| Kode | Komplek | Harga Tanah | Harga 1 Rmh / Hotel (5×) | Jual Balik Bank (50%) | Sewa Dasar | 1 rmh | 2 rmh | 3 rmh | 4 rmh | Hotel |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A** | Cokelat | 60 / 60 | **50** / 250 | Tanah 30 · Rmh 25 | 2 / 4 | 10 / 10 | 30 / 30 | 90 / 90 | 160 / 160 | 250 / 250 |
| **B** | Biru Muda | 100 / 100 / 120 | **75** / 375 | Tanah 50–60 · Rmh 37 | 6 / 6 / 8 | 30 / 30 / 40 | 90 / 90 / 100 | 270 / 270 / 300 | 400 / 400 / 400 | 550 / 550 / 550 |
| **C** | Merah Muda | 140 / 140 / 160 | **100** / 500 | Tanah 70–80 · Rmh 50 | 10 / 10 / 12 | 50 / 50 / 60 | 150 / 150 / 180 | 450 / 450 / 500 | 625 / 625 / 625 | 750 / 750 / 750 |
| **D** | Oranye | 180 / 180 / 200 | **125** / 625 | Tanah 90–100 · Rmh 62 | 14 / 14 / 16 | 70 / 70 / 80 | 200 / 200 / 220 | 550 / 550 / 600 | 750 / 750 / 750 | 950 / 950 / 950 |
| **E** | Merah | 220 / 220 / 240 | **150** / 750 | Tanah 110–120 · Rmh 75 | 18 / 18 / 20 | 90 / 90 / 100 | 250 / 250 / 270 | 700 / 700 / 750 | 875 / 875 / 875 | 1050 / 1050 / 1050 |
| **F** | Kuning | 260 / 260 / 280 | **175** / 875 | Tanah 130–140 · Rmh 87 | 22 / 22 / 24 | 110 / 110 / 120 | 330 / 330 / 360 | 800 / 800 / 850 | 975 / 975 / 975 | 1150 / 1150 / 1150 |
| **G** | Hijau | 300 / 300 / 320 | **200** / 1.000 | Tanah 150–160 · Rmh 100 | 26 / 26 / 28 | 130 / 130 / 140 | 390 / 390 / 420 | 900 / 900 / 950 | 1100 / 1100 / 1100 | 1300 / 1300 / 1300 |
| **H** | Biru Tua | 350 / 400 | **225** / 1.125 | Tanah 175–200 · Rmh 112 | 35 / 50 | 175 / 200 | 500 / 600 | 1100 / 1400 | 1300 / 1500 | 1500 / 2000 |
| — | **Stasiun (4 petak)** | **200** / stasiun | — | Tanah 100 | 25 (1 st) · 50 (2 st) · 100 (3 st) · 200 (4 st) | — | — | — | — | — |
| — | **Utilitas PLN/PDAM (2)** | **150** / utilitas | — | Tanah 75 | 4× angka dadu ( punya 1) · 10× angka dadu (punya 2) | — | — | — | — | — |

## 2b. Daftar Lengkap Denda & Punish (Papan, Penjara, Berita & Kartu)

| Kategori Punish / Denda | Nama Petak / Kartu | Nominal Mode Lama | Nominal Mode Cepat | Keterangan Efek |
| :--- | :--- | :--- | :--- | :--- |
| **Pajak Papan** | Petak #4 Pajak Penghasilan | **Rp 200 jt** | **Rp 200 jt** | Bayar langsung ke Bank saat mendarat |
| **Pajak Papan** | Petak #37 Pajak Mewah | **Rp 100 jt** | **Rp 100 jt** | Bayar langsung ke Bank saat mendarat |
| **Penjara** | Petak #29 Ditangkap Polisi / Kartu H14 / 3× Dadu Kembar | **Rp 50 jt** (tebusan) | **Rp 50 jt** (tebusan) | Masuk tanpa gaji Start; bebas jika dadu kembar / bayar 50 jt / pakai C18 / otomatis bebas setelah 2 giliran |
| **Berita Ekonomi** | `E03` Pajak Likuiditas | **30% Kas Tunai** | **30% Kas Tunai** | Menyasar 1 pemain dengan kas tunai terbanyak saat itu |
| **Berita Ekonomi** | `E08` Inflasi Liar | **Sewa +50%** | **Sewa +50%** | Berlaku 2 putaran (gaji Start ikut naik ×2 jadi Rp 800 jt) |
| **Berita Ekonomi** | `E02` Booming Kawasan | **Sewa ×2 (200%)** | **Sewa ×2 (200%)** | Tarif sewa seluruh papan lipat dua selama 2 putaran |
| **Berita Ekonomi** | `E09` Skandal AMDAL | **Sewa komplek termahal = 0 (2 putaran)** atau **denda 20% valuasi** | *(Tidak aktif)* | Menyasar 1 komplek dengan valuasi tertinggi; Landmark tidak kebal; denda dibayar ke Bank oleh pemilik |
| **Obligasi** | Tebus Obligasi Kawasan | **1,5× harga obligasi** | *(Tidak aktif)* | Dibayar pemilik petak ke pemegang obligasi untuk membatalkan bagi hasil 20% |
| **Kartu Umum** | `C02` Pajak Tahunan | **Rp 200 jt** | **Rp 1.000 jt** (×5) | Bayar ke Bank |
| **Kartu Umum** | `C06` Opname Rumah Sakit | **Rp 150 jt** | **Rp 750 jt** (×5) | Bayar ke Bank |
| **Kartu Umum** | `C04` Cicilan Gadget & `C08` Servis Motor | **Rp 100 jt** | **Rp 500 jt** (×5) | Bayar ke Bank |
| **Kartu Umum** | `C16` Renovasi Pagar Ambruk | **Rp 80 jt** | **Rp 400 jt** (×5) | Bayar ke Bank |
| **Kartu Umum** | `C10` Iuran RT & `C14` Tilang Parkir | **Rp 50 jt** | **Rp 250 jt** (×5) | Bayar ke Bank |
| **Kartu Umum** | `C12` Amplop Kondangan Nikahan | **Rp 50 jt / lawan** | **Rp 250 jt / lawan** (×5) | Bayar ke **setiap** pemain lawan yang masih aktif |
| **Kartu Kesempatan** | `H07` Inspeksi Tata Kota (Perbaikan) | **Rp 25 jt / rumah** (Rp 75 jt / hotel) | **Rp 25 jt / rumah** (Rp 75 jt / hotel) | Pajak progresif kepemilikan bangunan (tetap skala papan) |
| **Kartu Kesempatan** | `H18` Tagihan Pajak PBB | **Rp 40 jt / petak** | **Rp 40 jt / petak** | Pajak progresif per sertifikat tanah yang dimiliki |
| **Kartu Kesempatan** | `H05` Dilema Warga | **Rp 150 jt** (atau mundur 4 petak) | **Rp 750 jt** (atau mundur 4 petak) | Pilihan bayar denda atau mundur 4 langkah |
| **Kartu Kesempatan** | `H04` Hama Gudang & `H20` Kalah Taruhan Dadu | **Rp 100 jt** | **Rp 500 jt** (×5) | Bayar ke Bank (`H20` jika dadu ganjil) |
| **Kartu Kesempatan** | `H06` Bancakan Tetangga | **Rp 50 jt** | **Rp 250 jt** (×5) | Bayar ke Bank |
| **Kartu Kesempatan** | `H16` Busi Klelep Banjir (Mogok) | **Skip 1 Giliran** | **Skip 1 Giliran** | Hukuman waktu: kehilangan 1 giliran jalan berikutnya |

> Catatan: harga petak mengikuti `board-sheet.md`; tarif di atas proporsional klasik. **~~Mode Cepat perlu faktor pengali uniform~~** — **DITUTUP 2026-10-24:** modal 7.500 + kuota tangga sudah meng-cover pacing; tabel sewa seragam kedua mode (verifikasi sim: blowout Cepat ~1%, Gini 0,14).

## 2c. Tabel Landmark per Komplek (Mode Lama · v0.6 `[asumsi — belum disimulasikan]`)

Biaya = 7,5× harga rumah komplek · Sewa Landmark = sewa hotel × 1,25 (angka dasar, **belum** termasuk ×2 komplek utuh) · pembulatan ke atas kelipatan 5 · Jual Darurat = 50% biaya Landmark (dibulatkan ke bawah).

| Kode | Komplek | Harga 1 Rmh | **Biaya Landmark** | Sewa Hotel | **Sewa Landmark** | Jual Darurat Landmark |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A** | Cokelat | 50 | **375** | 250 | **315** | 187 |
| **B** | Biru Muda | 75 | **565** | 550 | **690** | 282 |
| **C** | Merah Muda | 100 | **750** | 750 | **940** | 375 |
| **D** | Oranye | 125 | **940** | 950 | **1.190** | 470 |
| **E** | Merah | 150 | **1.125** | 1.050 | **1.315** | 562 |
| **F** | Kuning | 175 | **1.315** | 1.150 | **1.440** | 657 |
| **G** | Hijau | 200 | **1.500** | 1.300 | **1.625** | 750 |
| **H** | Biru Tua | 225 | **1.690** | 1.500 / 2.000 | **1.875 / 2.500** | 845 |

> Catatan skala: modal awal Mode Lama hanya Rp 2.000 jt dan target Net Worth 8.000 jt, jadi Landmark komplek mahal (G/H) praktis baru terjangkau di paruh akhir game — memang disengaja sebagai *endgame anchor*.

## 3. Anti-Snowball Valve (dipantau saat playtest)

| Valve | Mekanisme | Yang diukur |
| :--- | :--- | :--- |
| Pajak Likuiditas (E03) | 30% kas pemain terkaya | Berapa % sesi berakhir dekat (bukan blowout)? |
| Krisis Properti (E01) | Valuasi −50% → caplop murah | Apakah comeback benar-benar terjadi saat krisis? |
| Moratorium (E07) | Larangan bangun 2 putaran | Apakah leader tertahan atau tetap melesat? |
| Biaya takeover 2× | Penguras kas terbesar | Apakah pemain menahan kas untuk menangkal? |
| Broken Set | Tarif warna turun | Seberapa sering korban bisa pulih? |
| Skandal AMDAL (E09, Lama) | Komplek termahal disegel 2 putaran (sewa 0) kecuali bayar denda 20% valuasi | Apakah leader (termasuk pemilik Landmark) benar-benar tertahan, atau selalu memilih bayar denda? |
| Obligasi Kawasan (Lama) | Pemain berkantong tipis dapat 20% sewa komplek yang ramai | Apakah ROI obligasi masuk akal (tidak dominan, tidak dihindari)? Seberapa sering ditebus 1,5×? |
| Landmark (Lama) | Kebal caplok, tapi mahal & maks 2/pemain | Apakah Landmark menurunkan blowout (aman dari jarahan) atau menaikkannya (leader makin tak tersentuh)? |

## 4. Log Playtest (diisi tiap iterasi)

| Tgl | Sesi (mode, pemain) | Durasi rata² | Pemenang diprediksi menit ke- | Catatan balance | Perubahan angka |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2026-10-24 | Simulasi Fase 1 (kedua mode, 4p, 300 run/bucket × 4 arketipe + kalibrasi 400 run) | Cepat 15 mnt (penuh clock) · Lama 42 mnt | Cepat: ditimbang menit 15 (median NW pemenang 11.320) · Lama: target 8.000 terpicu ~17% game, median crossing menit 35 | **8/8 bucket 🟢 FAIR.** Cepat: mid 46–49% · lock 64–71% · blowout ~1% · Gini 0,14 · arketipe imbang 37/32/31. Lama: mid 54–59% · blowout 21–27% (valve Fase 2 belum masuk — baseline) · LMS 6% | Ending kedua mode diganti timer+Net Worth; modal Cepat 7.500 / Lama 2.000; **target Lama 50.000 → 8.000** (50 Miliar mustahil: suplai uang ≈39.000) |
| 2026-11-07 | Simulasi Fase 2 (berita/kartu/takeover/penjara/lelang AKTIF; kedua mode, 4p, 300 run/bucket × 4 arketipe + kalibrasi 400 run + diagnosis blowout 200×4 batch) | Cepat 15 mnt (penuh clock) · Lama 40–44 mnt | Cepat: ditimbang menit 15 · Lama: target 8.000 terpicu ~44% game (median crossing menit 35) | **Cepat 4/4 bucket 🟢 FAIR** (mid 43–49% · lock 79% · blowout 7–10% · Gini 0,20–0,22 · seat spread 3,4%). **Lama: random 🔴 blowout 57% · MAKELAR/PENIMBUN 🟡** — biang = **caplop** (matikan takeover → blowout 50,5%→28,5%; news −3pp, kartu −1,5pp); AGRESIF menang 60% di bucket campur (dulu 30%) · target 8.000 **tetap rekomendasi** | **OQ#8 ditutup: urutan giliran diacak/sesi**; Fase 2 rules masuk sim (23/23 test); temuan baru OQ#10 (edge posisi pertama Cepat 34% vs 17%) |
| 2026-11-07 | **Desain tambahan v0.6 — TIDAK disimulasikan** (playtest-sim sudah dihapus) | — | — | Menambah Landmark, Obligasi Kawasan, berita E09, Perfect Bullseye. **Dampak ke blowout Mode Lama (terakhir terukur 🔴 57%) belum diketahui** — wajib diukur ulang (playtest manusia atau sim baru) sebelum angka dikunci | Landmark 7,5× / sewa ×1,25 · Obligasi 25% / bagi hasil 20% / tebus 1,5× · denda AMDAL 20% · penanda Bullseye 12° — semua `[asumsi]` |

> Metode uji (Aturan 130/131): jalankan **tanpa berita RNG dulu** supaya tren strategi dominan terbaca, lalu nyalakan berita lapis demi lapis. Catat distribusi N run: berapa % sesi berakhir dengan pemenang vs dipaksa berhenti.
