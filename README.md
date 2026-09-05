# FISI Trainer – Leer-Vorlage

Eine komplett offline lauffähige Lernkarten-App zur Prüfungsvorbereitung für Fachinformatiker Systemintegration (AP1/AP2) – **als leere Vorlage ohne vorgefertigten Karteninhalt**. Du befüllst sie selbst mit deinem eigenen Lernmaterial.

Läuft als **eine einzige HTML-Datei** (ca. 2 MB) – kein Server, kein Internet nötig, einfach im Browser öffnen. Am besten in **Chrome oder Edge** (Desktop), da einige Funktionen das voraussetzen (siehe unten).

Entwickelt von **[dolunay38](https://github.com/dolunay38)**.

---

## 1. Erste Schritte

1. Datei im Browser öffnen (Doppelklick oder ins Browserfenster ziehen)
2. Beim ersten Start optional einen Speicherordner verbinden (siehe Kapitel 2) – nicht zwingend, macht die App aber robuster
3. Import-Tab öffnen und loslegen: eigene Prüfungen/Lernzettel als JSON importieren, per KI aus PDF/Foto automatisch Karten erstellen lassen, oder direkt beim Lernen mit "+ Karte hinzufügen" von Hand Karten anlegen

Die Vorlagen-Struktur für den JSON-Import steht direkt im Import-Tab der App.

---

## 2. Speicherordner verbinden (empfohlen)

### Welcher Browser das kann

| Browser | Ordner-Anbindung möglich? |
|---|---|
| Chrome / Edge am Desktop | ✅ Ja |
| Firefox, Safari, Mobile Browser | ❌ Nein (File System Access API dort nicht implementiert) |

Ohne Unterstützung läuft die App automatisch im **Fallback-Modus** über IndexedDB (browserintern) – funktional kein Unterschied beim Lernen, nur ohne echte Dateien auf der Festplatte und ohne automatische Datei-Backups.

### Warum verbinden

- Unabhängig vom Browser-Cache (der kann beim "Daten löschen" verschwinden, ein echter Ordner nicht)
- Automatische tägliche Backups (bis zu 30, älteste wird gelöscht)
- Lässt sich in einen Cloud-synchronisierten Ordner (Google Drive, OneDrive, Dropbox) legen – synchronisiert sich dann automatisch zwischen Geräten, ganz ohne dass die App selbst etwas davon merkt

### Die entstehende Ordnerstruktur

```
Dein-Ordner/
  daten/        Hauptdatei (fisi_daten.json) - Karten, Fortschritt, Einstellungen
  backups/      automatische taegliche Sicherungen (max. 30)
  exporte/      Module, die du ueber "Export" exportierst
  pruefungen/   Kopien aller per JSON importierten Module
  bilder/       Bilder, die in Karten eingefuegt werden
```

Nach jedem Browser-Neustart verlangt Chrome/Edge aus Sicherheitsgründen eine kurze erneute Bestätigung, bevor die App wieder schreiben darf – die eigentliche Ordner-Auswahl bleibt aber dauerhaft gespeichert.

---

## 3. Karten anlegen – drei Wege

1. **JSON-Import** (Import-Tab): Datei mit dem passenden Schema (siehe Kapitel 8) reinziehen oder auswählen
2. **KI-Material-Upload** (Import-Tab): PDF oder Foto hochladen, KI erstellt automatisch mehrere Karten daraus – eigener API-Key nötig (siehe Kapitel 5)
3. **Manuell beim Lernen**: Button "+ Karte hinzufügen" (immer sichtbar in der Lernansicht) legt sofort eine leere Karte im gerade offenen Thema an und öffnet direkt das Bearbeiten-Formular dafür

Jede Karte lässt sich jederzeit über den Bearbeiten-Modus wieder anpassen oder über den Button "Karte löschen" im Bearbeiten-Formular entfernen.

---

## 4. Lernfunktionen

- **Fünf Lernmodi**: Normal, Prüfung (mit Zeitdruck/Bewertung), Shuffle, Fokus, Wiederholung (Spaced Repetition), plus Schwächen-Modus
- **Schwachstellen-Radar**, **Prüfungssimulation mit Punktebewertung**, **12-Wochen-Lernplan**
- **Volltextsuche** über Frage, Antwort, IHK-Feld und Tags aller Karten
- **Mermaid-Diagramme** in Karten möglich (UML, Netzpläne als Code)
- **Vollbild-Zoom** für Bilder und Diagramme

---

## 5. KI-Integration (optional, eigener API-Key)

Bring-your-own-key, direkt im Browser. Unterstützte Anbieter: Anthropic, Google Gemini, DeepSeek, GLM/Z.ai, Qwen, Groq.

- **Kartenerklärungen**, **Freitext-Antwortbewertung** (auch mit gezeichneter Antwort, siehe Kapitel 6), **Foto-zu-Karte**, **KI-Chat**, **Spickzettel-Generator**
- **Material-Upload**: PDF/Foto → automatisch mehrere Karten. PDF nativ bei Anthropic/Google, bei anderen Anbietern übernimmt das eingebettete pdf.js automatisch Text-Extraktion oder Seiten-als-Bild-Rendering je nach Fähigkeit des gewählten Modells. Seitenweise Verarbeitung mit automatischer Wiederholung bei Rate-Limits.
- **"Karten erstellen"**-Button direkt in der Suche und im KI-Chat: erzeugt neue Karten passend zum Suchbegriff bzw. zum gerade geführten Gespräch

---

## 6. Zeichenwerkzeug

Voll ausgestatteter Zeichen-Editor direkt in jedem Textfeld einer Karte (Frage, Antwort, Ausgangssituation, Zusatzblatt) – kein externes Programm nötig.

**Vier Tabs:**

| Tab | Enthält |
|---|---|
| ✏️ Zeichnen | Stift, Linie, Pfeil, Rechteck, Abgerundet, Raute, Kreis, Text, Auswählen – plus Farbe, Strichstärke, Gestrichelt, Textgröße |
| 🌐 Netzwerk | Router, Switch, Server, PC/Client, Firewall, Internet, Access Point, NAS, Modem, Hub/Repeater, Patch-Panel, Laptop, Smartphone, Drucker, USV, Datenbank |
| 🔌 Hardware | USB-A, USB-C, HDMI, RJ45, VGA, DisplayPort, Klinke 3,5mm, SATA, DVI, PS/2, Kaltgerätestecker |
| 💻 Komponenten | RAM, CPU, Mainboard, Netzteil, HDD, SSD |

**Bedienung:** Symbol/Werkzeug anklicken, auf die Fläche klicken (Symbole fragen optional nach einer Beschriftung). Mit dem Werkzeug "Auswählen" lässt sich jede Form danach frei verschieben, per Ziehpunkt an den Endpunkten in Größe/Richtung ändern (z. B. Pfeilrichtung), die Farbe nachträglich ändern, oder wieder löschen.

Für Tabellen gibt's zusätzlich einen eigenen **Tabellen-Editor** (Klick-Zellen, +/- Zeile/Spalte, Kopfzeile an/aus) statt HTML von Hand schreiben zu müssen – erkennt automatisch, wenn im Feld schon eine Tabelle steht, und öffnet sie zum Weiterbearbeiten.

---

## 7. Import / Export

- **JSON-Import**: Datei reinziehen, Kategorie wird automatisch an der ID erkannt
- **Modul-Export / Umbenennen / Löschen**: direkt in der Import-Liste
- **Vollexport**: bündelt alle aktuellen Module inkl. Bilder in eine neue, komplette HTML-Datei
- **Leer-Vorlage exportieren**: erzeugt aus dem aktuellen Stand eine frische, inhaltsleere Kopie der App (genau diese Datei hier) – praktisch, falls du selbst mal eine eigene Version ohne deinen Lerninhalt weitergeben willst
- **Für Handy exportieren**: Variante mit eingebetteten Bildern für den mobilen Workflow (Android unterstützt "Ordner verbinden" nicht, siehe Kapitel 2)

---

## 8. Schema für den JSON-Import

**Karte:**
```json
{
  "id": "eindeutige_id",
  "nr": "1a",
  "punkte": 4,
  "typ": "theorie",
  "frage": "...",
  "antwort": "...",
  "ihk": "knappe Klartext-Kurzfassung (optional)",
  "tags": ["Thema1", "Thema2"],
  "diagram": "Mermaid-Code (optional)"
}
```
`typ` ∈ `theorie | rechnung | sql | subnetting | pseudocode | netzplan | zeichnung | zuordnung | nutzwertanalyse | text`

**Modul:**
```json
{
  "id": "eigene_kategorie_beispiel",
  "label": "Anzeigename",
  "icon": "📝",
  "accent": "#e3b341",
  "datum": "Beschreibungstext",
  "situation": "Ausgangssituation / Intro",
  "aufgaben": [
    { "id": "g1", "label": "Themenblock", "punkte": 10, "karten": [ /* Karten */ ] }
  ]
}
```

**ID-Konvention für die Tab-Zuordnung:**

| Vorsilbe | Landet in Tab |
|---|---|
| `ap1_...` | AP1 |
| `ki_...` | KI Prüfungen |
| `ap2_...` | AP2 |
| `ap2ki_...` | AP2 KI Prüfungen |
| `ap2katalog_...` | AP2 Lernkatalog |
| alles andere | Lernkatalog |

---

## 9. Bekannte Einschränkungen

- **API-Keys** liegen aktuell in `localStorage`, nicht im verbundenen Ordner – gehen beim Wechsel auf eine andere HTML-Datei verloren (Fortschritt/Karten bleiben erhalten)
- **Mobile Sync**: File System Access API funktioniert nicht in Android/iOS-Browsern – dort über "Für Handy exportieren" plus manuellem Datei-Transfer (z. B. via Cloud-Speicher)
- **Gescannte PDFs ohne Textebene** funktionieren beim Material-Upload nicht mit reinen Textmodellen – dort stattdessen ein Foto hochladen oder ein Modell mit nativer PDF-Unterstützung wählen (Anthropic/Google)

---

## Lizenz

MIT License – siehe [LICENSE](./LICENSE). Kurz gesagt: jeder darf den Code frei nutzen, verändern, weiterverbreiten, auch kommerziell – solange der Original-Copyright-Hinweis erhalten bleibt.
