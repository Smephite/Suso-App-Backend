***Konzept: Vertretungsplan Applikation***
==========================================

Funktionalität:
---------------

Eine Vertretungsplan App, ist wie der Name bereits vermuten lässt, für
die Darstellung eines Vertretungsplanes zu gebrauchen. Der von diesem
Projekt angezielte Verwendungsbereich, liegt im Schulischen.

Eine derartige App, kann jedoch auch für andere Zwecke genutzt werden.
So könnte z.B. mit Hilfe eines eingebunden Stundenplans, der konkrete
Ablauf eines Tages mit Vertretung, Raumänderung, etc. einfach
dargestellt werden und der Nutzer einfach über Änderungen informiert
werden.

Ebenfalls kann eine solche App, wenn sie modular entwickelt wurde, auch
Bereiche übernehmen, wie das Informieren der Nutzer über Schulrelevante
Ereignisse wie in etwa einem Elternabend oder einem bevorstehenden
Schulkonzertes.

Die Aufgabe der App könnte ebenfalls sein die außerschulische
Kommunikation zwischen Lehrer und Schüler zu vereinfachen. Hierbei
könnten beispielsweise Klausuren oder Hausaufgaben, direkt in der App
vergeben bzw. angekündigt werden und die Schüler an diese frühzeitig und
zuverlässig erinnert werden. Gleichermaßen könnte sich durch die App ein
Schüler am Morgen krank melden, wobei hierbei die Lehrer des Schülers
über dessen Abwesenheit benachrichtigt werden und so bei einer
vielleicht geplanten Präsentation des Schülers den Unterricht frühzeitig
anpassen könnten. Für eine solche Funktionalität wäre es natürlich im
Sinne des Lehrers nur Benachrichtigungen bestimmter Kurse zu empfangen.

Mithilfe der Tatsache, dass der Applikation der Stundenplan und die
Abwesenheit der Schüler bekannt sind, könnte diese auch als eine
digitale Anwesenheitsliste fungieren, in der die Fachlehrer die
Anwesenheit bzw. Abwesenheit eines Schülers digital vermerken und
überprüfen können.

Zielgruppen:
------------

Nach der oben genannten Funktionalität, ergeben sich drei Zielgruppen.

Die Schülerschaft, welche durch diese Applikation digitalen Zugriff auf
ihren aktuellen Stunden/Vertretungsplan haben und digital eine Übersicht
über Klausuren und Hausaufgaben behalten können.

Die Lehrerschaft, welche mit Hilfe dieser Applikation ihren Unterricht
besser planen, ausführen und auch digitalisieren kann, da sie einfacher
über Änderungen in der anwesenden Schülerliste informiert wird und
sichergehen kann, dass es jedem Schüler möglich ist die Hausaufgaben
auch nachträglich einzusehen.

Die SMV, welche einen Kommunikationskanal durch die App hätte, wodurch
diese zum Beispiel eine digitale Version einer Schülerzeitung im Format
eines Blogs veröffentlichen oder über aktuell wichtige Themen
informieren könnte.

Aufbau:
-------

Die eigentliche Applikation ist nur die anzeigende Einheit. Sie holt
sich bei jedem Start der App die aktuell für den Nutzer relevanten Daten
von einem Backend Server. Das einheitliche senden von
Push-Benachrichtigungen wird durch den externen Dienst ‚Google Firebase‘
realisiert. Dieser ist für die Distribution verantwortlich und setzt zu
diesem Zweck ‚Device-Tokens ‘ ein, welche genutzt werden um einem
Bestimmen Gerät Benachrichtigen zu senden.

Eine Datenbank ist benötigt, um diese ‚Device-Token‘ mit dem
spezifischen Nutzer zu verknüpfen. Ebenfalls wird sie benötigt, um
diesen Nutzer einer Klasse und einem API-Key zuzuordnen. Ein weiterer
Nutzen liegt in der Speicherung einer Zeit, zu der sich ein Client
wieder verifizieren muss.

Die Verifikation wird durch eine Verbindung mit einem Schulinternen
Novell System ermöglicht, welche durch die Authentifizierung mit Hilfe
des Schulinternen Nutzernamen und Passworts geschieht und bei einem
Erfolg eine eindeutige ID zurückgibt. Diese ID wird an das Backend
weitergeleitet, welche von dem Novell System Informationen wie etwa die
Klasse des Schülers geliefert bekommt, welche in der Datenbank
gespeichert werden. Mit der Methode einer eindeutigen ID müssen keine
privaten Nutzerdaten an das Backend weitergegeben werden.

Bei der Anfrage eines Clients nach einem Vertretungsplans, wird der
Vertretungsplan und der Stundenplan des Anfragestellers aus einem Cache
(bzw. beim Ablaufen des Caches von einem Schulinternen Interface)
geladen und von der „Processing Unit“ verarbeitet. Diese „Processing
Unit“ wird ebenfalls regelmäßig von einem cronjob aufgerufen, welcher
das senden der Push Benachrichtigungen an ‚Google Firebase‘ auslöst.

Die „Processing Unit“ verarbeitet die Eingangsdaten und gibt diese für
den spezifischen Nutzer zugeschnitten aus. So in etwa werden nur die
Kurse, welche ein Schüler wirklich belegt diesem auch angezeigt.
