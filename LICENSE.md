# NASKit License

Copyright (c) 2026 anggaaaaaaaaaaar (https://github.com/anggaaaaaaaaaaar).
All rights reserved.

An Indonesian version of this license is in [LISENSI.md](LISENSI.md).
Both versions apply equally. Where they differ in meaning, the Indonesian
version prevails.

This file covers NASKit: the `naskit` program, the admin site built into
it, the configuration templates it writes to `/opt/naskit`, `install.sh`,
the Android app, and this source code. It does not cover the open-source
programs NASKit installs and runs next to itself. Those keep their own
licenses, listed under [Third-party software](#third-party-software).

NASKit is not open source. The source code is private and is not licensed
to anyone outside the project. Customers get the binary only, under the
terms below.

## Using NASKit

You may download the `naskit` binary from the official release page and
run it on machines you own or manage, for yourself, your family or your
business.

Without a license key NASKit runs on the free plan, at no cost and with no
time limit. The free plan has 1 managed user (the super admin created at
install does not count), Nextcloud, Samba, local snapshots kept for 7 days,
alerts on the admin site, two-factor sign-in and the activity log. Disks,
updates and Tailscale can be managed from the command line.

A Pro key adds what it was signed for: more users, per-user quota, group
folders, backup outside the NAS, Telegram and email alerts, disk changes,
updates and Tailscale sign-in from the admin site, and snapshots kept for
8 weeks. `naskit license status` lists what this machine's key includes.

## License keys

- A key is sold for one machine and is bound to that machine's ID
  (`naskit license machine-id`). It does not move to another NAS. Replacing
  the hardware or reinstalling the operating system changes the ID; ask the
  seller for a new key when that happens.
- A key may carry a user limit and an expiry date. After the expiry date
  the key keeps working for 14 days with a warning, then falls back to the
  free plan until it is renewed.
- A trial key is not bound to a machine but always has an expiry date.
- You may not share, publish or resell a key, or install one key on more
  than one machine.
- A key that was leaked, shared, or paid for with a refunded or disputed
  payment can be revoked. Revoked keys are listed in `revoked.txt`, which
  `naskit update` fetches. A revoked key stops working at once, with no
  grace period, and the NAS falls back to the free plan.

A key never locks your files. When a key lapses or is revoked, nothing is
deleted except snapshots older than the free plan keeps. Existing users,
groups and quotas keep working, and old backups can still be restored.
Only new paid actions and scheduled backups and alerts stop.

## What you may not do

Unless the law where you live allows it regardless of this license, you
may not:

- remove, bypass or patch the license check, or hand out a build, tool or
  instructions that do;
- decompile, disassemble or reverse engineer the binary or the Android app;
- copy, sell, rent or redistribute the binary, the Android app or this
  source code, except linking people to the official release page;
- sell NASKit as part of your own product or service, for example
  preinstalled on hardware you sell, without a written agreement with the
  copyright holder;
- remove this notice or the copyright lines.

## Your data

Your files, accounts and settings belong to you. NASKit does not send your
files, your usage or any analytics anywhere. It only reaches the internet
to:

- check for updates and fetch `revoked.txt` from the release page;
- pull the pinned container images from their official registries;
- install and run Tailscale, when you turn it on;
- send email and Telegram messages through servers you configure;
- write backups to destinations you configure.

License keys are checked offline. The NAS does not need internet access to
verify one.

## Third-party software

NASKit does not modify or bundle the source of the programs below. It
installs them from Debian or Ubuntu packages and pulls the official
container images from their own registries, with versions pinned in
`internal/assets/versions.go`. Each one is
covered by its own license, and nothing in this file limits the rights
those licenses give you. The source of each is available from the links
below.

### Container images

| Component | License | Source |
|---|---|---|
| Nextcloud Server (`nextcloud`) | AGPL-3.0-or-later | https://github.com/nextcloud/server |
| PostgreSQL (`postgres`) | PostgreSQL License | https://www.postgresql.org/ftp/source/ |
| Valkey (`valkey/valkey`) | BSD-3-Clause | https://github.com/valkey-io/valkey |
| Caddy (`caddy`) | Apache-2.0 | https://github.com/caddyserver/caddy |
| cloudflared (`cloudflare/cloudflared`), only with the tunnel profile | Apache-2.0 | https://github.com/cloudflare/cloudflared |

The images also contain Debian or Alpine base packages, each under its own
license. Their notices are inside the images.

### Installed on the host

| Component | License | Source |
|---|---|---|
| Docker Engine and Compose | Apache-2.0 | https://github.com/moby/moby, https://github.com/docker/compose |
| Samba | GPL-3.0-or-later | https://www.samba.org/samba/download/ |
| btrfs-progs | GPL-2.0 | https://github.com/kdave/btrfs-progs |
| smartmontools | GPL-2.0-or-later | https://github.com/smartmontools/smartmontools |
| restic, for backup | BSD-2-Clause | https://github.com/restic/restic |
| Tailscale client, when turned on | BSD-3-Clause | https://github.com/tailscale/tailscale |

The Tailscale client is open source, but its coordination server is a
service run by Tailscale Inc. You sign in with your own Tailscale account
and accept their terms; NASKit does not resell it.

### Compiled into NASKit

The `naskit` binary is built only from the Go standard library
(BSD-3-Clause, notice below). The Android app uses OkHttp and Okio
(Apache-2.0), AndroidX WorkManager (Apache-2.0) and the Kotlin standard
library (Apache-2.0).

### Names and logos

Nextcloud, PostgreSQL, Valkey, Caddy, Docker, Samba, Tailscale, Cloudflare
and Android are names and trademarks of their owners. NASKit uses them only
to say what it works with. NASKit is not made, endorsed or supported by any
of them.

## No warranty

NASKit is provided as is, without warranty of any kind, to the extent the
law allows. Keep backups of anything you cannot lose. The copyright holder
is not liable for lost data, downtime or any other damage from using
NASKit, except where the law where you live does not allow that limit.
If you paid for a key, the most the copyright holder owes you is what you
paid for it.

Support, refunds and custom terms are agreed directly with the seller.

## Governing law

This license is governed by the laws of the Republic of Indonesia. A
dispute is first settled by talking it through. If that fails within 30
days, it goes to a court in Indonesia that has jurisdiction over it.

Nothing in this license takes away rights a buyer has under Indonesian
consumer protection law (Undang-Undang Nomor 8 Tahun 1999 tentang
Perlindungan Konsumen). Where a term here conflicts with that law, that
term does not apply and the rest stays in force.

---

## Go standard library notice

```
Copyright 2009 The Go Authors.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

   * Redistributions of source code must retain the above copyright
notice, this list of conditions and the following disclaimer.
   * Redistributions in binary form must reproduce the above
copyright notice, this list of conditions and the following disclaimer
in the documentation and/or other materials provided with the
distribution.
   * Neither the name of Google LLC nor the names of its
contributors may be used to endorse or promote products derived from
this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```
