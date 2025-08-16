Dies ist eine interaktive Web-Anwendung zur Anzeige und Verwaltung des Stundenplans der MS Schwarzau im Gebirge. Sie ermöglicht es, den Stundenplan nach Lehrern, Fächern und Schulstufen zu filtern, die aktuelle Stunde hervorzuheben und Supplierungen sowie entfallene Stunden zu planen und zu verwalten. Die Änderungen können lokal im Browser oder optional in einer Cloud-Datei gespeichert werden.

## Funktionen

*   **Dynamische Stundenplan-Anzeige**: Übersichtliche Darstellung des Stundenplans für Desktop und mobile Geräte.
*   **Filter-Optionen**:
    *   Filtern nach Lehrern.
    *   Filtern nach Gegenständen (Fächern).
    *   Filtern nach Schulstufen.
    *   "Alle anzeigen"-Button zum Zurücksetzen aller Filter.
*   **Anpassbare Ansicht (Header-Controls oben rechts)**:
    *   "L"-Button: Blendet Lehrer-Badges (L1, L2 etc.) in den Stundenplan-Zellen ein/aus (standardmäßig ausgeblendet).
    *   "ᵍ"-Button: Blendet Schulstufen-Badges in den Stundenplan-Zellen ein/aus (standardmäßig ausgeblendet).
    *   "SUP"-Button: Öffnet das Supplierungs-Panel.
*   **Auto-Skalierung**: Der gesamte Wochen-Stundenplan passt sich automatisch an die Bildschirmgröße an, sodass kein horizontales Scrollen erforderlich ist.
*   **Aktuelle Stunde-Hervorhebung**: Die aktuell laufende Unterrichtsstunde (Wochentag und Zeitfenster) wird farblich hervorgehoben.
*   **Supplierungs-Planung (SUP)**:
    *   Wähle einen abwesenden Lehrer und die betroffenen Tage.
    *   "Vorschläge finden": Das System schlägt passende Ersatzlehrer vor, die in der jeweiligen Stunde frei sind und an diesem Tag generell Unterricht haben. Die Vorschläge werden nach "Freistunden-Optimierung" (minimale Lücken vor/nach der Supplierung) gereiht.
    *   Manuelle Auswahl: Du kannst jeden Lehrer der Schule als Ersatz wählen, auch wenn das System ihn nicht vorgeschlagen hat oder er nicht verfügbar ist. Der Status des Lehrers (frei, Unterricht vorher/später, kein Unterricht am Tag) wird angezeigt.
    *   "Übernehmen"-Button: Weist die Supplierung zu. Die betroffene Stunde wird im Stundenplan halb-halb (Farbe des kranken Lehrers / Farbe des Ersatzlehrers) dargestellt und mit einem "SUP"-Badge markiert.
    *   "Entfällt"-Button: Markiert eine Stunde als entfallen (grau hinterlegt mit "ENTFÄLLT"-Badge), ohne dass eine Supplierung nötig ist.
    *   Einzelzuweisung: Jeder Slot kann nur einmal zugewiesen (suppliert oder entfallen) werden.
    *   Verschiebbares Panel: Das SUP-Panel kann frei auf dem Bildschirm verschoben werden, um die Übersicht über den Stundenplan zu behalten.
*   **Supplierungs-Zusammenfassung (unterhalb des Stundenplans)**:
    *   Zeigt alle aktiven Supplierungen und entfallenen Stunden übersichtlich in einer Grid-Ansicht pro Tag an.
    *   Jeder Eintrag kann einzeln mit "Entfernen" rückgängig gemacht werden.
    *   Export-Optionen: "Drucken" (Gesamtseite), "Nur SUP drucken" (nur Titel und SUP-Übersicht), "Als Text speichern" (Export als `supplierungen.txt`).
*   **Daten-Persistenz**:
    *   Standardmäßig: Speicherung der Supplierungen im `localStorage` deines Browsers (lokal auf deinem Gerät).
    *   Optional: Synchronisierung mit einer Cloud-JSON-Datei (JSONBin.io), um die Daten geräteübergreifend verfügbar zu machen.
*   **Sync-Status-Anzeige**: Ein Indikator oben rechts in der Filterleiste zeigt den Verbindungs- und Speicherstatus an (Grün für Online/OK, Blau blinkend für Synchronisieren, Rot für Offline/Fehler).

## Einrichtung

1.  **Dateien herunterladen**: Lade alle Projektdateien (`Stundenplan.html`, `styles.css`, `script.js`) in ein gemeinsames Verzeichnis herunter.
2.  **Im Browser öffnen**: Öffne die Datei `Stundenplan.html` mit einem modernen Webbrowser (Chrome, Firefox, Edge etc.).

### Optionale Cloud-Synchronisierung (über JSONBin.io)

Um deine Supplierungsdaten geräteübergreifend zu speichern und abzurufen, kannst du den kostenlosen Dienst [JSONBin.io](https://jsonbin.io/) nutzen.

1.  **Registriere dich bei JSONBin.io**: Erstelle einen kostenlosen Account.
2.  **Erstelle einen neuen Bin**:
    *   Klicke auf "Create a Bin".
    *   Füge folgenden initialen JSON-Inhalt ein:
        ```json
        {
          "applied": [],
          "assignedKeys": [],
          "canceled": []
        }
        ```
    *   Setze die Sichtbarkeit auf "Private" (empfohlen).
    *   Klicke auf "Save Bin".
3.  **Hole deine BIN_ID und API_KEY**:
    *   Nach dem Speichern siehst du die **BIN ID** (z.B. `689cddaed0ea881f40588d04`). Kopiere diese.
    *   Gehe zu deinen "Account Settings" und finde deinen **X-Master-Key**. Kopiere diesen ebenfalls.
4.  **Konfiguriere `script.js`**:
    *   Öffne die Datei `script.js` mit einem Texteditor.
    *   Suche nach dem Abschnitt `const CLOUD_SUP = { ... }` (ungefähr am Ende der Datei).
    *   Ersetze die Platzhalter mit deinen kopierten Werten:

        ```javascript
        const CLOUD_SUP = {
            provider: 'jsonbin',
            BIN_ID: 'DEINE_BIN_ID_HIER_EINSETZEN', // Beispiel: '689cddaed0ea881f40588d04'
            API_KEY: 'DEIN_X_MASTER_KEY_HIER_EINSETZEN' // Beispiel: '$2a$10$7hoR2ze7YtrsAEg6Sg0w9.fBtfDeVgXllHPdlM5oXK7CPsKGnA/4C'
        };
        ```
    *   Speichere die Datei `script.js`.

Beim nächsten Öffnen von `Stundenplan.html` werden die Supplierungen automatisch von JSONBin.io geladen und dort gespeichert. Der Sync-Status-Indikator oben rechts zeigt dir den Status an.

## Verwendung

### Filter

*   **Lehrer-Filter**: Klicke auf die Lehrer-Buttons in der horizontalen Leiste, um Stundenplan-Einträge des jeweiligen Lehrers hervorzuheben. Mehrere Lehrer können gleichzeitig ausgewählt werden.
*   **Gegenstands-Filter**: Wähle ein Fach aus dem "Gegenstand"-Dropdown, um Stundenplan-Einträge dieses Faches hervorzuheben.
*   **Schulstufen-Filter**: Klicke auf die Schulstufen-Buttons, um Stundenplan-Einträge der jeweiligen Schulstufe hervorzuheben. Mehrere Schulstufen können gleichzeitig ausgewählt werden.
*   **"Alle anzeigen"**: Setzt alle Lehrer-, Gegenstands- und Schulstufenfilter zurück.

### Ansicht-Steuerung (Header-Buttons oben rechts)

*   **L**: Blendet die Lehrer-Kürzel (z.B. L1, L2) in den Stundenplan-Zellen ein oder aus.
*   **ᵍ**: Blendet die Schulstufen-Badges (z.B. 5., 6.) in den Stundenplan-Zellen ein oder aus.
*   **SUP**: Öffnet und schließt das Supplierungs-Planungs-Panel.

### Supplierungs-Panel (SUP-Panel)

1.  Klicke auf den **SUP-Button** oben rechts, um das Panel zu öffnen.
2.  **Lehrer (krank)**: Wähle den Lehrer aus, der ausfällt.
3.  **Tage**: Wähle die Tage aus, an denen der Lehrer abwesend ist.
4.  **"Vorschläge finden"**: Das Panel zeigt eine Liste der Stunden an, die der kranke Lehrer unterrichtet hätte. Für jede Stunde werden Vorschläge für Ersatzlehrer gemacht, die möglichst wenige Freistunden um die Supplierung haben.
    *   Jeder Vorschlag enthält den vorgeschlagenen Ersatzlehrer und dessen Verfügbarkeits-Status.
    *   Du kannst über das Dropdown auch jeden anderen Lehrer der Schule auswählen.
5.  **Aktionen pro Stunde**:
    *   **"Übernehmen" (Blauer Button)**: Weist den gewählten Ersatzlehrer für diese Stunde zu. Die Zelle im Stundenplan wird zweifarbig dargestellt (kranker Lehrer / Ersatzlehrer) und mit "SUP" markiert. Der Slot wird als belegt markiert und kann nicht erneut zugewiesen werden.
    *   **"Entfällt" (Roter Button)**: Markiert die Stunde als entfallen. Die Zelle im Stundenplan wird grau dargestellt und mit "ENTFÄLLT" markiert. Der Slot wird ebenfalls als belegt markiert.
6.  **"Zurücksetzen"**: Löscht alle gespeicherten Supplierungen und entfallenen Stunden und setzt den Plan auf den Originalzustand zurück.
7.  **Panel verschieben**: Klicke und ziehe die Titelzeile des Panels, um es an eine beliebige Stelle auf dem Bildschirm zu verschieben. Schließe es mit dem "×"-Symbol.

### Supplierungs-Zusammenfassung (unterhalb des Stundenplans)

Dieser Bereich listet alle zugewiesenen Supplierungen und entfallenen Stunden übersichtlich nach Tagen gruppiert auf.

*   Jeder Eintrag zeigt Stunde, Zeit, Schulstufe, Fach und den Einspringer für den ausgefallenen Lehrer oder "ENTFÄLLT" an.
*   **"Entfernen"**: Macht eine einzelne Supplierung oder Entfall rückgängig.
*   **"Drucken"**: Druckt die gesamte Stundenplan-Ansicht.
*   **"Nur SUP drucken"**: Druckt eine saubere Übersicht nur der Supplierungs-Zusammenfassung, ohne den Stundenplan selbst. Ideal für den Ausdruck.
*   **"Als Text speichern"**: Exportiert die Supplierungs-Zusammenfassung als einfache Textdatei (`supplierungen.txt`).

## Dateistruktur

*   `Stundenplan.html`: Die Haupt-HTML-Datei, die die Struktur der Anwendung definiert und CSS/JS einbindet.
*   `styles.css`: Enthält alle visuellen Styles (CSS) für das Layout, die Filter, die Tabellen und die speziellen Hervorhebungen.
*   `script.js`: Enthält die gesamte Logik (JavaScript) für die dynamische Generierung des Stundenplans, die Filterung, die Zeit-Hervorhebung, das SUP-System und die Daten-Persistenz. 