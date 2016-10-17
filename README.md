msdtrigger - Lizenz und Dokumentation
-----------------------------------------------------------------------------

Voraussetzungen:
- 1. Laufzeitumgebung .NET Framework 4 Client Profile, getestet mit Version 4.0.30319
- 2. Fertig eingerichtetes MySQLDumper-Paket auf einem Server
- 3. Konfigurationsdatei "msdtrigger.xml" im Programmverzeichnis (Beispiel wird mitgeliefert)
- 4. Die Ausführung des Programmes muss zwingend im jeweiligen Arbeitsverzeichnis erfolgen. (Aufgabenplanung oder AutohotKey Script, etc.)

Programmfeatures:
- Aufruf von MySQLDumper Backup-URL der Form http(s)://example.com/dump.php?config=mysqldumper
- Aufruf von MySQLDumper Bereinigungs-URL der Form http(s)://example.com/filemanagement.php?action=files
- Mehrere URLs / Backup-Ziele in einem Durchgang sind möglich
- SSL-Unterstützung (https, auch mit selbst generierten Zertifikaten)
- Programmausführung komplett im Hintergrund
- Logdatei mit einstellbarem Pfad

Lizenz:
- Open Source, der Quelltext ist frei verwendbar, ohne Einschränkungen. (Kommerziell oder Privat)

Konfiguration:
Die Konfigurationsdatei "msdtrigger.xml" muss im Programmverzeichnis liegen.
Die Struktur der Datei kann dem mitgelieferten Beispiel entnommen werden.
Ist die Datei nicht vorhanden, beendet sich das Programm ohne weitere Aktion.

Optionen im Einzelnen:
<ConfigEntry>: Ein Eintrag, bestehend aus Backup- und Bereinigungs-URL sowie Benutzername und Passwort.
Mehrere Einträge sind möglich - diese werden in der Reihenfolge nacheinander abgearbeitet.
<LogFile>: Pfad zur Logdatei
<DisableCertValidation>: true, wenn selbsterstellte SSL-Zertifikate zum Einsatz kommen sollen.

VORSICHT: Diese Einstellung setzt Sicherheitsmechanismen der internen WebBrowser-Komponente außer Kraft.
Verwenden Sie diese Option nur in vertrauenswürdigen Netzwerken! Sie können Zertifikatsfehler vermeiden, indem Sie selbsterstellte Zertifikate auf ihrem System zur Liste verstrauenswürdiger Zertifikate hinzufügen.

<ResumeOnError>: True, wenn das Programm bei einem Fehler während der Verarbeitung eines ConfigEntry beendet werden soll. False, wenn der Fehler nur protokolliert werden soll.

Programmablauf:
Das Programm liest zu Beginn die Konfigurationsdatei "msdtrigger.xml" ein. Alle ConfigEntry-Einträge werden nacheinander abgearbeitet.
Für jeden Eintrag wird die Backup-URL mit der WebBrowser-Komponente aufgerufen, wodurch ein MySQLDumper-Backup initiiert wird.
Das Programm wartet, bis das Backup beendet ist, und ruft dann die Bereinigungs-URL zum Löschen alter Backups auf.
(Die Anzahl der aufzubewahrenden Backups kann in der MySQLDumper Konfiguration eingestellt werden)
