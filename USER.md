# Linux: Benutzer, Gruppen und Rechte einfach erklärt

Linux verwendet Benutzer, Gruppen und Dateirechte, um zu bestimmen, wer auf welche Dateien und Programme zugreifen darf.

## 1. Benutzerarten

| Art                  | Einfache Erklärung                                | Übliche UID     |
|----------------------|---------------------------------------------------|-----------------|
| **root**             | Administrator mit fast allen Rechten              | `0`             |
| **Systembenutzer**   | Konten für Dienste wie Webserver oder Datenbanken | meist `1–999`   |
| **Normale Benutzer** | Konten für Personen                               | meist ab `1000` |
| **nobody**           | Konto mit besonders wenigen Rechten               | `65534`         |

Die **UID** ist die eindeutige Nummer eines Benutzers. Linux arbeitet intern vor allem mit dieser Nummer und nicht mit dem Benutzernamen.

## 2. Wie Benutzer, Gruppen und Rechte zusammenhängen

### Benutzer und Gruppen

Jeder Benutzer hat:

- genau **eine primäre Gruppe**
- beliebig viele **zusätzliche Gruppen**

Die primäre Gruppe wird normalerweise neuen Dateien des Benutzers zugeordnet. Zusätzliche Gruppen geben weitere Rechte, zum Beispiel für `sudo`, Docker oder gemeinsame Projektdateien.

Beispiel:

```text
phil → primäre Gruppe: phil
phil → zusätzliche Gruppen: sudo, docker
```

Mit `id phil` oder `groups phil` sieht man die Gruppen eines Benutzers.

### Besitzer, Gruppe und Andere

Jede Datei und jedes Verzeichnis gehört:

1. einem **Besitzer** (Owner)
2. einer **Gruppe**

Die Rechte werden für drei Bereiche festgelegt:

```text
-rwxr-xr-- 1 phil entwickler 1234 datei.sh
 ||| ||| |||
  |   |   └── Andere: lesen
  |   └────── Gruppe: lesen und ausführen
  └────────── Besitzer: lesen, schreiben und ausführen
```

Linux prüft beim Zugriff:

1. Ist der Benutzer der Besitzer? Dann gelten die Besitzerrechte.
2. Gehört der Benutzer zur Dateigruppe? Dann gelten die Gruppenrechte.
3. Sonst gelten die Rechte für Andere.

Gruppen sind praktisch, weil man damit mehreren Benutzern gleichzeitig dieselben Rechte geben kann.

### root, sudo und su

`root` ist der Administrator von Linux und hat die UID `0`. Dieses Konto kann fast alle normalen Dateirechte umgehen. Deshalb sollte man root-Rechte nur verwenden, wenn sie wirklich nötig sind.

- `sudo befehl`: führt einen einzelnen Befehl mit erhöhten Rechten aus
- `sudo -i`: öffnet eine root-Shell
- `su -`: wechselt zu root und verlangt normalerweise das root-Passwort

Ob ein Benutzer `sudo` verwenden darf, steht in `/etc/sudoers`. Häufig erhalten Mitglieder der Gruppe `sudo` oder `wheel` diese Erlaubnis.

## 3. Wichtige Dateien

| Datei             | Inhalt                                                       |
|-------------------|--------------------------------------------------------------|
| `/etc/passwd`     | Benutzerkonten, UID, primäre GID, Home-Verzeichnis und Shell |
| `/etc/shadow`     | Passwort-Hashes und Regeln zum Ablauf von Passwörtern        |
| `/etc/group`      | Gruppen und ihre Mitglieder                                  |
| `/etc/gshadow`    | Geschützte Informationen zu Gruppen                          |
| `/etc/sudoers`    | Regeln für `sudo`; immer mit `visudo` bearbeiten             |
| `/etc/sudoers.d/` | Zusätzliche `sudo`-Regeln                                    |
| `/etc/login.defs` | Standardwerte für neue Benutzer                              |
| `/etc/skel/`      | Vorlagen für neue Home-Verzeichnisse                         |

### Beispiel für `/etc/passwd`

```text
phil:x:1000:1000:Phil:/home/phil:/bin/bash
```

Die Felder bedeuten:

```text
Name:Passwort-Platzhalter:UID:GID:Info:Home-Verzeichnis:Login-Shell
```

Das `x` bedeutet, dass der Passwort-Hash in `/etc/shadow` liegt.

## 4. Benutzer verwalten

| Befehl                           | Bedeutung                                       |
|----------------------------------|-------------------------------------------------|
| `useradd -m -s /bin/bash name`   | Benutzer mit Home-Verzeichnis und Bash anlegen  |
| `adduser name`                   | Benutzer interaktiv anlegen (Debian/Ubuntu)     |
| `usermod -aG gruppe name`        | Benutzer einer zusätzlichen Gruppe hinzufügen   |
| `usermod -l neuername altername` | Benutzernamen ändern                            |
| `usermod -d /neues/home -m name` | Home-Verzeichnis ändern und Dateien verschieben |
| `usermod -s /bin/zsh name`       | Login-Shell ändern                              |
| `userdel name`                   | Benutzer löschen, Home-Verzeichnis behalten     |
| `userdel -r name`                | Benutzer und Home-Verzeichnis löschen           |
| `passwd name`                    | Passwort setzen oder ändern                     |
| `passwd -l name`                 | Passwort-Login sperren                          |
| `passwd -u name`                 | Passwort-Login entsperren                       |
| `chage -l name`                  | Regeln zum Passwortablauf anzeigen              |
| `chage -M 90 name`               | Passwort höchstens 90 Tage gültig machen        |

**Wichtig:** Bei `usermod -aG` darf `-a` nicht fehlen. Ohne `-a` werden die bisherigen zusätzlichen Gruppen ersetzt.

### Benutzerinformationen anzeigen

| Befehl               | Bedeutung                                |
|----------------------|------------------------------------------|
| `id name`            | UID, primäre GID und Gruppen anzeigen    |
| `whoami`             | Eigenen Benutzernamen anzeigen           |
| `who` oder `w`       | Angemeldete Benutzer anzeigen            |
| `last`               | Frühere Anmeldungen anzeigen             |
| `getent passwd name` | Informationen zu einem Benutzer anzeigen |

## 5. Gruppen verwalten

| Befehl                   | Bedeutung                                |
|--------------------------|------------------------------------------|
| `groupadd gruppe`        | Gruppe anlegen                           |
| `groupdel gruppe`        | Gruppe löschen                           |
| `groupmod -n neu alt`    | Gruppe umbenennen                        |
| `gpasswd -a name gruppe` | Benutzer zur Gruppe hinzufügen           |
| `gpasswd -d name gruppe` | Benutzer aus der Gruppe entfernen        |
| `groups name`            | Gruppen eines Benutzers anzeigen         |
| `newgrp gruppe`          | Gruppe für die aktuelle Sitzung wechseln |

Nach dem Hinzufügen zu einer Gruppe muss sich der Benutzer meist ab- und wieder anmelden, damit die Änderung überall gilt.

## 6. Dateirechte

### Die Rechte `r`, `w` und `x`

| Recht                 | Bei einer Datei | Bei einem Verzeichnis        |
|-----------------------|-----------------|------------------------------|
| `r` (read, Wert 4)    | Datei lesen     | Inhalt auflisten             |
| `w` (write, Wert 2)   | Datei ändern    | Dateien anlegen oder löschen |
| `x` (execute, Wert 1) | Datei ausführen | Verzeichnis betreten         |

### Ausgabe von `ls -l` lesen

```text
-rwxr-xr-- 1 phil entwickler 1234 Aug 24 10:00 datei.sh
```

- Erstes Zeichen: Typ (`-` Datei, `d` Verzeichnis, `l` Link)
- Zeichen 2–4: Rechte des Besitzers
- Zeichen 5–7: Rechte der Gruppe
- Zeichen 8–10: Rechte für Andere

### Rechte als Zahlen

Die Werte der gewünschten Rechte werden addiert:

| Wert | Rechte                              |
|------|-------------------------------------|
| `7`  | `rwx` = lesen, schreiben, ausführen |
| `6`  | `rw-` = lesen und schreiben         |
| `5`  | `r-x` = lesen und ausführen         |
| `4`  | `r--` = nur lesen                   |
| `0`  | `---` = keine Rechte                |

Beispiele:

- `chmod 755 datei`: Besitzer darf alles, alle anderen dürfen lesen und ausführen.
- `chmod 644 datei`: Besitzer darf lesen und schreiben, alle anderen nur lesen.
- `chmod 700 datei`: Nur der Besitzer hat Rechte.

### Rechte und Besitzer ändern

| Befehl                         | Bedeutung                                     |
|--------------------------------|-----------------------------------------------|
| `chmod 644 datei`              | Rechte mit Zahlen setzen                      |
| `chmod u+x datei`              | Datei für den Besitzer ausführbar machen      |
| `chmod g-w datei`              | Der Gruppe das Schreibrecht entziehen         |
| `chmod -R 755 ordner/`         | Rechte im gesamten Ordner ändern              |
| `chown user datei`             | Besitzer ändern                               |
| `chown user:gruppe datei`      | Besitzer und Gruppe ändern                    |
| `chown -R user:gruppe ordner/` | Besitzer und Gruppe im gesamten Ordner ändern |
| `chgrp gruppe datei`           | Nur die Gruppe ändern                         |
| `umask`                        | Standardmaske anzeigen                        |

`umask 022` führt normalerweise zu:

- neuen Dateien mit `644`
- neuen Verzeichnissen mit `755`

## 7. Besondere Rechte

| Recht          | Wert   | Einfache Erklärung                                                                                |
|----------------|--------|---------------------------------------------------------------------------------------------------|
| **SUID**       | `4000` | Ein Programm läuft mit den Rechten seines Besitzers                                               |
| **SGID**       | `2000` | Ein Programm läuft mit den Rechten seiner Gruppe; in Verzeichnissen erben neue Dateien die Gruppe |
| **Sticky Bit** | `1000` | In einem gemeinsamen Verzeichnis darf jeder nur seine eigenen Dateien löschen                     |

Beispiele:

- `/usr/bin/passwd` verwendet SUID, damit Benutzer ihr Passwort ändern können.
- `/tmp` verwendet das Sticky Bit, damit Benutzer keine fremden Dateien löschen können.
- `chmod 4755 datei` setzt SUID und die normalen Rechte `755`.

SUID und SGID sollten nur verwendet werden, wenn sie wirklich nötig sind.

## 8. ACLs: zusätzliche Rechte

Mit ACLs kann man einzelnen Benutzern oder Gruppen zusätzliche Rechte geben, ohne Besitzer oder Dateigruppe zu ändern.

| Befehl                         | Bedeutung                        |
|--------------------------------|----------------------------------|
| `getfacl datei`                | ACLs anzeigen                    |
| `setfacl -m u:name:rwx datei`  | Einem Benutzer Rechte geben      |
| `setfacl -m g:gruppe:rx datei` | Einer Gruppe Rechte geben        |
| `setfacl -x u:name datei`      | ACL eines Benutzers entfernen    |
| `setfacl -b datei`             | Alle zusätzlichen ACLs entfernen |

## 9. sudo-Regeln

Beispiel aus `/etc/sudoers`:

```text
%sudo ALL=(ALL:ALL) ALL
phil  ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx
```

- Zeile 1: Mitglieder der Gruppe `sudo` dürfen alle Befehle mit `sudo` ausführen.
- Zeile 2: `phil` darf genau den angegebenen Befehl ohne Passwort ausführen.
- Ein `%` vor dem Namen steht für eine Gruppe.

Die Datei `/etc/sudoers` immer mit `visudo` bearbeiten. Das Programm prüft die Syntax und verhindert dadurch viele Fehler.

## 10. Prozesse und Benutzer

Jeder Prozess läuft unter einem Benutzer und übernimmt dessen Rechte.

| Befehl                | Bedeutung                             |
|-----------------------|---------------------------------------|
| `ps aux`              | Prozesse und ihre Benutzer anzeigen   |
| `id`                  | Eigene UID, GID und Gruppen anzeigen  |
| `sudo -u name befehl` | Befehl als anderer Benutzer ausführen |

## 11. Schnellübersicht

| Aufgabe                               | Befehl                          |
|---------------------------------------|---------------------------------|
| Benutzer anlegen                      | `useradd -m -s /bin/bash name`  |
| Benutzer zur sudo-Gruppe hinzufügen   | `usermod -aG sudo name`         |
| Passwort setzen                       | `passwd name`                   |
| Konto sperren                         | `passwd -l name`                |
| Benutzer mit Home-Verzeichnis löschen | `userdel -r name`               |
| Rechte anzeigen                       | `ls -l datei` oder `stat datei` |
| Besitzer und Gruppe ändern            | `chown user:gruppe datei`       |
| Nur dem Besitzer alle Rechte geben    | `chmod 700 datei`               |
| Datei für alle lesbar machen          | `chmod 644 datei`               |
| Skript ausführbar machen              | `chmod +x script.sh`            |
| Gruppen anzeigen                      | `groups` oder `id`              |
| Root-Shell öffnen                     | `sudo -i` oder `su -`           |

## 12. Wichtige Sicherheitsregeln

- Root-Rechte nur verwenden, wenn sie nötig sind.
- Benutzern nur die Rechte geben, die sie wirklich brauchen.
- Direktes root-Login über SSH abschalten (`PermitRootLogin no`).
- Dienstkonten ohne normale Login-Shell anlegen, zum Beispiel mit `/usr/sbin/nologin`.
- SUID- und SGID-Dateien regelmäßig prüfen.
- `/etc/sudoers` immer mit `visudo` bearbeiten.
- Vor rekursiven Befehlen wie `chmod -R` und `chown -R` den Pfad genau prüfen.

---

Die genauen Standardwerte können sich je nach Linux-Distribution unterscheiden.
