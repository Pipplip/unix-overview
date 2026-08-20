# linux-overview

Overview of Unix and commands

# Commands

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

---

## 2. Dateien

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

> ⚠️ `rm -rf` ist besonders gefährlich: Es löscht rekursiv und ohne Nachfrage.

---

## 3. Dateien lesen & bearbeiten

| Command   | Bedeutung                 | Beispiel               |
| --------- | ------------------------- | ---------------------- |
| `cat`     | Datei komplett ausgeben   | `cat file.txt`         |
| `less`    | Datei seitenweise ansehen | `less /var/log/syslog` |
| `more`    | Einfacher Pager           | `more file.txt`        |
| `head`    | Anfang einer Datei        | `head -n 20 file.txt`  |
| `tail`    | Ende einer Datei          | `tail -n 20 file.txt`  |
| `tail -f` | Datei live verfolgen      | `tail -f app.log`      |
| `nano`    | Einfacher Editor          | `nano file.txt`        |
| `vim`     | Leistungsfähiger Editor   | `vim file.txt`         |

---

## 4. Suchen

| Command   | Bedeutung                | Beispiel               |
| --------- | ------------------------ | ---------------------- |
| `find`    | Dateien suchen           | `find . -name "*.log"` |
| `locate`  | Schnelle Dateisuche      | `locate nginx.conf`    |
| `which`   | Position eines Programms | `which python`         |
| `whereis` | Programm + Manual finden | `whereis bash`         |
| `grep`    | Text suchen              | `grep "error" app.log` |
| `grep -r` | Rekursiv suchen          | `grep -r "TODO" .`     |

### Praktisches Beispiel

```bash
grep -rin "error" /var/log/
```

* `-r` = rekursiv
* `-i` = Groß-/Kleinschreibung ignorieren
* `-n` = Zeilennummer anzeigen

---

## 5. Textverarbeitung

| Command | Bedeutung                    | Beispiel                     |
| ------- | ---------------------------- | ---------------------------- |
| `sort`  | Zeilen sortieren             | `sort names.txt`             |
| `uniq`  | Duplikate entfernen          | `sort names.txt \| uniq`     |
| `wc`    | Zeilen/Wörter/Zeichen zählen | `wc -l file.txt`             |
| `cut`   | Spalten/Zeichen ausschneiden | `cut -d: -f1 /etc/passwd`    |
| `tr`    | Zeichen ersetzen             | `tr 'a-z' 'A-Z'`             |
| `sed`   | Text bearbeiten/ersetzen     | `sed 's/foo/bar/g' file.txt` |
| `awk`   | Text/Spalten verarbeiten     | `awk '{print $1}' file.txt`  |
| `diff`  | Dateien vergleichen          | `diff file1 file2`           |

---

## 6. Pipes & Umleitungen

Eines der wichtigsten Unix-Konzepte:

```bash
command1 | command2
```

Beispiel:

```bash
ps aux | grep nginx
```

### Ausgabe in eine Datei

```bash
ls -la > files.txt
```

### Ausgabe an eine Datei anhängen

```bash
echo "hello" >> file.txt
```

### Eingabe aus Datei

```bash
sort < names.txt
```

### Fehlerausgabe umleiten

```bash
command 2> errors.txt
```

### Standardausgabe und Fehlerausgabe umleiten

```bash
command > output.txt 2>&1
```

---

## 7. Prozesse

| Command   | Bedeutung                               | Beispiel        |
| --------- | --------------------------------------- | --------------- |
| `ps`      | Prozesse anzeigen                       | `ps aux`        |
| `top`     | Prozesse live anzeigen                  | `top`           |
| `htop`    | Komfortabler Prozessmonitor             | `htop`          |
| `pgrep`   | Prozess nach Name suchen                | `pgrep nginx`   |
| `kill`    | Prozess beenden                         | `kill 1234`     |
| `killall` | Prozesse nach Name beenden              | `killall nginx` |
| `jobs`    | Hintergrundjobs anzeigen                | `jobs`          |
| `fg`      | Job in Vordergrund holen                | `fg %1`         |
| `bg`      | Job im Hintergrund fortsetzen           | `bg %1`         |
| `nohup`   | Prozess nach Logout weiterlaufen lassen | `nohup ./app &` |

### Prozess im Hintergrund starten

```bash
./server &
```

---

## 8. Benutzer & Rechte

| Command  | Bedeutung                          | Beispiel       |
| -------- | ---------------------------------- | -------------- |
| `whoami` | Aktuellen Benutzer anzeigen        | `whoami`       |
| `id`     | Benutzer-ID/Gruppen anzeigen       | `id`           |
| `who`    | Angemeldete Benutzer anzeigen      | `who`          |
| `passwd` | Passwort ändern                    | `passwd`       |
| `sudo`   | Befehl mit Admin-Rechten ausführen | `sudo command` |
| `su`     | Benutzer wechseln                  | `su - user`    |
| `groups` | Eigene Gruppen anzeigen            | `groups`       |

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

### Praktisches Beispiel

```bash
du -sh *
```

Zeigt die Größe der Dateien und Ordner im aktuellen Verzeichnis.

---

## 10. Netzwerk

| Command      | Bedeutung                       | Beispiel                        |
| ------------ | ------------------------------- | ------------------------------- |
| `ip`         | Netzwerk konfigurieren/anzeigen | `ip addr`                       |
| `ping`       | Erreichbarkeit testen           | `ping 8.8.8.8`                  |
| `curl`       | HTTP/API-Anfragen ausführen     | `curl https://example.com`      |
| `wget`       | Dateien herunterladen           | `wget https://example.com/file` |
| `ssh`        | Remote-Verbindung herstellen    | `ssh user@server`               |
| `scp`        | Dateien über SSH kopieren       | `scp file user@server:/tmp/`    |
| `sftp`       | Dateien über SSH übertragen     | `sftp user@server`              |
| `ss`         | Netzwerkverbindungen anzeigen   | `ss -tulpn`                     |
| `dig`        | DNS-Abfragen durchführen        | `dig example.com`               |
| `traceroute` | Netzwerkroute anzeigen          | `traceroute example.com`        |
| `hostname`   | Hostname anzeigen               | `hostname`                      |

---

## 11. Archive & Kompression

### TAR-Archiv erstellen

```bash
tar -cf archive.tar folder/
```

### TAR-Archiv entpacken

```bash
tar -xf archive.tar
```

### TAR + gzip erstellen

```bash
tar -czf archive.tar.gz folder/
```

### TAR.GZ entpacken

```bash
tar -xzf archive.tar.gz
```

### GZIP

```bash
gzip file.txt
gunzip file.txt.gz
```

---

## 12. Pakete installieren

### Debian / Ubuntu

```bash
sudo apt update
sudo apt install nginx
sudo apt remove nginx
```

### Fedora / RHEL

```bash
sudo dnf install nginx
sudo dnf remove nginx
```

### Arch Linux

```bash
sudo pacman -S nginx
sudo pacman -R nginx
```

---

## 13. Dienste & systemd

Auf modernen Linux-Systemen sehr wichtig:

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

---

## 15. Hilfe & Dokumentation

### Manual

```bash
man ls
```

### Kurze Hilfe

```bash
ls --help
```

### Info-Seiten

```bash
info coreutils
```

### Nach passenden Befehlen suchen

```bash
apropos network
```

### Herausfinden, welches Programm verwendet wird

```bash
command -v python
```

---

# Besonders wichtig: Unix-Befehle kombinieren

Die eigentliche Stärke von Unix entsteht durch das **Kombinieren** von Befehlen.

## Pipe

```bash
command1 | command2
```

## Ausgabe umleiten

```bash
command > output.txt
```

## Ausgabe anhängen

```bash
command >> output.txt
```

## Fehler umleiten

```bash
command 2> errors.txt
```

## Beispiel

```bash
ps aux | grep nginx
```

Oder eine komplexere Pipeline:

```bash
cat access.log | grep "404" | sort | uniq -c | sort -nr
```

Dabei wird:

1. `cat` → Datei ausgeben
2. `grep` → nur HTTP-404-Zeilen auswählen
3. `sort` → Zeilen sortieren
4. `uniq -c` → gleiche Zeilen zählen
5. `sort -nr` → nach Anzahl absteigend sortieren

> **Kernprinzip von Unix:** Kleine Programme erledigen jeweils eine Aufgabe und werden über Pipes und Umleitungen zu leistungsfähigen Befehlsketten kombiniert.
