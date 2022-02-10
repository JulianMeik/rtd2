# Statusanzeige

In der Snap-in Leiste befindet sich der Button für den Status-Bereich.

Nach Klick auf den Button und einer Verbindung öffnet sich dafür das Statusfenster:

![Router-Status](<.gitbook/assets/status (2) (3) (3) (3) (4) (3).png>)

## Das Statuschart

Das Statuschart bietet detaillierte Informationen zu den einzelnen Datentransfers. Das Statuschart starten Sie über das entsprechende Snap-In im linken Seitenrand.

![Statuschart](<.gitbook/assets/statuschart_neu (2) (3) (3) (3) (4) (2).png>)

* Sie haben die Möglichkeit den anzuzeigenden Zeitraum einzugrenzen, indem Sie die Regler unter dem Statuschart entsprechend bewegen.
* Grüne Transferpunkte stellen die einzelnen Transfers da, welche in Ordnung waren und die Transfer Values werden in der Short Storage gespeichert. Die Vorhaltezeit wird dafür in den Einstellungen definiert. Klickt man auf einen Transferpunkt, bei dem die Vorhaltezeit abgelaufen ist, erscheint die Meldung „Transferwerte können nicht angezeigt werden, da die Vorhaltezeit der Werte abgelaufen ist“. Die roten Transferpunkte zeigen dagegen fehlerhafte Transfers an und werden dauerhaft in der Long Storage vorgehalten.
* Wenn Sie einen Transferpunkt anklicken, wird dieser hellblau dargestellt und die Daten unter dem Statuschart angezeigt. Mit den Pfeiltasten können Sie nach Markierung eines Transferpunktes zwischen den einzelnen Punkten hin- und herspringen.
* Wenn Sie mit der Maus auf einen Transferpunkt gehen, wird Ihnen die Ausführungszeit angezeigt.
* Über dem Statuschart finden Sie die Buttons „Vorheriger Transfer“ und „Nächster Transfer“, um sich jeweils den Transfer neben dem bisher ausgewählten Transfer anzeigen zu lassen. Mit dem Button Zur Live-Ansicht wechseln, können Sie den Verlauf der einzelnen Transfers beobachten.
* Über dem Statuschart finden Sie außerdem Buttons für die Zoomfunktionen („Zoom vergrößern“, „Zoom verkleinern“ und „Zoom zurücksetzen“). Der Zoom kann auch mit dem Mausrad verändert werden.
* Zusätzlich finden Sie über dem Statuschart den Button „Transferierte Werte durchsuchen“. Über diese Option lassen sich alle aufgezeichneten Werte, der aktuell geöffneten Verbindung, durchsuchen. Über den Button „Ansicht“ können Sie sich anschließend den Transfer im Statuschart anzeigen lassen. Die gefilterten Listen können Sie sich für weitere Auswertungen über den Button „Exportieren“ als Excel Dokument oder CSV Liste exportieren.
* In der Statusansicht können Sie nicht mit Doppelklick auf die einzelnen Verbindungselemente klicken. Angezeigt wird dies auch durch den Cursor, der sich in ein Verbotszeichen verwandelt, wenn Sie mit der Maus über ein Element in der Statusansicht gehen.
* Sind Strings oder Arrays zu lang, wird der transferierte Wert in der Darstellung abgeschnitten – er wird dennoch vollständig übertragen. Die Länge der Darstellung kann in den [Einstellungen](settings/) unter „Maximale Anzahl von Zeichen in der Statusanzeige“ angepasst werden. Der Standardwert beträgt 1000 Zeichen. 
* Fehler werden über die rote Kennzeichnung im Statuschart angezeigt und wenn Sie mit der Maus auf das Transferobjektfeld unter dem Statuschart fahren, bekommen Sie detaillierte Informationen zum Fehler angezeigt:

![Fehleranzeige](.gitbook/assets/fehlermeldungtransfer.png)

* Der Statusbalken ändert die Farbe, wenn ein Fehler auftritt, eine Warnung auftaucht oder die Verbindung abgebrochen wird. Der Statusbalken wird orange dargestellt (Prüfen der Verbindung), wenn die Verbindung geprüft wird und rot dargestellt, wenn die Verbindung im Zustand Error ist (Fehler im Plug-in). Wenn die Verbindung korrekt arbeitet, dann erscheint der Statusbalken in grün (Bereit).
* Auch Meldungen der Plug-ins können Sie sich unter dem Status-Snap-in anzeigen lassen.
* Wenn Sie vom Status in das Plug-in Snap-in wechseln, gelangen Sie automatisch in den Bearbeitungsmodus der geöffneten Verbindung.
* Wählen Sie in dem Status-Snap-im Plug-in-Baum eine Anbindung aus und lassen sich die Meldungen dafür anzeigen:

![Plug-in-Status](<.gitbook/assets/pluginstatus (2) (3) (3) (3) (4) (3).png>)

Wenn der OPC Router heruntergefahren wird, bekommen alle Verbindungen den Status „Shutdown“. In der Historie erscheint der Status dann in der Farbe rot.

Im Statusbaum können Sie über einen Rechtsklick der Transfer einer Verbindung manuell gestartet werden. Dafür ist es nicht nötig, dass ein Trigger in der Verbindung vorhanden ist. Die manuell gestarteten Transfers werden blau im Chart angezeigt. Zusätzlich wird aufgezeichnet, wer diesen Transfer gestartet hat.

Mit rechtem Mausklick können Sie im Verbindungsbereich Ihrer Statusanzeige das Pop-up-Menü „Ansicht exportieren“ sichtbar machen. Dieses Menü bietet Ihnen die Möglichkeit Ihre Verbindung als Bild zu exportieren oder in die Zwischenablage zu kopieren. Auf dem Bild wird jedoch nur die Verbindung mit den transferierten Werten dargestellt und nicht das Status Diagramm. Die Bilder können als Bitmap, PNG, JPEG oder GIF gespeichert werden.

TODO: Bewegt man die Maus über eine Übertragung wird das vollständige Array oder der vollständige Stream angezeigt.  Plus Bild zum besseren Verständnis.

## Eskalationsstufen für Statusaufzeichnung

Der OPC Router erkennt nun, wann zu viele Statusdaten aufgezeichnet werden oder der Datenbankspeicher fast gefüllt ist. Um einen vollen RAM-Speicher zu verhindern, leitet der OPC Router automatisch immer stärker werdende Gegenmaßnahmen ein. Die Übertragung von Nutzdaten wird durch diese Maßnahmen NICHT angepasst! Die Maßnahmen betreffen nur die Statusaufzeichnungen des OPC Routers. Die Aufzeichnung der Nutzdaten soll dadurch sichergestellt werden. In den Grundeinstellungen des OPC Routers stellen Sie ein, wie weit der OPC Router die Statusdatenbanken befüllen darf.

Folgende Eskalationsstufen gibt es:

* Eskalationsstufe 0:
  * Normales Verhalten
* Eskalationsstufe 1:
  * Ringspeicher Batchgröße überschritten
  * Statusdatenbank zu 60% gefüllt
  * Maßnahme: Keine Transferwerte von erfolgreichen Transfers mehr loggen (nur für Spam-Verbindungen)
* Eskalationstufe 2:
  * Ringspeicher Batchgröße um das Dreifache überschritten
  * Statusdatenbank zu 80% gefüllt
  * Maßnahme: Keine Transferwerte von erfolgreichen Transfers mehr loggen
* Eskalationsstufe 3:
  * Ringspeicher Batchgröße um das Sechsfache überschritten
  * Statusdatenbank zu 90% gefüllt
  * Maßnahme: Keine Transferwerte mehr loggen
* Eskalationsstufe 4:
  * Ringspeicher Batchgröße um das Zehnfache überschritten
  * Statusdatenbank zu 100% gefüllt
  * Maßnahme: Statusaufzeichnung von Transfers komplett deaktivieren

Wenn die Statusaufzeichnung deaktiviert wurde, gibt es eine Warnung in der Statusanzeige. Wenn die Aufzeichnung bei Eskalationsstufe 4 komplett deaktiviert wurde, wird der betroffene Zeitraum grau schraffiert.
