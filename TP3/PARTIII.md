# III. Blob storage

## 2. Let's go¶
🌞 Compléter votre plan Terraform pour déployer du Blob Storage pour votre VM
```sh
voire storage.tf
```

## 3. Proooooooofs¶
🌞 Prouvez que tout est bien configuré, depuis la VM Azure
```sh
[gustave@cloud-tp2-terraform ~]$ curl -sSL -O https://packages.microsoft.com/config/rhel/9/packages-microsoft-prod.rpm
[gustave@cloud-tp2-terraform ~]$ sudo rpm -i packages-microsoft-prod.rpm
warning: packages-microsoft-prod.rpm: Header V4 RSA/SHA256 Signature, key ID be1229cf: NOKEY
[gustave@cloud-tp2-terraform ~]$ rm packages-microsoft-prod.rpm
[gustave@cloud-tp2-terraform ~]$ sudo dnf update
Microsoft Production                                                                                                                                      1.1 kB/s | 481  B     00:00
Microsoft Production                                                                                                                                      960 kB/s | 983  B     00:00
Importing GPG key 0xBE1229CF:
 Userid     : "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
 Fingerprint: BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-Microsoft
Is this ok [y/N]: Y
Microsoft Production                                                                                                                                       35 MB/s |  21 MB     00:00
Last metadata expiration check: 0:00:05 ago on Tue 24 Mar 2026 07:57:54 AM UTC.
Dependencies resolved.
==========================================================================================================================================================================================
 Package                                            Architecture                      Version                                                  Repository                            Size
==========================================================================================================================================================================================
Installing:
 kernel                                             x86_64                            5.14.0-611.41.1.el9_7                                    baseos                               1.1 M
 kernel-core                                        x86_64                            5.14.0-611.41.1.el9_7                                    baseos                                17 M
 kernel-modules                                     x86_64                            5.14.0-611.41.1.el9_7                                    baseos                                40 M
 kernel-modules-core                                x86_64                            5.14.0-611.41.1.el9_7                                    baseos                                31 M
Upgrading:
 WALinuxAgent                                       noarch                            2.13.1.1-3.el9_7.2                                       appstream                            545 k
 WALinuxAgent-udev                                  noarch                            2.13.1.1-3.el9_7.2                                       appstream                             10 k
 binutils                                           x86_64                            2.35.2-67.el9_7.1                                        baseos                               4.5 M
 binutils-gold                                      x86_64                            2.35.2-67.el9_7.1                                        baseos                               734 k
 cloud-init                                         noarch                            24.4-7.el9_7.1.alma.1                                    appstream                            1.1 M
 curl                                               x86_64                            7.76.1-35.el9_7.3                                        baseos                               292 k
 device-mapper                                      x86_64                            9:1.02.206-2.el9_7.1                                     baseos                               138 k
 device-mapper-libs                                 x86_64                            9:1.02.206-2.el9_7.1                                     baseos                               179 k
 dracut                                             x86_64                            057-104.git20250919.el9_7                                baseos                               385 k
 dracut-config-generic                              x86_64                            057-104.git20250919.el9_7                                baseos                                10 k
 dracut-network                                     x86_64                            057-104.git20250919.el9_7                                baseos                                68 k
 dracut-squash                                      x86_64                            057-104.git20250919.el9_7                                baseos                                12 k
 glib2                                              x86_64                            2.68.4-18.el9_7.1                                        baseos                               2.6 M
 glibc                                              x86_64                            2.34-231.el9_7.10                                        baseos                               2.0 M
 glibc-common                                       x86_64                            2.34-231.el9_7.10                                        baseos                               297 k
 glibc-gconv-extra                                  x86_64                            2.34-231.el9_7.10                                        baseos                               1.5 M
 glibc-langpack-en                                  x86_64                            2.34-231.el9_7.10                                        baseos                               554 k
 gnupg2                                             x86_64                            2.3.3-5.el9_7                                            baseos                               2.5 M
 gnutls                                             x86_64                            3.8.3-10.el9_7                                           baseos                               1.1 M
 grub2-common                                       noarch                            1:2.06-114.el9_7.1.alma.1                                baseos                               907 k
 grub2-efi-x64                                      x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                               1.3 M
 grub2-pc                                           x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                                13 k
 grub2-pc-modules                                   noarch                            1:2.06-114.el9_7.1.alma.1                                baseos                               923 k
 grub2-tools                                        x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                               1.8 M
 grub2-tools-minimal                                x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                               611 k
 kernel-tools                                       x86_64                            5.14.0-611.41.1.el9_7                                    baseos                               1.4 M
 kernel-tools-libs                                  x86_64                            5.14.0-611.41.1.el9_7                                    baseos                               1.1 M
 kpartx                                             x86_64                            0.8.7-39.el9_7.1                                         baseos                                49 k
 libarchive                                         x86_64                            3.5.3-7.el9_7                                            baseos                               387 k
 libblkid                                           x86_64                            2.37.4-21.el9_7                                          baseos                               105 k
 libbrotli                                          x86_64                            1.0.9-9.el9_7                                            baseos                               311 k
 libcurl                                            x86_64                            7.76.1-35.el9_7.3                                        baseos                               283 k
 libdnf                                             x86_64                            0.69.0-17.el9_7.alma.1                                   baseos                               653 k
 libfdisk                                           x86_64                            2.37.4-21.el9_7                                          baseos                               151 k
 libldb                                             x86_64                            4.22.4-18.el9_7                                          baseos                               180 k
 libmount                                           x86_64                            2.37.4-21.el9_7                                          baseos                               132 k
 libnfsidmap                                        x86_64                            1:2.5.4-38.el9_7.3                                       baseos                                60 k
 libsmartcols                                       x86_64                            2.37.4-21.el9_7                                          baseos                                60 k
 libssh                                             x86_64                            0.10.4-17.el9_7                                          baseos                               214 k
 libssh-config                                      noarch                            0.10.4-17.el9_7                                          baseos                               8.1 k
 libuuid                                            x86_64                            2.37.4-21.el9_7                                          baseos                                25 k
 libwbclient                                        x86_64                            4.22.4-18.el9_7                                          baseos                                42 k
 microcode_ctl                                      noarch                            4:20250812-1.20251111.1.el9_7                            baseos                                15 M
 nfs-utils                                          x86_64                            1:2.5.4-38.el9_7.3                                       baseos                               434 k
 openssh                                            x86_64                            8.7p1-47.el9_7.alma.1                                    baseos                               453 k
 openssh-clients                                    x86_64                            8.7p1-47.el9_7.alma.1                                    baseos                               707 k
 openssh-server                                     x86_64                            8.7p1-47.el9_7.alma.1                                    baseos                               455 k
 openssl                                            x86_64                            1:3.5.1-7.el9_7                                          baseos                               1.4 M
 openssl-fips-provider                              x86_64                            1:3.5.1-7.el9_7                                          baseos                               812 k
 openssl-libs                                       x86_64                            1:3.5.1-7.el9_7                                          baseos                               2.3 M
 python3                                            x86_64                            3.9.25-3.el9_7.1                                         baseos                                26 k
 python3-hawkey                                     x86_64                            0.69.0-17.el9_7.alma.1                                   baseos                               100 k
 python3-libdnf                                     x86_64                            0.69.0-17.el9_7.alma.1                                   baseos                               770 k
 python3-libs                                       x86_64                            3.9.25-3.el9_7.1                                         baseos                               7.5 M
 python3-pyasn1                                     noarch                            0.4.8-7.el9_7                                            appstream                            131 k
 python3-urllib3                                    noarch                            1.26.5-6.el9_7.1                                         baseos                               191 k
 samba-client-libs                                  x86_64                            4.22.4-18.el9_7                                          baseos                               5.3 M
 samba-common                                       noarch                            4.22.4-18.el9_7                                          baseos                               173 k
 samba-common-libs                                  x86_64                            4.22.4-18.el9_7                                          baseos                               104 k
 selinux-policy                                     noarch                            38.1.65-1.el9_7.1                                        baseos                                37 k
 selinux-policy-targeted                            noarch                            38.1.65-1.el9_7.1                                        baseos                               6.5 M
 shim-x64                                           x86_64                            16.1-5.el9.alma.1                                        baseos                               498 k
 sos                                                noarch                            4.10.2-2.el9_7                                           baseos                               915 k
 tar                                                x86_64                            2:1.34-9.el9_7                                           baseos                               876 k
 tzdata                                             noarch                            2026a-1.el9                                              baseos                               496 k
 util-linux                                         x86_64                            2.37.4-21.el9_7                                          baseos                               2.2 M
 util-linux-core                                    x86_64                            2.37.4-21.el9_7                                          baseos                               431 k
Installing dependencies:
 freetype                                           x86_64                            2.10.4-10.el9_5                                          baseos                               385 k
 graphite2                                          x86_64                            1.3.14-9.el9                                             baseos                                94 k
 grub2-tools-efi                                    x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                               546 k
 grub2-tools-extra                                  x86_64                            1:2.06-114.el9_7.1.alma.1                                baseos                               850 k
 harfbuzz                                           x86_64                            2.7.4-10.el9                                             baseos                               623 k
 libpng                                             x86_64                            2:1.6.37-12.el9_7.2                                      baseos                               115 k

Transaction Summary
==========================================================================================================================================================================================
Install  10 Packages
Upgrade  67 Packages

Total download size: 168 M
Is this ok [y/N]: Y
Downloading Packages:
(1/77): graphite2-1.3.14-9.el9.x86_64.rpm                                                                                                                 780 kB/s |  94 kB     00:00
(2/77): grub2-tools-efi-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                                4.0 MB/s | 546 kB     00:00
(3/77): freetype-2.10.4-10.el9_5.x86_64.rpm                                                                                                               2.6 MB/s | 385 kB     00:00
(4/77): harfbuzz-2.7.4-10.el9.x86_64.rpm                                                                                                                   31 MB/s | 623 kB     00:00
(5/77): grub2-tools-extra-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                               20 MB/s | 850 kB     00:00
(6/77): kernel-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                                            31 MB/s | 1.1 MB     00:00
(7/77): kernel-core-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                                       21 MB/s |  17 MB     00:00
(8/77): libpng-1.6.37-12.el9_7.2.x86_64.rpm                                                                                                                15 MB/s | 115 kB     00:00
(9/77): WALinuxAgent-2.13.1.1-3.el9_7.2.noarch.rpm                                                                                                         33 MB/s | 545 kB     00:00
(10/77): WALinuxAgent-udev-2.13.1.1-3.el9_7.2.noarch.rpm                                                                                                  1.7 MB/s |  10 kB     00:00
(11/77): cloud-init-24.4-7.el9_7.1.alma.1.noarch.rpm                                                                                                       47 MB/s | 1.1 MB     00:00
(12/77): python3-pyasn1-0.4.8-7.el9_7.noarch.rpm                                                                                                           14 MB/s | 131 kB     00:00
(13/77): binutils-2.35.2-67.el9_7.1.x86_64.rpm                                                                                                            5.4 MB/s | 4.5 MB     00:00
(14/77): binutils-gold-2.35.2-67.el9_7.1.x86_64.rpm                                                                                                       6.1 MB/s | 734 kB     00:00
(15/77): kernel-modules-core-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                              15 MB/s |  31 MB     00:02
(16/77): curl-7.76.1-35.el9_7.3.x86_64.rpm                                                                                                                1.3 MB/s | 292 kB     00:00
(17/77): device-mapper-1.02.206-2.el9_7.1.x86_64.rpm                                                                                                      3.5 MB/s | 138 kB     00:00
(18/77): device-mapper-libs-1.02.206-2.el9_7.1.x86_64.rpm                                                                                                  15 MB/s | 179 kB     00:00
(19/77): dracut-057-104.git20250919.el9_7.x86_64.rpm                                                                                                       26 MB/s | 385 kB     00:00
(20/77): dracut-config-generic-057-104.git20250919.el9_7.x86_64.rpm                                                                                       576 kB/s |  10 kB     00:00
(21/77): dracut-network-057-104.git20250919.el9_7.x86_64.rpm                                                                                              4.8 MB/s |  68 kB     00:00
(22/77): dracut-squash-057-104.git20250919.el9_7.x86_64.rpm                                                                                               1.5 MB/s |  12 kB     00:00
(23/77): glibc-2.34-231.el9_7.10.x86_64.rpm                                                                                                                64 MB/s | 2.0 MB     00:00
(24/77): glib2-2.68.4-18.el9_7.1.x86_64.rpm                                                                                                                29 MB/s | 2.6 MB     00:00
(25/77): glibc-common-2.34-231.el9_7.10.x86_64.rpm                                                                                                        4.4 MB/s | 297 kB     00:00
(26/77): kernel-modules-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                                   16 MB/s |  40 MB     00:02
(27/77): glibc-gconv-extra-2.34-231.el9_7.10.x86_64.rpm                                                                                                   4.2 MB/s | 1.5 MB     00:00
(28/77): glibc-langpack-en-2.34-231.el9_7.10.x86_64.rpm                                                                                                   1.4 MB/s | 554 kB     00:00
(29/77): gnutls-3.8.3-10.el9_7.x86_64.rpm                                                                                                                  39 MB/s | 1.1 MB     00:00
(30/77): grub2-common-2.06-114.el9_7.1.alma.1.noarch.rpm                                                                                                   18 MB/s | 907 kB     00:00
(31/77): gnupg2-2.3.3-5.el9_7.x86_64.rpm                                                                                                                   17 MB/s | 2.5 MB     00:00
(32/77): grub2-pc-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                                      254 kB/s |  13 kB     00:00
(33/77): grub2-efi-x64-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                                 9.6 MB/s | 1.3 MB     00:00
(34/77): grub2-pc-modules-2.06-114.el9_7.1.alma.1.noarch.rpm                                                                                               14 MB/s | 923 kB     00:00
(35/77): grub2-tools-minimal-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                            31 MB/s | 611 kB     00:00
(36/77): grub2-tools-2.06-114.el9_7.1.alma.1.x86_64.rpm                                                                                                    16 MB/s | 1.8 MB     00:00
(37/77): kernel-tools-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                                     21 MB/s | 1.4 MB     00:00
(38/77): kpartx-0.8.7-39.el9_7.1.x86_64.rpm                                                                                                               2.9 MB/s |  49 kB     00:00
(39/77): kernel-tools-libs-5.14.0-611.41.1.el9_7.x86_64.rpm                                                                                                15 MB/s | 1.1 MB     00:00
(40/77): libarchive-3.5.3-7.el9_7.x86_64.rpm                                                                                                               16 MB/s | 387 kB     00:00
(41/77): libblkid-2.37.4-21.el9_7.x86_64.rpm                                                                                                              4.2 MB/s | 105 kB     00:00
(42/77): libbrotli-1.0.9-9.el9_7.x86_64.rpm                                                                                                                15 MB/s | 311 kB     00:00
(43/77): libcurl-7.76.1-35.el9_7.3.x86_64.rpm                                                                                                              15 MB/s | 283 kB     00:00
(44/77): libfdisk-2.37.4-21.el9_7.x86_64.rpm                                                                                                               13 MB/s | 151 kB     00:00
(45/77): libldb-4.22.4-18.el9_7.x86_64.rpm                                                                                                                 16 MB/s | 180 kB     00:00
(46/77): libmount-2.37.4-21.el9_7.x86_64.rpm                                                                                                               12 MB/s | 132 kB     00:00
(47/77): libnfsidmap-2.5.4-38.el9_7.3.x86_64.rpm                                                                                                          6.4 MB/s |  60 kB     00:00
(48/77): libdnf-0.69.0-17.el9_7.alma.1.x86_64.rpm                                                                                                          15 MB/s | 653 kB     00:00
(49/77): libsmartcols-2.37.4-21.el9_7.x86_64.rpm                                                                                                          3.5 MB/s |  60 kB     00:00
(50/77): libssh-config-0.10.4-17.el9_7.noarch.rpm                                                                                                         1.0 MB/s | 8.1 kB     00:00
(51/77): libuuid-2.37.4-21.el9_7.x86_64.rpm                                                                                                               2.9 MB/s |  25 kB     00:00
(52/77): libwbclient-4.22.4-18.el9_7.x86_64.rpm                                                                                                           4.2 MB/s |  42 kB     00:00
(53/77): libssh-0.10.4-17.el9_7.x86_64.rpm                                                                                                                6.6 MB/s | 214 kB     00:00
(54/77): nfs-utils-2.5.4-38.el9_7.3.x86_64.rpm                                                                                                             26 MB/s | 434 kB     00:00
(55/77): openssh-8.7p1-47.el9_7.alma.1.x86_64.rpm                                                                                                          13 MB/s | 453 kB     00:00
(56/77): openssh-clients-8.7p1-47.el9_7.alma.1.x86_64.rpm                                                                                                 9.6 MB/s | 707 kB     00:00
(57/77): openssh-server-8.7p1-47.el9_7.alma.1.x86_64.rpm                                                                                                  7.6 MB/s | 455 kB     00:00
(58/77): openssl-3.5.1-7.el9_7.x86_64.rpm                                                                                                                  32 MB/s | 1.4 MB     00:00
(59/77): openssl-fips-provider-3.5.1-7.el9_7.x86_64.rpm                                                                                                    18 MB/s | 812 kB     00:00
(60/77): python3-3.9.25-3.el9_7.1.x86_64.rpm                                                                                                              4.4 MB/s |  26 kB     00:00
(61/77): python3-hawkey-0.69.0-17.el9_7.alma.1.x86_64.rpm                                                                                                 4.7 MB/s | 100 kB     00:00
(62/77): openssl-libs-3.5.1-7.el9_7.x86_64.rpm                                                                                                             42 MB/s | 2.3 MB     00:00
(63/77): python3-libdnf-0.69.0-17.el9_7.alma.1.x86_64.rpm                                                                                                  12 MB/s | 770 kB     00:00
(64/77): python3-urllib3-1.26.5-6.el9_7.1.noarch.rpm                                                                                                      8.1 MB/s | 191 kB     00:00
(65/77): microcode_ctl-20250812-1.20251111.1.el9_7.noarch.rpm                                                                                              25 MB/s |  15 MB     00:00
(66/77): samba-common-4.22.4-18.el9_7.noarch.rpm                                                                                                           10 MB/s | 173 kB     00:00
(67/77): samba-common-libs-4.22.4-18.el9_7.x86_64.rpm                                                                                                     5.9 MB/s | 104 kB     00:00
(68/77): python3-libs-3.9.25-3.el9_7.1.x86_64.rpm                                                                                                          13 MB/s | 7.5 MB     00:00
(69/77): selinux-policy-38.1.65-1.el9_7.1.noarch.rpm                                                                                                      206 kB/s |  37 kB     00:00
(70/77): shim-x64-16.1-5.el9.alma.1.x86_64.rpm                                                                                                             10 MB/s | 498 kB     00:00
(71/77): samba-client-libs-4.22.4-18.el9_7.x86_64.rpm                                                                                                     7.6 MB/s | 5.3 MB     00:00
(72/77): sos-4.10.2-2.el9_7.noarch.rpm                                                                                                                    6.6 MB/s | 915 kB     00:00
(73/77): tar-1.34-9.el9_7.x86_64.rpm                                                                                                                       17 MB/s | 876 kB     00:00
(74/77): tzdata-2026a-1.el9.noarch.rpm                                                                                                                     12 MB/s | 496 kB     00:00
(75/77): util-linux-core-2.37.4-21.el9_7.x86_64.rpm                                                                                                        17 MB/s | 431 kB     00:00
(76/77): util-linux-2.37.4-21.el9_7.x86_64.rpm                                                                                                             20 MB/s | 2.2 MB     00:00
(77/77): selinux-policy-targeted-38.1.65-1.el9_7.1.noarch.rpm                                                                                              12 MB/s | 6.5 MB     00:00
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                      32 MB/s | 168 MB     00:05
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Running scriptlet: selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                                 1/1
  Preparing        :                                                                                                                                                                  1/1
  Upgrading        : selinux-policy-38.1.65-1.el9_7.1.noarch                                                                                                                        1/144
  Running scriptlet: selinux-policy-38.1.65-1.el9_7.1.noarch                                                                                                                        1/144
  Running scriptlet: selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                               2/144
  Upgrading        : selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                               2/144
  Running scriptlet: selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                               2/144
  Upgrading        : tzdata-2026a-1.el9.noarch                                                                                                                                      3/144
  Upgrading        : glibc-common-2.34-231.el9_7.10.x86_64                                                                                                                          4/144
  Upgrading        : glibc-gconv-extra-2.34-231.el9_7.10.x86_64                                                                                                                     5/144
  Running scriptlet: glibc-gconv-extra-2.34-231.el9_7.10.x86_64                                                                                                                     5/144
  Upgrading        : glibc-langpack-en-2.34-231.el9_7.10.x86_64                                                                                                                     6/144
  Running scriptlet: glibc-2.34-231.el9_7.10.x86_64                                                                                                                                 7/144
  Upgrading        : glibc-2.34-231.el9_7.10.x86_64                                                                                                                                 7/144
  Running scriptlet: glibc-2.34-231.el9_7.10.x86_64                                                                                                                                 7/144
  Upgrading        : libuuid-2.37.4-21.el9_7.x86_64                                                                                                                                 8/144
  Upgrading        : libblkid-2.37.4-21.el9_7.x86_64                                                                                                                                9/144
  Running scriptlet: libblkid-2.37.4-21.el9_7.x86_64                                                                                                                                9/144
  Upgrading        : libmount-2.37.4-21.el9_7.x86_64                                                                                                                               10/144
  Upgrading        : libsmartcols-2.37.4-21.el9_7.x86_64                                                                                                                           11/144
  Upgrading        : util-linux-core-2.37.4-21.el9_7.x86_64                                                                                                                        12/144
  Running scriptlet: util-linux-core-2.37.4-21.el9_7.x86_64                                                                                                                        12/144
  Upgrading        : gnutls-3.8.3-10.el9_7.x86_64                                                                                                                                  13/144
  Upgrading        : glib2-2.68.4-18.el9_7.1.x86_64                                                                                                                                14/144
  Upgrading        : libdnf-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                          15/144
  Upgrading        : libbrotli-1.0.9-9.el9_7.x86_64                                                                                                                                16/144
  Upgrading        : libldb-4.22.4-18.el9_7.x86_64                                                                                                                                 17/144
  Running scriptlet: samba-common-4.22.4-18.el9_7.noarch                                                                                                                           18/144
  Upgrading        : samba-common-4.22.4-18.el9_7.noarch                                                                                                                           18/144
  Running scriptlet: samba-common-4.22.4-18.el9_7.noarch                                                                                                                           18/144
  Running scriptlet: libwbclient-4.22.4-18.el9_7.x86_64                                                                                                                            19/144
  Upgrading        : libwbclient-4.22.4-18.el9_7.x86_64                                                                                                                            19/144
  Upgrading        : samba-client-libs-4.22.4-18.el9_7.x86_64                                                                                                                      20/144
  Upgrading        : samba-common-libs-4.22.4-18.el9_7.x86_64                                                                                                                      21/144
  Upgrading        : device-mapper-libs-9:1.02.206-2.el9_7.1.x86_64                                                                                                                22/144
  Upgrading        : device-mapper-9:1.02.206-2.el9_7.1.x86_64                                                                                                                     23/144
  Upgrading        : kpartx-0.8.7-39.el9_7.1.x86_64                                                                                                                                24/144
  Upgrading        : libfdisk-2.37.4-21.el9_7.x86_64                                                                                                                               25/144
  Upgrading        : util-linux-2.37.4-21.el9_7.x86_64                                                                                                                             26/144
  Upgrading        : grub2-common-1:2.06-114.el9_7.1.alma.1.noarch                                                                                                                 27/144
  Upgrading        : grub2-tools-minimal-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                          28/144
  Upgrading        : grub2-pc-modules-1:2.06-114.el9_7.1.alma.1.noarch                                                                                                             29/144
  Installing       : graphite2-1.3.14-9.el9.x86_64                                                                                                                                 30/144
  Installing       : libpng-2:1.6.37-12.el9_7.2.x86_64                                                                                                                             31/144
  Installing       : harfbuzz-2.7.4-10.el9.x86_64                                                                                                                                  32/144
  Installing       : freetype-2.10.4-10.el9_5.x86_64                                                                                                                               33/144
  Upgrading        : binutils-gold-2.35.2-67.el9_7.1.x86_64                                                                                                                        34/144
  Upgrading        : binutils-2.35.2-67.el9_7.1.x86_64                                                                                                                             35/144
  Running scriptlet: binutils-2.35.2-67.el9_7.1.x86_64                                                                                                                             35/144
  Upgrading        : kernel-tools-libs-5.14.0-611.41.1.el9_7.x86_64                                                                                                                36/144
  Running scriptlet: kernel-tools-libs-5.14.0-611.41.1.el9_7.x86_64                                                                                                                36/144
  Upgrading        : libnfsidmap-1:2.5.4-38.el9_7.3.x86_64                                                                                                                         37/144
  Upgrading        : openssl-fips-provider-1:3.5.1-7.el9_7.x86_64                                                                                                                  38/144
  Upgrading        : openssl-libs-1:3.5.1-7.el9_7.x86_64                                                                                                                           39/144
  Upgrading        : dracut-057-104.git20250919.el9_7.x86_64                                                                                                                       40/144
  Installing       : kernel-modules-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                              41/144
  Installing       : kernel-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                                      42/144
  Running scriptlet: kernel-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                                      42/144
  Running scriptlet: openssh-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                          43/144
  Upgrading        : openssh-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                          43/144
  Upgrading        : python3-3.9.25-3.el9_7.1.x86_64                                                                                                                               44/144
  Upgrading        : python3-libs-3.9.25-3.el9_7.1.x86_64                                                                                                                          45/144
  Running scriptlet: grub2-tools-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                  46/144
  Upgrading        : grub2-tools-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                  46/144
  Upgrading        : openssl-1:3.5.1-7.el9_7.x86_64                                                                                                                                47/144
  Upgrading        : grub2-efi-x64-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                48/144
  Upgrading        : python3-libdnf-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                  49/144
  Upgrading        : python3-pyasn1-0.4.8-7.el9_7.noarch                                                                                                                           50/144
  Running scriptlet: openssh-server-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                   51/144
  Upgrading        : openssh-server-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                   51/144
  Running scriptlet: openssh-server-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                   51/144
  Installing       : kernel-modules-5.14.0-611.41.1.el9_7.x86_64                                                                                                                   52/144
  Running scriptlet: kernel-modules-5.14.0-611.41.1.el9_7.x86_64                                                                                                                   52/144
  Upgrading        : libssh-config-0.10.4-17.el9_7.noarch                                                                                                                          53/144
  Upgrading        : libssh-0.10.4-17.el9_7.x86_64                                                                                                                                 54/144
  Upgrading        : libcurl-7.76.1-35.el9_7.3.x86_64                                                                                                                              55/144
  Upgrading        : WALinuxAgent-udev-2.13.1.1-3.el9_7.2.noarch                                                                                                                   56/144
  Upgrading        : WALinuxAgent-2.13.1.1-3.el9_7.2.noarch                                                                                                                        57/144
  Running scriptlet: WALinuxAgent-2.13.1.1-3.el9_7.2.noarch                                                                                                                        57/144
  Upgrading        : curl-7.76.1-35.el9_7.3.x86_64                                                                                                                                 58/144
  Installing       : kernel-5.14.0-611.41.1.el9_7.x86_64                                                                                                                           59/144
  Upgrading        : python3-hawkey-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                  60/144
  Upgrading        : shim-x64-16.1-5.el9.alma.1.x86_64                                                                                                                             61/144
  Upgrading        : cloud-init-24.4-7.el9_7.1.alma.1.noarch                                                                                                                       62/144
  Running scriptlet: cloud-init-24.4-7.el9_7.1.alma.1.noarch                                                                                                                       62/144
  Upgrading        : grub2-pc-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                     63/144
  Upgrading        : kernel-tools-5.14.0-611.41.1.el9_7.x86_64                                                                                                                     64/144
  Running scriptlet: kernel-tools-5.14.0-611.41.1.el9_7.x86_64                                                                                                                     64/144
  Running scriptlet: nfs-utils-1:2.5.4-38.el9_7.3.x86_64                                                                                                                           65/144
  Upgrading        : nfs-utils-1:2.5.4-38.el9_7.3.x86_64                                                                                                                           65/144
  Running scriptlet: nfs-utils-1:2.5.4-38.el9_7.3.x86_64                                                                                                                           65/144
  Upgrading        : python3-urllib3-1.26.5-6.el9_7.1.noarch                                                                                                                       66/144
  Upgrading        : sos-4.10.2-2.el9_7.noarch                                                                                                                                     67/144
  Upgrading        : openssh-clients-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                  68/144
  Running scriptlet: openssh-clients-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                  68/144
  Upgrading        : dracut-config-generic-057-104.git20250919.el9_7.x86_64                                                                                                        69/144
  Upgrading        : dracut-network-057-104.git20250919.el9_7.x86_64                                                                                                               70/144
  Upgrading        : dracut-squash-057-104.git20250919.el9_7.x86_64                                                                                                                71/144
  Upgrading        : libarchive-3.5.3-7.el9_7.x86_64                                                                                                                               72/144
  Installing       : grub2-tools-extra-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                            73/144
  Installing       : grub2-tools-efi-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                              74/144
  Upgrading        : gnupg2-2.3.3-5.el9_7.x86_64                                                                                                                                   75/144
  Upgrading        : tar-2:1.34-9.el9_7.x86_64                                                                                                                                     76/144
  Upgrading        : microcode_ctl-4:20250812-1.20251111.1.el9_7.noarch                                                                                                            77/144
  Running scriptlet: microcode_ctl-4:20250812-1.20251111.1.el9_7.noarch                                                                                                            77/144
  Running scriptlet: WALinuxAgent-2.13.1.1-3.el9.noarch                                                                                                                            78/144
  Cleanup          : WALinuxAgent-2.13.1.1-3.el9.noarch                                                                                                                            78/144
  Running scriptlet: WALinuxAgent-2.13.1.1-3.el9.noarch                                                                                                                            78/144
  Cleanup          : grub2-pc-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                       79/144
  Running scriptlet: cloud-init-24.4-7.el9.alma.1.noarch                                                                                                                           80/144
  Cleanup          : cloud-init-24.4-7.el9.alma.1.noarch                                                                                                                           80/144
  Running scriptlet: cloud-init-24.4-7.el9.alma.1.noarch                                                                                                                           80/144
  Running scriptlet: nfs-utils-1:2.5.4-38.el9.x86_64                                                                                                                               81/144
  Cleanup          : nfs-utils-1:2.5.4-38.el9.x86_64                                                                                                                               81/144
  Running scriptlet: nfs-utils-1:2.5.4-38.el9.x86_64                                                                                                                               81/144
  Cleanup          : device-mapper-9:1.02.206-2.el9.x86_64                                                                                                                         82/144
  Cleanup          : openssl-1:3.5.1-4.el9_7.x86_64                                                                                                                                83/144
  Running scriptlet: kernel-tools-5.14.0-611.13.1.el9_7.x86_64                                                                                                                     84/144
  Cleanup          : kernel-tools-5.14.0-611.13.1.el9_7.x86_64                                                                                                                     84/144
  Running scriptlet: kernel-tools-5.14.0-611.13.1.el9_7.x86_64                                                                                                                     84/144
  Running scriptlet: openssh-server-8.7p1-46.el9.alma.1.x86_64                                                                                                                     85/144
  Cleanup          : openssh-server-8.7p1-46.el9.alma.1.x86_64                                                                                                                     85/144
  Running scriptlet: openssh-server-8.7p1-46.el9.alma.1.x86_64                                                                                                                     85/144
  Running scriptlet: openssh-clients-8.7p1-46.el9.alma.1.x86_64                                                                                                                    86/144
  Cleanup          : openssh-clients-8.7p1-46.el9.alma.1.x86_64                                                                                                                    86/144
  Cleanup          : openssh-8.7p1-46.el9.alma.1.x86_64                                                                                                                            87/144
  Cleanup          : gnupg2-2.3.3-4.el9.x86_64                                                                                                                                     88/144
  Running scriptlet: binutils-2.35.2-67.el9.x86_64                                                                                                                                 89/144
  Cleanup          : binutils-2.35.2-67.el9.x86_64                                                                                                                                 89/144
  Running scriptlet: binutils-2.35.2-67.el9.x86_64                                                                                                                                 89/144
  Cleanup          : libarchive-3.5.3-6.el9_6.x86_64                                                                                                                               90/144
  Cleanup          : tar-2:1.34-7.el9.x86_64                                                                                                                                       91/144
  Cleanup          : samba-client-libs-4.22.4-6.el9_7.x86_64                                                                                                                       92/144
  Cleanup          : libwbclient-4.22.4-6.el9_7.x86_64                                                                                                                             93/144
  Cleanup          : samba-common-libs-4.22.4-6.el9_7.x86_64                                                                                                                       94/144
  Cleanup          : libldb-4.22.4-6.el9_7.x86_64                                                                                                                                  95/144
  Cleanup          : curl-7.76.1-34.el9.x86_64                                                                                                                                     96/144
  Cleanup          : sos-4.10.0-4.el9_7.noarch                                                                                                                                     97/144
  Running scriptlet: selinux-policy-38.1.65-1.el9.noarch                                                                                                                           98/144
  Cleanup          : selinux-policy-38.1.65-1.el9.noarch                                                                                                                           98/144
  Running scriptlet: selinux-policy-38.1.65-1.el9.noarch                                                                                                                           98/144
  Cleanup          : grub2-pc-modules-1:2.06-114.el9_7.alma.1.noarch                                                                                                               99/144
  Cleanup          : python3-pyasn1-0.4.8-6.el9.noarch                                                                                                                            100/144
  Cleanup          : shim-x64-15.8-4.el9_3.alma.2.x86_64                                                                                                                          101/144
  Cleanup          : grub2-efi-x64-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                 102/144
  Cleanup          : python3-urllib3-1.26.5-6.el9.noarch                                                                                                                          103/144
  Cleanup          : dracut-squash-057-102.git20250818.el9.x86_64                                                                                                                 104/144
  Cleanup          : dracut-network-057-102.git20250818.el9.x86_64                                                                                                                105/144
  Cleanup          : dracut-config-generic-057-102.git20250818.el9.x86_64                                                                                                         106/144
  Cleanup          : selinux-policy-targeted-38.1.65-1.el9.noarch                                                                                                                 107/144
  Running scriptlet: selinux-policy-targeted-38.1.65-1.el9.noarch                                                                                                                 107/144
  Cleanup          : samba-common-4.22.4-6.el9_7.noarch                                                                                                                           108/144
  Cleanup          : WALinuxAgent-udev-2.13.1.1-3.el9.noarch                                                                                                                      109/144
  Running scriptlet: microcode_ctl-4:20250812-1.el9.noarch                                                                                                                        110/144
  Cleanup          : microcode_ctl-4:20250812-1.el9.noarch                                                                                                                        110/144
  Running scriptlet: microcode_ctl-4:20250812-1.el9.noarch                                                                                                                        110/144
  Cleanup          : libcurl-7.76.1-34.el9.x86_64                                                                                                                                 111/144
  Cleanup          : libssh-0.10.4-15.el9_7.x86_64                                                                                                                                112/144
  Cleanup          : grub2-tools-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                   113/144
  Cleanup          : grub2-tools-minimal-1:2.06-114.el9_7.alma.1.x86_64                                                                                                           114/144
  Cleanup          : dracut-057-102.git20250818.el9.x86_64                                                                                                                        115/144
  Cleanup          : kpartx-0.8.7-39.el9.x86_64                                                                                                                                   116/144
  Cleanup          : device-mapper-libs-9:1.02.206-2.el9.x86_64                                                                                                                   117/144
  Cleanup          : binutils-gold-2.35.2-67.el9.x86_64                                                                                                                           118/144
  Cleanup          : python3-hawkey-0.69.0-16.el9.alma.1.x86_64                                                                                                                   119/144
  Cleanup          : python3-libdnf-0.69.0-16.el9.alma.1.x86_64                                                                                                                   120/144
  Cleanup          : python3-libs-3.9.23-2.el9.x86_64                                                                                                                             121/144
  Cleanup          : python3-3.9.23-2.el9.x86_64                                                                                                                                  122/144
  Cleanup          : libdnf-0.69.0-16.el9.alma.1.x86_64                                                                                                                           123/144
  Cleanup          : glib2-2.68.4-18.el9_7.x86_64                                                                                                                                 124/144
  Cleanup          : gnutls-3.8.3-9.el9.x86_64                                                                                                                                    125/144
  Cleanup          : libnfsidmap-1:2.5.4-38.el9.x86_64                                                                                                                            126/144
  Cleanup          : openssl-fips-provider-1:3.5.1-4.el9_7.x86_64                                                                                                                 127/144
  Cleanup          : openssl-libs-1:3.5.1-4.el9_7.x86_64                                                                                                                          128/144
  Cleanup          : libbrotli-1.0.9-7.el9_5.x86_64                                                                                                                               129/144
  Cleanup          : kernel-tools-libs-5.14.0-611.13.1.el9_7.x86_64                                                                                                               130/144
  Running scriptlet: kernel-tools-libs-5.14.0-611.13.1.el9_7.x86_64                                                                                                               130/144
  Cleanup          : grub2-common-1:2.06-114.el9_7.alma.1.noarch                                                                                                                  131/144
  Cleanup          : libssh-config-0.10.4-15.el9_7.noarch                                                                                                                         132/144
  Cleanup          : util-linux-2.37.4-21.el9.x86_64                                                                                                                              133/144
  Cleanup          : util-linux-core-2.37.4-21.el9.x86_64                                                                                                                         134/144
  Cleanup          : libfdisk-2.37.4-21.el9.x86_64                                                                                                                                135/144
  Cleanup          : libmount-2.37.4-21.el9.x86_64                                                                                                                                136/144
  Cleanup          : libblkid-2.37.4-21.el9.x86_64                                                                                                                                137/144
  Cleanup          : libuuid-2.37.4-21.el9.x86_64                                                                                                                                 138/144
  Cleanup          : libsmartcols-2.37.4-21.el9.x86_64                                                                                                                            139/144
  Cleanup          : glibc-2.34-231.el9_7.2.x86_64                                                                                                                                140/144
  Cleanup          : glibc-langpack-en-2.34-231.el9_7.2.x86_64                                                                                                                    141/144
  Cleanup          : glibc-gconv-extra-2.34-231.el9_7.2.x86_64                                                                                                                    142/144
  Running scriptlet: glibc-gconv-extra-2.34-231.el9_7.2.x86_64                                                                                                                    142/144
  Cleanup          : glibc-common-2.34-231.el9_7.2.x86_64                                                                                                                         143/144
  Cleanup          : tzdata-2025b-2.el9.noarch                                                                                                                                    144/144
  Running scriptlet: selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                             144/144
  Running scriptlet: grub2-common-1:2.06-114.el9_7.1.alma.1.noarch                                                                                                                144/144
Generating grub stub config for drive  050b8d52-f03b-4fbc-87b3-fee63a357e2c
GRUB_DIR= /grub2
EFI_HOME= /boot/efi/EFI/almalinux

  Running scriptlet: kernel-modules-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                             144/144
  Running scriptlet: kernel-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                                     144/144
  Running scriptlet: kernel-modules-5.14.0-611.41.1.el9_7.x86_64                                                                                                                  144/144
  Running scriptlet: microcode_ctl-4:20250812-1.20251111.1.el9_7.noarch                                                                                                           144/144
  Running scriptlet: tzdata-2025b-2.el9.noarch                                                                                                                                    144/144
  Verifying        : freetype-2.10.4-10.el9_5.x86_64                                                                                                                                1/144
  Verifying        : graphite2-1.3.14-9.el9.x86_64                                                                                                                                  2/144
  Verifying        : grub2-tools-efi-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                               3/144
  Verifying        : grub2-tools-extra-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                             4/144
  Verifying        : harfbuzz-2.7.4-10.el9.x86_64                                                                                                                                   5/144
  Verifying        : kernel-5.14.0-611.41.1.el9_7.x86_64                                                                                                                            6/144
  Verifying        : kernel-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                                       7/144
  Verifying        : kernel-modules-5.14.0-611.41.1.el9_7.x86_64                                                                                                                    8/144
  Verifying        : kernel-modules-core-5.14.0-611.41.1.el9_7.x86_64                                                                                                               9/144
  Verifying        : libpng-2:1.6.37-12.el9_7.2.x86_64                                                                                                                             10/144
  Verifying        : WALinuxAgent-2.13.1.1-3.el9_7.2.noarch                                                                                                                        11/144
  Verifying        : WALinuxAgent-2.13.1.1-3.el9.noarch                                                                                                                            12/144
  Verifying        : WALinuxAgent-udev-2.13.1.1-3.el9_7.2.noarch                                                                                                                   13/144
  Verifying        : WALinuxAgent-udev-2.13.1.1-3.el9.noarch                                                                                                                       14/144
  Verifying        : cloud-init-24.4-7.el9_7.1.alma.1.noarch                                                                                                                       15/144
  Verifying        : cloud-init-24.4-7.el9.alma.1.noarch                                                                                                                           16/144
  Verifying        : python3-pyasn1-0.4.8-7.el9_7.noarch                                                                                                                           17/144
  Verifying        : python3-pyasn1-0.4.8-6.el9.noarch                                                                                                                             18/144
  Verifying        : binutils-2.35.2-67.el9_7.1.x86_64                                                                                                                             19/144
  Verifying        : binutils-2.35.2-67.el9.x86_64                                                                                                                                 20/144
  Verifying        : binutils-gold-2.35.2-67.el9_7.1.x86_64                                                                                                                        21/144
  Verifying        : binutils-gold-2.35.2-67.el9.x86_64                                                                                                                            22/144
  Verifying        : curl-7.76.1-35.el9_7.3.x86_64                                                                                                                                 23/144
  Verifying        : curl-7.76.1-34.el9.x86_64                                                                                                                                     24/144
  Verifying        : device-mapper-9:1.02.206-2.el9_7.1.x86_64                                                                                                                     25/144
  Verifying        : device-mapper-9:1.02.206-2.el9.x86_64                                                                                                                         26/144
  Verifying        : device-mapper-libs-9:1.02.206-2.el9_7.1.x86_64                                                                                                                27/144
  Verifying        : device-mapper-libs-9:1.02.206-2.el9.x86_64                                                                                                                    28/144
  Verifying        : dracut-057-104.git20250919.el9_7.x86_64                                                                                                                       29/144
  Verifying        : dracut-057-102.git20250818.el9.x86_64                                                                                                                         30/144
  Verifying        : dracut-config-generic-057-104.git20250919.el9_7.x86_64                                                                                                        31/144
  Verifying        : dracut-config-generic-057-102.git20250818.el9.x86_64                                                                                                          32/144
  Verifying        : dracut-network-057-104.git20250919.el9_7.x86_64                                                                                                               33/144
  Verifying        : dracut-network-057-102.git20250818.el9.x86_64                                                                                                                 34/144
  Verifying        : dracut-squash-057-104.git20250919.el9_7.x86_64                                                                                                                35/144
  Verifying        : dracut-squash-057-102.git20250818.el9.x86_64                                                                                                                  36/144
  Verifying        : glib2-2.68.4-18.el9_7.1.x86_64                                                                                                                                37/144
  Verifying        : glib2-2.68.4-18.el9_7.x86_64                                                                                                                                  38/144
  Verifying        : glibc-2.34-231.el9_7.10.x86_64                                                                                                                                39/144
  Verifying        : glibc-2.34-231.el9_7.2.x86_64                                                                                                                                 40/144
  Verifying        : glibc-common-2.34-231.el9_7.10.x86_64                                                                                                                         41/144
  Verifying        : glibc-common-2.34-231.el9_7.2.x86_64                                                                                                                          42/144
  Verifying        : glibc-gconv-extra-2.34-231.el9_7.10.x86_64                                                                                                                    43/144
  Verifying        : glibc-gconv-extra-2.34-231.el9_7.2.x86_64                                                                                                                     44/144
  Verifying        : glibc-langpack-en-2.34-231.el9_7.10.x86_64                                                                                                                    45/144
  Verifying        : glibc-langpack-en-2.34-231.el9_7.2.x86_64                                                                                                                     46/144
  Verifying        : gnupg2-2.3.3-5.el9_7.x86_64                                                                                                                                   47/144
  Verifying        : gnupg2-2.3.3-4.el9.x86_64                                                                                                                                     48/144
  Verifying        : gnutls-3.8.3-10.el9_7.x86_64                                                                                                                                  49/144
  Verifying        : gnutls-3.8.3-9.el9.x86_64                                                                                                                                     50/144
  Verifying        : grub2-common-1:2.06-114.el9_7.1.alma.1.noarch                                                                                                                 51/144
  Verifying        : grub2-common-1:2.06-114.el9_7.alma.1.noarch                                                                                                                   52/144
  Verifying        : grub2-efi-x64-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                53/144
  Verifying        : grub2-efi-x64-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                  54/144
  Verifying        : grub2-pc-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                     55/144
  Verifying        : grub2-pc-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                       56/144
  Verifying        : grub2-pc-modules-1:2.06-114.el9_7.1.alma.1.noarch                                                                                                             57/144
  Verifying        : grub2-pc-modules-1:2.06-114.el9_7.alma.1.noarch                                                                                                               58/144
  Verifying        : grub2-tools-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                                  59/144
  Verifying        : grub2-tools-1:2.06-114.el9_7.alma.1.x86_64                                                                                                                    60/144
  Verifying        : grub2-tools-minimal-1:2.06-114.el9_7.1.alma.1.x86_64                                                                                                          61/144
  Verifying        : grub2-tools-minimal-1:2.06-114.el9_7.alma.1.x86_64                                                                                                            62/144
  Verifying        : kernel-tools-5.14.0-611.41.1.el9_7.x86_64                                                                                                                     63/144
  Verifying        : kernel-tools-5.14.0-611.13.1.el9_7.x86_64                                                                                                                     64/144
  Verifying        : kernel-tools-libs-5.14.0-611.41.1.el9_7.x86_64                                                                                                                65/144
  Verifying        : kernel-tools-libs-5.14.0-611.13.1.el9_7.x86_64                                                                                                                66/144
  Verifying        : kpartx-0.8.7-39.el9_7.1.x86_64                                                                                                                                67/144
  Verifying        : kpartx-0.8.7-39.el9.x86_64                                                                                                                                    68/144
  Verifying        : libarchive-3.5.3-7.el9_7.x86_64                                                                                                                               69/144
  Verifying        : libarchive-3.5.3-6.el9_6.x86_64                                                                                                                               70/144
  Verifying        : libblkid-2.37.4-21.el9_7.x86_64                                                                                                                               71/144
  Verifying        : libblkid-2.37.4-21.el9.x86_64                                                                                                                                 72/144
  Verifying        : libbrotli-1.0.9-9.el9_7.x86_64                                                                                                                                73/144
  Verifying        : libbrotli-1.0.9-7.el9_5.x86_64                                                                                                                                74/144
  Verifying        : libcurl-7.76.1-35.el9_7.3.x86_64                                                                                                                              75/144
  Verifying        : libcurl-7.76.1-34.el9.x86_64                                                                                                                                  76/144
  Verifying        : libdnf-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                          77/144
  Verifying        : libdnf-0.69.0-16.el9.alma.1.x86_64                                                                                                                            78/144
  Verifying        : libfdisk-2.37.4-21.el9_7.x86_64                                                                                                                               79/144
  Verifying        : libfdisk-2.37.4-21.el9.x86_64                                                                                                                                 80/144
  Verifying        : libldb-4.22.4-18.el9_7.x86_64                                                                                                                                 81/144
  Verifying        : libldb-4.22.4-6.el9_7.x86_64                                                                                                                                  82/144
  Verifying        : libmount-2.37.4-21.el9_7.x86_64                                                                                                                               83/144
  Verifying        : libmount-2.37.4-21.el9.x86_64                                                                                                                                 84/144
  Verifying        : libnfsidmap-1:2.5.4-38.el9_7.3.x86_64                                                                                                                         85/144
  Verifying        : libnfsidmap-1:2.5.4-38.el9.x86_64                                                                                                                             86/144
  Verifying        : libsmartcols-2.37.4-21.el9_7.x86_64                                                                                                                           87/144
  Verifying        : libsmartcols-2.37.4-21.el9.x86_64                                                                                                                             88/144
  Verifying        : libssh-0.10.4-17.el9_7.x86_64                                                                                                                                 89/144
  Verifying        : libssh-0.10.4-15.el9_7.x86_64                                                                                                                                 90/144
  Verifying        : libssh-config-0.10.4-17.el9_7.noarch                                                                                                                          91/144
  Verifying        : libssh-config-0.10.4-15.el9_7.noarch                                                                                                                          92/144
  Verifying        : libuuid-2.37.4-21.el9_7.x86_64                                                                                                                                93/144
  Verifying        : libuuid-2.37.4-21.el9.x86_64                                                                                                                                  94/144
  Verifying        : libwbclient-4.22.4-18.el9_7.x86_64                                                                                                                            95/144
  Verifying        : libwbclient-4.22.4-6.el9_7.x86_64                                                                                                                             96/144
  Verifying        : microcode_ctl-4:20250812-1.20251111.1.el9_7.noarch                                                                                                            97/144
  Verifying        : microcode_ctl-4:20250812-1.el9.noarch                                                                                                                         98/144
  Verifying        : nfs-utils-1:2.5.4-38.el9_7.3.x86_64                                                                                                                           99/144
  Verifying        : nfs-utils-1:2.5.4-38.el9.x86_64                                                                                                                              100/144
  Verifying        : openssh-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                         101/144
  Verifying        : openssh-8.7p1-46.el9.alma.1.x86_64                                                                                                                           102/144
  Verifying        : openssh-clients-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                 103/144
  Verifying        : openssh-clients-8.7p1-46.el9.alma.1.x86_64                                                                                                                   104/144
  Verifying        : openssh-server-8.7p1-47.el9_7.alma.1.x86_64                                                                                                                  105/144
  Verifying        : openssh-server-8.7p1-46.el9.alma.1.x86_64                                                                                                                    106/144
  Verifying        : openssl-1:3.5.1-7.el9_7.x86_64                                                                                                                               107/144
  Verifying        : openssl-1:3.5.1-4.el9_7.x86_64                                                                                                                               108/144
  Verifying        : openssl-fips-provider-1:3.5.1-7.el9_7.x86_64                                                                                                                 109/144
  Verifying        : openssl-fips-provider-1:3.5.1-4.el9_7.x86_64                                                                                                                 110/144
  Verifying        : openssl-libs-1:3.5.1-7.el9_7.x86_64                                                                                                                          111/144
  Verifying        : openssl-libs-1:3.5.1-4.el9_7.x86_64                                                                                                                          112/144
  Verifying        : python3-3.9.25-3.el9_7.1.x86_64                                                                                                                              113/144
  Verifying        : python3-3.9.23-2.el9.x86_64                                                                                                                                  114/144
  Verifying        : python3-hawkey-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                 115/144
  Verifying        : python3-hawkey-0.69.0-16.el9.alma.1.x86_64                                                                                                                   116/144
  Verifying        : python3-libdnf-0.69.0-17.el9_7.alma.1.x86_64                                                                                                                 117/144
  Verifying        : python3-libdnf-0.69.0-16.el9.alma.1.x86_64                                                                                                                   118/144
  Verifying        : python3-libs-3.9.25-3.el9_7.1.x86_64                                                                                                                         119/144
  Verifying        : python3-libs-3.9.23-2.el9.x86_64                                                                                                                             120/144
  Verifying        : python3-urllib3-1.26.5-6.el9_7.1.noarch                                                                                                                      121/144
  Verifying        : python3-urllib3-1.26.5-6.el9.noarch                                                                                                                          122/144
  Verifying        : samba-client-libs-4.22.4-18.el9_7.x86_64                                                                                                                     123/144
  Verifying        : samba-client-libs-4.22.4-6.el9_7.x86_64                                                                                                                      124/144
  Verifying        : samba-common-4.22.4-18.el9_7.noarch                                                                                                                          125/144
  Verifying        : samba-common-4.22.4-6.el9_7.noarch                                                                                                                           126/144
  Verifying        : samba-common-libs-4.22.4-18.el9_7.x86_64                                                                                                                     127/144
  Verifying        : samba-common-libs-4.22.4-6.el9_7.x86_64                                                                                                                      128/144
  Verifying        : selinux-policy-38.1.65-1.el9_7.1.noarch                                                                                                                      129/144
  Verifying        : selinux-policy-38.1.65-1.el9.noarch                                                                                                                          130/144
  Verifying        : selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                                                                                                             131/144
  Verifying        : selinux-policy-targeted-38.1.65-1.el9.noarch                                                                                                                 132/144
  Verifying        : shim-x64-16.1-5.el9.alma.1.x86_64                                                                                                                            133/144
  Verifying        : shim-x64-15.8-4.el9_3.alma.2.x86_64                                                                                                                          134/144
  Verifying        : sos-4.10.2-2.el9_7.noarch                                                                                                                                    135/144
  Verifying        : sos-4.10.0-4.el9_7.noarch                                                                                                                                    136/144
  Verifying        : tar-2:1.34-9.el9_7.x86_64                                                                                                                                    137/144
  Verifying        : tar-2:1.34-7.el9.x86_64                                                                                                                                      138/144
  Verifying        : tzdata-2026a-1.el9.noarch                                                                                                                                    139/144
  Verifying        : tzdata-2025b-2.el9.noarch                                                                                                                                    140/144
  Verifying        : util-linux-2.37.4-21.el9_7.x86_64                                                                                                                            141/144
  Verifying        : util-linux-2.37.4-21.el9.x86_64                                                                                                                              142/144
  Verifying        : util-linux-core-2.37.4-21.el9_7.x86_64                                                                                                                       143/144
  Verifying        : util-linux-core-2.37.4-21.el9.x86_64                                                                                                                         144/144

Upgraded:
  WALinuxAgent-2.13.1.1-3.el9_7.2.noarch                            WALinuxAgent-udev-2.13.1.1-3.el9_7.2.noarch                  binutils-2.35.2-67.el9_7.1.x86_64
  binutils-gold-2.35.2-67.el9_7.1.x86_64                            cloud-init-24.4-7.el9_7.1.alma.1.noarch                      curl-7.76.1-35.el9_7.3.x86_64
  device-mapper-9:1.02.206-2.el9_7.1.x86_64                         device-mapper-libs-9:1.02.206-2.el9_7.1.x86_64               dracut-057-104.git20250919.el9_7.x86_64
  dracut-config-generic-057-104.git20250919.el9_7.x86_64            dracut-network-057-104.git20250919.el9_7.x86_64              dracut-squash-057-104.git20250919.el9_7.x86_64
  glib2-2.68.4-18.el9_7.1.x86_64                                    glibc-2.34-231.el9_7.10.x86_64                               glibc-common-2.34-231.el9_7.10.x86_64
  glibc-gconv-extra-2.34-231.el9_7.10.x86_64                        glibc-langpack-en-2.34-231.el9_7.10.x86_64                   gnupg2-2.3.3-5.el9_7.x86_64
  gnutls-3.8.3-10.el9_7.x86_64                                      grub2-common-1:2.06-114.el9_7.1.alma.1.noarch                grub2-efi-x64-1:2.06-114.el9_7.1.alma.1.x86_64
  grub2-pc-1:2.06-114.el9_7.1.alma.1.x86_64                         grub2-pc-modules-1:2.06-114.el9_7.1.alma.1.noarch            grub2-tools-1:2.06-114.el9_7.1.alma.1.x86_64
  grub2-tools-minimal-1:2.06-114.el9_7.1.alma.1.x86_64              kernel-tools-5.14.0-611.41.1.el9_7.x86_64                    kernel-tools-libs-5.14.0-611.41.1.el9_7.x86_64
  kpartx-0.8.7-39.el9_7.1.x86_64                                    libarchive-3.5.3-7.el9_7.x86_64                              libblkid-2.37.4-21.el9_7.x86_64
  libbrotli-1.0.9-9.el9_7.x86_64                                    libcurl-7.76.1-35.el9_7.3.x86_64                             libdnf-0.69.0-17.el9_7.alma.1.x86_64
  libfdisk-2.37.4-21.el9_7.x86_64                                   libldb-4.22.4-18.el9_7.x86_64                                libmount-2.37.4-21.el9_7.x86_64
  libnfsidmap-1:2.5.4-38.el9_7.3.x86_64                             libsmartcols-2.37.4-21.el9_7.x86_64                          libssh-0.10.4-17.el9_7.x86_64
  libssh-config-0.10.4-17.el9_7.noarch                              libuuid-2.37.4-21.el9_7.x86_64                               libwbclient-4.22.4-18.el9_7.x86_64
  microcode_ctl-4:20250812-1.20251111.1.el9_7.noarch                nfs-utils-1:2.5.4-38.el9_7.3.x86_64                          openssh-8.7p1-47.el9_7.alma.1.x86_64
  openssh-clients-8.7p1-47.el9_7.alma.1.x86_64                      openssh-server-8.7p1-47.el9_7.alma.1.x86_64                  openssl-1:3.5.1-7.el9_7.x86_64
  openssl-fips-provider-1:3.5.1-7.el9_7.x86_64                      openssl-libs-1:3.5.1-7.el9_7.x86_64                          python3-3.9.25-3.el9_7.1.x86_64
  python3-hawkey-0.69.0-17.el9_7.alma.1.x86_64                      python3-libdnf-0.69.0-17.el9_7.alma.1.x86_64                 python3-libs-3.9.25-3.el9_7.1.x86_64
  python3-pyasn1-0.4.8-7.el9_7.noarch                               python3-urllib3-1.26.5-6.el9_7.1.noarch                      samba-client-libs-4.22.4-18.el9_7.x86_64
  samba-common-4.22.4-18.el9_7.noarch                               samba-common-libs-4.22.4-18.el9_7.x86_64                     selinux-policy-38.1.65-1.el9_7.1.noarch
  selinux-policy-targeted-38.1.65-1.el9_7.1.noarch                  shim-x64-16.1-5.el9.alma.1.x86_64                            sos-4.10.2-2.el9_7.noarch
  tar-2:1.34-9.el9_7.x86_64                                         tzdata-2026a-1.el9.noarch                                    util-linux-2.37.4-21.el9_7.x86_64
  util-linux-core-2.37.4-21.el9_7.x86_64
Installed:
  freetype-2.10.4-10.el9_5.x86_64                                 graphite2-1.3.14-9.el9.x86_64                            grub2-tools-efi-1:2.06-114.el9_7.1.alma.1.x86_64
  grub2-tools-extra-1:2.06-114.el9_7.1.alma.1.x86_64              harfbuzz-2.7.4-10.el9.x86_64                             kernel-5.14.0-611.41.1.el9_7.x86_64
  kernel-core-5.14.0-611.41.1.el9_7.x86_64                        kernel-modules-5.14.0-611.41.1.el9_7.x86_64              kernel-modules-core-5.14.0-611.41.1.el9_7.x86_64
  libpng-2:1.6.37-12.el9_7.2.x86_64

Complete!
[gustave@cloud-tp2-terraform ~]$ sudo dnf install azcopy
Last metadata expiration check: 0:03:58 ago on Tue 24 Mar 2026 07:57:54 AM UTC.
Dependencies resolved.
==========================================================================================================================================================================================
 Package                               Architecture                          Version                                     Repository                                                  Size
==========================================================================================================================================================================================
Installing:
 azcopy                                x86_64                                10.32.2-1                                   packages-microsoft-com-prod                                 22 M

Transaction Summary
==========================================================================================================================================================================================
Install  1 Package

Total download size: 22 M
Installed size: 56 M
Is this ok [y/N]: Y
Downloading Packages:
azcopy-10.32.2-1.x86_64.rpm                                                                                                                                25 MB/s |  22 MB     00:00
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                      25 MB/s |  22 MB     00:00
Microsoft Production                                                                                                                                      960 kB/s | 983  B     00:00
Importing GPG key 0xBE1229CF:
 Userid     : "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
 Fingerprint: BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-Microsoft
Is this ok [y/N]: Y
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                  1/1
  Installing       : azcopy-10.32.2-1.x86_64                                                                                                                                          1/1
  Running scriptlet: azcopy-10.32.2-1.x86_64                                                                                                                                          1/1
  Verifying        : azcopy-10.32.2-1.x86_64                                                                                                                                          1/1

Installed:
  azcopy-10.32.2-1.x86_64

Complete!
[gustave@cloud-tp2-terraform ~]$ azcopy --version
azcopy version 10.32.2
```

- azcopy login
  ```sh
  [gustave@cloud-tp2-terraform ~]$ azcopy login --identity
  INFO: Login with identity succeeded.
  ```

- Ecrire et lire le ficher avec azcopy
```sh
[gustave@cloud-tp2-terraform ~]$
echo "hello LEO you are the man you think you are. You are this fucking guy's " > test.txt
[gustave@cloud-tp2-terraform ~]$ azcopy copy test.txt "https://cloudtp2ciao01.blob.core.windows.net/gustavecontainer/test.txt"
INFO: Autologin not specified.
INFO: Authenticating to destination using Azure AD
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: Scanning...

Job 11892066-5096-0f4f-446f-fda1600b857d has started
Log file is located at: /home/gustave/.azcopy/11892066-5096-0f4f-446f-fda1600b857d.log

100.0 %, 1 Done, 0 Failed, 0 Pending, 0 Skipped, 1 Total, 2-sec Throughput (Mb/s): 0.0003


Job 11892066-5096-0f4f-446f-fda1600b857d summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 1
Number of Folder Property Transfers: 0
Number of Symlink Transfers: 0
Total Number of Transfers: 1
Number of File Transfers Completed: 1
Number of Folder Transfers Completed: 0
Number of File Transfers Failed: 0
Number of Folder Transfers Failed: 0
Number of File Transfers Skipped: 0
Number of Folder Transfers Skipped: 0
Number of Symbolic Links Skipped: 0
Number of Hardlinks Converted: 0
Number of Hardlinks Skipped: 0
Number of Special Files Skipped: 0
Total Number of Bytes Transferred: 73
Final Job Status: Completed

[gustave@cloud-tp2-terraform ~]$ azcopy copy "https://cloudtp2ciao01.blob.core.windows.net/gustavecontainer/test.txt" ./test_download.txt
cat test_download.txt
INFO: Autologin not specified.
INFO: Authenticating to source using Azure AD
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: Scanning...

Job d1b8ec3d-963e-ed4b-7315-8804388a03a4 has started
Log file is located at: /home/gustave/.azcopy/d1b8ec3d-963e-ed4b-7315-8804388a03a4.log

100.0 %, 1 Done, 0 Failed, 0 Pending, 0 Skipped, 1 Total, 2-sec Throughput (Mb/s): 0.0003


Job d1b8ec3d-963e-ed4b-7315-8804388a03a4 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 1
Number of Folder Property Transfers: 0
Number of Symlink Transfers: 0
Total Number of Transfers: 1
Number of File Transfers Completed: 1
Number of Folder Transfers Completed: 0
Number of File Transfers Failed: 0
Number of Folder Transfers Failed: 0
Number of File Transfers Skipped: 0
Number of Folder Transfers Skipped: 0
Number of Symbolic Links Skipped: 0
Number of Hardlinks Converted: 0
Number of Hardlinks Skipped: 0
Number of Special Files Skipped: 0
Total Number of Bytes Transferred: 73
Final Job Status: Completed

hello LEO you are the man you think you are. You are this fucking guy's
[gustave@cloud-tp2-terraform ~]$
```

🌞 Déterminez comment azcopy login --identity vous a authentifié
```sh
La VM contacte le metadata endpoint interne d'Azure pour récupérer le token (le fameux JWT) signé par Azure AD, qui contient mon identité et mes droits. azcopy l'utilise donc directement pour s'auth sur le Storage Account, zéro mot de passe recquis , et on se co aisément.
```

🌞 Requêtez un JWT d'authentification auprès du service que vous venez d'identifier, manuellement
```sh[gustave@cloud-tp2-terraform ~]$ curl -s -H "Metadata:true" \
  "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://storage.azure.com/"
{"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlFaZ045SHFOa0dORU00R2VLY3pEMDJQY1Z2NCIsImtpZCI6IlFaZ045SHFOa0dORU00R2VLY3pEMDJQY1Z2NCJ9.eyJhdWQiOiJodHRwczovL3N0b3JhZ2UuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzQxMzYwMGNmLWJkNGUtNGM3Yy04YTYxLTY5ZTczY2RkZjczMS8iLCJpYXQiOjE3NzQzNDAyMDEsIm5iZiI6MTc3NDM0MDIwMSwiZXhwIjoxNzc0NDI2OTAxLCJhaW8iOiJrMlpnWUpCWHJhMFZjVTJ0bXYvNS91UE4yMUpxTmhzYUJacmZubXRoc3FOdDA4T0U5ZmtBIiwiYXBwaWQiOiI3NDg5NjZiMC1hYmJhLTRhZGQtOTlhNi1iMWRkNGYxODJiOWMiLCJhcHBpZGFjciI6IjIiLCJpZHAiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC80MTM2MDBjZi1iZDRlLTRjN2MtOGE2MS02OWU3M2NkZGY3MzEvIiwiaWR0eXAiOiJhcHAiLCJvaWQiOiJjMTgzMTIzYi1mMGM5LTQ5ZmMtOTYyMy1kOWQ2YzhhOWM4NjkiLCJyaCI6IjEuQVRzQXp3QTJRVTY5ZkV5S1lXbm5QTjMzTVlHbUJ1VFU4NmhDa0xiQ3NDbEpldkVBQUFBN0FBLiIsInN1YiI6ImMxODMxMjNiLWYwYzktNDlmYy05NjIzLWQ5ZDZjOGE5Yzg2OSIsInRpZCI6IjQxMzYwMGNmLWJkNGUtNGM3Yy04YTYxLTY5ZTczY2RkZjczMSIsInV0aSI6IkttSDlfUG1OaDB5Q3pobEhPaHRHQUEiLCJ2ZXIiOiIxLjAiLCJ4bXNfYWNiIjpbImhDMGdkd2RjcmtUMVFpQlMvcld3bCs2OUp2OUpHMWp0K054Q2VwMzhqTGs9Il0sInhtc19hY3RfZmN0IjoiMyA5IiwieG1zX2Z0ZCI6InkzVURRdW9kVDRYR0JFTUVISVZWbDh5X0F3SmJuaFQ1N0JxS0J2X3FQWFFCYzNCaGFXNWpMV1J6YlhNIiwieG1zX2lkcmVsIjoiMTAgNyIsInhtc19taXJpZCI6Ii9zdWJzY3JpcHRpb25zL2YyNzYwMDU4LWE0OTQtNDhlYS1iYjFhLTJjN2U3ZTY3YTU3Mi9yZXNvdXJjZWdyb3Vwcy9jbG91ZC10cDItdGVycmFmb3JtX2dyb3VwL3Byb3ZpZGVycy9NaWNyb3NvZnQuQ29tcHV0ZS92aXJ0dWFsTWFjaGluZXMvY2xvdWQtdHAyLXRlcnJhZm9ybSIsInhtc19yZCI6IjAuNDJMbFlCSml0QllTNGVBVUVsRHA5YlZidWUyMjc2UXY2Ym95bWsxNlFGRU9JWUhHWld4UHJueGU0VFJoMjZFTm1wNVZINEdpM0VJQ3RTS05wN2hlWkt3by1TTDgwTXZKYWdrQSIsInhtc19zdWJfZmN0IjoiOSAzIiwieG1zX3RkYnIiOiJFVSJ9.BiNopuB5l0pbXg-D3QDkaA-3ptGNzSnyspDT4vPmSHIGnaE927H370yBbxHDd4oLlT3igs4ZQCtq4a7rp80RGXMv2wJYtYCrwF5O1Q6EurjpNGy1VX6eaG_gl3wAwUdR51N6wlUurud3h8FqNTxgBg0L6428GbEq5U5Pcxb-88jQFMwnQbNmG1jWfKyxm2Oq95QBFs3RrJRzQlPGiEWpxMCCvl1IqAbQhBSULEDC12VjvUNlD62O50rhsEo6EfMXhM2MZmMbloP08dtSmnQSuYSvkrd3-Ux6uXAIFQbq1W_VYVNlUuo4AZ7nhDBKKyqxh28V73oGHyn8_sdsTJxZRQ","client_id":"748966b0-abba-4add-99a6-b1dd4f182b9c","expires_in":"86400","expires_on":"1774426901","ext_expires_in":"86399","not_before":"1774340201","resource":"https://storage.azure.com/","token_type":"Bearer"}[gustave@cloud-tp2-terraform ~]$
```

🌞 Expliquez comment l'IP 169.254.169.254 peut être joignable
```sh
C'est une adresse link-local (169.254.0.0/16), non routable sur internet, uniquement accessible localement. Azure l'utilise pour exposer l'Instance Metadata Service directement au niveau de l'hyperviseur — la VM peut donc la joindre sans aucune config réseau particulière.
```



  

