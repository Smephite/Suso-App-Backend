***Konzept: Vertretungsplan Applikation***
==========================================

Funktionalit�t:
---------------

Eine Vertretungsplan App, ist wie der Name bereits vermuten l�sst, f�r
die Darstellung eines Vertretungsplanes zu gebrauchen. Der von diesem
Projekt angezielte Verwendungsbereich, liegt im Schulischen.

Eine derartige App, kann jedoch auch f�r andere Zwecke genutzt werden.
So k�nnte z.B. mit Hilfe eines eingebunden Stundenplans, der konkrete
Ablauf eines Tages mit Vertretung, Raum�nderung, etc. einfach
dargestellt werden und der Nutzer einfach �ber �nderungen informiert
werden.

Ebenfalls kann eine solche App, wenn sie modular entwickelt wurde, auch
Bereiche �bernehmen, wie das Informieren der Nutzer �ber Schulrelevante
Ereignisse wie in etwa einem Elternabend oder einem bevorstehenden
Schulkonzertes.

Die Aufgabe der App k�nnte ebenfalls sein die au�erschulische
Kommunikation zwischen Lehrer und Sch�ler zu vereinfachen. Hierbei
k�nnten beispielsweise Klausuren oder Hausaufgaben, direkt in der App
vergeben bzw. angek�ndigt werden und die Sch�ler an diese fr�hzeitig und
zuverl�ssig erinnert werden. Gleicherma�en k�nnte sich durch die App ein
Sch�ler am Morgen krank melden, wobei hierbei die Lehrer des Sch�lers
�ber dessen Abwesenheit benachrichtigt werden und so bei einer
vielleicht geplanten Pr�sentation des Sch�lers den Unterricht fr�hzeitig
anpassen k�nnten. F�r eine solche Funktionalit�t w�re es nat�rlich im
Sinne des Lehrers nur Benachrichtigungen bestimmter Kurse zu empfangen.

Mithilfe der Tatsache, dass der Applikation der Stundenplan und die
Abwesenheit der Sch�ler bekannt sind, k�nnte diese auch als eine
digitale Anwesenheitsliste fungieren, in der die Fachlehrer die
Anwesenheit bzw. Abwesenheit eines Sch�lers digital vermerken und
�berpr�fen k�nnen.

Zielgruppen:
------------

Nach der oben genannten Funktionalit�t, ergeben sich drei Zielgruppen.

Die Sch�lerschaft, welche durch diese Applikation digitalen Zugriff auf
ihren aktuellen Stunden/Vertretungsplan haben und digital eine �bersicht
�ber Klausuren und Hausaufgaben behalten k�nnen.

Die Lehrerschaft, welche mit Hilfe dieser Applikation ihren Unterricht
besser planen, ausf�hren und auch digitalisieren kann, da sie einfacher
�ber �nderungen in der anwesenden Sch�lerliste informiert wird und
sichergehen kann, dass es jedem Sch�ler m�glich ist die Hausaufgaben
auch nachtr�glich einzusehen.

Die SMV, welche einen Kommunikationskanal durch die App h�tte, wodurch
diese zum Beispiel eine digitale Version einer Sch�lerzeitung im Format
eines Blogs ver�ffentlichen oder �ber aktuell wichtige Themen
informieren k�nnte.

Aufbau:
-------

Die eigentliche Applikation ist nur die anzeigende Einheit. Sie holt
sich bei jedem Start der App die aktuell f�r den Nutzer relevanten Daten
von einem Backend Server. Das einheitliche senden von
Push-Benachrichtigungen wird durch den externen Dienst �Google Firebase�
realisiert. Dieser ist f�r die Distribution verantwortlich und setzt zu
diesem Zweck �Device-Tokens � ein, welche genutzt werden um einem
Bestimmen Ger�t Benachrichtigen zu senden.

Eine Datenbank ist ben�tigt, um diese �Device-Token� mit dem
spezifischen Nutzer zu verkn�pfen. Ebenfalls wird sie ben�tigt, um
diesen Nutzer einer Klasse und einem API-Key zuzuordnen. Ein weiterer
Nutzen liegt in der Speicherung einer Zeit, zu der sich ein Client
wieder verifizieren muss.

Die Verifikation wird durch eine Verbindung mit einem Schulinternen
Novell System erm�glicht, welche durch die Authentifizierung mit Hilfe
des Schulinternen Nutzernamen und Passworts geschieht und bei einem
Erfolg eine eindeutige ID zur�ckgibt. Diese ID wird an das Backend
weitergeleitet, welche von dem Novell System Informationen wie etwa die
Klasse des Sch�lers geliefert bekommt, welche in der Datenbank
gespeichert werden. Mit der Methode einer eindeutigen ID m�ssen keine
privaten Nutzerdaten an das Backend weitergegeben werden.

Bei der Anfrage eines Clients nach einem Vertretungsplans, wird der
Vertretungsplan und der Stundenplan des Anfragestellers aus einem Cache
(bzw. beim Ablaufen des Caches von einem Schulinternen Interface)
geladen und von der �Processing Unit� verarbeitet. Diese �Processing
Unit� wird ebenfalls regelm��ig von einem cronjob aufgerufen, welcher
das senden der Push Benachrichtigungen an �Google Firebase� ausl�st.

Die �Processing Unit� verarbeitet die Eingangsdaten und gibt diese f�r
den spezifischen Nutzer zugeschnitten aus. So in etwa werden nur die
Kurse, welche ein Sch�ler wirklich belegt diesem auch angezeigt.
