Notes
=====

#Woche 1.1

##Kurzhilfe in R

Um die Hilfe zu einer Funktion aufzurufen `?Funktionsname` oder `help.search("Funktionsname")` im Terminal eingeben.

Die für eine Funktion möglichen Argumente werden mit `args("Funktionsname")` aufgelistet. Den Code einer Funktion kann man mit `Funktionsname` ohne Angabe von Klammern einsehen. Ein Cheat-Sheet ist unter [cran.r-project.org/doc/contrib/Short-refcard.pdf](http://cran.r-project.org/doc/contrib/Short-refcard.pdf) verfügbar.

#Woche 1.2

###Installieren von Paketen

Pakete werden mit `install.packages("Paketname")` installiert. Im Anschluss werden sie mit `library(Paketname)` ohne Anführungszeichen eingebunden.

#Woche 1.3

##Arten der Datenanalyse

Die einfachste Art der Datenanlyse ist die *deskriptive Analyse*. Sie beschreibt den Datensatz ohne ihn zu interpretieren. Zum Beispiel Demographische Grafiken oder Google Ngram.
*Explorative Analyse* versucht Zusammenhänge im Datensatz oder zwischen Datensätzen herzustellen. Dabei immer den Grundstz **Korrelation begründet keine Kausalität** beachten. Als Beispiel werden Untersuchungen an beschädigten Hirnen genannt, bei welchen sich verschiedene zerstörte Areale aufeinander auswirken.
Die *inferentielle Statistik* will Aussagen, die anhand einer kleinen Menge (n) getroffen wurden auf eine große Menge (N) übertragen.
In der *Predictive Analysis* ist ein gängier Fehler, den Faktor, der eine Veränderung von B vorhergesagt hat automatisch als Ursache der Veränderung anzunehmen. Sie versucht Daten auf einzelne Objekte anzuwenden, um damit das Verhalten anderer Objekte vorherzusehen. Klassiker ist hier die Wahlprognose oder auch die Kundenanalyse a lá "Wer A kaufte, kauft auch B".
Bei der *Kausalanalyse* werden erhobene Daten auf vermutete Ursache-Wirkungs-Beziehungen zwischen den Merkmalen überprüft. Diese wird zum Beispiel bei medizinischen Studien angewendet. Eine randomisierte Gruppe wird in Kontroll- und Patientengruppe gespalten um Kausalität zwischen einem eingenommenen Medikament und einer Veränderung feststellen zu können.
Die *Mechanistic Analysis* versucht deterministische Zusammenhänge zwischen zwei oder mehreren Faktoren herzustellen. Wenn A sich ändert, ändert sich auch B. Diese Art der Analyse ist vor allem bei ungenauen und großen Datensätzen schwierig. Sie wird vor allem in den Ingenieurswissenschaften und den Naturwissenschaften angewandt.

##Was sind Daten?

Daten sind Werte von qualitativen oder quantitativen Variablen, die einer Menge von Dingen zugeordnet werden können. Qualitative Daten sind Werte wie Nationalität, Name und Geschlecht; Quantitative Daten sind Werte wie Blutdruck, Alter und Größe.
Daten tauchen meist als Rohdaten in Form von CSV oder XLS-Dateien auf oder werden über APIs bezogen.


##Aufbau der Studien und Experimente

Um Daten zu teilen und so kollaborativ arbeiten zu können, empfiehlt es sich [Figshare](https://figshare.com) zu verwenden. Leek hat außerdem einen [Leitfaden](https://github.com/jtleek/datasharing) zum Teilen von Datensätzen entwickelt.

#Woche 2.1

## ASDF

+ **seq(m, n, by)** erstellt eine Zahlenreihe von m nach n mit Iterationsweite by
+ **m:n** erstellt eine Zahlenreihe von m nach n.
+ **length()** gibt die Länge eines Vektors aus.
+ **class(x)** gibt die Klasse von x aus.

## Subsetting vectors

Der erste Eintrag eines Vektors in R hat die Nummer 1, nicht 0 wie bei den meisten anderen Sprachen.

+ **?Funktionsname** gibt die Hilfeseite aus.
+ **[n:m]** gibt die ganzen Zahlen zwischen n und m aus. Funktioniert auch rückwärts, wenn n < m.
+ **is.na** Nimmt Vektor als Argument und gibt Vektor mit Bool-Werten zurück. TRUE wenn NA, FALSE wenn nicht NA7
..+ **y[!is.na(y)]** gibt eine Teilmenge aus, die nur Werte enthält, die nicht NA sind.
..+ **y[y>0]** gibt eine Teilmenge aus, die nur die positiven Werte von y ausgibt. NA ist positiv und negativ.
+ **x[n]** gibt den n-ten Wert von x aus. Nummerierung beginnt bei 1.
+ **x[-n]** gibt alle Werte von x bis auf n aus.
+ **x["name1"]** gibt den Wert namens "name1" eines benannten Vektors aus.
+ **x[-c(m, n, o)]** gibt alle Werte bis auf m, n und o aus.
+ **c(name1 = 1, name2 = 2, ...)** Erstellt benannten Vektor
+ **names()** gibt den Namen von benannten Vektoren aus.
+ **identical()** überprüft, ob zwei Vektoren gleich sind.

##Matrizen und Data Frames
Matrizen können nur einen spezifischen Datentyp beinhalten. Data Frames dahingegen verschiedene. Matrizen werden aus Vektoren erstellt, deren dim()-Attribut verändert wurde oder dem matrix()-Befehl.

+ **dim()** gibt das dim-Attribut aus
+ **dim(x) <- c(n, m)** gibt x n Zeilen und m Spalten
+ **matrix(x)** erstellt die Matrix x
+ **cbind(x, y)** verbindet die beiden Vektoren x und y. Nur bei selbem Datentyp anwenden (Int-Int, Str-Str)
+ **data.frame(x, y)** Erstellt Dataframe aus x und y. Belässt verschiedene Datentypen im Ausgangszustand und lässt gemischte Datensätze zu.
+ **`colnames`**


##Die Geschichte von S und R
R ist ein Dialekt von S. S wurde 1976 an den Bell Laboratories entwickelt um Statistiken zu verarbeiten. Es bastand aus Fortran Bibliotheken. S wurde sehr einsteigerfreundlich entwickelt, so dass die Nutzer nicht programmieren können mussten um mit S zu arbeiten und langsam in die Programmierumgebung eingeführt werden sollten. Dort konnten die Nutzer ihre eigenen Tools schreiben und wurden so langsam vom Nutzer zum Programmierer.

R wurde 1991 in Neuseeland entwickelt und wurde 95 unter GNU-Lizenz veröffentlicht. Die Entwicklung wird von der R-Core-Group vorangetrieben. R hat auch einige Nachteile, die zum Teil auf dem Alter von S beruhen. So werden 3D-Grafiken nur sehr schlecht unterstützt und alles was in R verarbeitet werden soll muss auf dem Rechner selbst gespeichert werden. Wenn der Datensatz also größer ist als die Festplatte kann er nicht bearbeitet werden.

Der R-Core besteht aus den R-base und R-recommended Paketen. Diese werden von der Core-Group maintained. Es sind auf CRAN (Comprehensive R Archive Network) über 4.000 weitere Pakete verfügbar, die von den Usern maintained werden. Auf der [Homepage](https://cran.r-project.org/) von CRAN sind verschiedene Manuals zum Download verfügbar. Vor allem seien das [Import/Export Manual](https://cran.r-project.org/doc/manuals/r-release/R-data.pdf) und das [Introduction-Manual](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf).

##Describe the differences between atomic data types


##Execute basic arithmetic operations


##Subset R objects using the "[", "[[", and "$" operators and logical vectors


##Describe the explicit coercion feature of R


##Remove missing (NA) values from a vector
