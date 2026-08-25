# Linux Verzeichnisstruktur – Nachschlagewerk

Dieses Dokument dient als Referenz für die wichtigsten Ordner in einem Linux-System gemäß dem
[Filesystem Hierarchy Standard (FHS)](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html).
Es hilft dabei, sich schnell zu orientieren, welche Datei wo abgelegt wird bzw. abgelegt werden sollte.

## Übersicht (Wurzelverzeichnis `/`)

| Ordner   | Bedeutung / Zweck |
|----------|-------------------|
| `/`      | Wurzelverzeichnis. Ausgangspunkt der gesamten Verzeichnisstruktur, alles hängt hier drunter. |
| `/bin`   | Essentielle Programme (Binaries) für alle Benutzer, z. B. `ls`, `cp`, `mv`, `cat`. Wird oft als Symlink auf `/usr/bin` geführt (moderne Distributionen). |
| `/sbin`  | Essentielle System-Binaries für die Systemadministration (z. B. `fdisk`, `reboot`, `ifconfig`), meist nur für `root` nutzbar. Oft Symlink auf `/usr/sbin`. |
| `/boot`  | Dateien, die für den Bootvorgang benötigt werden: Kernel-Images (`vmlinuz`), initrd/initramfs, Bootloader-Konfiguration (GRUB). |
| `/dev`   | Gerätedateien (Device Files). Repräsentiert Hardware und virtuelle Geräte als Dateien, z. B. `/dev/sda`, `/dev/null`, `/dev/tty`. |
| `/etc`   | Systemweite Konfigurationsdateien (statisch, nicht ausführbar), z. B. `/etc/passwd`, `/etc/fstab`, `/etc/hosts`, Netzwerk- und Dienstkonfigurationen. |
| `/home`  | Persönliche Home-Verzeichnisse der normalen Benutzer, z. B. `/home/phil`. |
| `/root`  | Home-Verzeichnis des Superusers (`root`), getrennt von `/home` aus historischen/sicherheitstechnischen Gründen. |
| `/lib`   | Essentielle Shared Libraries für Programme in `/bin` und `/sbin`, sowie Kernel-Module (`/lib/modules`). Oft Symlink auf `/usr/lib`. |
| `/lib64` | 64-Bit-Variante von `/lib` auf Multi-Arch-Systemen. |
| `/media` | Automatisch eingehängte Wechseldatenträger (USB-Sticks, CDs, externe Festplatten). |
| `/mnt`   | Temporärer Einhängepunkt für manuell gemountete Dateisysteme (z. B. Netzlaufwerke, zusätzliche Partitionen). |
| `/opt`   | Optionale/zusätzliche Software von Drittanbietern, die nicht über den Paketmanager der Distribution verwaltet wird (eigene Verzeichnisstruktur je Anwendung). |
| `/proc`  | Virtuelles Dateisystem mit Laufzeitinformationen über Kernel und Prozesse (z. B. `/proc/cpuinfo`, `/proc/<PID>/`). Existiert nur im Speicher, nicht auf der Festplatte. |
| `/run`   | Laufzeitdaten seit dem letzten Boot (PID-Dateien, Sockets, temporäre Zustände von Diensten). Volatil, wird bei jedem Neustart geleert (tmpfs). |
| `/srv`   | Daten für Dienste, die dieses System bereitstellt (z. B. Webserver-Daten, FTP-Verzeichnisse). |
| `/sys`   | Virtuelles Dateisystem, das Kernel-Objekte und Gerätetreiber-Informationen abbildet (moderneres Pendant/Ergänzung zu `/proc`). |
| `/tmp`   | Temporäre Dateien, die von Anwendungen oder Benutzern erzeugt werden. Wird häufig beim Neustart geleert. |
| `/usr`   | "Unix System Resources" – der größte Teil des Systems: Anwendungen, Bibliotheken, Dokumentationen für Benutzerprogramme (read-only, teilbar zwischen Hosts). |
| `/var`   | Variable Daten, die sich zur Laufzeit ändern: Logs, Caches, Spool-Verzeichnisse, Datenbanken. |

## Details zu wichtigen Unterordnern

### `/usr` – Benutzerprogramme und Ressourcen
| Ordner            | Bedeutung |
|-------------------|-----------|
| `/usr/bin`        | Ausführbare Programme für alle Benutzer (Hauptteil der Kommandozeilentools). |
| `/usr/sbin`       | Systemadministrations-Programme, nicht essentiell für den Boot-Prozess. |
| `/usr/lib`        | Bibliotheken für Programme in `/usr/bin` und `/usr/sbin`. |
| `/usr/local`      | Lokal installierte Software, die nicht Teil der Distribution ist (eigene Kompilate, manuell installierte Tools). Hat eigene Unterstruktur (`bin`, `lib`, `etc`, ...). |
| `/usr/share`      | Architekturunabhängige, gemeinsam genutzte Daten: Dokumentation, Icons, Man-Pages, Zeitzonendaten. |
| `/usr/include`    | Header-Dateien (`.h`) für die C/C++-Entwicklung. |
| `/usr/src`        | Quellcode, z. B. Kernel-Quellen. |

### `/var` – Variable Daten
| Ordner              | Bedeutung |
|---------------------|-----------|
| `/var/log`          | Log-Dateien des Systems und von Anwendungen (z. B. `syslog`, `auth.log`, `dmesg`). |
| `/var/cache`        | Zwischengespeicherte Daten von Anwendungen zur Beschleunigung (z. B. Paketmanager-Cache). |
| `/var/lib`          | Persistente Zustandsdaten von Anwendungen (z. B. Datenbanken unter `/var/lib/mysql`, Paketverwaltung unter `/var/lib/dpkg`). |
| `/var/spool`        | Warteschlangen-Daten für später zu verarbeitende Aufgaben (Druckaufträge, Mails, Cron-Jobs). |
| `/var/run`          | Historischer Ort für Laufzeitdaten, heute meist Symlink auf `/run`. |
| `/var/tmp`          | Temporäre Dateien, die einen Neustart überdauern sollen (im Gegensatz zu `/tmp`). |
| `/var/www`          | Häufig genutzter (nicht FHS-standardisierter, aber weit verbreiteter) Speicherort für Webserver-Inhalte (Apache/Nginx). |

### `/etc` – Konfiguration
| Ordner/Datei              | Bedeutung |
|----------------------------|-----------|
| `/etc/passwd`             | Liste der Benutzerkonten (Name, UID, GID, Home-Verzeichnis, Shell). |
| `/etc/shadow`             | Verschlüsselte Passwörter der Benutzer (nur root-lesbar). |
| `/etc/group`              | Gruppendefinitionen. |
| `/etc/fstab`              | Statische Informationen über Dateisysteme, die beim Boot gemountet werden. |
| `/etc/hosts`              | Statische Zuordnung von Hostnamen zu IP-Adressen. |
| `/etc/network/` bzw. `/etc/netplan/` | Netzwerkkonfiguration (distributionsabhängig). |
| `/etc/systemd/`           | Konfiguration von systemd-Units und -Diensten. |
| `/etc/cron.d/`, `/etc/crontab` | Geplante Aufgaben (Cron-Jobs). |
| `/etc/sudoers`            | Konfiguration, welche Benutzer `sudo`-Rechte haben. |

### `/proc` – Virtuelles Prozess-Dateisystem (Auswahl)
| Pfad                  | Bedeutung |
|-----------------------|-----------|
| `/proc/cpuinfo`      | Informationen zur CPU. |
| `/proc/meminfo`      | Informationen zum Arbeitsspeicher. |
| `/proc/version`      | Kernel-Version. |
| `/proc/<PID>/`       | Informationen zu einem laufenden Prozess (z. B. `cmdline`, `status`, `fd/`). |
| `/proc/mounts`       | Aktuell eingehängte Dateisysteme. |

## Wichtige Konzepte

- **FHS (Filesystem Hierarchy Standard):** Standardisiert die Struktur, damit Software distributionsübergreifend funktioniert und vorhersehbare Pfade nutzt.
- **Virtuelle Dateisysteme:** `/proc` und `/sys` existieren nur im RAM und spiegeln Kernel-/Hardwarezustand wider – sie belegen keinen Speicherplatz auf der Festplatte.
- **tmpfs:** `/run` (und teils `/tmp`) werden im Arbeitsspeicher gehalten und gehen bei einem Neustart verloren.
- **Symlink-Vereinheitlichung (usrmerge):** Viele moderne Distributionen (z. B. Fedora, Arch, neuere Debian/Ubuntu) haben `/bin`, `/sbin`, `/lib` als Symlinks auf die jeweiligen `/usr`-Pendants zusammengeführt.
- **Trennung von statischen und variablen Daten:** `/usr` enthält meist unveränderliche, teilbare Daten; `/var` enthält Daten, die sich zur Laufzeit ändern (Logs, Caches, Datenbanken).
- **Trennung von Konfiguration und Programm:** Konfigurationsdateien liegen in `/etc`, die zugehörigen Programme in `/usr/bin` bzw. `/usr/sbin`.

## Schnellreferenz: "Wo finde ich...?"

| Frage | Antwort |
|-------|---------|
| Wo liegen Logs? | `/var/log` |
| Wo liegt die Konfiguration eines Dienstes? | `/etc/<dienstname>/` |
| Wo installiere ich manuell kompilierte Software? | `/usr/local` oder `/opt` |
| Wo liegen Kernel und Bootloader? | `/boot` |
| Wo finde ich Informationen zu laufenden Prozessen? | `/proc/<PID>/` |
| Wo werden USB-Sticks eingehängt? | `/media` oder `/mnt` |
| Wo liegen temporäre Dateien? | `/tmp` (flüchtig) oder `/var/tmp` (persistenter) |
| Wo liegen Benutzerdaten? | `/home/<benutzername>` |
| Wo liegen Gerätedateien? | `/dev` |

---
*Quelle: Filesystem Hierarchy Standard (FHS) 3.0, ergänzt um praxisübliche Konventionen gängiger Linux-Distributionen (Debian/Ubuntu, RHEL/Fedora, Arch).*

