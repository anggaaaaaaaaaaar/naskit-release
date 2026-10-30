# NASKit

NASKit mengubah mini PC atau PC bekas menjadi NAS untuk rumah, keluarga,
atau kantor kecil. Setiap pengguna punya folder pribadi, super admin bisa
melihat semua folder, dan file bisa dibuka dari browser, aplikasi
Nextcloud, jaringan lokal (Samba), atau dari luar rumah lewat Tailscale
tanpa membuka port di router.

Repo ini hanya berisi file rilis. Source code NASKit tidak publik.

## Isinya

- `naskit`, satu program untuk Linux amd64 dan arm64. Program ini memasang
  dan mengatur Nextcloud, PostgreSQL, Valkey, Caddy, dan Samba.
- Situs admin di port 8088 untuk mengatur pengguna, grup, disk, snapshot,
  backup, peringatan, dan update.
- Snapshot Btrfs tiap jam. File yang terhapus dikembalikan dengan
  `naskit snapshot restore`.
- Login dua langkah (2FA), log aktivitas, dan lupa password lewat email.

Aplikasi Android belum diterbitkan di sini.

## Gratis dan Pro

NASKit bisa dipakai tanpa kunci lisensi, gratis dan tanpa batas waktu.

| | Gratis | Pro |
|---|---|---|
| Pengguna terkelola (super admin awal tidak dihitung) | 1 | sesuai kunci |
| Nextcloud, Samba, 2FA, log aktivitas | ya | ya |
| Peringatan di situs admin | ya | ya |
| Notifikasi Telegram dan email | tidak | ya |
| Kuota per pengguna | tidak | ya |
| Folder grup | tidak | ya |
| Backup ke luar NAS (restic) | tidak | ya |
| Ganti disk, pasang update, masuk Tailscale | lewat command line | juga dari situs admin |
| Snapshot yang disimpan | 24 per jam, 7 harian | 24 per jam, 14 harian, 8 mingguan |

Kunci Pro dibeli per mesin. Jalankan `naskit license machine-id` di NAS,
kirim hasilnya ke penjual, lalu pasang kunci yang Anda terima:

```sh
sudo naskit license install <kunci>
naskit license status
```

Kunci dicek secara offline. Kalau kunci habis atau dicabut, file Anda
tidak ikut terkunci. Pengguna, grup, dan backup lama tetap jalan; yang
berhenti hanya fitur Pro untuk hal baru serta backup dan notifikasi
terjadwal.

## Kebutuhan

- Debian atau Ubuntu 64-bit (amd64 atau arm64), dengan akses root.
- RAM minimal 4 GB. Untuk sampai 10 pengguna, 8 sampai 16 GB lebih nyaman.
- Satu disk sistem dan minimal satu disk data. Disk data diformat Btrfs
  oleh `naskit storage init`, jadi isinya akan dihapus.

## Pasang

Cara paling cepat:

```sh
curl -fsSL https://github.com/anggaaaaaaaaaaar/naskit-release/releases/latest/download/install.sh | sudo sh
```

Installer ini memilih build yang cocok dengan CPU, mencocokkan checksum
SHA-256 dengan `checksums.txt`, memasang `/usr/local/bin/naskit`, memasang
Docker, Samba, btrfs-progs, smartmontools, restic, dan Tailscale kalau
belum ada, lalu menjalankan `naskit install`. Kalau checksum tidak cocok,
instalasi dibatalkan.

Pilihan lewat variabel lingkungan:

| Variabel | Fungsi |
|---|---|
| `NASKIT_VERSION=v0.15.2` | pasang versi tertentu, bukan yang terbaru |
| `NASKIT_NO_INSTALL=1` | hanya pasang program, jangan jalankan `naskit install` |
| `NASKIT_NO_DOCKER=1` | jangan pasang Docker otomatis |

Kalau ingin membaca installer sebelum menjalankannya:

```sh
curl -fsSLO https://github.com/anggaaaaaaaaaaar/naskit-release/releases/latest/download/install.sh
less install.sh
sudo NASKIT_VERSION=v0.15.2 sh install.sh
```

### Unduh dan cek sendiri

Setiap rilis di halaman [Releases](https://github.com/anggaaaaaaaaaaar/naskit-release/releases)
berisi:

- `naskit_<versi>_linux_amd64.tar.gz` dan `naskit_<versi>_linux_arm64.tar.gz`,
  isinya `naskit`, `CHANGELOG.md`, dan file lisensi;
- `checksums.txt`, berisi SHA-256 kedua arsip;
- `install.sh` dan `revoked.txt` (daftar kunci lisensi yang dicabut).

Unduh arsip untuk CPU Anda dan `checksums.txt` dari rilis yang sama, lalu
cek. Ganti `amd64` dengan `arm64` untuk mesin ARM.

```sh
V=0.15.2
curl -fsSLO https://github.com/anggaaaaaaaaaaar/naskit-release/releases/download/v$V/naskit_${V}_linux_amd64.tar.gz
curl -fsSLO https://github.com/anggaaaaaaaaaaar/naskit-release/releases/download/v$V/checksums.txt
sha256sum -c --ignore-missing checksums.txt
```

Hasilnya harus `naskit_0.15.2_linux_amd64.tar.gz: OK`. Kalau tertulis
`FAILED`, jangan pakai arsip itu. Setelah itu:

```sh
tar -xzf naskit_${V}_linux_amd64.tar.gz
sudo install -m 0755 naskit /usr/local/bin/naskit
sudo naskit install
```

Cara manual ini tidak memasang Docker dan paket lain. Pasang Docker beserta
plugin compose lebih dulu, atau pakai `install.sh`.

## Setelah terpasang

```sh
sudo naskit storage list              # disk yang belum dipakai
sudo naskit storage init /dev/sdb     # disk data pertama, dipasang di /srv/nas
sudo naskit user add budi             # pengguna baru, ditanya password
```

Lalu buka `https://<alamat NAS>:8088` dan masuk dengan akun super admin.
Sertifikatnya self-signed, jadi browser akan memberi peringatan sekali.
Jangan buka port 8088 dan 445 di router. Untuk akses dari luar, pakai
Tailscale.

Konfigurasi ada di `/opt/naskit`, file pengguna di `/srv/nas`.

## Update

```sh
naskit update --check    # ada versi baru?
sudo naskit update       # pasang; program lama disimpan sebagai naskit.prev
sudo naskit rollback     # kembali ke versi sebelumnya
```

`naskit update` mengambil rilis dari repo ini dan mengecek `checksums.txt`
yang sama. Rilis dengan akhiran seperti `v0.16.0-rc.1` adalah pre-release
dan hanya dipasang kalau diminta dengan `--to`.

Catatan perubahan tiap versi ada di `CHANGELOG.md` di dalam arsip rilis.

## Lisensi

NASKit bukan open source. Ketentuan pemakaian, aturan kunci lisensi, data
apa saja yang dikirim NASKit ke internet, dan lisensi program pihak ketiga
(Nextcloud, Samba, dan lainnya) ada di:

- [LISENSI.md](LISENSI.md), bahasa Indonesia
- [LICENSE.md](LICENSE.md), bahasa Inggris

Keduanya berlaku sama. Kalau ada perbedaan arti, yang dipakai versi bahasa
Indonesia. Lisensi ini tunduk pada hukum Republik Indonesia.

## In English

NASKit turns a mini PC or an old PC into a NAS for a home or small office:
a private folder per user, a super admin who can see everything, and
access from the browser, the Nextcloud apps, the LAN (Samba) and
Tailscale. This repository only holds release files; the source is
private. Install with the `install.sh` command above, or download an
archive and `checksums.txt` from Releases and run
`sha256sum -c --ignore-missing checksums.txt` before using it. The free
plan needs no key; Pro keys are sold per machine. The terms are in
[LICENSE.md](LICENSE.md).
