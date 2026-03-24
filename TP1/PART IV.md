# Part IV : Docker security

## 1. Le groupe docker

🌞 Prouvez que vous pouvez devenir root

```sh
gustave@debian:~$ docker run --rm -v /etc/shadow:/etc/shadow alpine cat /etc/shadow
root:$y$j9T$oNuMQl2OPa9/Ni38nQKeG1$41677U5BmsiyrXy7rmoLJ29lqzBWu64UbYc7jW9lUy1:20531:0:99999:7:::
daemon:*:20531:0:99999:7:::
bin:*:20531:0:99999:7:::
sys:*:20531:0:99999:7:::
sync:*:20531:0:99999:7:::
games:*:20531:0:99999:7:::
man:*:20531:0:99999:7:::
lp:*:20531:0:99999:7:::
mail:*:20531:0:99999:7:::
news:*:20531:0:99999:7:::
uucp:*:20531:0:99999:7:::
proxy:*:20531:0:99999:7:::
www-data:*:20531:0:99999:7:::
backup:*:20531:0:99999:7:::
list:*:20531:0:99999:7:::
irc:*:20531:0:99999:7:::
_apt:*:20531:0:99999:7:::
nobody:*:20531:0:99999:7:::
systemd-network:!*:20531:::::1:
dhcpcd:!:20531::::::
tss:!:20531::::::
systemd-timesync:!*:20531:::::1:
messagebus:!*:20531::::::
sshd:!*:20531::::::
dnsmasq:!:20531::::::
avahi:!:20531::::::
speech-dispatcher:!:20531::::::
usbmux:!:20531::::::
cups-pk-helper:!:20531::::::
fwupd-refresh:!*:20531::::::
geoclue:!:20531::::::
gnome-remote-desktop:!*:20531::::::
saned:!:20531::::::
polkitd:!*:20531::::::
rtkit:!:20531::::::
colord:!:20531::::::
Debian-gdm:!:20531::::::
gustave:$y$j9T$361DRAIb7ZIPNHh9iVpJO0$7YxzowLI2Q4P2WNUsVvS22svP3nrMw0x7IyEQufVqJ9:20531:0:99999:7:::
gustave@debian:~$
```

# 2. Scan de vuln

🌞 Utilisez Trivy

```sh
gustave@debian:~$ sudo apt install wget gnupg -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee /etc/apt/sources.list.d/trivy.list
sudo apt update && sudo apt install trivy -y
[sudo] Mot de passe de gustave :
wget est déjà la version la plus récente (1.25.0-2).
gnupg est déjà la version la plus récente (2.4.7-21+deb13u1).
Sommaire :
  Mise à niveau de : 0. Installation de : 0Supprimé : 0. Non mis à jour : 4
deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main
Atteint : 1 http://security.debian.org/debian-security trixie-security InRelease
Atteint : 2 http://deb.debian.org/debian trixie InRelease
Réception de : 3 http://deb.debian.org/debian trixie-updates InRelease [47,3 kB]
Réception de : 4 https://download.docker.com/linux/debian trixie InRelease [32,5 kB]
Atteint : 5 https://aquasecurity.github.io/trivy-repo/deb generic InRelease
Réception de : 6 https://download.docker.com/linux/debian trixie/stable amd64 Packages [29,3 kB]
109 ko réceptionnés en 1s (189 ko/s)
5 paquets peuvent être mis à jour. Exécutez « apt list --upgradable » pour les voir.
trivy est déjà la version la plus récente (0.69.3).
Sommaire :
  Mise à niveau de : 0. Installation de : 0Supprimé : 0. Non mis à jour : 5
gustave@debian:~$
```

# 2. Scan de vuln

🌞 Utilisez Trivy

-celle de WikiJS
```sh
gustave@debian:~$ # Affiche uniquement le tableau récapitulatif, sans les détails
trivy image --severity HIGH,CRITICAL --format table --quiet ghcr.io/requarks/wiki:2 2>/dev/null | tail -20
│ undici (package.json)                  │ CVE-2026-1526       │          │          │ 6.23.0            │ 6.24.0, 7.24.0                                          │ undici: undici: Denial of Service via unbounded memory       │
│                                        │                     │          │          │                   │                                                         │ consumption during WebSocket permessage-deflate...           │
│                                        │                     │          │          │                   │                                                         │ https://avd.aquasec.com/nvd/cve-2026-1526                    │
│                                        ├─────────────────────┤          │          │                   │                                                         ├──────────────────────────────────────────────────────────────┤
│                                        │ CVE-2026-1528       │          │          │                   │                                                         │ undici: undici: Denial of Service via crafted WebSocket      │
│                                        │                     │          │          │                   │                                                         │ frame with large length...                                   │
│                                        │                     │          │          │                   │                                                         │ https://avd.aquasec.com/nvd/cve-2026-1528                    │
│                                        ├─────────────────────┤          │          │                   │                                                         ├──────────────────────────────────────────────────────────────┤
│                                        │ CVE-2026-2229       │          │          │                   │                                                         │ undici: Undici: Denial of Service via invalid WebSocket      │
│                                        │                     │          │          │                   │                                                         │ permessage-deflate extension parameter                       │
│                                        │                     │          │          │                   │                                                         │ https://avd.aquasec.com/nvd/cve-2026-2229                    │
├────────────────────────────────────────┼─────────────────────┤          │          ├───────────────────┼─────────────────────────────────────────────────────────┼──────────────────────────────────────────────────────────────┤
│ ws (package.json)                      │ CVE-2024-37890      │          │          │ 7.4.5             │ 5.2.4, 6.2.3, 7.5.10, 8.17.1                            │ nodejs-ws: denial of service when handling a request with    │
│                                        │                     │          │          │                   │                                                         │ many HTTP headers...                                         │
│                                        │                     │          │          │                   │                                                         │ https://avd.aquasec.com/nvd/cve-2024-37890                   │
│                                        │                     │          │          │                   │                                                         │                                                              │
│                                        │                     │          │          │                   │                                                         │                                                              │
│                                        │                     │          │          │                   │                                                         │                                                              │
│                                        │                     │          │          │                   │                                                         │                                                              │
└────────────────────────────────────────┴─────────────────────┴──────────┴──────────┴───────────────────┴─────────────────────────────────────────────────────────┴──────────────────────────────────────────────────────────────┘
gustave@debian:~$

```
- Base de données

```sh
gustave@debian:~$ trivy image --severity HIGH,CRITICAL --format table --quiet postgres:15-alpine 2>/dev/null | tail -20
│         ├────────────────┼──────────┤        │                   ├──────────────────────────────┼──────────────────────────────────────────────────────────────┤
│         │ CVE-2025-58183 │ HIGH     │        │                   │ 1.24.8, 1.25.2               │ golang: archive/tar: Unbounded allocation when parsing GNU   │
│         │                │          │        │                   │                              │ sparse map                                                   │
│         │                │          │        │                   │                              │ https://avd.aquasec.com/nvd/cve-2025-58183                   │
│         ├────────────────┤          │        │                   ├──────────────────────────────┼──────────────────────────────────────────────────────────────┤
│         │ CVE-2025-61726 │          │        │                   │ 1.24.12, 1.25.6              │ golang: net/url: Memory exhaustion in query parameter        │
│         │                │          │        │                   │                              │ parsing in net/url                                           │
│         │                │          │        │                   │                              │ https://avd.aquasec.com/nvd/cve-2025-61726                   │
│         ├────────────────┤          │        │                   │                              ├──────────────────────────────────────────────────────────────┤
│         │ CVE-2025-61728 │          │        │                   │                              │ golang: archive/zip: Excessive CPU consumption when building │
│         │                │          │        │                   │                              │ archive index in archive/zip                                 │
│         │                │          │        │                   │                              │ https://avd.aquasec.com/nvd/cve-2025-61728                   │
│         ├────────────────┤          │        │                   ├──────────────────────────────┼──────────────────────────────────────────────────────────────┤
│         │ CVE-2025-61729 │          │        │                   │ 1.24.11, 1.25.5              │ crypto/x509: golang: Denial of Service due to excessive      │
│         │                │          │        │                   │                              │ resource consumption via crafted...                          │
│         │                │          │        │                   │                              │ https://avd.aquasec.com/nvd/cve-2025-61729                   │
│         ├────────────────┤          │        │                   ├──────────────────────────────┼──────────────────────────────────────────────────────────────┤
│         │ CVE-2026-25679 │          │        │                   │ 1.25.8, 1.26.1               │ net/url: Incorrect parsing of IPv6 host literals in net/url  │
│         │                │          │        │                   │                              │ https://avd.aquasec.com/nvd/cve-2026-25679                   │
└─────────┴────────────────┴──────────┴────────┴───────────────────┴──────────────────────────────┴──────────────────────────────────────────────────────────────┘
gustave@debian:~$
```

-Image Nginx
```sh
gustave@debian:~$ trivy image --scanners vuln --vuln-type os --severity LOW,MEDIUM,HIGH,CRITICAL --format table nginx:latest
2026-03-20T12:51:21+01:00       WARN    '--vuln-type' is deprecated. Use '--pkg-types' instead.
2026-03-20T12:51:21+01:00       INFO    [vuln] Vulnerability scanning is enabled
2026-03-20T12:51:27+01:00       INFO    Detected OS     family="debian" version="13.4"
2026-03-20T12:51:27+01:00       INFO    [debian] Detecting vulnerabilities...   os_version="13" pkg_num=151
2026-03-20T12:51:28+01:00       WARN    Using severities from other vendors for some vulnerabilities. Read https://trivy.dev/docs/v0.69/guide/scanner/vulnerability#severity-selection for details.

Report Summary

┌────────────────────────────┬────────┬─────────────────┐
│           Target           │  Type  │ Vulnerabilities │
├────────────────────────────┼────────┼─────────────────┤
│ nginx:latest (debian 13.4) │ debian │       154       │
└────────────────────────────┴────────┴─────────────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)


nginx:latest (debian 13.4)

Total: 154 (LOW: 126, MEDIUM: 24, HIGH: 4, CRITICAL: 0)

┌─────────────────────────┬─────────────────────┬──────────┬──────────────┬──────────────────────────────────────┬───────────────────────┬──────────────────────────────────────────────────────────────┐
│         Library         │    Vulnerability    │ Severity │    Status    │          Installed Version           │     Fixed Version     │                            Title                             │
├─────────────────────────┼─────────────────────┼──────────┼──────────────┼──────────────────────────────────────┼───────────────────────┼──────────────────────────────────────────────────────────────┤
│ apt                     │ CVE-2011-3374       │ LOW      │ affected     │ 3.0.3                                │                       │ It was found that apt-key in apt, all versions, do not       │
│                         │                     │          │              │                                      │                       │ correctly...                                                 │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2011-3374                    │
├─────────────────────────┼─────────────────────┤          │              ├──────────────────────────────────────┼───────────────────────┼──────────────────────────────────────────────────────────────┤
│ bash                    │ TEMP-0841856-B18BAF │          │              │ 5.2.37-2+b8                          │                       │ [Privilege escalation possible to other user than root]      │
│                         │                     │          │              │                                      │                       │ https://security-tracker.debian.org/tracker/TEMP-0841856-B1- │
│                         │                     │          │              │                                      │                       │ 8BAF                                                         │
├─────────────────────────┼─────────────────────┤          │              ├──────────────────────────────────────┼───────────────────────┼──────────────────────────────────────────────────────────────┤
│ bsdutils                │ CVE-2022-0563       │          │              │ 1:2.41-5                             │                       │ util-linux: partial disclosure of arbitrary files in chfn    │
│                         │                     │          │              │                                      │                       │ and chsh when compiled...                                    │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2025-14104      │          │              │                                      │                       │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                         │                     │          │              │                                      │                       │ when processing 256-byte usernames                           │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2026-3184       │          │              │                                      │                       │ util-linux: util-linux: Access control bypass due to         │
│                         │                     │          │              │                                      │                       │ improper hostname canonicalization                           │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2026-3184                    │
├─────────────────────────┼─────────────────────┤          │              ├──────────────────────────────────────┼───────────────────────┼──────────────────────────────────────────────────────────────┤
│ coreutils               │ CVE-2017-18018      │          │              │ 9.7-3                                │                       │ coreutils: race condition vulnerability in chown and chgrp   │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2017-18018                   │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2025-5278       │          │              │                                      │                       │ coreutils: Heap Buffer Under-Read in GNU Coreutils sort via  │
│                         │                     │          │              │                                      │                       │ Key Specification                                            │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2025-5278                    │
├─────────────────────────┼─────────────────────┼──────────┤              ├──────────────────────────────────────┼───────────────────────┼──────────────────────────────────────────────────────────────┤
│ curl                    │ CVE-2025-13034      │ MEDIUM   │              │ 8.14.1-2+deb13u2                     │                       │ When using `CURLOPT_PINNEDPUBLICKEY` option with libcurl or  │
│                         │                     │          │              │                                      │                       │ `--pinnedp ...                                               │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2025-13034                   │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2026-1965       │          │              │                                      │                       │ curl: curl: Authentication bypass due to incorrect           │
│                         │                     │          │              │                                      │                       │ connection reuse with Negotiate authentication...            │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2026-1965                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2026-3783       │          │              │                                      │                       │ curl: curl: Information disclosure via OAuth2 bearer token   │
│                         │                     │          │              │                                      │                       │ leakage during HTTP(S) redirect...                           │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2026-3783                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2026-3784       │          │              │                                      │                       │ curl: curl: Unauthorized access due to improper HTTP proxy   │
│                         │                     │          │              │                                      │                       │ connection reuse                                             │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2026-3784                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2026-3805       │          │              │                                      │                       │ curl: curl: Arbitrary code execution or Denial of Service    │
│                         │                     │          │              │                                      │                       │ via use-after-free in...                                     │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2026-3805                    │
│                         ├─────────────────────┼──────────┤              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2025-10966      │ LOW      │              │                                      │                       │ curl: Curl missing SFTP host verification with wolfSSH       │
│                         │                     │          │              │                                      │                       │ backend                                                      │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2025-10966                   │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2025-14017      │          │              │                                      │                       │ curl: curl: Security bypass due to global TLS option changes │
│                         │                     │          │              │                                      │                       │ in multi-threaded...                                         │
│                         │                     │          │              │                                      │                       │ https://avd.aquasec.com/nvd/cve-2025-14017                   │
│                         ├─────────────────────┤          │              │                                      ├───────────────────────┼────────────────────────────────────────────────────

```

-Image Apache

```sh
gustave@debian:~$ trivy image --scanners vuln --vuln-type os --severity LOW,MEDIUM,HIGH,CRITICAL --format table my_apache:latest
2026-03-20T12:53:32+01:00       WARN    '--vuln-type' is deprecated. Use '--pkg-types' instead.
2026-03-20T12:53:32+01:00       INFO    [vuln] Vulnerability scanning is enabled
2026-03-20T12:53:51+01:00       INFO    Detected OS     family="debian" version="13.4"
2026-03-20T12:53:51+01:00       INFO    [debian] Detecting vulnerabilities...   os_version="13" pkg_num=133
2026-03-20T12:53:51+01:00       WARN    Using severities from other vendors for some vulnerabilities. Read https://trivy.dev/docs/v0.69/guide/scanner/vulnerability#severity-selection for details.

Report Summary

┌────────────────────────────────┬────────┬─────────────────┐
│             Target             │  Type  │ Vulnerabilities │
├────────────────────────────────┼────────┼─────────────────┤
│ my_apache:latest (debian 13.4) │ debian │       162       │
└────────────────────────────────┴────────┴─────────────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)


my_apache:latest (debian 13.4)

Total: 162 (LOW: 146, MEDIUM: 15, HIGH: 1, CRITICAL: 0)

┌─────────────────────────┬─────────────────────┬──────────┬──────────────┬──────────────────────────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│         Library         │    Vulnerability    │ Severity │    Status    │          Installed Version           │ Fixed Version │                            Title                             │
├─────────────────────────┼─────────────────────┼──────────┼──────────────┼──────────────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ apache2                 │ CVE-2001-1534       │ LOW      │ affected     │ 2.4.66-1~deb13u2                     │               │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                         │                     │          │              │                                      │               │ session ID's u ...                                           │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1307       │          │              │                                      │               │ The mod_php module for the Apache HTTP Server allows local   │
│                         │                     │          │              │                                      │               │ users with...                                                │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1580       │          │              │                                      │               │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                         │                     │          │              │                                      │               │ enabled for clie...                                          │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1581       │          │              │                                      │               │ httpd: Injection of arbitrary text into log files when DNS   │
│                         │                     │          │              │                                      │               │ resolution is...                                             │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2007-0086       │          │              │                                      │               │ The Apache HTTP Server, when accessed through a TCP          │
│                         │                     │          │              │                                      │               │ connection with a...                                         │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2007-0086                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2007-1743       │          │              │                                      │               │ suexec in Apache HTTP Server (httpd) 2.2.3 does not verify   │
│                         │                     │          │              │                                      │               │ combination ......                                           │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2007-1743                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2007-3303       │          │              │                                      │               │ Apache httpd 2.0.59 and 2.2.4, with the Prefork MPM module,  │
│                         │                     │          │              │                                      │               │ allows loc...                                                │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2007-3303                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2008-0456       │          │              │                                      │               │ httpd: mod_negotiation CRLF injection via untrusted file     │
│                         │                     │          │              │                                      │               │ names in directories with MultiViews...                      │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2008-0456                    │
├─────────────────────────┼─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│ apache2-bin             │ CVE-2001-1534       │          │              │                                      │               │ mod_usertrack in Apache 1.3.11 through 1.3.20 generates      │
│                         │                     │          │              │                                      │               │ session ID's u ...                                           │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2001-1534                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1307       │          │              │                                      │               │ The mod_php module for the Apache HTTP Server allows local   │
│                         │                     │          │              │                                      │               │ users with...                                                │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1307                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1580       │          │              │                                      │               │ The Apache HTTP Server 2.0.44, when DNS resolution is        │
│                         │                     │          │              │                                      │               │ enabled for clie...                                          │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1580                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤
│                         │ CVE-2003-1581       │          │              │                                      │               │ httpd: Injection of arbitrary text into log files when DNS   │
│                         │                     │          │              │                                      │               │ resolution is...                                             │
│                         │                     │          │              │                                      │               │ https://avd.aquasec.com/nvd/cve-2003-1581                    │
│                         ├─────────────────────┤          │              │                                      ├───────────────┼──────────────────────────────────────────────────────────────┤

```









             
