# Unix/Linux Command Overview

Overview of Unix and commands

# Commands

<div id="top"></div>

# Inhaltsverzeichnis

- [1. Navigation & Verzeichnisse](#1-navigation--verzeichnisse)
- [2. Dateien & Links](#2-dateien--links)
- [3. Dateien anzeigen & bearbeiten](#3-dateien-anzeigen--bearbeiten)
- [4. Suchen](#4-suchen)
- [5. Textverarbeitung](#5-textverarbeitung)
- [6. Pipes & Umleitungen](#6-pipes--umleitungen)
- [7. Prozesse](#7-prozesse)
- [8. Benutzer & Rechte](#8-benutzer--rechte)
- [9. Speicher & Systeminformationen](#9-speicher--systeminformationen)
- [10. Netzwerk](#10-netzwerk)
- [11. Archive & Kompression](#11-archive--kompression)
- [12. Pakete verwalten](#12-pakete-verwalten)
- [13. Dienste & systemd](#13-dienste--systemd)
- [14. Shell & Umgebungsvariablen](#14-shell--umgebungsvariablen)
- [15. Hilfe & Dokumentation](#15-hilfe--dokumentation)


# Unix/Linux Commands – Übersicht

## 1. Navigation & Verzeichnisse

| Command | Bedeutung                      | Beispiel      |
| ------- | ------------------------------ | ------------- |
| `pwd`   | Aktuelles Verzeichnis anzeigen | `pwd`         |
| `ls`    | Dateien/Ordner anzeigen        | `ls -la`      |
| `cd`    | Verzeichnis wechseln           | `cd /var/log` |
| `cd ..` | Eine Ebene nach oben           | `cd ..`       |
| `cd ~`  | Home-Verzeichnis               | `cd ~`        |
| `mkdir` | Verzeichnis erstellen          | `mkdir test`  |
| `rmdir` | Leeres Verzeichnis löschen     | `rmdir test`  |
| `tree`  | Verzeichnisbaum anzeigen       | `tree`        |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 2. Dateien & Links

| Command | Bedeutung                     | Beispiel                 |
| ------- | ----------------------------- | ------------------------ |
| `touch` | Datei erstellen/Zeiten ändern | `touch file.txt`         |
| `cp`    | Kopieren                      | `cp file.txt backup.txt` |
| `mv`    | Verschieben/Umbenennen        | `mv old.txt new.txt`     |
| `rm`    | Löschen                       | `rm file.txt`            |
| `rm -r` | Verzeichnis rekursiv löschen  | `rm -r folder`           |
| `file`  | Dateityp erkennen             | `file image.png`         |
| `stat`  | Dateiinformationen anzeigen   | `stat file.txt`          |
| `ln`    | Link erstellen                | `ln -s /path/file link`  |

> ⚠️ `rm -rf`: Es löscht rekursiv und ohne Nachfrage.
 
<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 3. Dateien anzeigen & bearbeiten

| Command   | Bedeutung                      | Beispiel                                                                          |
|-----------|--------------------------------|-----------------------------------------------------------------------------------|
| `cat`     | Datei komplett ausgeben        | `cat file.txt`                                                                    |
| `less`    | Datei seitenweise ansehen      | `less /var/log/syslog`                                                            |
| `more`    | Einfacher Pager                | `more file.txt`                                                                   |
| `head`    | Anfang einer Datei             | `head -n 20 file.txt`                                                             |
| `tail`    | Ende einer Datei               | `tail -n 20 file.txt`                                                             |
| `tail -f` | Datei live verfolgen           | `tail -f app.log`                                                                 |
| `nano`    | Einfacher Editor               | `nano file.txt`                                                                   |
| `vim`     | Leistungsfähiger Editor        | `vim file.txt` - i für Editmode, ESC : wq um vim zu verlassen und Datei speichern |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 4. Suchen

| Command   | Bedeutung                                 | Beispiel                                                                                           |
|-----------|-------------------------------------------|----------------------------------------------------------------------------------------------------|
| `find`    | Dateien suchen                            | `find . -name "*.log"`                                                                             |
| `find`    | Verzeichnisse suchen                      | `find /home -type d -iname "*logs*"` (Hier: nur in /home suchen und mit iname nicht case sensitiv) |
| `locate`  | Schnelle Dateisuche                       | `locate nginx.conf`                                                                                |
| `which`   | Pfad eines Programms anzeigen             | `which python`                                                                                     |
| `whereis` | Programm + Manual finden                  | `whereis bash`                                                                                     |
| `whatis`  | Kurze Beschreibung eines Befehls anzeigen | `whatis bash`                                                                                      |
| `grep`    | Text in Dateien suchen                    | `grep "error" app.log`                                                                             |
| `grep -r` | Rekursiv suchen                           | `grep -r "TODO" .`                                                                                 |

### Praktisches Beispiel

```bash
grep -rin "error" /var/log/
```

* `-r` = rekursiv
* `-i` = Groß-/Kleinschreibung ignorieren
* `-n` = Zeilennummer anzeigen

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 5. Textverarbeitung

| Command | Bedeutung                       | Beispiel                      |
| ------- |---------------------------------|-------------------------------|
| `sort`  | Zeilen sortieren                | `sort names.txt`              |
| `uniq`  | Duplikate entfernen             | `sort names.txt \| uniq`      |
| `wc`    | Zeilen/Wörter/Zeichen zählen    | `wc -l file.txt`              |
| `cut`   | Spalten/Zeichen ausschneiden    | `cut -d: -f1 /etc/passwd`     |
| `tr`    | Zeichen ersetzen oder entfernen | `tr 'a-z' 'A-Z'`              |
| `sed`   | Text bearbeiten/ersetzen        | `sed 's/foo/bar/g' file.txt`  |
| `awk`   | Text/Spalten verarbeiten        | `awk '{print $1}' file.txt`   |
| `diff`  | Dateien zeilenweise vergleichen | `diff file1 file2`            |
| `cmp`   | Dateien byteweise vergleichen   | `cmp file1.txt file2.txt`     |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 6. Pipes & Umleitungen

| Funktion             | Syntax                 | Bedeutung                                                    | Beispiel                    |
| -------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| **Pipe**             | `command1 \| command2` | Ausgabe von `command1` wird Eingabe von `command2`           | `ps aux \| grep nginx`      |
| **Ausgabe umleiten** | `command > file`       | Ausgabe in Datei schreiben, vorhandenen Inhalt überschreiben | `ls > files.txt`            |
| **Ausgabe anhängen** | `command >> file`      | Ausgabe an Datei anhängen                                    | `echo "hello" >> file.txt`  |
| **Eingabe umleiten** | `command < file`       | Eingabe aus Datei lesen                                      | `sort < names.txt`          |
| **Fehler umleiten**  | `command 2> file`      | Fehlermeldungen in Datei schreiben                           | `command 2> errors.txt`     |
| **Ausgabe + Fehler** | `command > out 2>&1`   | Standardausgabe und Fehler in dieselbe Datei schreiben       | `command > output.txt 2>&1` |

### Beispiel

```bash
ps aux | grep nginx
```
Hier wird die Ausgabe von `ps aux` an `grep` weitergegeben.

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 7. Prozesse

| Command   | Bedeutung                               | Beispiel        |
| --------- |-----------------------------------------| --------------- |
| `ps`      | Prozesse anzeigen                       | `ps aux`        |
| `top`     | Prozesse live überwachen                | `top`           |
| `htop`    | Komfortabler Prozessmonitor             | `htop`          |
| `pgrep`   | Prozess nach Name suchen                | `pgrep nginx`   |
| `kill`    | Prozess anhand der PID beenden          | `kill 1234`     |
| `killall` | Prozesse anhand des Namens beenden      | `killall nginx` |
| `jobs`    | Hintergrundjobs anzeigen                | `jobs`          |
| `fg`      | Job in Vordergrund holen                | `fg %1`         |
| `bg`      | Job im Hintergrund fortsetzen           | `bg %1`         |
| `nohup`   | Prozess nach Logout weiterlaufen lassen | `nohup ./app &` |

### Prozess im Hintergrund starten

```bash
./server &
```

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 8. Benutzer & Rechte

| Command   | Bedeutung                          | Beispiel          |
|-----------|------------------------------------|-------------------|
| `whoami`  | Aktuellen Benutzer anzeigen        | `whoami`          |
| `id`      | Benutzer-ID/Gruppen anzeigen       | `id`              |
| `who`     | Angemeldete Benutzer anzeigen      | `who`             |
| `passwd`  | Passwort ändern                    | `passwd userName` |
| `sudo`    | Befehl mit Admin-Rechten ausführen | `sudo command`    |
| `su`      | Benutzer wechseln                  | `su - user`       |
| `groups`  | Gruppen des Benutzers anzeigen     | `groups`          |
| `useradd` | Neuer Benutzer anlegen             | `useradd user1`   |
| `adduser` | Neuer Benutzer interaktiv anlegen  | `adduser user1`   |

### Dateirechte anzeigen

```bash
ls -l
```

Beispiel:

```text
-rwxr-xr--
```

### Rechte ändern

```bash
chmod 755 script.sh
chmod +x script.sh
```

### Besitzer ändern

```bash
chown user:group file.txt
```

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 9. Speicher & Systeminformationen

| Command    | Bedeutung                                  |
| ---------- | ------------------------------------------ |
| `df -h`    | Freien Speicher auf Dateisystemen anzeigen |
| `du -sh`   | Größe eines Verzeichnisses anzeigen        |
| `free -h`  | RAM-Auslastung anzeigen                    |
| `uname -a` | Systeminformationen anzeigen               |
| `hostname` | Rechnernamen anzeigen                      |
| `uptime`   | Laufzeit und Load anzeigen                 |
| `date`     | Datum/Uhrzeit anzeigen                     |
| `lscpu`    | CPU-Informationen anzeigen                 |
| `lsblk`    | Blockgeräte/Datenträger anzeigen           |
| `lsusb`    | USB-Geräte anzeigen                        |
| `dmesg`    | Kernel-Meldungen anzeigen                  |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 10. Netzwerk

| Command      | Bedeutung                               | Beispiel                                        |
|--------------|-----------------------------------------|-------------------------------------------------|
| `ip`         | Netzwerk konfigurieren/anzeigen         | `ip addr`                                       |
| `ping`       | Erreichbarkeit testen                   | `ping 8.8.8.8`                                  |
| `curl`       | HTTP/API-Anfragen ausführen             | `curl https://example.com`                      |
| `wget`       | Dateien herunterladen                   | `wget https://example.com/file`                 |
| `ssh`        | Remote-Verbindung herstellen            | `ssh user@server`                               |
| `scp`        | Dateien über SSH kopieren               | `scp file user@server:/tmp/`                    |
| `sftp`       | Dateien über SSH übertragen             | `sftp user@server`                              |
| `ss`         | Netzwerkverbindungen und Ports anzeigen | `ss -tulpn`                                     |
| `dig`        | DNS-Abfragen durchführen                | `dig example.com`                               |
| `traceroute` | Netzwerkroute anzeigen                  | `traceroute example.com`                        |
| `hostname`   | Hostname anzeigen                       | `hostname`                                      |
| `netstat`    | Ports anzeigen                          | `netstat -tulpn`                                |
| `iptables`   | Firewall                                | `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` |
| `nftables`   | Firewall - auf modernen Linux Dist.     |                                                 |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 11. Archive & Kompression

| Format     | Aktion             | Befehl                            |
| ---------- | ------------------ | --------------------------------- |
| **ZIP**    | Archiv erstellen   | `zip zipname.zip folder/`         |
| **ZIP**    | Archiv entpacken   | `unzip zipname.zip`               |
| **TAR**    | Archiv erstellen   | `tar -cf archive.tar folder/`     |
| **TAR**    | Archiv entpacken   | `tar -xf archive.tar`             |
| **TAR.GZ** | Archiv erstellen   | `tar -czf archive.tar.gz folder/` |
| **TAR.GZ** | Archiv entpacken   | `tar -xzf archive.tar.gz`         |
| **GZIP**   | Datei komprimieren | `gzip file.txt`                   |
| **GZIP**   | Datei entpacken    | `gunzip file.txt.gz`              |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 12. Pakete verwalten

### Debian / Ubuntu

| Aktion                                | Befehl                         |
|---------------------------------------|--------------------------------|
| Paketquellen aktualisieren            | `sudo apt update`              |
| Installierte Pakete aktualisieren     | `sudo apt upgrade`             |
| System vollständig aktualisieren      | `sudo apt full-upgrade`        |
| Paket installieren                    | `sudo apt install nginx`       |
| Paket entfernen                       | `sudo apt remove nginx`        |
| Paket inkl. Konfiguration entfernen   | `sudo apt purge nginx`         |
| Paket suchen                          | `apt search nginx`             |
| Installierte Pakete auflisten         | `apt list --installed`         |
| Paketinformationen anzeigen           | `apt show nginx`               |
| Nicht mehr benötigte Pakete entfernen | `sudo apt autoremove`          |
| `.deb`-Paket installieren             | `sudo apt install ./paket.deb` |
| Paketstatus anzeigen                  | `dpkg -s nginx`                |
| Alle installierten Pakete auflisten   | `dpkg --get-selections`        |

### Fedora / RHEL

| Aktion                                | Befehl                   |
|---------------------------------------|--------------------------|
| Paket-Metadaten aktualisieren         | `sudo dnf makecache`     |
| System aktualisieren                  | `sudo dnf upgrade`       |
| Paket installieren                    | `sudo dnf install nginx` |
| Paket entfernen                       | `sudo dnf remove nginx`  |
| Paket suchen                          | `dnf search nginx`       |
| Installierte Pakete auflisten         | `dnf list --installed`   |
| Verfügbare Pakete auflisten           | `dnf list available`     |
| Paketinformationen anzeigen           | `dnf info nginx`         |
| Nicht mehr benötigte Pakete entfernen | `sudo dnf autoremove`    |
| Installierbare Updates anzeigen       | `dnf check-update`       |

### Arch Linux

| Aktion                                     | Befehl                   |
|--------------------------------------------|--------------------------|
| System aktualisieren                       | `sudo pacman -Syu`       |
| Paket installieren                         | `sudo pacman -S nginx`   |
| Paket entfernen                            | `sudo pacman -R nginx`   |
| Paket inkl. Abhängigkeiten entfernen       | `sudo pacman -Rns nginx` |
| Paket suchen                               | `pacman -Ss nginx`       |
| Installierte Pakete auflisten              | `pacman -Q`              |
| Explizit installierte Pakete auflisten     | `pacman -Qe`             |
| Paketinformationen anzeigen                | `pacman -Si nginx`       |
| Installiertes Paket prüfen                 | `pacman -Q nginx`        |
| Nicht mehr benötigte Abhängigkeiten finden | `pacman -Qdt`            |
| Paketdateien anzeigen                      | `pacman -Ql nginx`       |
| Paket-Cache bereinigen                     | `sudo pacman -Sc`        |

### Snap (zusätzliche Paketverwaltung)

| Aktion                             | Befehl                      |
|------------------------------------|-----------------------------|
| Installierte Snap-Pakete auflisten | `snap list`                 |
| Paket installieren                 | `sudo snap install firefox` |
| Paket entfernen                    | `sudo snap remove firefox`  |
| Pakete aktualisieren               | `sudo snap refresh`         |
| Paket suchen                       | `snap find firefox`         |
| Paketinformationen anzeigen        | `snap info firefox`         |

### Flatpak (zusätzliche Paketverwaltung)

| Aktion                           | Befehl                                        |
|----------------------------------|-----------------------------------------------|
| Installierte Programme auflisten | `flatpak list --app`                          |
| Programm installieren            | `flatpak install flathub org.mozilla.firefox` |
| Programm entfernen               | `flatpak uninstall org.mozilla.firefox`       |
| Alle Programme aktualisieren     | `flatpak update`                              |
| Programm suchen                  | `flatpak search firefox`                      |
| Programminformationen anzeigen   | `flatpak info org.mozilla.firefox`            |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 13. Dienste & systemd

Auf vielen modernen Linux-Systemen werden Dienste mit systemd verwaltet.

```bash
systemctl status nginx
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl enable nginx
```

### Logs eines Dienstes anzeigen

```bash
journalctl -u nginx
```

### Logs live verfolgen

```bash
journalctl -f
```

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 14. Shell & Umgebungsvariablen

| Command   | Bedeutung                   |
| --------- | --------------------------- |
| `echo`    | Text/Variable ausgeben      |
| `env`     | Umgebungsvariablen anzeigen |
| `export`  | Variable exportieren        |
| `alias`   | Alias erstellen             |
| `history` | Befehlshistorie anzeigen    |
| `clear`   | Terminal leeren             |
| `exit`    | Shell verlassen             |
| `source`  | Shell-Datei ausführen       |

### Beispiel

```bash
export NAME="Max"
echo "$NAME"
```

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

## 15. Hilfe & Dokumentation

| Zweck                          | Befehl              | Beschreibung                                            |
| ------------------------------ | ------------------- | ------------------------------------------------------- |
| **Manpage anzeigen**           | `man ls`            | Zeigt die ausführliche Dokumentation zu `ls`            |
| **Kurze Hilfe anzeigen**       | `ls --help`         | Zeigt eine kurze Übersicht der Optionen                 |
| **Info-Seiten anzeigen**       | `info coreutils`    | Zeigt ausführlichere GNU-Info-Dokumentation             |
| **Nach Befehlen suchen**       | `apropos network`   | Sucht in den Beschreibungen der Manpages nach „network“ |
| **Programm-Pfad herausfinden** | `command -v python` | Zeigt, welches `python`-Programm verwendet wird         |

<p align="right"><sup><a href="#top">Nach oben ↑</a></sup></p>
---

# Besonders wichtig: Unix-Befehle kombinieren

Die eigentliche Stärke von Unix entsteht durch das **Kombinieren** von Befehlen.

```bash
cat access.log | grep "404" | sort | uniq -c | sort -nr
```

Die Pipeline verarbeitet die Daten Schritt für Schritt:

1. `cat` → Datei ausgeben
2. `grep` → nur HTTP-404-Zeilen auswählen
3. `sort` → Zeilen sortieren
4. `uniq -c` → gleiche Zeilen zählen
5. `sort -nr` → nach Anzahl absteigend sortieren

> **Kernprinzip von Unix:** Kleine Programme erledigen jeweils eine Aufgabe und werden über Pipes und Umleitungen zu leistungsfähigen Befehlsketten kombiniert.
