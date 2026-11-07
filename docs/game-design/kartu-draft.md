# Draf Kartu Bilingual — Kartu Umum & Kartu Kesempatan

> **Status:** DRAFT LENGKAP v2.1 (49 Kartu Total: 9 Berita Ekonomi + 20 Kartu Umum + 20 Kartu Kesempatan).
> **Nada bahasa Indonesia:** **Gaul Ramah** — slang populer yang dipahami seluruh Indonesia (gas, cuan, viral, manyun), tanpa medok Jawa berat supaya semua pemain Indo paham.
> **Aturan teknis:** Tabel disimpan dua kolom teks (ID Gaul Ramah / EN) + metadata efek dan parameter angka. Engine (Unity C#, Roblox Lua, Qt C++) membaca parameter efek secara terpisah dari string teks lokalisasi agar perubahan *balance* tidak perlu mengubah terjemahan.  
> **Kartu Kesempatan merangkap Sistem Berita Ekonomi RNG** — world-event dipisahkan menjadi sub-deck khusus yang dipicu setiap kali ada pemain melewati atau mendarat di petak Start.

---

## 1. Arsitektur Dek & Aturan Pemicu Berita Ekonomi

Permainan menggunakan 3 tumpukan kartu:
1. **Sub-Deck Berita Ekonomi (World Event - 9 Kartu):** Berlaku **global untuk seluruh papan**. Dipicu secara otomatis setiap kali ada pemain melewati atau mendarat di petak Start.
2. **Sub-Deck Kartu Umum (Community Chest - 20 Kartu):** Ditarik saat pemain mendarat di petak Dana Umum. Berfokus pada arus kas pribadi, iuran sosial, rezeki mendadak, denda ringan, dan interaksi saweran antar pemain.
3. **Sub-Deck Kartu Kesempatan (Chance - 20 Kartu):** Ditarik saat pemain mendarat di petak Kesempatan. Berfokus pada pergerakan papan, renovasi properti, taktik *Hostile Takeover*, sertifikat perlindungan, dan pertukaran aset.

### Aturan Resolusi Berita Ekonomi:
* **Durasi Efek:** Berlangsung selama **2 atau 3 putaran penuh** (dihitung sejak giliran pemain pemecah berita).
* **Penanganan Berita Bertumpuk (*Stacking Rule*):** Jika berita baru muncul saat berita lama masih aktif:
  * Efek yang sejenis (misal: Krisis Properti muncul lagi) **memperpanjang durasi** (maksimal 5 putaran).
  * Efek yang bertolak belakang (misal: Booming Kawasan vs Resesi Sewa) saling **menghapus (netral)**.
  * Efek yang berbeda kategori (misal: Pajak Likuiditas + Krisis Properti) **berjalan paralel**.
  * **E09 Skandal AMDAL** (kategori `hazard`) tidak bertumpuk pada komplek yang sama: jika komplek termahal sedang tersegel, target pindah ke komplek termahal berikutnya; jika belum ada komplek utuh di papan, kartu ditarik ulang.
* **Mode Cepat vs Mode Lama:**
  * Mode Lama memakai seluruh kartu (termasuk akuisisi paksa dan barter tanah).
  * Mode Cepat menonaktifkan kartu barter/akuisisi rumit dan melipatgandakan nominal uang tunai (skala 5x lipat).
  * Dek berita Mode Cepat = **7 kartu** (tanpa E04 Hot Takeover dan E09 Skandal AMDAL, karena keduanya bergantung pada ekosistem caplok/Landmark yang hanya ada di Mode Lama).

---

## 2. Sub-Deck Berita Ekonomi (World Events) — 9 Kartu

> **Pemicu:** Otomatis ditarik dan disiarkan ke seluruh papan saat ada pion yang melewati atau mendarat di petak Start.  
> **Sifat:** Efek global ke seluruh pemain & seluruh petak.

| # | Efek Game Logic | Indonesia (Gaul Ramah) | English |
|---|---|---|---|
| **E01** | `EVENT_PROPERTY_CRISIS`<br>Valuasi tanah & rumah -50% (3 Putaran) | **KRISIS PROPERTI!**<br>*"Valuasi tanah dan rumah jatuh -50% selama 3 putaran. Yang nyimpan uang tunai banyak — gas, sikat caplok murah sekarang juga!"* | **PROPERTY CRISIS!**<br>*"Property & house valuations plunge -50% for 3 rounds. Cash holders — hostile takeover is on huge discount!"* |
| **E02** | `EVENT_REGIONAL_BOOM`<br>Tarif sewa seluruh papan naik 2x (2 Putaran) | **BOOMING KAWASAN!**<br>*"Sewa di semua kawasan naik 2x lipat selama 2 putaran. Para juragan senang, penyewa manyun!"* | **REGIONAL BOOM!**<br>*"Rent rates across all districts double for 2 rounds. Landlords rejoice, tenants beware!"* |
| **E03** | `EVENT_LIQUIDITY_TAX`<br>Pemain cash terbanyak bayar pajak 30% ke Bank (Instan) | **PAJAK LIKUIDITAS!**<br>*"Awas, razia orang kaya! Pemain dengan uang tunai terbanyak kena pajak dadakan 30%. Jangan simpan uang menganggur, buruan jadi aset!"* | **LIQUIDITY TAX!**<br>*"Wealth tax alert! The player holding the highest cash pays an instant 30% tax to the Bank. Idle cash hurts!"* |
| **E04** | `EVENT_TAKEOVER_FRENZY`<br>Biaya Hostile Takeover diskon 25% (1 Putaran) *(Khusus Mode Lama)* | **HOT TAKEOVER!**<br>*"Momen emas buat ngecaplok! Biaya akuisisi paksa diskon 25% putaran ini. Gas, jangan mikir lama!"* | **TAKEOVER FRENZY!**<br>*"Hostile Takeovers are 25% off during this entire round. Strike while property is vulnerable!"* |
| **E05** | `EVENT_BANK_STIMULUS`<br>Semua pemain dapat subsidi Rp 200 juta & diskon biaya bangun 20% (2 Putaran) | **STIMULUS PERBANKAN!**<br>*"Bank mengucurkan dana! Semua pemain dapat subsidi Rp 200 juta, plus diskon bangun rumah 20% selama 2 putaran."* | **ECONOMIC STIMULUS!**<br>*"The Central Bank injects liquidity! All players receive 200 cash, plus 20% off house construction for 2 rounds."* |
| **E06** | `EVENT_RENT_RECESSION`<br>Semua tarif sewa diskon -50% (2 Putaran) | **RESESI SEWA!**<br>*"Daya beli anjlok! Semua tarif sewa petak diskon -50% selama 2 putaran. Juragan kos manyun, yang jalan-jalan adem tentrem."* | **RENT HOLIDAY RECESSION!**<br>*"Consumer freeze! All rental fees cut by 50% for 2 rounds. Landlords groan while visitors breathe easy."* |
| **E07** | `EVENT_BUILDING_FREEZE`<br>Dilarang membangun rumah baru di seluruh papan (2 Putaran) | **MORATORIUM IZIN BANGUN!**<br>*"Birokrasi ribet! Izin bangun rumah baru ditutup total selama 2 putaran. Rumah yang sudah berdiri makin mahal!"* | **ZONING FREEZE!**<br>*"Permits suspended! No new houses may be constructed across the board for 2 rounds."* |
| **E08** | `EVENT_WILD_INFLATION`<br>Gaji Start naik 2x lipat (Rp 800 jt), tapi sewa naik +50% (2 Putaran) | **INFLASI LIAR!**<br>*"Gaji lewat Start naik jadi Rp 800 juta, tapi hati-hati — semua sewa juga melonjak +50% selama 2 putaran!"* | **RUNAWAY INFLATION!**<br>*"Passing GO salary doubles to 800, but all rents spike +50% for 2 rounds. High stakes, big burns!"* |
| **E09** | `EVENT_ENV_SCANDAL`<br>Komplek valuasi tertinggi disegel: sewa 0 selama 2 putaran, kecuali pemilik bayar denda 20% valuasi ke Bank. Landmark tidak kebal. *(Khusus Mode Lama)* | **SKANDAL AMDAL!**<br>*"Waduh, pabrik limbah ketahuan! Komplek paling mahal se-papan disegel — sewanya mati 2 putaran, kecuali pemiliknya langsung bayar denda AMDAL 20% dari valuasi ke Bank. Cuan disetop, nama tercoreng!"* | **ENVIRONMENTAL SCANDAL!**<br>*"A toxic dump has been exposed! The most valuable complex on the board is sealed — rent drops to 0 for 2 rounds unless the owner immediately pays a 20% valuation fine to the Bank."* |

---

## 3. Sub-Deck Kartu Umum (Community Chest) — 20 Kartu

> **Pemicu:** Mendarat di petak Dana Umum (Community Chest).  
> **Karakter Mekanik:** Transaksi uang tunai langsung, iuran warga, pajak, kesehatan, dan interaksi saweran sosial antar pemain.

| # | Efek Game Logic | Indonesia (Gaul Ramah) | English |
|---|---|---|---|
| **C01** | `CASH_ADD:500`<br>Pemain dapat +Rp 500 jt | *"Waduh, dapat warisan Rp 500 juta dari saudara jauh yang tiba-tiba ingat kamu. Langsung cair!"* | *"Lo and behold! An old relative remembered you exist. Collect 500 inheritance money!"* |
| **C02** | `CASH_SUB:200`<br>Pemain bayar Rp 200 jt ke Bank | *"Belum kerasa gajian habis — kena pajak penghasilan tahunan. Bayar Rp 200 juta, transfer sekarang!"* | *"Well, that stings. Annual income tax assessment — pay 200 to the Bank."* |
| **C03** | `CASH_ADD:150`<br>Pemain dapat +Rp 150 jt | *"Jajananmu viral di medsos, untung bersih Rp 150 juta. Mantap!"* | *"Your food truck side-hustle went viral. Collect 150 clean profit!"* |
| **C04** | `CASH_SUB:100`<br>Pemain bayar Rp 100 jt ke Bank | *"Nekad beli gadget mahal pakai paylater — waktunya nyicil. Bayar Rp 100 juta."* | *"You bought a fancy gadget on installments. Time to pay 100!"* |
| **C05** | `CASH_ADD:100`<br>Pemain dapat +Rp 100 jt | *"Menang lomba karaoke antar kampung — hadiah trofi plus Rp 100 juta. Asyik!"* | *"You won the neighborhood karaoke contest. Collect 100 prize money!"* |
| **C06** | `CASH_SUB:150`<br>Pemain bayar Rp 150 jt ke Bank | *"Stres berlebihan sampai harus opname di rumah sakit — bayar tagihan Rp 150 juta."* | *"Stress overload! You spent the weekend in hospital. Pay 150 medical fees."* |
| **C07** | `CASH_ADD:200`<br>Pemain dapat +Rp 200 jt | *"THR cair dari bos! Dompet langsung hangat, ambil Rp 200 juta."* | *"Holiday bonus approved by the boss! Collect 200."* |
| **C08** | `CASH_SUB:100`<br>Pemain bayar Rp 100 jt ke Bank | *"Motormu rewel sampai turun mesin — biaya servis bengkel Rp 100 juta."* | *"Your motorbike engine broke down completely. Pay 100 for repairs."* |
| **C09** | `CASH_ADD:200`<br>Pemain dapat +Rp 200 jt | *"Nomormu tembus undian belanja supermarket — rezeki nomplok Rp 200 juta!"* | *"Your shopping receipt won the grand raffle! Collect 200 instant cash."* |
| **C10** | `CASH_SUB:50`<br>Pemain bayar Rp 50 jt ke Bank | *"Bayar iuran kas RT dan ronda malam bulan ini — Rp 50 juta."* | *"Neighborhood security & sanitation dues are in. Pay 50."* |
| **C11** | `COLLECT_FROM_EACH_PLAYER:50`<br>Setiap lawan wajib bayar Rp 50 jt ke pemain | *"Hari ini ulang tahunmu! Semua pemain lain wajib nyawer masing-masing Rp 50 juta!"* | *"It's your birthday! Collect 50 gift money from every other player on the board."* |
| **C12** | `PAY_TO_EACH_PLAYER:50`<br>Pemain wajib bayar Rp 50 jt ke setiap lawan | *"Kondangan pernikahan besar di kampung — wajib sumbang amplop Rp 50 juta buat SETIAP pemain lain!"* | *"Big neighborhood wedding! Hand out a 50 gift envelope to EVERY other player."* |
| **C13** | `CASH_ADD:150`<br>Pemain dapat +Rp 150 jt | *"Dividen koperasi warung kelontong cair — tambah modal Rp 150 juta."* | *"Local grocery cooperative pays out dividends. Collect 150."* |
| **C14** | `CASH_SUB:50`<br>Pemain bayar Rp 50 jt ke Bank | *"Kena tilang parkir liar di trotoar — bayar denda Rp 50 juta."* | *"Illegal parking citation! Pay 50 in municipal fines."* |
| **C15** | `CASH_ADD:120`<br>Pemain dapat +Rp 120 jt | *"Panen durian di kebun belakang rumah laris manis diborong bakul — dapat Rp 120 juta."* | *"Backyard fruit harvest sold out at premium prices. Collect 120."* |
| **C16** | `CASH_SUB:80`<br>Pemain bayar Rp 80 jt ke Bank | *"Pagar rumah ambruk keserempet gerobak bakso — ongkos bangun ulang Rp 80 juta."* | *"Your front gate got smashed by a street cart. Pay 80 in masonry repairs."* |
| **C17** | `CASH_ADD:100`<br>Pemain dapat +Rp 100 jt | *"Dapat beasiswa pelatihan wirausaha digital — dana pembinaan Rp 100 juta cair."* | *"Awarded a digital entrepreneurship stipend. Collect 100."* |
| **C18** | `ITEM_KEEP_JAIL_FREE`<br>Kartu Simpanan: Bebas Penjara 1x (Bisa dijual ke lawan) | *"Surat sakti dari lurah: 'Anak ini warga teladan'. Simpan kartunya buat bebas penjara sekali, atau jual ke temanmu!"* | *"Pardon Letter from the Mayor. Keep this card to Get Out of Jail Free, or trade it to rivals!"* |
| **C19** | `CASH_ADD:300`<br>Pemain dapat +Rp 300 jt | *"Giliran kocokan arisan kampung jatuh ke namamu! Gas, ambil Rp 300 juta."* | *"Your name came up in the community savings pot! Collect 300."* |
| **C20** | `CASH_ADD:250`<br>Pemain dapat +Rp 250 jt | *"Salah transfer bank! Bank keliru setor saldo dan tidak minta balik — untung Rp 250 juta."* | *"Bank error in your favor! A misdirected deposit is credited to you. Collect 250."* |

---

## 4. Sub-Deck Kartu Kesempatan (Chance) — 20 Kartu

> **Pemicu:** Mendarat di petak Kesempatan (Chance).  
> **Karakter Mekanik:** Gerakan pion, renovasi properti per rumah, voucher taktik hostile takeover, teleport, dan pertukaran tanah.

| # | Efek Game Logic | Indonesia (Gaul Ramah) | English |
|---|---|---|---|
| **H01** | `MOVE_RELATIVE:-3`<br>Pion mundur 3 petak | *"Jalan raya rusak karena kontraktornya kabur — mundur 3 petak, siapa tahu ketemu rezeki."* | *"Highway maintenance abandoned midway! Step back 3 spaces."* |
| **H02** | `MOVE_TO_START`<br>Maju ke Start & dapat gaji penuh Rp 400 jt | *"Tol lancar jaya tanpa macet! Maju langsung ke Start — ambil gaji penuh Rp 400 juta."* | *"Expressway is wide open! Advance straight to GO and collect full salary of 400."* |
| **H03** | `ITEM_KEEP_HOUSE_DISCOUNT_50`<br>Kartu Simpanan: Biaya bangun rumah diskon 50% untuk 1 komplek | *"Cuci gudang material bangunan! Bangun rumah setengah harga — simpan kartunya, bisa dipakai KAPAN SAJA tanpa kedaluwarsa!"* | *"Building materials liquidation sale! Build houses at half price. Keep this card to use anytime!"* |
| **H04** | `CASH_SUB:100`<br>Pemain bayar Rp 100 jt ke Bank | *"Rayap dan semut rangrang ngerusak gudang sembakomu — bayar renovasi Rp 100 juta."* | *"Termites infested your inventory warehouse! Pay 100 pest control & repair fees."* |
| **H05** | `CHOICE_PAY_OR_MOVE`<br>Pilih: Bayar Rp 150 jt ATAU Mundur 4 petak | *"Dilema warga: bayar iuran semen Rp 150 juta, ATAU mundur 4 petak!"* | *"Citizen dilemma: Pay 150 for road paving, OR retreat 4 spaces back!"* |
| **H06** | `CASH_SUB:50`<br>Pemain bayar Rp 50 jt ke Bank | *"Jadi bahan gosip tetangga gara-gara beli mobil baru — bayar Rp 50 juta buat syukuran kecil."* | *"Neighborhood gossip flared up over your new ride. Pay 50 for a feast to quiet them down."* |
| **H07** | `ASSESS_PROPERTY_REPAIRS:25:75`<br>Bayar Rp 25 jt per rumah & Rp 75 jt per komplek | *"Inspeksi tata kota dadakan! Bayar biaya perbaikan Rp 25 juta untuk SETIAP rumah yang kamu punya di papan."* | *"Municipal safety audit! Pay 25 for every house you own across the entire board."* |
| **H08** | `ITEM_KEEP_TAKEOVER_SHIELD`<br>Kartu Simpanan: Tangkal 1x Hostile Takeover lawan *(Khusus Mode Lama)* | *"Sertifikat Hak Milik (SHM) asli! Simpan kartunya buat NANGKAL 1 kali usulan caplok paksa lawan — uangnya balik, tanah tetap milikmu!"* | *"Ironclad Land Title! Keep this card to block 1 Hostile Takeover attempt. Rival's cash is refunded, property stays yours!"* |
| **H09** | `INSTANT_FREE_HOUSE`<br>Bangun 1 rumah gratis di komplek milikmu | *"Program bedah rumah kilat! Pasang langsung 1 rumah GRATIS di petak komplekmu yang paling mahal."* | *"Emergency Housing Grant! Erect 1 house instantly for FREE on any eligible complex tile you own."* |
| **H10** | `MOVE_TO_NEXT_ENEMY_COMPLEX`<br>Maju ke komplek lawan terdekat (Sewa x1) | *"Naik tol layang! Maju langsung ke petak komplek lawan terdekat — siapin dompet atau siapin doa!"* | *"Flyover detour! Advance directly to the nearest opponent-owned complex tile. Prepare your wallet!"* |
| **H11** | `MOVE_TO_NEXT_UNOWNED_TILE`<br>Terbang ke tanah kosong terdekat & berhak beli | *"Survei tanah lelang murah! Maju ke petak tanah kosong terdekat dan langsung dapat hak beli."* | *"Government auction scout! Advance to the nearest unowned property tile and claim buying rights!"* |
| **H12** | `ITEM_KEEP_TAKEOVER_DISCOUNT_50`<br>Kartu Simpanan: Diskon 50% biaya Hostile Takeover *(Khusus Mode Lama)* | *"Voucher investor kakap! Simpan kartunya — potong 50% biaya caplok paksa berikutnya ke komplek lawan!"* | *"Hostile Takeover Voucher! Keep this card to slash 50% off the cost of your next Hostile Takeover!"* |
| **H13** | `SWAP_SINGLE_TILES`<br>Paksa barter 1 tanah tunggal milikmu dg milik lawan *(Khusus Mode Lama)* | *"Tukar guling sengketa tanah! Tukar 1 tanah kosongmu dengan 1 tanah kosong milik lawan secara paksa!"* | *"Eminent Domain Swap! Forcibly trade 1 of your single unbuilt tiles with 1 single tile of any opponent!"* |
| **H14** | `GO_TO_JAIL`<br>Langsung masuk Penjara, tidak lewat Start, tidak dapat gaji | *"Kena ciduk razia pajak malam hari! Langsung masuk Penjara sekarang — jangan lewat Start, jangan ambil gaji!"* | *"Tax fraud dragnet! Go directly to Jail. Do not pass GO, do not collect 400 salary."* |
| **H15** | `SELL_SINGLE_TILE_TO_BANK_2X`<br>Jual 1 tanah tunggal ke Bank seharga 2x lipat | *"Proyek tol strategis nasional! Bank beli 1 tanah kosongmu dengan harga 2x lipat harga beli. Cuan gede!"* | *"Strategic Highway Acquisition! Sell 1 of your unbuilt single tiles to the Bank for 2x original price!"* |
| **H16** | `SKIP_NEXT_TURN`<br>Pion mogok, lewati 1 giliran berikutnya | *"Mesin motormu mogok kebanjiran — istirahat sebentar, lewati 1 giliran berikutnya."* | *"Engine flooded during torrential rain. Sit tight on the shoulder and skip your next turn."* |
| **H17** | `ITEM_KEEP_FREE_RENT_PASS`<br>Kartu Simpanan: Bebas 1x biaya sewa di petak lawan manapun | *"Kupon nginep gratis dari saudara! Simpan kartunya — bebas 1 kali bayar sewa saat menginjak komplek lawan mana pun."* | *"VIP Guest Pass! Keep this card to negate 1 rent payment when landing on an opponent's high-tier complex."* |
| **H18** | `TAX_PER_TILE:40`<br>Bayar pajak bumi dan bangunan Rp 40 jt per petak tanah | *"Tagihan PBB tahunan datang! Bayar pajak bumi dan bangunan Rp 40 juta untuk SETIAP petak tanah yang kamu pegang."* | *"Property Tax Bill! Pay 40 property assessment tax for each deed title you own on the board."* |
| **H19** | `BONUS_PER_COMPLEX:100`<br>Dapat Rp 100 jt per set komplek utuh yang dimiliki | *"Sponsor baliho masuk! Ada pemasang iklan di semua komplek warna utuhmu — ambil Rp 100 juta per komplek!"* | *"Billboard sponsorship deals! Collect 100 advertising revenue for each completed color complex you operate."* |
| **H20** | `GAMBLE_DICE_EVEN_ODD`<br>Lempar 1 dadu: Genap dapat Rp 200 jt, Ganjil denda Rp 100 jt | *"Taruhan balap liar pasar malam! Lempar 1 dadu: angka genap dapat Rp 200 juta, angka ganjil denda Rp 100 juta!"* | *"Midnight street race wager! Roll 1 die: Even rolls collect 200, Odd rolls pay 100 fine to the Bank!"* |

---

## 5. Ringkasan Kategori Efek & Penyeimbangan (Balancing Rationale)

1. **Rasio Uang Masuk vs Uang Keluar (Cash Inflow vs Outflow):**
   * Di Kartu Umum, perbandingan kartu untung (10 kartu) vs kartu rugi/denda (8 kartu) vs interaksi/simpanan (2 kartu) didesain sedikit positif (+35% net inflow) untuk menjaga likuiditas pemain agar perang *Hostile Takeover* tidak mandek.
2. **Kartu Simpanan (*Keepable Items*):**
   * Terdapat 4 kartu simpanan taktis (`H03`, `H08`, `H12`, `H17`) yang bisa disimpan di kantong inventaris pemain dan digunakan saat momen kritis. Ini menambah kedalaman taktik (*Lens 20: Challenge*) dan memunculkan dinamika perdagangan kartu antar pemain.
3. **Penyelamat Kebekuan Papan (*Anti-Stalemate Mechanics*):**
   * Kartu `H13` (Tukar Guling Sengketa Tanah) memecahkan kebuntuan ketika para pemain saling mengunci komplek dan menolak bernegosiasi.
   * Kartu `E01` (Krisis Properti) dan `H12` (Voucher Takeover) memberi pemain yang tertinggal peluang emas untuk membalikkan keadaan (*comeback dynamic*).

---

## 6. Struktur Data Teknis (Untuk Pemrograman Engine)

Struktur objek kartu siap diimpor ke C#, Lua, atau JSON format:

```json
{
  "cardId": "H08",
  "deckType": "CHANCE",
  "subDeck": "TACTICAL_ITEM",
  "isKeepable": true,
  "actionType": "TAKEOVER_SHIELD",
  "value": 1,
  "allowedModes": ["LONG_TERM_STRATEGY"],
  "text": {
    "id": "Sertifikat Hak Milik (SHM) asli! Simpan kartunya buat NANGKAL 1 kali usulan caplok paksa lawan — uangnya balik, tanah tetap milikmu!",
    "en": "Ironclad Land Title! Keep this card to block 1 Hostile Takeover attempt. Rival's cash is refunded, property stays yours!"
  }
}
```
