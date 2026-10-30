# Lisensi NASKit

Hak cipta (c) 2026 anggaaaaaaaaaaar (https://github.com/anggaaaaaaaaaaar).
Seluruh hak dilindungi.

Ini adalah versi bahasa Indonesia dari [LICENSE.md](LICENSE.md). Kedua
versi berlaku sama. Kalau ada perbedaan arti di antara keduanya, yang
dipakai adalah versi bahasa Indonesia ini.

Lisensi ini berlaku untuk NASKit, yaitu program `naskit`, situs admin di
dalamnya, template konfigurasi yang ditulisnya ke `/opt/naskit`,
`install.sh`, aplikasi Android, dan source code-nya. Program open source
yang dipasang dan dijalankan NASKit tidak termasuk. Program-program itu
tetap memakai lisensinya masing-masing, yang tercantum di bagian
[Perangkat lunak pihak ketiga](#perangkat-lunak-pihak-ketiga).

NASKit bukan open source. Source code-nya privat dan tidak dilisensikan
kepada siapa pun di luar proyek. Pelanggan hanya menerima binary, dengan
ketentuan di bawah ini.

## Memakai NASKit

Anda boleh mengunduh binary `naskit` dari halaman rilis resmi dan
menjalankannya di mesin milik Anda atau yang Anda kelola, untuk diri
sendiri, keluarga, atau usaha Anda.

Tanpa kunci lisensi, NASKit berjalan dengan paket gratis, tanpa biaya dan
tanpa batas waktu. Paket gratis mencakup 1 pengguna terkelola (super admin
yang dibuat saat instalasi tidak dihitung), Nextcloud, Samba, snapshot
lokal yang disimpan 7 hari, peringatan di situs admin, login dua langkah
(2FA), dan log aktivitas. Disk, update, dan Tailscale bisa diatur lewat
command line.

Kunci Pro menambahkan apa yang tercantum di kunci itu: pengguna lebih
banyak, kuota per pengguna, folder grup, backup ke luar NAS, notifikasi
Telegram dan email, ganti disk, pasang update, dan masuk Tailscale dari
situs admin, serta snapshot yang disimpan 8 minggu. `naskit license status`
menampilkan isi kunci di mesin ini.

## Kunci lisensi

- Satu kunci dijual untuk satu mesin dan terikat ke ID mesin itu
  (`naskit license machine-id`). Kunci tidak bisa dipindah ke NAS lain.
  Ganti hardware atau pasang ulang sistem operasi akan mengubah ID-nya.
  Kalau itu terjadi, minta kunci baru ke penjual.
- Kunci bisa memuat batas jumlah pengguna dan tanggal habis. Setelah
  tanggal habis, kunci masih berjalan 14 hari dengan peringatan, lalu
  kembali ke paket gratis sampai diperpanjang.
- Kunci trial tidak terikat ke mesin, tapi selalu punya tanggal habis.
- Anda tidak boleh membagikan, menyebarkan, atau menjual ulang kunci, atau
  memasang satu kunci di lebih dari satu mesin.
- Kunci yang bocor, dibagikan, atau dibayar dengan pembayaran yang
  dikembalikan atau disengketakan bisa dicabut. Kunci yang dicabut tercatat
  di `revoked.txt`, yang diunduh oleh `naskit update`. Kunci yang dicabut
  langsung berhenti berlaku tanpa masa tenggang, dan NAS kembali ke paket
  gratis.

Kunci tidak pernah mengunci file Anda. Kalau kunci habis atau dicabut,
tidak ada yang dihapus kecuali snapshot yang lebih lama dari yang disimpan
paket gratis. Pengguna, grup, dan kuota yang sudah ada tetap berjalan, dan
backup lama tetap bisa dipulihkan. Yang berhenti hanya tindakan berbayar
yang baru serta backup dan notifikasi terjadwal.

## Yang tidak boleh dilakukan

Kecuali hukum di tempat Anda tinggal tetap mengizinkannya, Anda tidak
boleh:

- menghapus, melewati, atau mengubah pengecekan lisensi, atau membagikan
  build, alat, atau petunjuk untuk melakukannya;
- mendekompilasi, membongkar, atau merekayasa balik binary atau aplikasi
  Android;
- menyalin, menjual, menyewakan, atau menyebarkan ulang binary, aplikasi
  Android, atau source code ini, kecuali memberi tautan ke halaman rilis
  resmi;
- menjual NASKit sebagai bagian dari produk atau layanan Anda sendiri,
  misalnya sudah terpasang di hardware yang Anda jual, tanpa perjanjian
  tertulis dengan pemegang hak cipta;
- menghapus pemberitahuan ini atau baris hak ciptanya.

## Data Anda

File, akun, dan pengaturan Anda adalah milik Anda. NASKit tidak mengirim
file, data pemakaian, atau analitik apa pun ke mana pun. NASKit hanya
tersambung ke internet untuk:

- mengecek update dan mengunduh `revoked.txt` dari halaman rilis;
- mengunduh image container yang versinya sudah dikunci, dari registry
  resminya;
- memasang dan menjalankan Tailscale, kalau Anda menyalakannya;
- mengirim email dan pesan Telegram lewat server yang Anda atur;
- menulis backup ke tujuan yang Anda atur.

Kunci lisensi dicek secara offline. NAS tidak butuh internet untuk
memeriksanya.

## Perangkat lunak pihak ketiga

NASKit tidak mengubah atau membundel source code program di bawah ini.
NASKit memasangnya dari paket Debian atau Ubuntu dan mengunduh image
container resminya dari registry masing-masing, dengan versi yang dikunci
di `internal/assets/versions.go`. Setiap
program tunduk pada lisensinya sendiri, dan tidak ada isi lisensi ini yang
membatasi hak yang diberikan lisensi-lisensi tersebut. Source code
masing-masing tersedia di tautan berikut.

### Image container

| Komponen | Lisensi | Sumber |
|---|---|---|
| Nextcloud Server (`nextcloud`) | AGPL-3.0-or-later | https://github.com/nextcloud/server |
| PostgreSQL (`postgres`) | PostgreSQL License | https://www.postgresql.org/ftp/source/ |
| Valkey (`valkey/valkey`) | BSD-3-Clause | https://github.com/valkey-io/valkey |
| Caddy (`caddy`) | Apache-2.0 | https://github.com/caddyserver/caddy |
| cloudflared (`cloudflare/cloudflared`), hanya dengan profil tunnel | Apache-2.0 | https://github.com/cloudflare/cloudflared |

Image tersebut juga berisi paket dasar Debian atau Alpine, masing-masing
dengan lisensinya sendiri. Pemberitahuan lisensinya ada di dalam image.

### Dipasang di host

| Komponen | Lisensi | Sumber |
|---|---|---|
| Docker Engine dan Compose | Apache-2.0 | https://github.com/moby/moby, https://github.com/docker/compose |
| Samba | GPL-3.0-or-later | https://www.samba.org/samba/download/ |
| btrfs-progs | GPL-2.0 | https://github.com/kdave/btrfs-progs |
| smartmontools | GPL-2.0-or-later | https://github.com/smartmontools/smartmontools |
| restic, untuk backup | BSD-2-Clause | https://github.com/restic/restic |
| Client Tailscale, kalau dinyalakan | BSD-3-Clause | https://github.com/tailscale/tailscale |

Client Tailscale adalah open source, tapi server koordinasinya adalah
layanan yang dijalankan Tailscale Inc. Anda masuk dengan akun Tailscale
Anda sendiri dan menyetujui ketentuan mereka. NASKit tidak menjual ulang
layanan itu.

### Dikompilasi ke dalam NASKit

Binary `naskit` hanya dibangun dari library standar Go (BSD-3-Clause,
pemberitahuannya ada di akhir [LICENSE.md](LICENSE.md) dan wajib
disertakan dalam bahasa aslinya). Aplikasi Android memakai OkHttp dan Okio
(Apache-2.0), AndroidX WorkManager (Apache-2.0), dan library standar
Kotlin (Apache-2.0).

### Nama dan logo

Nextcloud, PostgreSQL, Valkey, Caddy, Docker, Samba, Tailscale, Cloudflare,
dan Android adalah nama dan merek dagang milik pemiliknya masing-masing.
NASKit memakai nama-nama itu hanya untuk menyebut dengan apa NASKit
bekerja. NASKit tidak dibuat, didukung, atau dijamin oleh pihak mana pun
dari mereka.

## Tanpa jaminan

Sejauh diizinkan hukum, NASKit diberikan apa adanya, tanpa jaminan apa
pun. Simpan backup untuk apa pun yang tidak boleh hilang. Pemegang hak
cipta tidak bertanggung jawab atas data yang hilang, layanan yang mati,
atau kerugian lain akibat memakai NASKit, kecuali jika hukum di tempat
Anda tinggal tidak mengizinkan batasan ini. Kalau Anda membayar untuk
sebuah kunci, tanggung jawab terbesar pemegang hak cipta kepada Anda
adalah sebesar harga yang Anda bayar untuk kunci itu.

Dukungan, pengembalian dana, dan ketentuan khusus disepakati langsung
dengan penjual.

## Hukum yang berlaku

Lisensi ini tunduk pada hukum Republik Indonesia. Sengketa diselesaikan
lebih dulu secara musyawarah. Kalau dalam 30 hari tidak tercapai
kesepakatan, sengketa dibawa ke pengadilan di Indonesia yang berwenang
mengadilinya.

Tidak ada isi lisensi ini yang menghapus hak pembeli menurut
Undang-Undang Nomor 8 Tahun 1999 tentang Perlindungan Konsumen. Kalau ada
ketentuan di sini yang bertentangan dengan undang-undang itu, ketentuan
tersebut tidak berlaku, dan ketentuan lainnya tetap berlaku.
