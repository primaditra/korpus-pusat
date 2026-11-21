# korpus-pusat

Korpus peraturan perundang-undangan tingkat pusat untuk keperluan pemeriksaan BPK (Badan Pemeriksa Keuangan). Korpus ini menjadi sumber bagi skill cari-kriteria, yaitu skill pencari kriteria pemeriksaan sampai level pasal.

Repositori ini hanya berisi teks peraturan publik dan metadatanya. Catatan penugasan, nama entitas yang diperiksa, data entitas, dan kredensial tidak boleh ditulis ke file, laporan, nama file, maupun pesan commit.

## Struktur

```
indeks/<jenis>/<ID>.md   satu file per peraturan, dipecah per pasal
katalog.csv              satu baris per peraturan
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
- PDF di Kotak-Masuk yang ID-nya sudah ada di katalog dipindah ke `Kotak-Masuk/duplikat/` dengan nama asli, bila korpus sudah memiliki PDF atau tautan sumber resmi. Bila salinan itu satu-satunya PDF, ia diproses sebagai PDF korpus. Bila versinya berbeda atau mutunya lebih baik dari yang terindeks, ia dibiarkan di Kotak-Masuk dan dicantumkan di daftar perlu dicek.
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
