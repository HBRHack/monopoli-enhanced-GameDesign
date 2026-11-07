# Question Framework: Monopoli Enhanced Rule (Hostile Takeover & Dynamic Economy)

> **Genre:** Digital Board Game / Property Trading Tycoon / Turn-based Strategy  
> **Platform Target:** Multiplatform (Unity C#, Roblox Lua, atau Qt C++ — PC/Mobile/Roblox)  
> **Konteks Game:** Pengembangan aturan Monopoli modern yang memecahkan masalah kebekuan papan klasik (board lock) melalui Fase Tanah Tunggal (kebal akuisisi untuk blocking aman), Syarat Kompleksitas (buka hak bangun rumah), Akuisisi Paksa (*Hostile Takeover* 2x lipat valuasi dengan kompensasi 100% ke pemilik lama), dua pilihan tempo main (*Fast-Elimination* vs *Long-Term Strategy*), dan Sistem Berita Ekonomi Dinamis (RNG krisis/booming/pajak likuiditas).

---

## Memahami Kerangka MDA (Mechanics – Dynamics – Aesthetics)

Sebelum masuk ke daftar pertanyaan, kerangka kerja ini dibangun di atas fondasi **MDA Framework** (Hunicke, LeBlanc, Zubek, 2004) dengan arah alur yang berlawanan antara perancang dan pemain:

```
Arah Perancang:   Aturan Main (Mechanics)  ──▶  Situasi Permainan (Dynamics)  ──▶  Rasa Pemain (Aesthetics)
Arah Pemain:      Rasa Pemain (Aesthetics) ◀──  Situasi Permainan (Dynamics) ◀──  Aturan Main (Mechanics)
```

1. **Aturan Main (Mechanics):** Komponen konkret yang ditulis programmer di kode — rumus perhitungan, state machine 4 status petak (*Unowned*, *Single*, *Complex*, *Acquired*), biaya akuisisi paksa 2x lipat, angka dadu, dan probabilitas berita ekonomi.
2. **Situasi Permainan (Dynamics):** Perilaku nyata yang muncul saat aturan dijalankan bersama pemain dan waktu — perang likuiditas (kapan pegang uang tunai vs beli tanah), aksi pemblokiran kawasan, pencaplokan agresif yang memicu balas dendam, dan kepanikan pasar saat berita krisis tiba.
3. **Rasa yang Dirasakan Pemain (Aesthetics):** Pengalaman emosional yang sebenarnya dijual kepada pemain dari 8 rasa baku: *Sensation* (keindahan indra), *Fantasy* (menjadi sosok lain), *Narrative* (drama cerita), *Challenge* (uji kecerdasan & taktik), *Fellowship* (keseruan sosial), *Discovery* (menemukan hal baru), *Expression* (kreasi gaya sendiri), dan *Submission* (hiburan santai).

> **Prinsip Utama:** Perancang merancang aturan main agar memunculkan situasi yang melahirkan rasa emosional yang diinginkan. Sebaliknya, pemain merasakan pengalaman emosionalnya terlebih dahulu baru kemudian memahami aturan mainnya.

---

## Catatan Riset & Pembuktian Fakta (Research Protocol)

Dukungan riset data dari game sejenis untuk memastikan setiap opsi dan contoh konkret berpijak pada tolok ukur industri:

| Aspek | Temuan Riset | Sumber Rujukan | Dampak ke Pertanyaan |
| :--- | :--- | :--- | :--- |
| **Kompetitor & Mekanik Akuisisi** | *Fortune Street* (*Itadaki Street*) memakai sistem *forced buyout* sebesar 5x lipat valuasi untuk memecah monopoli distrik tanpa mematikan lawan secara instan. Sedangkan di *LINE Let's Get Rich*, biaya ambil alih (*takeover*) adalah 2x lipat total biaya beli + bangun, dengan *Landmark* sebagai satu-satunya aset yang kebal. | [GameSpot Fortune Street Review](https://www.gamespot.com/reviews/fortune-street-review/1900-6347310/) & [LINE Let's Get Rich Analysis](https://medium.com) | Menanyakan batasan akuisisi paksa 2x lipat: apakah petak komplek yang dicaplok tetap memiliki bangunan utuh, dan apakah pemain bisa membuat satu petak kebal permanen atau selalu bisa dibeli. |
| **Pacing & Durasi Sesi** | *Monopoly GO!* sukses di mobile lewat sesi mikro 3–10 menit (asinkron/solo), sedangkan game meja kompetitif sinkron seperti *Business Tour* (PC Steam/Mobile) membutuhkan 20–45 menit per ronde penuh 4 pemain untuk mencapai kondisi bangkrut/kemenangan. | [MobileGamer.biz Analysis](https://mobilegamer.biz) & [HowLongToBeat Business Tour](https://howlongtobeat.com/game/47854) | Membagi pertanyaan tempo ke dalam dua mode: Mode Cepat (10–15 menit) dan Mode Panjang (30–45 menit), serta menguji aturan giliran pemain (timer 20–30 detik). |
| **Model Transaksi & Multiplatform** | Pada game kompetitif papan meja dan tycoon di platform seperti Roblox maupun Steam/Mobile F2P, pembelian yang diterima pemain adalah murni barang hiasan/kosmetik (skin dadu beranimasi, token pion avatar 3D, efek visual papan), sedangkan transaksi yang menjual uang tunai langsung memicu tuduhan *pay-to-win* yang merusak retensi. | [Roblox Developer Hub & Obby.fun Tycoon Monetization](https://create.roblox.com) | Menajamkan pertanyaan cara mendapatkan uang agar fokus pada kustomisasi visual tanpa merusak adilnya kompetisi ekonomi di atas papan. |

---

## ✅ Keputusan Desain Terkunci (Final — 2026-10-24)

Semua keputusan di bawah sudah final dan mengunci sebagian pertanyaan di kelompok C & G di bawah.

### Matras 2 Mode Permainan

| Aturan | **Mode Cepat (Rapid)** | **Mode Lama (Long-Term)** |
| :--- | :--- | :--- |
| **Syarat bangun rumah** | **NO COMPLEK RULE** — beli rumah di petak tunggal yang dimiliki, bayar, selesai | **WAJIB BERKOMPLEKS** — bangun hanya setelah satu set warna utuh dikuasai (barter P2P jadi nyawa mode ini) |
| **Tangga batas bangunan** | **Per petak**, sesi = putaran papan dihitung **personal** (naik saat pemain sendiri lewat Start): Sesi 1 = maks **2 rumah/petak** → Sesi 2 = maks **4 rumah/petak** → Sesi 3+ = boleh **1 hotel** (syarat 4 rumah dulu) | **Tanpa tangga** — bebas bangun (Hukum Cepat tidak berlaku) |
| **Akuisisi paksa** | **TIDAK ADA** — mendarat di tanah orang = hanya bayar sewa | **BERLAKU** — caplok **2x lipat valuasi**, kompensasi 100% ke pemilik lama + **momen reset** (komplek yang pernah dicaplok & balik ke tangan → status balik sesi 1) |
| **Modal awal** | **7.500 tunai + 2 petak properti acak** (KEPUTUSAN 2026-10-24, OQ#5 ditutup — sim: Gini 0,14, arketipe imbang) | **2.000 tunai** papan kosong — sabar menabung & barter ("dikasih napas" dari 1.500; KEPUTUSAN 2026-10-24) |

### Aturan Umum (kedua mode)

- **Berita Ekonomi RNG** dipicu **setiap pemain melewati Start** — selain gaji, seluruh papan dapat 1 notifikasi berita acak (Krisis Properti / Booming Kawasan / Pajak Likuiditas / Hot Takeover), lihat [`kartu-draft.md`](./kartu-draft.md).
- **Kartu Diskon material bangunan** boleh dipakai **kapan saja** selama kartu aktif (tidak terikat giliran/kunjungan).
- **Kartu bilingual** — seluruh Kartu Umum & Kesempatan punya teks Indonesia **Gaul Ramah** (slang nasional yang dipahami semua orang, tanpa medok berat) + English; engine memilih kolom sesuai locale (Kelompok G).
- **State Machine tetap satu** — perbedaan mode hanya 3 flag: `requireComplex`, `allowHostileTakeover`, `useLapBuildCap` (v0.6: Landmark, Obligasi Kawasan, dan berita E04/E09 ikut `allowHostileTakeover`, tidak menambah flag) (arsitektur modular multiplatform).
- **Urutan giliran diacak per sesi** (KEPUTUSAN 2026-11-07, OQ#8 ditutup) — seat spread turun ke 3,4% (Cepat) / 4,0% (Lama) dari dulu k0/k1 ~55–60%; tak ada pemain yang bisa mengklaim kursi hoki.

---

## A. Target Pemain & Perangkat (Player & Platform)

- [x] Siapa target pemain utama yang disasar game ini? **(KEPUTUSAN: Pemain berusia 13–24 tahun di platform Roblox/Mobile yang menyukai persaingan gengsi yang cepat & intens, serta komunitas strategi-kasual 18–35 tahun di PC/Steam yang menginginkan alternatif Monopoli modern yang dinamis dan bebas dari kebuntuan papan)**
- [x] Di perangkat dan wadah mana game ini akan pertama kali dirilis? **(KEPUTUSAN: Mobile (Android/iOS) dan Roblox Studio sebagai arena debut tercepat untuk validasi komunitas, dibangun di atas arsitektur logika C#/Lua modular yang siap di-porting ke PC Steam via Unity dan desktop ringan via Qt C++)**
- [x] Berapa lama durasi bermain yang paling pas dalam satu sesi permainan? **(KEPUTUSAN: Mode Cepat dikunci pada 10–15 menit untuk sesi santai di sela waktu luang, sedangkan Mode Lama dikunci pada 30–45 menit untuk sesi kompetitif berbobot bersama teman)** — **KEPUTUSAN REVISI 2026-10-24 (playtest-sim):** nilai presisi dikunci **seragam 15 menit** (Mode Cepat, semua jumlah pemain — hotel baru kebuka menit ~11–12 di 4 pemain, dipotong lebih awal = momen hotel war nggak pernah kejadian) dan **45 menit** (Mode Lama, ujung atas rentang — simulasi 42 mnt rata-rata, masuk jendela)
- [x] Bagaimana pemain saling terhubung saat bermain bersama? **(KEPUTUSAN: Ruang multipemain online 4 orang secara sinkron (Quick Match + Private Lobby Kode 6-Digit), dilengkapi mode luring/offline melawan 3 Bot AI cerdas dengan profil kepribadian variatif: si Agresif, si Penimbun Kas, dan si Makelar Tanah)**
- [x] Berapa batas waktu giliran untuk tiap pemain agar alur permainan tidak membosankan? **(KEPUTUSAN: Batas waktu 20 detik per giliran dengan efek audio detak jam visual. Jika waktu habis, Bot AI otomatis mengambil alih giliran dengan aksi paling konservatif: roll dadu otomatis dan bayar sewa standar)**

---

## B. Ragam Permainan & Referensi (Genre & Benchmarks)

- [x] Game papan digital mana yang menjadi pembanding utama untuk rasa permainan yang ingin kamu capai? **(KEPUTUSAN: Tri-hibrida antara ketegangan pencaplokan distrik di *Fortune Street*, kecepatan duel dan kepuasan aksi di *LINE Let's Get Rich*, serta kebersihan antarmuka 3D dan interaksi sosial meja di *Business Tour*)**
- [x] Bagian apa dari game pembanding tersebut yang ingin kamu tiru dan sempurnakan? **(KEPUTUSAN: Menyederhanakan rumus pencaplokan 5x Fortune Street menjadi 2x lipat valuasi tunai langsung, membalik aturan imunitas agar tanah eceran aman untuk blocking awal, serta mengadopsi pemicu Berita Ekonomi global otomatis saat lewat Start)**
- [x] Hal apa dari Monopoli konvensional yang ingin kamu buang agar pemain tidak merasa jenuh? **(KEPUTUSAN: Membuang fenomena *board lock* (kebekuan permainan akibat pemain enggan bertukar tanah) dan menghapus eliminasi pasif dini (korban akuisisi paksa menerima 100% uang tunai dari nilai asetnya, sehingga punya amunisi kas untuk langsung membalas lawan))**
- [x] Apa satu kalimat daya tarik utama yang membedakan game ini dari Monopoli lainnya? **(KEPUTUSAN: "Monopoli modern di mana aset lawan bisa kamu caplok paksa kapan saja dengan uang tunai, dan krisis ekonomi mendadak bisa membalikkan nasib dalam satu lemparan dadu!")**

---

## C. Kegiatan Inti yang Diulang (Core Loop & System Rules)

- [x] Apa kegiatan inti yang dilakukan pemain setiap kali gilirannya tiba (durasi 30–60 detik)? **(KEPUTUSAN: Lempar 2 Dadu → Pion Bergerak → Aksi Petak: [Tanah Kosong: Beli/Lelang] / [Tanah Sendiri: Bangun Rumah sesuai kuota mode] / [Komplek Lawan: Bayar Sewa ATAU bayar 2x lipat valuasi untuk Hostile Takeover] / [Dana Umum & Kesempatan: Buka Kartu] → Jika melewati/mendarat di Start: Ambil gaji Rp 400 jt + Siarkan 1 Berita Ekonomi acak global ke seluruh papan)**
- [x] Bagaimana aturan batas bangunan per mode? **(KEPUTUSAN: Mode Cepat = tangga per-petak per-sesi personal 2 → 4 rumah → 1 hotel; Mode Lama = bebas bangun — lihat Matras 2 Mode di atas)**
- [x] Bagaimana rumus perhitungan valuasi saat seorang pemain melakukan akuisisi paksa 2x lipat? **(KEPUTUSAN: Formula Valuasi = `[Harga Beli Tanah + (Jumlah Rumah × Harga Beli Rumah)]`. Biaya Hostile Takeover = `Valuasi Total × 2`, dibayar 100% tunai dari pencaplok ke pemilik lama. Jika sedang aktif Berita Krisis Properti (-50%), biaya caplok menjadi `(Valuasi Total × 0.5) × 2 = Valuasi Normal`)**
- [x] Kapan sebuah ronde permainan dinyatakan selesai dan siapa pemenangnya? **(KEPUTUSAN: Mode Cepat berakhir dengan Last Man Standing (tersisa 1 pemain tidak bangkrut) ATAU pemain pertama yang membangun 3 Hotel; Mode Lama berakhir dengan Net Worth Victory (pemain pertama yang menyentuh total kekayaan Rp 50 Miliar tanah + rumah + kas saat lewat Start) ATAU semua lawan bangkrut)** — **KEPUTUSAN REVISI 2026-10-24 (diuji playtest-sim, ≥4.800 game):** ending LAMA DIGANTI TOTAL — (a) "3 Hotel menang" memicu **tie di garis finish di 26–33% game** + first-mover edge (kursi 0: 40% menang vs kursi 3: 9%) → **Mode Cepat = timer keras 15 menit seragam, pemenang = Net Worth (aset+bangunan+kas) tertinggi, 3 hotel = milestone;** (b) "50 Miliar" **terbukti mustahil** (total suplai uang ≈ 39.000 juta; 0/1.200 run) → **Mode Lama = timer 45 menit + Net Worth target 8.000 juta (terkalibrasi sim: ~p80 pemenang, crossing median menit 35, terpicu ~23% game) + LMS;** (c) tie-break seragam: Net Worth → kas tunai terbanyak → adu 1 dadu. Hasil re-run: 8/8 bucket 🟢 FAIR (Cepat mid 46–49%, blowout ~1%; Lama durasi ~42 mnt)
- [x] Apa yang terjadi pada komplek warna jika satu petak di dalamnya dicaplok secara paksa oleh lawan? **(KEPUTUSAN: Status komplek langsung PECAH (Broken Set). Hak membangun rumah di petak lain pada warna tersebut langsung terkunci kembali, dan tarif sewa petak-petak saudaranya turun kembali ke tarif sewa tanah tunggal)**
- [x] Apa yang terjadi pada bangunan rumah yang sudah berdiri di atas petak yang baru saja dicaplok paksa? **(KEPUTUSAN: Rumah yang sudah berdiri tetap utuh dan berpindah kepemilikan 100% ke pencaplok. Ini memberi insentif agresif bagi pembeli, sekaligus memberikan kompensasi kas masif 2x lipat kepada korban untuk membangun strategi baru)**
- [x] Kapan dan seberapa sering berita ekonomi mendadak (RNG) muncul di atas papan? **(KEPUTUSAN: setiap pemain melewati Start — selain gaji, seluruh papan dapat 1 notifikasi berita acak, lihat [`kartu-draft.md`](./kartu-draft.md) bagian Aturan Pemicu)**
- [x] Kalau berita baru datang sebelum efek berita lama habis — menumpuk, menimpa, atau perpanjang durasi? **(KEPUTUSAN: Efek sejenis memperpanjang durasi (maksimal 5 putaran); efek bertolak belakang saling menghapus/menetralkan (misal: Booming Kawasan vs Resesi Sewa); efek beda kategori berjalan paralel berdampingan)**
- [x] Apa aturan penahan agar pemain yang memiliki uang tunai melimpah tidak mencaplok seluruh papan dalam satu putaran? **(KEPUTUSAN: Dibatasi maksimal 1 kali aksi Hostile Takeover per giliran pemain, diperkuat oleh ancaman kartu Berita Pajak Likuiditas yang menyita 30% uang kas milik pemain terkaya)**
- [x] Bagaimana pembagian petak tanah acak di awal permainan pada Mode Cepat dilakukan agar tetap adil? **(KEPUTUSAN: Sistem membagikan 2–3 petak tanah eceran ke setiap pemain di putaran pertama dengan Color Distribution Guarantee — dilarang ada pemain yang menerima 2 petak dari kelompok warna yang sama)**

---

## D. Cara Mendapatkan Penghasilan dari Game (Monetization & Business Model)

- [x] Model rilis apa yang paling tepat untuk game ini? **(KEPUTUSAN: Free-to-Play (F2P) di platform mobile dan Roblox, dengan opsi rilisan Premium berbayar di Steam yang langsung menyertakan seluruh bundel tema papan)**
- [x] Barang apa saja di dalam game yang dapat dibeli pemain tanpa membuat permainan terasa berat sebelah (*anti pay-to-win*)? **(KEPUTUSAN: 100% Kosmetik Visual: Skin Pion 3D (Sultan Konglomerat, Mobil Balap Neon, Bebek Emas), Animasi Dadu & Trail Efek (Dadu Kristal, Jejak Api), Tema Visual Papan Permainan (Cyberpunk, Batavia Kuno, Kerajaan Megah), dan Emote Reaksi Meja)**
- [x] Jika game dirilis secara gratis, bagaimana sistem hadiah dan iklan disusun agar tidak merusak kenyamanan bermain? **(KEPUTUSAN: Zero Forced Ads — tanpa iklan tiba-tiba yang memotong permainan. Hanya ada iklan sukarela (Rewarded Video) di lobi utama untuk memutar roda keberuntungan kosmetik harian atau bonus perolehan poin XP battle pass)**
- [x] Apakah ada sistem tiket musiman (*Season Pass*) untuk pemain yang setia? **(KEPUTUSAN: Ya, "Taipan Pass" berdurasi 30 hari dengan jalur gratis dan premium yang menghadiahkan skin dadu eksklusif, animasi selebrasi, dan tema papan musiman tanpa atribut mekanik penambah status)**

---

## E. Batasan Ruang Lingkup & Teknis (Scope & Technical Boundaries)

- [x] Berapa jumlah personel di dalam tim dan berapa target waktu pengerjaan versi mini pertama? **(KEPUTUSAN: Tim mini 1–2 orang (1 Core Logic Programmer + 1 3D/UI Generalist). Target: Prototipe State Machine teruji (1 bulan) → Alpha Playtest Lokal (2 bulan) → MVP Multiplatform Siap Rilis (4 bulan))**
- [x] Mesin game (*game engine*) mana yang menjadi prioritas utama untuk implementasi *State Machine* 4 status petak? **(KEPUTUSAN: Membangun Core Game Logic terpisah memakai arsitektur Command Pattern berbasis C# (Unity) dan Lua (Roblox), dengan pemisahan mutlak antara kalkulasi transaksi ekonomi dan lapisan antarmuka grafis)**
- [x] Bagaimana sistem menangani pemain yang tiba-tiba keluar atau terputus sambungan internetnya (*disconnect*)? **(KEPUTUSAN: Grace period 30 detik untuk penyambungan ulang. Jika lewat batas, Server-Authoritative Engine langsung menggantikan peran pemain dengan AI Bot Pengganti (Mode Defensif). Pemain dapat bergabung kembali (rejoin) kapan saja selama permainan belum usai)**
- [x] Fitur apa yang sengaja ditunda dan tidak akan dibuat pada versi pertama (v1)? **(KEPUTUSAN: Fitur pasar bursa saham distrik spekulatif ala Fortune Street, turnamen berperingkat global (Ranked ELO Ladder), dan fitur kustomisasi denah papan (Map Editor) resmi ditunda ke versi lanjutan v2)**

---

## F. Pengalaman Emosional yang Ditargetkan (Aesthetic Target MDA-8)

- [x] Dari 8 rasa pengalaman bermain, apa **2 rasa utama** yang ingin dijual oleh game ini kepada pemain?
  - Prioritas 1: **Tantangan Taktik & Kecerdasan (Challenge)** — kepuasan mengelola likuiditas kas, menentukan momen emas akuisisi paksa saat pasar krisis, dan mengoptimalkan penempatan komplek.
  - Prioritas 2: **Kebersamaan & Ketegangan Sosial (Fellowship)** — ledakan tawa, teriakan dramatis, dan intrik persaingan di antara teman saat properti mewah direbut paksa di depan mata.
- [x] Rasa apa yang **sengaja dikesampingkan** dari game ini?
  - **Cerita & Narasi Fiksi (Narrative):** Permainan murni menjual intrik kompetisi ekonomi di atas papan tanpa perlu alur cerita fiksi ataupun dialog tokoh yang berlarut-larut.
- [x] Rasa apa yang **WAJIB dicegah** agar pemain tidak kecewa atau jera bermain?
  - Mencegah rasa **kelesuan pasrah tanpa daya (Unwanted Submission)** — tidak boleh ada kondisi papan terkunci mati di mana pemain merasa nasibnya 100% ditentukan oleh lemparan dadu tanpa ada opsi strategi perlawanan.
- [x] Dalam satu kalimat lugas, pengalaman esensial apa yang akan diceritakan seorang pemain kepada kawannya setelah bermain? **(KEPUTUSAN: "Sensasi membalikkan keadaan saat lawan jumawa punya komplek mewah, tapi berhasil kurebut paksa saat harga properti anjlok karena krisis ekonomi!")**

---

## G. Bahasa & Nada Kartu (Lokalisasi Bilingual)

- [x] Tingkat "medok" bahasa Indonesia pada teks kartu seperti apa? **(KEPUTUSAN REVISI 2026-10-24: GAUL RAMAH — slang populer yang dipahami seluruh Indonesia (gas, cuan, viral, manyun), TANPA medok Jawa berat supaya pemain Indo mana pun tetap paham. Kata Jawa yang dipakai hanya yang sudah jadi slang nasional)**
- [x] Status versi Inggris seperti apa? **(KEPUTUSAN: Setara Penuh (Full Parity) — setiap kartu memiliki terjemahan bahasa Inggris yang disesuaikan secara kultural dan memiliki dampak mekanik yang persis sama)**
- [x] Kalau meja online isinya pemain campuran bahasa, tampilan kartu ikut bahasa siapa? **(KEPUTUSAN: Client-side Localization — setiap pemain melihat teks kartu dalam bahasa yang dipilih pada profil masing-masing, sementara engine hanya menyiarkan ID kartu dan parameter logikanya)**
- [x] Isi Kartu Umum (Community Chest) tetap klasik (warisan, pajak, rezeki nomplok) atau ikut konteks ekonomi Indonesia? **(KEPUTUSAN: Diadaptasi penuh ke dinamika sosial Indonesia yang sangat relatable: warisan simbah, arisan kampung, uang THR, amplop kondangan, iuran RT, durian kebun, hingga tilang motor)**
- [x] Kartu Kesempatan (Chance) dipakai khusus untuk Sistem Berita Ekonomi RNG (krisis properti / booming kawasan / pajak likuiditas), atau tetap campuran nasib baik-buruk seperti Monopoli asli? **(KEPUTUSAN: Sub-deck Berita Ekonomi dipicu otomatis saat pemain lewat Start; sisa Kartu Kesempatan = nasib baik-buruk, pergerakan pion, renovasi rumah, dan voucher taktis)**
- [x] Ada kalimat yang wajib dihindari demi kesopanan dan umur game? **(KEPUTUSAN: Wajib bebas dari unsur SARA, tidak membawa simbol agama, dan menghindari lelucon soal pinjaman online predator atau utang piutang dunia nyata)**

---

> **Draf lengkap 49 kartu bilingual (9 Berita Ekonomi RNG + 20 Kartu Umum + 20 Kartu Kesempatan, Indonesia Gaul Ramah + English) ada di [`kartu-draft.md`](./kartu-draft.md).** Seluruh keputusan di atas telah sinkron dan siap dijadikan masukan langsung ke tahap Game Design Document (GDD) 9-seksi formal.

---

> **Langkah Selanjutnya:**  
> Seluruh poin pertanyaan dan hasil kesepakatan di dalam dokumen ini telah **100% TERJAWAB dan TERKUNCI**. Dokumen ini siap menjadi input langsung untuk menyusun Dokumen Desain Game (GDD) formal 9-seksi melalui perintah slash command:  
> 👉 **/game-design-grill-with-docs**
