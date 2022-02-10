Test2
===

.. autosummary::
   :toctree: generated

   test2as
   
   # Datenbanken

## Select immer mit Filter

Verwenden Sie SQL-Select nur in Verbindung mit Filtern (WHERE-Klausel), um nicht die ganze Tabelle in den Arbeitsspeicher zu laden. In Verbindung mit Transfermarkierungen filtern Sie z. B. nach `<Transferflag> <> 1`

## Transferierte Datensätze markieren

Markieren Sie transferierte Datensätze. Halten Sie in Ihren Tabellen Spalten vor, in denen der OPC Router transferierte Datensätze markieren kann („Transferflag“ nicht übertragen, übertragen, Transferfehler). Die Transferflag-Spalten sollten mit dem Standardwert „0“ belegt werden und nicht NULL annehmen dürfen, damit immer eine korrekte Zuordnung zu den drei Status gewährleistet ist.

**Transferflag indizieren**

Zur Verbesserung der Leistung sollte die Transferflag-Spalte wie folgt indiziert werden:

*   Wenn der OPC Router nach Transferflag = 0 filtern soll:

    ```
    CREATE NONCLUSTERED INDEX [IX_TransferTable_Transferflag] ON [dbo].[TransferTable]
    (
      [Transferflag] ASC
    )
    WHERE ([Transferflag]=(0))
    GO
    ```
*   Wenn der OPC Router nach Transferflag _<>_ 1 filtern soll:

    ```
    CREATE NONCLUSTERED INDEX [IX_TransferTable_Transferflag] ON [dbo].[TransferTable]
    (
      [Transferflag] ASC
    )
    WHERE ([Transferflag]<>(1))
    GO
    ```

## Select-Ergebnisse sortieren

Sortieren Sie die Tabelle nach dem Transfer-Flag aufsteigend. So werden zuerst die nicht transferierten Datensätze übertragen; fehlerhafte Einzeltransfers werden erst am Ende des Transfers erneut versucht. Zur Leistungsoptimierung kann nach der Transfer-Flag-Spalte gefiltert werden (Transfer-Flag = 0 oder = 2). In der Datenbank kann dazu ein entsprechend gefilterter Index angelegt werden.

## Datenbank-Design

Datenbanktabellen sollten sinnvoll indiziert werden:

* Spalten, innerhalb derer häufig gesucht wird, sollten indiziert werden.
* Werden indizierte Spalten bestehender Datensätze häufig aktualisiert, wird der Index nach und nach fragmentiert und muss regelmäßig neu erstellt werden. Anderenfalls wären Leistungseinbußen die Folge.

Weitere Hinweise, auch zur Verwendung von Diagnose-Scripts, finden Sie im inray-Inbetriebnahme-Handbuch, das Sie auf der Installationsquelle unter Additionals/Doku finden.
