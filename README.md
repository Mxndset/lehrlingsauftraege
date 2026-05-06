# lehrlingsauftraege

Aufgaben für Schnupperlehrlinge

---

# Schnupperlehrlings-Auftrag: Linux Basics – Pakete, Benutzer und Prozesse

## Ziel des Auftrags

Du lernst weitere Grundlagen von Linux kennen. In diesem Auftrag arbeitest du mit Paketen, Benutzern, Prozessen und Textverarbeitung. Am Ende hast du ein eigenes kleines Wartungs-Skript geschrieben, mit dem man wichtige Informationen über das System auf einen Blick sehen kann.

Zusätzlich gibt es schwierigere Zusatzaufgaben, bei denen du selbstständig recherchieren und Probleme lösen sollst.

---

## Dauer

Ca. **3 bis 4 Stunden**

---

## Ausgangslage

Du arbeitest auf einem vorbereiteten Ubuntu-Laptop.

In einem typischen IT-Arbeitsalltag muss man unter Linux häufig Programme installieren, Benutzer verwalten, herausfinden welche Prozesse laufen oder grosse Logdateien durchsuchen. Genau diese Themen schaust du dir heute an.

Wichtig ist nicht, dass du alles auswendig kannst. Probiere Befehle aus, lies Fehlermeldungen, dokumentiere deine Schritte und frage nach, wenn etwas unklar ist.

---

# Teil 1: Vorbereitung

## Aufgabe 1: Arbeitsordner erstellen

Erstelle in deinem Home-Verzeichnis einen Arbeitsordner für diesen Auftrag.

```bash
mkdir ~/linux-basics
cd ~/linux-basics
```

Erstelle danach folgende Ordnerstruktur:

```text
linux-basics/
├── dokumente/
├── logs/
├── scripts/
└── systeminfos/
```

```bash
mkdir dokumente logs scripts systeminfos
ls
```

---

# Teil 2: Paketverwaltung kennenlernen

## Aufgabe 2: Pakete suchen und installieren

Unter Ubuntu werden Programme mit dem Paketmanager `apt` verwaltet.

Führe folgende Befehle aus:

```bash
sudo apt update
apt list --installed | head
apt search htop
sudo apt install -y htop
```

Beantworte kurz schriftlich:

1. Was macht `apt update`?
2. Was zeigt `apt list --installed`?
3. Was macht `apt search`?
4. Was macht `apt install`?
5. Wozu wird `sudo` verwendet?

Speichere deine Antworten in:

```text
~/linux-basics/dokumente/paketverwaltung.txt
```

---

## Aufgabe 3: Programm ausprobieren

Starte das eben installierte Programm:

```bash
htop
```

Beobachte kurz, was angezeigt wird. Beende das Programm danach mit `q`.

Schreibe in `paketverwaltung.txt`:

1. Was zeigt `htop` an?
2. Welcher Unterschied fällt dir zu `top` auf?

---

# Teil 3: Benutzer und Rechte

## Aufgabe 4: Benutzerinformationen anzeigen

Führe folgende Befehle aus:

```bash
whoami
id
groups
who
last | head
```

Schreibe kurz auf, was jeder Befehl zeigt.

| Befehl | Bedeutung |
|---|---|
| `whoami` | Zeigt den aktuellen Benutzer an |
| `id` | ... |

Speichere die Tabelle in:

```text
~/linux-basics/dokumente/benutzer.txt
```

---

## Aufgabe 5: Mit Dateirechten arbeiten

Erstelle eine Testdatei und schaue dir die Rechte an:

```bash
cd ~/linux-basics
touch testdatei.txt
ls -l testdatei.txt
```

Ändere danach die Rechte:

```bash
chmod 600 testdatei.txt
ls -l testdatei.txt
chmod 644 testdatei.txt
ls -l testdatei.txt
```

Beantworte schriftlich in `benutzer.txt`:

1. Was bedeuten die Buchstaben `r`, `w`, `x`?
2. Was bedeuten die drei Blöcke (Besitzer, Gruppe, Andere)?
3. Was bedeutet die Zahl `600`?
4. Was bedeutet die Zahl `644`?

---

# Teil 4: Prozesse und System

## Aufgabe 6: Prozesse anschauen

Führe folgende Befehle aus und speichere die Ausgabe in Dateien:

```bash
ps aux > systeminfos/prozesse.txt
uptime > systeminfos/laufzeit.txt
free -h > systeminfos/arbeitsspeicher.txt
df -h > systeminfos/speicherplatz.txt
```

Prüfe danach mit `ls systeminfos`, dass alle Dateien vorhanden sind.

Öffne eine Datei mit:

```bash
cat systeminfos/laufzeit.txt
```

Beantworte schriftlich in `~/linux-basics/dokumente/system.txt`:

1. Wie lange läuft der Computer schon?
2. Wie viel Arbeitsspeicher ist frei?
3. Wie viel Speicherplatz hat die Festplatte noch?

---

# Teil 5: Mit Textdateien arbeiten

## Aufgabe 7: Logdatei vorbereiten

Erstelle eine Beispiel-Logdatei mit folgendem Inhalt:

```bash
nano ~/linux-basics/logs/server.log
```

Füge ein:

```text
2026-05-06 08:00:01 INFO  Server gestartet
2026-05-06 08:01:14 INFO  Benutzer anna angemeldet
2026-05-06 08:02:45 WARN  Hohe CPU-Auslastung
2026-05-06 08:03:10 ERROR Verbindung zu Datenbank fehlgeschlagen
2026-05-06 08:03:12 INFO  Wiederverbindung erfolgreich
2026-05-06 08:05:22 INFO  Benutzer luca angemeldet
2026-05-06 08:07:01 ERROR Zeitüberschreitung beim Backup
2026-05-06 08:08:15 INFO  Backup neu gestartet
2026-05-06 08:09:55 WARN  Speicherplatz wird knapp
2026-05-06 08:12:00 INFO  Backup erfolgreich beendet
```

Speichere und schliesse die Datei (`CTRL+O`, `Enter`, `CTRL+X`).

---

## Aufgabe 8: Logdatei analysieren

Probiere folgende Befehle aus:

```bash
cat ~/linux-basics/logs/server.log
head -3 ~/linux-basics/logs/server.log
tail -3 ~/linux-basics/logs/server.log
wc -l ~/linux-basics/logs/server.log
grep ERROR ~/linux-basics/logs/server.log
grep WARN ~/linux-basics/logs/server.log
```

Beantworte schriftlich in `~/linux-basics/dokumente/loganalyse.txt`:

1. Wie viele Zeilen hat die Datei?
2. Wie viele `ERROR`-Einträge gibt es?
3. Wie viele `WARN`-Einträge gibt es?
4. Welche Benutzer haben sich angemeldet?

---

# Teil 6: Erstes Wartungs-Skript

## Aufgabe 9: Skript erstellen

Wechsle in den Ordner `scripts`:

```bash
cd ~/linux-basics/scripts
nano wartung.sh
```

Füge folgenden Inhalt ein:

```bash
#!/bin/bash

echo "Wartungs-Skript"
echo "---------------"
echo "Datum: $(date)"
echo "Benutzer: $(whoami)"
echo "Computer: $(hostname)"
echo ""
echo "Laufzeit:"
uptime
echo ""
echo "Speicherplatz:"
df -h /
echo ""
echo "Arbeitsspeicher:"
free -h
echo ""
echo "Anzahl Fehler in Logdatei:"
grep -c ERROR ~/linux-basics/logs/server.log
```

Speichere und schliesse die Datei.

Mache das Skript ausführbar und starte es:

```bash
chmod +x wartung.sh
./wartung.sh
```

---

# Teil 7: Abschlussbericht

## Aufgabe 10: Bericht schreiben

Erstelle die Datei:

```bash
nano ~/linux-basics/dokumente/abschlussbericht.txt
```

Beantworte darin:

```text
Abschlussbericht Linux Basics

1. Was ist ein Paketmanager?
2. Welche Befehle habe ich heute neu gelernt?
3. Was war einfach?
4. Was war schwierig?
5. Wozu kann man `grep` verwenden?
6. Was macht ein Shell-Skript?
```

---

# Teil 8: Schwierige Zusatzaufgaben – Selbstständige Recherche

## Ziel

Bei den folgenden Aufgaben sollst du selbstständig recherchieren. Du darfst Internet, Dokumentationen oder die eingebaute Hilfe (`man`, `--help`) verwenden.

Wichtig ist nicht nur das Resultat, sondern auch dass du erklären kannst, **wie du zur Lösung gekommen bist**.

---

## Aufgabe 11.1: Hilfe im Terminal

Finde selbstständig heraus, wie man unter Linux zu einem Befehl die Hilfe anzeigt.

Löse danach folgende Anforderungen:

1. Zeige die Hilfe zum Befehl `ls`.
2. Zeige die Hilfe zum Befehl `grep`.
3. Finde mindestens drei nützliche Optionen pro Befehl.

Dokumentiere in `~/linux-basics/dokumente/hilfe-recherche.txt`:

```text
Hilfe im Terminal

1. Welche Befehle/Wege habe ich gefunden, um Hilfe anzuzeigen?
2. Welche Optionen habe ich für `ls` entdeckt?
3. Welche Optionen habe ich für `grep` entdeckt?
4. Welche Quelle habe ich verwendet?
```

---

## Aufgabe 11.2: Fehler im Log zählen

Du hast die Logdatei `server.log`. Finde selbstständig heraus, wie man die Anzahl bestimmter Einträge zählt.

Löse:

1. Zähle alle `INFO`-Einträge.
2. Zähle alle `WARN`-Einträge.
3. Zähle alle `ERROR`-Einträge.
4. Zähle alle Zeilen, in denen das Wort `Backup` vorkommt.
5. Speichere alle Zahlen in:

```text
~/linux-basics/systeminfos/log-statistik.txt
```

Dokumentiere in `~/linux-basics/dokumente/log-statistik-loesung.txt`:

```text
Log-Statistik

1. Welchen Befehl habe ich verwendet?
2. Welche Optionen habe ich genutzt?
3. Welche Befehle habe ich genau ausgeführt?
4. Welche Resultate habe ich bekommen?
5. Welche Quelle habe ich verwendet?
```

---

## Aufgabe 11.3: Befehle kombinieren mit Pipe

In der IT verkettet man oft mehrere Befehle. Finde selbstständig heraus, wie das mit dem Pipe-Zeichen `|` funktioniert.

Löse:

1. Gib `ps aux` so aus, dass nur Zeilen erscheinen, die `bash` enthalten.
2. Zähle, wie viele Prozesse aktuell von dir laufen (Tipp: `ps -u $(whoami)` und `wc -l`).
3. Zeige die ersten fünf Einträge aus `~/linux-basics/logs/server.log`, die das Wort `INFO` enthalten.

Dokumentiere in `~/linux-basics/dokumente/pipe-loesung.txt`:

```text
Befehle kombinieren

1. Welche Befehle habe ich kombiniert?
2. Welches Zeichen verbindet sie?
3. Was passiert in welcher Reihenfolge?
4. Welche Resultate habe ich erhalten?
5. Welche Quelle habe ich verwendet?
```

---

## Aufgabe 11.4: Eigenen Benutzer untersuchen

Finde selbstständig heraus:

1. In welchen Gruppen ist dein Benutzer Mitglied?
2. Wo befindet sich dein Home-Verzeichnis?
3. Welche Shell wird für deinen Benutzer verwendet?
4. Wer war zuletzt am Computer angemeldet?

Dokumentiere in `~/linux-basics/dokumente/benutzer-recherche.txt`:

```text
Benutzer-Recherche

1. Welche Befehle habe ich verwendet?
2. Welche Antworten habe ich gefunden?
3. Wo musste ich genauer hinschauen, um die Information zu finden?
4. Welche Quelle habe ich verwendet?
```

---

## Aufgabe 11.5: Fehler analysieren

Führe absichtlich einen falschen Befehl aus, zum Beispiel:

```bash
cat datei-die-es-nicht-gibt.txt
cd /existiert/nicht
sudo apt installl htop
```

Löse:

1. Notiere mindestens zwei verschiedene Fehlermeldungen.
2. Erkläre in eigenen Worten, was die Fehlermeldung bedeutet.
3. Schreibe auf, wie man den Fehler beheben kann.
4. Führe danach einen korrigierten Befehl aus.

Dokumentiere in `~/linux-basics/dokumente/fehleranalyse.txt`:

```text
Fehleranalyse

1. Welche fehlerhaften Befehle habe ich ausgeführt?
2. Welche Fehlermeldungen kamen?
3. Was bedeuten diese Fehlermeldungen?
4. Wie habe ich die Fehler korrigiert?
5. Welche korrigierten Befehle haben funktioniert?
```

---

## Aufgabe 11.6: Wartungs-Skript erweitern

Erweitere dein Skript `wartung.sh` selbstständig um mindestens **zwei zusätzliche Informationen**.

Mögliche Ideen:

```text
- Anzahl angemeldeter Benutzer
- aktuelle IP-Adresse
- Linux-Kernel-Version
- Anzahl installierter Pakete
- Top 5 Prozesse nach CPU-Verbrauch
- Top 5 grösste Dateien im Home-Verzeichnis
```

Anforderungen:

1. Das Skript muss weiterhin ausführbar sein.
2. Das Skript muss ohne Fehlermeldung starten.
3. Jede neue Information muss eine Überschrift haben.
4. Das Skript bleibt unter:

```text
~/linux-basics/scripts/wartung.sh
```

Dokumentiere in `~/linux-basics/dokumente/skript-erweiterung.txt`:

```text
Skript-Erweiterung

1. Welche zwei Informationen habe ich ergänzt?
2. Welche Befehle habe ich dafür verwendet?
3. Was machen diese Befehle?
4. Wie habe ich getestet, ob das Skript funktioniert?
5. Welche Quelle habe ich verwendet?
```

---

# Teil 9: Abschlussfragen schriftlich beantworten

## Aufgabe 12: Antworten in einer Datei speichern

Die Abschlussfragen sollen nicht nur mündlich besprochen, sondern auch schriftlich festgehalten werden.

Erstelle die Datei:

```bash
nano ~/linux-basics/dokumente/abschlussfragen.txt
```

Übernimm die folgenden Fragen in die Datei und beantworte jede Frage in eigenen Worten. Schreibe ganze Sätze und nicht nur Stichworte.

```text
Abschlussfragen Linux Basics

1. Was ist ein Paketmanager und wozu braucht man ihn?
   Antwort:

2. Was bedeutet `sudo`?
   Antwort:

3. Was bedeuten die Rechte `r`, `w`, `x`?
   Antwort:

4. Welche Befehle hast du heute neu gelernt?
   Antwort:

5. Welche Aufgabe war am einfachsten?
   Antwort:

6. Welche Aufgabe war am schwierigsten?
   Antwort:

7. Wie bist du vorgegangen, als du einen Befehl nicht kanntest?
   Antwort:

8. Welche Fehlermeldung hast du erhalten und wie hast du sie behoben?
   Antwort:

9. Was hast du selbstständig herausgefunden?
   Antwort:

10. Was würdest du beim nächsten Mal anders machen?
    Antwort:
```

Speichere und schliesse die Datei (`CTRL+O`, `Enter`, `CTRL+X`).

Prüfe danach, dass die Datei wirklich existiert und Inhalt hat:

```bash
ls -l ~/linux-basics/dokumente/abschlussfragen.txt
cat ~/linux-basics/dokumente/abschlussfragen.txt
```

Anforderungen:

1. Jede Frage muss beantwortet sein.
2. Mindestens ein Satz pro Antwort.
3. Die Datei muss am vereinbarten Ort liegen.

---

# Erwartetes Endergebnis

Am Ende sollte ungefähr diese Struktur vorhanden sein:

```text
linux-basics/
├── dokumente/
│   ├── abschlussbericht.txt
│   ├── benutzer.txt
│   ├── benutzer-recherche.txt
│   ├── fehleranalyse.txt
│   ├── hilfe-recherche.txt
│   ├── loganalyse.txt
│   ├── log-statistik-loesung.txt
│   ├── paketverwaltung.txt
│   ├── pipe-loesung.txt
│   ├── skript-erweiterung.txt
│   └── system.txt
├── logs/
│   └── server.log
├── scripts/
│   └── wartung.sh
└── systeminfos/
    ├── arbeitsspeicher.txt
    ├── laufzeit.txt
    ├── log-statistik.txt
    ├── prozesse.txt
    └── speicherplatz.txt
```

---

# Hinweis für den Schnupperlehrling

In der IT muss man nicht jeden Befehl auswendig können.

Viel wichtiger ist, dass man:

- gute Informationen findet,
- Dinge ausprobiert,
- Fehlermeldungen liest,
- Lösungen überprüft,
- und erklären kann, was man gemacht hat.
