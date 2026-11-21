# korpus-pusat

Korpus peraturan perundang-undangan tingkat pusat untuk keperluan pemeriksaan BPK (Badan Pemeriksa Keuangan). Korpus ini menjadi sumber bagi skill cari-kriteria, yaitu skill pencari kriteria pemeriksaan sampai level pasal.

Repositori ini hanya berisi teks peraturan publik dan metadatanya. Catatan penugasan, nama entitas yang diperiksa, data entitas, dan kredensial tidak boleh ditulis ke file, laporan, nama file, maupun pesan commit.

## Struktur

```
indeks/<jenis>/<ID>.md   satu file per peraturan, dipecah per pasal
katalog.csv              satu baris per peraturan
perubahan.csv            peta perubahan per pasal
tag.csv                  daftar tag isu (dipakai juga oleh korpus-daerah)
laporan/AAAA-BB.md       laporan berkala
```

Nilai `<jenis>`: `uu`, `perppu`, `pp`, `perpres`, `permen`, `peraturan-lembaga`, `kepmen`, `keputusan-pejabat`, `se`.

Jenis yang diterima:

| Jenis | Kepanjangan |
|---|---|
| UU | Undang-Undang |
| Perppu | Peraturan Pemerintah Pengganti Undang-Undang |
| PP | Peraturan Pemerintah |
| Perpres | Peraturan Presiden |
| Permen | Peraturan Menteri |
| Peraturan Lembaga | Peraturan lembaga negara/pemerintah |
| Kepmen | Keputusan Menteri |
| Keputusan pejabat | Keputusan pejabat di bawah menteri atau keputusan pimpinan lembaga, misalnya Keputusan Direktur Jenderal (Kepdirjen), Keputusan Kepala Lembaga (Kepka), dan Keputusan Deputi |
| SE | Surat Edaran |

Jenis di luar daftar ini tidak dimasukkan tanpa persetujuan pemilik korpus.

## Google Drive

Naskah PDF disimpan di Google Drive akun khusus, di bawah folder induk `Peraturan/`:

```
Peraturan/
├── Kotak-Masuk/              PDF yang belum diproses, nama file bebas (pusat maupun daerah)
│   └── duplikat/             PDF duplikat dari Kotak-Masuk; tidak dipindai, dikosongkan pemilik korpus secara berkala
├── Korpus-Pusat/naskah/<jenis>/<ID>.pdf (lampiran terpisah: <ID>_LAMPIRAN-I.pdf, ...)
└── Korpus-Daerah/<provinsi>/<entitas>/<ID>.pdf
```

- Kotak-Masuk bukan bagian korpus dan tidak dicatat di katalog. Identitas naskah dibaca dari isi PDF, bukan dari nama file.
- PDF yang sudah terindeks dipindah dari Kotak-Masuk ke folder korpusnya dengan nama `<ID>.pdf`.
- PDF di Kotak-Masuk yang identitasnya (dibaca dari isi naskah) cocok dengan ID yang sudah ada di katalog dan file indeksnya sudah di-push langsung dipindah ke `Kotak-Masuk/duplikat/` dengan nama asli, tanpa diproses ulang dan tanpa menunggu persetujuan, berapa pun jumlah filenya. Satu-satunya pengecualian: bila korpus belum memiliki PDF maupun tautan sumber resmi untuk ID itu, salinan tersebut diproses sebagai PDF korpus (`<ID>.pdf`). Setiap pemindahan dicatat di bagian "duplikat dipindah" pada laporan.
- File yang bukan peraturan atau tidak terbaca dibiarkan di Kotak-Masuk dan dicantumkan di daftar perlu dicek.
- PDF wajib disimpan hanya untuk naskah yang tidak tersedia di sumber resmi daring.
- File di Drive tidak dihapus.

## Konvensi penamaan

- ID peraturan sekaligus menjadi nama file: `<ID>.md` di repositori, `<ID>.pdf` di Google Drive.
- ID ditulis huruf kapital dengan garis bawah sebagai pemisah: `<JENIS>_<NOMOR>_<TAHUN>`.
- Untuk Permen, Kepmen, Peraturan Lembaga, dan SE, `<JENIS>` memuat singkatan penerbit agar unik: `PERMEN<PENERBIT>`, `KEPMEN<PENERBIT>`, `PER<LEMBAGA>`, `SE<PENERBIT>`.
- Untuk keputusan pejabat, `<JENIS>` memuat jabatan dan unit atau lembaga penerbit: `KEPDIRJEN<UNIT>`, `KEPKA<LEMBAGA>`, `KEPDEPUTI<LEMBAGA>`. Contoh: `KEPKALKPP_<NOMOR>_<TAHUN>`.
- Nomor peraturan yang memuat kode unit (misalnya Peraturan Menteri Keuangan Nomor 58/PMK.03/2022) memakai nomor urut dan tahun pada ID (`PERMENKEU_58_2022`); nomor lengkap dicatat di kolom `nomor` katalog. Singkatan penerbit Peraturan Menteri Keuangan: `PERMENKEU`.
- Lampiran yang disimpan sebagai PDF terpisah diberi nama `<ID>_LAMPIRAN-I.pdf`, `<ID>_LAMPIRAN-II.pdf`, dan seterusnya, di folder yang sama dengan PDF induknya. Lampiran tunggal: `<ID>_LAMPIRAN.pdf`.
- Dokumen pendukung (buku manual, petunjuk teknis, atau pedoman terbitan instansi yang bukan naskah peraturan, tetapi dinyatakan sebagai lampiran atau dirujuk oleh peraturan induknya) disimpan di folder yang sama dengan peraturan induknya dengan nama `<ID-induk>_<KETERANGAN>.pdf`; `<KETERANGAN>` huruf kapital dengan tanda hubung, misalnya `PERMENKES_33_2015_BUKU-MANUAL-1.pdf`. Dokumen pendukung tidak mendapat ID, file indeks, atau baris katalog sendiri, dan tidak dicatat di kolom `tautan_pdf_drive`; judul, dasar keterkaitannya, dan tautan Drive-nya ditulis di bawah heading `## Lampiran` pada file indeks peraturan induk. Dokumen terbitan instansi yang tidak punya peraturan induk tidak disimpan di korpus.
- Singkatan penerbit yang belum pernah dipakai di katalog mengikuti singkatan yang tertulis di naskah atau di JDIH (Jaringan Dokumentasi dan Informasi Hukum) penerbitnya.
- Tanggal ditulis `AAAA-BB-HH`.

## katalog.csv

Kolom, berurutan:

| Kolom | Isi |
|---|---|
| id | ID peraturan sesuai konvensi |
| jenis | Jenis peraturan |
| nomor | Nomor peraturan |
| tahun | Tahun peraturan |
| judul | Judul lengkap |
| penerbit | Lembaga penetap |
| status | `berlaku`, `diubah`, atau `dicabut` |
| berlaku_sejak | Tanggal mulai berlaku menurut ketentuan penutup naskah |
| berlaku_sampai | Tanggal mulai berlakunya peraturan pencabut; kosong bila masih berlaku |
| diubah_dicabut_oleh | ID peraturan pengubah atau pencabut; beberapa ID dipisah titik koma |
| tautan_sumber | Tautan resmi (JDIH penerbit atau Pasal.id); kosong bila tidak ditemukan |
| tautan_pdf_drive | Tautan PDF di Google Drive, bila disimpan; bila lampiran disimpan terpisah, tautan induk lalu tautan lampiran, dipisah titik koma |
| tag_isu | Tag dari tag.csv, dipisah titik koma |
| tag_jenis_pemeriksaan | `keuangan`, `kinerja`, `pdtt` (Pemeriksaan Dengan Tujuan Tertentu); boleh lebih dari satu |
| tanggal_verifikasi | Tanggal terakhir status dicek ke sumber luar |
| status_review | `lolos-otomatis`, `perlu-dicek`, atau `terverifikasi` |
| catatan_cek | Alasan singkat bila `perlu-dicek` |

Nilai yang mengandung koma diapit tanda kutip ganda. Urutan dan nama kolom tidak diubah tanpa persetujuan pemilik korpus.

Peraturan yang dicabut tidak dihapus. Masa berlakunya dicatat di katalog karena kriteria dipilih berdasarkan periode yang diperiksa.

## perubahan.csv

Peta perubahan per pasal. Peta ini tidak menyalin bunyi pasal; bunyi yang berlaku dikutip langsung dari naskah pengubah yang ditunjuk. Versi konsolidasi tidak disusun.

Satu baris mewakili satu unsur naskah induk yang terkena oleh satu naskah pengubah. Kolom, berurutan:

| Kolom | Isi |
|---|---|
| id_induk | ID peraturan yang teksnya berubah |
| unsur | `pasal`, `bab`, `bagian`, `paragraf`, `judul-bagian`, `penjelasan`, `lampiran`, atau `naskah` (seluruh naskah) |
| rujukan | Alamat unsur di naskah induk, misalnya `12`, `9A`, `BAB VIII Bagian Keenam`, `Lampiran II` |
| jenis_perubahan | `diubah`, `disisipkan`, `dihapus`, `dicabut`, `tidak-mengikat-mk`, atau `ditetapkan-menjadi-uu` |
| id_pengubah | ID peraturan pengubah atau pencabut; untuk putusan Mahkamah Konstitusi (MK): `PUTUSANMK_<nomor>-PUU-<kode tahun register>_<tahun register>`, misalnya `PUTUSANMK_91-PUU-XVIII_2020` untuk perkara 91/PUU-XVIII/2020 |
| lokasi | Letak perintah perubahan di naskah pengubah, ditulis persis, misalnya `Pasal I angka 5` atau `Pasal 176 angka 3`; untuk putusan MK: `Amar angka <n>` |
| rincian | Kalimat perintah perubahan disalin dari naskah pengubah sampai sebelum kata "sehingga"; untuk putusan MK: bunyi amar yang menyangkut pasal itu |
| berlaku_sejak | Tanggal mulai berlaku perubahan menurut ketentuan penutup atau peralihan naskah pengubah; untuk putusan MK: tanggal putusan diucapkan; `AAAA-BB-HH` |
| status_review | `lolos-otomatis`, `perlu-dicek`, atau `terverifikasi` |
| catatan_cek | Alasan singkat bila `perlu-dicek` |

Aturan pengisian:

1. Satuan baris adalah pasal. Ayat, huruf, atau angka yang terkena dicatat di `rincian`, karena naskah pengubah menulis ulang pasal itu secara utuh ("sehingga Pasal N berbunyi sebagai berikut").
2. `diubah`: isi pasal berubah, termasuk ayat atau huruf yang disisipkan, ditambahkan, atau dihapus di dalamnya. `disisipkan`: pasal atau unsur baru. `dihapus`: pasal dihapus lewat perintah perubahan. `dicabut`: pasal dicabut atau dinyatakan tidak berlaku lewat ketentuan penutup peraturan lain. `tidak-mengikat-mk`: pasal, ayat, atau frasa dinyatakan bertentangan dengan UUD 1945 dan tidak mempunyai kekuatan hukum mengikat oleh putusan MK. Bila yang terkena hanya sebagian pasal (ayat, huruf, atau frasa), bagian itu disebut di `rincian`.
3. `id_induk` adalah naskah yang teksnya benar-benar berubah. Pasal sisipan tetap memakai `id_induk` peraturan asal, sehingga riwayatnya terbaca dengan mengurutkan baris per `id_induk` dan `rujukan` berdasarkan `berlaku_sejak`.
4. Naskah perubahan yang disebut dalam frasa "sebagaimana telah diubah dengan" tidak ikut diubah. Perubahan berikutnya tercatat pada `id_induk` asal, bukan pada naskah perubahan sebelumnya. Aturan yang sama berlaku untuk kolom `diubah_dicabut_oleh` di katalog: naskah perubahan berstatus `diubah` hanya bila norma miliknya sendiri diubah.
5. Isi diambil dari bunyi naskah pengubah yang dibaca, bukan dari judul atau ringkasan situs. Untuk putusan MK, isi diambil dari amar putusan yang dibaca (Pasal.id atau situs MK); putusan MK tidak diindeks dan tidak dicatat di katalog.
6. Perppu (Peraturan Pemerintah Pengganti Undang-Undang) yang ditetapkan menjadi UU: penetapan tidak mengubah isi, jadi status Perppu di katalog tetap `berlaku` dan UU penetapan tidak dicatat di `diubah_dicabut_oleh`. Hubungannya dicatat satu baris: `unsur` = `naskah`, `rujukan` = `seluruh`, `jenis_perubahan` = `ditetapkan-menjadi-uu`, `id_pengubah` = UU penetapan, `lokasi` = pasal penetapan. Perppu yang ditolak DPR berstatus `dicabut`. Perubahan yang dibuat Perppu atas peraturan lain memakai ID Perppu sebagai `id_pengubah`, karena teksnya ada di naskah Perppu. Bila naskah Perppu tidak diindeks terpisah dan teksnya hanya ada sebagai lampiran UU penetapan, ID UU penetapan yang dipakai. Saat dikutip: "Pasal N Perppu X yang telah ditetapkan menjadi Undang-Undang dengan UU Y".
7. Baris diberi `perlu-dicek` bila naskah pengubahnya berstatus `perlu-dicek` di katalog atau bila tanggal berlakunya tidak terbaca; alasannya ditulis di `catatan_cek`.

Cara membaca rantai perubahan:

- Ambil semua baris dengan `id_induk` dan `rujukan` yang dicari, lalu urutkan berdasarkan `berlaku_sejak`. Ambil juga baris `unsur` = `naskah` untuk `id_induk` yang sama: baris itu berlaku untuk seluruh naskah, dengan batasan yang tertulis di `rincian` (misalnya "sepanjang mengatur ..."). Bunyi yang berlaku pada suatu tanggal adalah bunyi pada baris terakhir yang `berlaku_sejak`-nya tidak melewati tanggal itu. Bila tidak ada baris sebelum tanggal itu, pakai bunyi naskah induk.
- Setiap kali mengutip pasal dari peta, baca juga ketentuan peralihan dan penutup setiap naskah pengubah dalam rantai (biasanya Pasal II), karena di sana dapat diatur penundaan, batas waktu, atau masa transisi untuk pasal tertentu.
- Baca `rincian` setiap baris: bila yang terkena hanya sebagian pasal, bagian lain pasal itu tetap mengikuti bunyi sebelumnya.
- Peta lengkap untuk suatu induk hanya bila setiap ID di `diubah_dicabut_oleh` pada katalog punya paling sedikit satu baris di perubahan.csv (putusan MK tidak tercatat di katalog, jadi tidak ikut pemeriksaan ini). Bila belum lengkap, misalnya karena naskah pengubah belum ada di korpus, sampaikan peringatan sebelum mengutip bunyi pasal induk.

## Format file indeks

```
---
id: <ID>
jenis: <jenis>
nomor: <nomor>
tahun: <tahun>
judul: <judul lengkap>
sumber_teks: teks-digital | ocr
---
# <judul lengkap>
## Pembukaan
## BAB I - <JUDUL BAB>
### Pasal 1
## Penutup
## Penjelasan
### Penjelasan Umum
### Penjelasan Pasal 1
## Lampiran
```

- Bunyi pasal disalin apa adanya. Perbaikan hanya untuk galat OCR (Optical Character Recognition) yang jelas, tanpa mengubah kata.
- Setiap pasal mendapat satu heading `### Pasal N`. Bagian dan Paragraf ditulis sebagai baris tebal di bawah heading BAB.
- Peraturan perubahan disimpan sebagai naskah tersendiri sesuai bunyinya (Pasal I, Pasal II beserta angka perubahannya). Tidak ada versi konsolidasi.
- SK dan SE yang tidak berpasal memakai heading sesuai diktum (KESATU, KEDUA) atau angka butirnya.
- Tabel lampiran yang tidak terekstrak rapi cukup dicatat judulnya dengan keterangan "lihat PDF".
- `## Penutup` memuat bagian setelah pasal terakhir: kalimat pengundangan, tempat dan tanggal penetapan dan pengundangan, penanda tangan, serta nomor Lembaran atau Berita Negara.
- `### Penjelasan Umum` memuat penjelasan umum sebelum penjelasan pasal demi pasal.
- Untuk peraturan perubahan berpasal Romawi, heading memakai `### Pasal I`, `### Pasal II`; pasal yang diubah di dalamnya ditulis sebagai baris `Pasal N` di dalam teks.

## Pemeriksaan otomatis dan status_review

Setiap naskah yang masuk melewati enam pemeriksaan: (1) identitas, (2) naskah final, (3) mutu OCR, (4) urutan pasal, (5) duplikat, (6) masa berlaku. Pada pemeriksaan identitas, nama file hanya dicocokkan bila sudah berpola `<ID>.pdf`; nama bebas dari Kotak-Masuk tidak dinilai.

- Semua lulus: `lolos-otomatis`.
- Ada yang gagal: `perlu-dicek`; `catatan_cek` memuat nomor pemeriksaan yang gagal dan alasannya.
- `terverifikasi` hanya diberikan setelah teks pasal dicocokkan dengan PDF.
- Pencocokan tidak harus halaman per halaman. Teks indeks dibandingkan kata per kata dengan sumber teks kedua (lapisan teks PDF atau OCR ulang), lalu setiap selisih dicocokkan dengan gambar halaman PDF.
- Pemeriksaan wajib saat pencocokan: tidak ada baris isi yang terbuang bersama kepala halaman, misalnya baris yang diawali "Republik Indonesia" atau "Presiden".
- Lampiran lebih dari 100 halaman yang teks OCR-nya hanya dapat dipastikan lewat gambar tidak dicocokkan. Di bawah heading `## Lampiran` ditulis penanda: `> Lampiran belum dicocokkan dengan gambar halaman PDF (...). Cocokkan mandiri dengan PDF sebelum mengutip.` `status_review` ditentukan oleh batang tubuh dan Penjelasan.
- Naskah yang teksnya belum dicocokkan karena terlalu panjang diberi penanda serupa di bawah judul (`# <judul>`) dan tetap `perlu-dicek`.

## tag.csv

Kolom: `tag`, `definisi`. Tag ditulis huruf kecil dengan tanda hubung. Tag baru ditambahkan hanya setelah disetujui pemilik korpus. Kolom `tag_isu` di katalog boleh kosong bila belum ada tag yang sesuai.

## Laporan

`laporan/AAAA-BB.md` berisi enam bagian tetap: naskah masuk, perubahan status, perlu dicek, usulan tag baru, kendala akses, dan duplikat dipindah. Laporan bulan yang sama diperbarui dengan menambah, bukan menimpa.

## Pesan commit

```
tambah: <ID> - <judul singkat> [<status_review>]
status: <ID> <status lama> -> <status baru> oleh <ID pengubah>
katalog: <perubahan metadata dan alasannya>
laporan: AAAA-BB
skema: <perubahan yang disetujui>
```
