# Zweiter Versuch, die Datei Troubleshooting.md zu speichern

# Speicherpfad
file_path = "/mnt/data/Troubleshooting.md"

# Dateiinhalt erneut definieren
markdown_content = """
# Troubleshooting – SSH-Key Probleme mit Windows 11

Während der Einrichtung der SSH-Schlüssel zur passwortlosen Authentifizierung traten insbesondere unter **Windows 11** wiederholt Probleme im Zusammenspiel mit den Linux-basierten Systemen auf.

## Problem 1: SSH-Keys wurden nicht korrekt in `authorized_keys` übernommen

Beim Übertragen der öffentlichen SSH-Schlüssel (`.pub`) von Windows 11 zu den Linux-Systemen wurden diese **nicht automatisch in die Datei `~/.ssh/authorized_keys`** übernommen. Stattdessen musste der Inhalt manuell eingefügt werden:

```bash
cat id_rsa.pub >> ~/.ssh/authorized_keys


## Problem 2: SSH von Linux zu Windows scheitert bei `PasswordAuthentication no`

Wurde in der Windows-sshd_config die Option PasswordAuthentication no gesetzt, war es nicht mehr möglich, Schlüssel von einem Linux-System aus an Windows zu senden, da der Zugriff ohne Passwort ebenfalls blockiert wurde.

Lösung:

    Temporär PasswordAuthentication yes setzen

    Key-Transfer durchführen

    Danach wieder auf no setzen und SSH neu starten:

    ```bash
    Restart-Service sshd

## Problem 3: Dateinamen beim Speichern unter Windows

Beim Zwischenspeichern von .pub- oder authorized_keys-Dateien unter Windows (z. B. im Editor) wird die Datei standardmäßig als .txt gespeichert, was zu Fehlern bei der Verwendung führt.

Lösung:
Beim Speichern den Dateinamen in Anführungszeichen setzen, z. B.:

"authorized_keys"
"id_rsa.pub"

So wird verhindert, dass Windows automatisch .txt anhängt.

