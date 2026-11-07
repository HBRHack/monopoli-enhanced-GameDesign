# Board Sheet — 40 Petak × 2 Theme Variant

> **Status:** DRAFT v1 — nama & tarif `[asumsi — perlu playtest]`
> **Aturan tema (GDD §3.6):** satu meja satu tema, dilarang campur. Papan ini satu layout 40 petak untuk **kedua** tema — hanya nama (kolom ID/EN) dan skin yang beda; **indeks petak, harga, tarif identik** di kedua tema.
> **Format:** layout klasik 4 sudut (0 Start · 10 Penjara · 19 Parkir Bebas · 29 Go-To-Jail) + 22 properti (8 kompleks) + 4 stasiun + 2 utilitas + 4 Dana Umum + 4 Kesempatan + pajak/lima lainnya.

---

## Tabel 40 Petak (indeks searah jarum jam, mulai dari Start = 0)

| # | Tipe | Warna/Kompleks | Nama — **Indonesia Mode** | Name — **International Mode** | Harga | Sewa dasar |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | Sudut | — | **START — Balai Kota** | **GO** | — | Gaji Rp 400 jt |
| 1 | Properti | Cokelat | Gang Mawar | Mediterranean Avenue | 60 | 2 |
| 2 | Kartu | — | Dana Umum | Community Chest | — | — |
| 3 | Properti | Cokelat | Gang Melati | Baltic Avenue | 60 | 4 |
| 4 | Pajak | — | Pajak Penghasilan (bayar 200) | Income Tax (pay 200) | — | — |
| 5 | Stasiun | — | Stasiun Pasar Senen | Reading Railroad | 200 | 25/50/100/200 |
| 6 | Properti | Biru Muda | Pasar Kliwon | Oriental Avenue | 100 | 6 |
| 7 | Kartu | — | Kesempatan | Chance | — | — |
| 8 | Properti | Biru Muda | Jalan Kenanga | Vermont Avenue | 100 | 6 |
| 9 | Properti | Biru Muda | Jalan Cendana | Connecticut Avenue | 120 | 8 |
| 10 | Sudut | — | ** PENJARA (lewat saja)** | **JAIL (just visiting)** | — | — |
| 11 | Properti | Merah Muda | Jalan Diponegoro | St. Charles Place | 140 | 10 |
| 12 | Utilitas | — | PLN | Electric Company | 150 | 4×/10× dadu |
| 13 | Properti | Merah Muda | Jalan Ahmad Yani | States Avenue | 140 | 10 |
| 14 | Properti | Merah Muda | Jalan Gajah Mada | Virginia Avenue | 160 | 12 |
| 15 | Stasiun | — | Stasiun Gubeng | Pennsylvania Railroad | 200 | 25/50/100/200 |
| 16 | Properti | Oranye | Jalan Sultan Agung | St. James Place | 180 | 14 |
| 17 | Properti | Oranye | Jalan Imam Bonjol | Tennessee Avenue | 180 | 14 |
| 18 | Properti | Oranye | Jalan Hayam Wuruk | New York Avenue | 200 | 16 |
| 19 | Sudut | — | ** WARUNG KOPI (parkir bebas)** | **FREE PARKING** | — | — |
| 20 | Properti | Merah | Jalan Merdeka | Kentucky Avenue | 220 | 18 |
| 21 | Kartu | — | Kesempatan | Chance | — | — |
| 22 | Properti | Merah | Jalan Majapahit | Indiana Avenue | 220 | 18 |
| 23 | Properti | Merah | Jalan Kartini | Illinois Avenue | 240 | 20 |
| 24 | Stasiun | — | Terminal Bekasi | B&O Railroad | 200 | 25/50/100/200 |
| 25 | Properti | Kuning | Terminal Utara | Atlantic Avenue | 260 | 22 |
| 26 | Properti | Kuning | Bandara Sentra | Ventnor Avenue | 260 | 22 |
| 27 | Utilitas | — | PDAM | Water Works | 150 | 4×/10× dadu |
| 28 | Properti | Kuning | Pelabuhan Ratu | Marvin Gardens | 280 | 24 |
| 29 | Sudut | — | **DITANGKAP POLISI!** (→ Penjara #10) | **GO TO JAIL** | — | — |
| 30 | Properti | Hijau | Kawasan Industri | Pacific Avenue | 300 | 26 |
| 31 | Properti | Hijau | Sentra Grosir | North Carolina Avenue | 300 | 26 |
| 32 | Kartu | — | Dana Umum | Community Chest | — | — |
| 33 | Properti | Hijau | Plaza Taipan | Pennsylvania Avenue | 320 | 28 |
| 34 | Stasiun | — | Stasiun Gambir | Short Line | 200 | 25/50/100/200 |
| 35 | Kartu | — | Kesempatan | Chance | — | — |
| 36 | Properti | Biru Tua | Gedung Keuangan | Park Place | 350 | 35 |
| 37 | Pajak | — | Pajak Mewah (bayar 100) | Luxury Tax (pay 100) | — | — |
| 38 | Properti | Biru Tua | Menara Sultan | Boardwalk | 400 | 50 |
| 39 | Kartu | — | Kesempatan | Chance | — | — |

---

## Catatan Desain

1. **Zona Perang** (bubblemap GDD §5): petak 16–28 (Oranye→Kuning) = intensitas mendarat tertinggi — tarif dijaga sedang agar kematian tidak instan; Biru Tua (#36, #38) jarang tapi mematikan (sesuai pola probabilitas Markov).
2. **Penjara #10 = sudut paling sibuk** — justru tempat strategis "parkir kas" di mid-game (bebas sewa), konsisten dengan aturan penjara GDD §3.7.
3. Nama Indonesia Mode dipilih dari kosakata yang dipahami nasional (Pasar Kliwon, Jalan Kartini, Terminal Bekasi) — tidak medok, khas kota mana pun.
4. Warna 8 kompleks memakai konvensi warna klasik (cokelat muda → biru tua) untuk aksesibilitas + familiaritas.
5. **Belum final:** nama perlu divalidasi playtest (apakah pemain luar "International Mode" merasa familiar; apakah pemain Indo Relation "Gang Mawar" terasa lucu atau cliché).

---

## Struktur Data (siap engine)

```json
{
  "tileIndex": 1,
  "type": "PROPERTY",
  "colorGroup": "BROWN_LIGHT",
  "price": 60,
  "baseRent": 2,
  "names": { "ID": "Gang Mawar", "EN": "Mediterranean Avenue" }
}
```
> Nama hanya field presentasi per `themeId` room (ID/EN) — indeks, harga, tarif seragam kedua tema.
