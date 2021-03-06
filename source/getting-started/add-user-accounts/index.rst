========================
 Erste Benutzeraufnahme
========================

In einer Schule müssen meist mehrere hundert bis einige tausend Schüler als
Benutzer angelegt werden müssen. Deshalb übernimmt diese komplexe
Aufgabe bei der *linuxmuster.net* das Programm *Sophomorix*.

*Sophomorix* liest alle Schüler aus einer Text-Datei ein, die z.B. aus
dem Schulverwaltungsprogramm der Schule bezogen wurde. Anschließend
werden alle Schüler dieser Liste, die im System noch nicht vorhanden
sind, angelegt, solche mit einer neuen Klasse versetzt und nicht mehr
aufgeführte Schüler aus dem System gelöscht.

Mit der *Schulkonsole* gibt es für den Netzwerkbetreuer ein
webbasiertes Werkzeug, das ihm die Bedienung von *Sophomorix* sehr
erleichtert. Die einzelnen Schritte werden im Folgenden erläutert. Der
Netzwerkbetreuer muss nur noch in Ausnahmefällen mit der Kommandozeile
arbeiten.

Um Benutzer neu aufzunehmen müssen die folgenden Schritte nacheinander
ausgeführt werden:

*   Schüler und Lehrerliste aus dem Schulverwaltungsprogramm exportieren.
*   Die Benutzerlisten auf dem Server einlesen. 
*   Alle Benutzerlisten auf Fehleingaben, oder Ähnlichkeiten mit vorhandenen Benutzern prüfen.
*   Danach evtl. die Benutzerlisten entsprechend korrigieren.
*   Benutzerdaten übernehmen, d.h. Benutzer jetzt tatsächlich anlegen
*   Passwortlisten bzw. Anmeldekärtchen ausdrucken (idR. durch das Lehrpersonal)

Im folgenden wird gezeigt wie die Erstaufnahme von Schülern vonstatten geht.

Erstaufnahme von Schülern
-------------------------
.. note:: Alle hier aufgelistete Schülernamen sind Beispielhaft und frei erfunden. Sollte es dennoch Menschen mit der gleichen Namenskombination geben, dann ist das Zufall.

Benutzerverwaltung ist Sache des Administrators, deshalb loggt sich der Administrator in die Schulkonsole ein

.. image:: media/school-console-admin-login.png

In der Schulkonsole wählen Sie  im Menü `Benutzer` `Schülerliste pflegen`

.. image:: media/menu-studentslist.png

und sehen ein leeres Fenster.

.. image:: media/user-management-students-empty.png

.. note:: Prinzipiell kann man die Schülerliste per `"Copy und Paste"`  in das leere Fenster einfügen. Hier wird gezeigt wie man die Datei importiert.

.. note:: Die Schülerliste muss im CSV-Format in der Form ``"Klasse; Zuname; Vorname; Geburtsdatum; Nr."`` vor liegen. Dabei ist das letzte Feld optional. Es enthält die im Schulverwaltungsprogramm eindeutig vergebene Schülernummer. Ist sie vorhanden, sollte man sie unbedingt mit übernehmen, das sie die Identifikation des richtigen Datensatzes bei Versetzungen, Namensänderungen usw. erheblich erleichtert. Falls die Nummer nicht vorhanden ist, besteht jede Zeile nur aus den 4 Feldern. 

.. note:: Die Schülerwaltungsprogramme der Länder besitzen idR. eine Funktion um Schülerdaten als .CSV-Datei zu exportieren. Diese Datei muss man sich als Administrator aushändigen lassen, wenn man nicht selbst Zugang zum Schülerverwaltungsprogramm hat.

Nach Klick auf `Durchsuchen`

.. image:: media/user-management-browse.png

navigiert man zu dem Ort an dem die aus der Schülerverwaltungsdatei exportierte Datei liegt. Hier auf dem ``Desktop`` die Datei ``schueler_aus_export.txt``.

.. image:: media/students-import-1.png

Man wählt die Datei durch Doppelklick aus und klickt im folgenden Fenster auf Hochladen

.. image:: media/students-import-3.png

Je nach Anzahl der Schüler dauert es eine Weile bis im folgenden Fenster die Liste der aufzunehmenden Schüler erscheint.

.. image:: media/students-import-4.png

Mit Klick auf `Änderungen speichern`

.. image:: media/students-import-5.png

werden die aufzunehmenden Schüler in der Datei ``schueler.txt`` auf dem Server unter ``/etc/sophomorix/user/`` abgespeichert

Nun muss die Datei schueler.txt überprüft werden. Dies geschieht durch Auswahl im Menü `Benutzer` `Benutzerlisten prüfen`,

.. image:: media/studentslist-check.png

um dann auf `Benutzerlisten überprüfen` zu klicken.

.. image:: media/studentslist-check-2.png

Ist das Überprüfen beendet erhält man eine Liste ähnlich der hier gezeigten

.. note :: Das Überprüfen ist nötig um eventuelle Fehler ausfindig zu machen. In mindestens einem Bundesland ist es möglich den Schüler-Namen mit Zahlen zu versehen. Solche Fehler meldet Sophomorix. Ebenfalls gemeldet werden Geburtsdaten die nicht der Realität entprechen bzw. nicht im Zeitraum der ``/etc/sophomorix/user/sophomorix.conf`` liegen.

.. note :: Um Probleme zu vermeiden ist es ratsam Sonderzeichen `ä; ö; ü; ß` umzuwandeln in `ae; oe; ue; ss`.

.. image:: media/studentslist-check-finished.png

Gegebenenfalls muss man die Datei schueler.txt noch überarbeiten, wenn in der Liste Fehler gemeldet werden. Das Überarbeiten kann selbstverständlich in der Schulkonsole erfolgen.

.. image:: media/studentslist-check-confirm.png

Sind alle Fehler beseitigt, dann klickt man auf `Benutzerdaten übernehmen`

.. note:: Man kann - auch wenn noch nicht alle Fehler beseitigt sind - auf `Benutzerdaten übernehmen` und `Benutzer anlegen` klicken. Dann werden die Schüler angelegt, bei denen die Datensätze in Ordnung sind. Man fährt danach mit dem Schritt `Benutzerlisten überprüfen` s.O. fort.

Es wird erneut eine Liste der anzulegenden Schüler angezeigt

.. image:: media/students-adduser.png

Unterhalb dieser Liste klickt man auf `Benutzer anlegen`.

Es folgen Statusmeldungen wie die im folgenden Bild gezeigten

.. image:: media/students-adduser-status.png 

Bei einer großen Schülerzahl kann es einige Stunden dauern bis das folgende Bild das Ende des Benutzerimports anzeigt

.. image:: media/students-adduser-finished.png

Damit ist die Erstaufnahme abgeschlossen.

.. note:: Im Sinne einer vernünftigen Arbeitsteilung sollte der Ausdruck der Kärtchen mit den Anmeldenamen und Passwörtern den Lehrern überlassen werden die mit den Schülern den Computerraum benutzen. Lehrer sollen auch die Passwörter von Schülern ändern, wenn das Passwort vergessen wurde.
