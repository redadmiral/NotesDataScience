Notes
=====

```
1. Everything that exists is an object. 2. Everything that happens is a function call.
  - John Chambers, Entwickler von R
```

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

##Die Geschichte von S und R
R ist ein Dialekt von S. S wurde 1976 an den Bell Laboratories entwickelt um Statistiken zu verarbeiten. Es bastand aus Fortran Bibliotheken. S wurde sehr einsteigerfreundlich entwickelt, so dass die Nutzer nicht programmieren können mussten um mit S zu arbeiten und langsam in die Programmierumgebung eingeführt werden sollten. Dort konnten die Nutzer ihre eigenen Tools schreiben und wurden so langsam vom Nutzer zum Programmierer.

R wurde 1991 in Neuseeland entwickelt und wurde 95 unter GNU-Lizenz veröffentlicht. Die Entwicklung wird von der R-Core-Group vorangetrieben. R hat auch einige Nachteile, die zum Teil auf dem Alter von S beruhen. So werden 3D-Grafiken nur sehr schlecht unterstützt und alles was in R verarbeitet werden soll muss auf dem Rechner selbst gespeichert werden. Wenn der Datensatz also größer ist als der Arbeitsspeicher kann er nicht bearbeitet werden. In der Helpfile von read.tables() stehen Tipps zum optimieren des Speicherbedarfs.


Der R-Core besteht aus den R-base und R-recommended Paketen. Diese werden von der Core-Group maintained. Es sind auf CRAN (Comprehensive R Archive Network) über 4.000 weitere Pakete verfügbar, die von den Usern maintained werden. Auf der [Homepage](https://cran.r-project.org/) von CRAN sind verschiedene Manuals zum Download verfügbar. Vor allem seien das [Import/Export Manual](https://cran.r-project.org/doc/manuals/r-release/R-data.pdf) und das [Introduction-Manual](https://cran.r-project.org/doc/manuals/r-release/R-intro.pdf).


## Erste Swirl-Übungen

+ **`seq(m, n, by)`** erstellt eine Zahlenreihe von `m` nach `n` mit Iterationsweite by
+ **`m:n`** erstellt eine Zahlenreihe von `m` nach n.
+ **`length()`** gibt die Länge eines Vektors aus.
+ **`class(x)`** gibt die Klasse von`x`aus.
+ **`list.files()`** zeigt alle Dateien im Arbeitsverzeichnis an
+ **`getwd()`** gibt das Arbeitsverzeichnis aus
+ **`setwd("Dateipfad")`** setzt das Arbeitsverzeichnis auf `Dateipfad`
+ **`mean(x)`** berechnet den Mittelwert von x
+ **`sample(n)`** gibt 1 bis n in zufälliger Reihenfolge aus.
+ **`Sys.Date()`** gibt die Systemzeit aus.
+ **`paste()`** nimmt eine beliebige Anzahl an Strings aus und verbindet sie zu einem. Standardtrenner ist das Leerzeichen.
+ **`na.rm(x)`** entfernt alle `NA`s aus `x`
+ **`invisible()`** verhindert dass das zurückgegebene Objekt auf dem Bildschirm ausgegeben wird.


## Subsetting vectors

Der erste Eintrag eines Vektors in R hat die Nummer 1, nicht 0 wie bei den meisten anderen Sprachen. Vektoren können nur einen Typ Daten speichern, also nur `numeric`, `logical`, `character`, `integer` und `complex`. Wenn diese vermischt werden, werden alle Datentypen zum am wenigsten speziellen, im Normalfall `character` gewandelt. Ausnahme ist die Kombination `logical` und `numeric`, der zu `numeric` wird.

+ **`?Funktionsname`** gibt die Hilfeseite aus.
+ **`[n:m]`** gibt die ganzen Zahlen zwischen `n` und `m` aus. Funktioniert auch rückwärts, wenn `n` < m.
+ **`is.na`** Nimmt Vektor als Argument und gibt Vektor mit Bool-Werten zurück. TRUE wenn NA, FALSE wenn nicht NA7
..+ **`y[!is.na(y)]`** gibt eine Teilmenge aus, die nur Werte enthält, die nicht NA sind.
..+ **`y[y>0]`** gibt eine Teilmenge aus, die nur die positiven Werte von`y`ausgibt. NA ist positiv und negativ.
+ **`x[n]`** gibt den n-ten Wert von`x`aus. Nummerierung beginnt bei 1.
+ **`x[-n]`** gibt alle Werte von`x`bis auf `n` aus.
+ **`x["name1"]`** gibt den Wert namens "name1" eines benannten Vektors aus.
+ **`x[-c(m, n, o)]`** gibt alle Werte bis auf m, `n` und o aus.
+ **`c(name1 = 1, name2 = 2, ...)`** Erstellt benannten Vektor
+ **`names()`** gibt den Namen von benannten Vektoren aus.
+ **`identical()`** überprüft, ob zwei Vektoren gleich sind.
+ **`as.numeric(x)`** wandelt `x` in Typ numeric um. Funktioniert auch mit `as.logical()` und `as.character()`

##Matrizen und Data Frames
Matrizen können nur einen spezifischen Datentyp beinhalten. Data Frames dahingegen verschiedene. Matrizen werden aus Vektoren erstellt, deren dim()-Attribut verändert wurde oder dem matrix()-Befehl.

+ **`matrix(nrow=n, ncol= m)`** erstellt eine leere n*m-Matrix
+ **`dim()`** gibt das dim-Attribut aus
+ **`dim(x) <- c(n, m)`** gibt`x`n Zeilen und `m` Spalten
+ **`matrix(x)`** erstellt die Matrix x
+ **`cbind(x, y)`** verbindet die beiden Vektoren`x`und `y`. Beide sind eine Spalte in der Matrix. Nur bei selbem Datentyp anwenden (Int-Int, Str-Str)
+ **`rbind(x, y)`** verbindet die beiden Vektoren `x` und `y`. Beide sind eine Zeile in der Matrix. Nur bei selbem Datentyp anwenden (Int-Int, Str-Str)
+ **`data.frame(x, y)`** Erstellt Dataframe aus `x` und `y`. Belässt verschiedene Datentypen im Ausgangszustand und lässt gemischte Datensätze zu.
+ **``colnames(x)`** greift auf die Spaltennamen einer Matrix oder eines Dataframes zu.
+ **``rownames(x)`** greift auf die Zeilennamen einer Matrix oder eines Dataframes zu.
+ **`colnames(x) <- vector`** weißt die in `vector` gespeicherten Strings den Spalten von `x` zu.

## Listen
Auch Listen können verschiedene Dateitypen beinhalten. Ihre einzelnen Bestandteiler werden durch eckige Doppelklammern `list[[n]]` aufgerufen.

+ **`list <- list(a=1, b=2, c=3)`** erstellt eine benannte Liste.

## Faktoren
Faktoren werden benutzt um Datenkategorien zu beschreiben. Sie nehmen verschiedene Datentypen auf, `character` macht jedoch am meisten Sinn, da sie benutzt werden um Daten zu beschreiben. Typische Werte eines Faktors sind bspw. `yes` und `no` oder `männlich` und `weiblich`. Die einzelnen Kategorien werden in einem Attribut `levels` gespeichert.

+ **`table(x)`** gibt die Anzahl aus, wie oft jedes der Levels verwendet wurde.
+ **`unclass(x)`** beschreibt die Levels in `integers`. So werden sie "unter der Haube" auch dargestellt. Aus `yes` und `no` wird `1` und `2`.
+ **`x <- factor(c("yes", "no", "no"), leves="yes", "no")`** Lässt den User selbst die Reihenfolge der Levels festlegen. Hier ist `yes` mit `1` und `no` mit `2` codiert. Default wäre andersrum, weil n im Alphabet vor y kommt.

## NA und NaN

NA (Not Available) und NaN (Not a Number) sind fehlende Werte. Sie entstehen bei unzlässigen Operationen wie 0/0. NA und NaN können verschiedene Klassen haben, je nachdem aus welcher Operation sie hervorgegangen sind. NaNs sind alle NA, aber NAs sind nicht alle NaNs.

+ **`is.na(x)`** checkt welcher Wert von x NA ist und gibt einen Vektor mit Bool-Werten zurück.
+ **`is.nan(x)`** checkt welcher Wert von x NaN ist und gibt einen Vektor mit Bool-Werten zurück.

#Daten einlesen

+ **`read.table`** um Tabellen einzulesen Standardseperator ist Leerzeichen.
+ **`read.csv`** um Tabellen einzulesen. Standardseperator ist Komma.
+ **`readLines`** um Zeilen einer Textdatei einzulesen
+ **`source`** um in R-Dateien zu lesen
+ **`dget`** um in R-Dateien zu lesen
+ **`load`** um Workspace zu laden
+ **`unserialize`** um einzelne R-Objekte als Binaries einzulesen

Der Speicherbedarf kann mit der Formel Zeilen*Spalten*8 Byte (wenn ausschließlich numerische Daten) berechnet werden. Wegen anfallender Bearbeitungen des Datensatzes beim einlesen sollte der verfügbare RAM etwa doppelt so groß sein wie der Datensatz.

Um den Speicherbedarf zu minimieren ist es hilfreich, R die Klassen der jeweilgen Spalten anzugeben. Dies geschieht am leichtesten mit:
```
initial <- read.table("database.txt", nrows=100) #Hier werden die ersten 100 Zeilen eingelesen und die Klassen automatisch erkannt.
`classes <- sapply(initial, class)` #Hier werden die Klassen aus initial im Vektor classes gespeichert
`tabAll <- read.table("database.txt", colClasses=classes)` #Hier werden die Klassen aus classes der ganzen Datenbank zugeordnet.
```
##Textformate
Textformate werden normalerweise mit `dump` oder `dput` erstellt. Sie enthalten Metadaten in der Datei selbst, mit der sie leichter von R verstanden werden können und im Zweifel auch leichter wieder hergestellt werden können falls die Datei beschädigt wurde. Textformate sind allerdings auch bedeutend größer als die reinen Matrizen oder Vektoren aus denen sie erstellt werden.

Eine Datenbank im Textformat kann mit
```
> y <- data.frame(a=1, b=a)
> y
a b
1 1 a
> dput(y)
structure(list(a = 1, b = structure(1L, .Label = "a", class = "factor")), .Names = c("a", "b"), row.names = c(NA, -1L), class = "data.frame")
```

+ **`dput(x, Dateiname.R)`** nimmt den Vektor `x` und schreibt ihn in `Dateiname.R`.
+ **`dget(Dateiname.R)`** importiert `Dateiname.R`
+ **`dump(c("x", "y"), Dateiname.R)`** nimmt `x` und `y` und schreibt es in `Dateiname.R`.
+ **``**

##Nach Hause telefonieren
Durch Fileconnections werden Dateien einer Variablen in R zugewiesen. Es gibt verschiedene Fileconnections:
+ **`file`**
+ **`gzfile`**
+ **`bzfile`**
+ **`url`**

`con <- file(Datei.txt, "r")` Dadurch wird con zum Fileconnector zu `Datei.txt`. Neben `r(ead)` gibt es noch `w(rite)` und `a(ppending)`.

Fileconnections werden auch verwendet um auf Webpages zuzugreifen und sie auszulesen:

```>  con <- url("http://marco-lehner.de", "r")
> x <- readLines(con)
> head(x)
[1] "<!DOCTYPE html>"                                                         
[2] "<html lang=\"de-DE\" prefix=\"og: http://ogp.me/ns#\">"                  
[3] "<head>"                                                                  
[4] "<meta charset=\"UTF-8\">"                                                
[5] "<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">"
[6] "<title>Marco Lehner - Netzkrams und Technologie</title>"                 
```

##Teilmengen - Subsetting
+ **`x[1]`** gibt das erste Objekt mit der selben Klasse wie das Ursprungsobjekt aus.
+ **`x[1, 2]`** gibt das erste Objekt in der zweiten Spalte einer Matrix als Vektor aus.
+ **`x[[1]]`** wird benutzt um den ersten Einzelwert aus Dataframes und Listen zu ziehen.
+ **`x[[Name]]`** wird benutzt um den Einzelwert `Name` aus Dataframes und Listen zu ziehen. Funktioniert auch mit der Variable `Name`.
+ **`x$Name`** zieht den Einzelwert `Name` aus Dataframes und Listen. Funktioniert nicht mit der Variable `Name`.

###NA-Werte entfernen
```
bad <- is.na(x)
good <- x[!bad]
```

+ **`is.na(x)`** gibt einen Bool-Vektor aus mit `TRUE` an den Stellen wo `NA`s sind.
+ **`complete.cases(x,y)`** gibt einen Bool-Vektor aus mit `FALSE` an den Stellen wo bei `x` _und_ `y` `NA`s sind. Bei Matrizen werden die Zeilen mit `FALSE` markiert, die mindestens ein `NA` enthalten.

##Bool-Werte

Die logischen Operatoren sind wie überall `<`, `>`, `==`, `!`. Die und/oder Operatoren gehen sowohl einzeln (`&`, `|`) als auch doppelt (`&&`, `||`). Exklusiv-Oder steht über die Funktion `xor()`bereit.  Bei einzelner Nennung wird bei einem Vektor jeder Wert mit dem anderen abgeglichen
```
> TRUE & c(TRUE, FALSE, FALSE)
[1]  TRUE FALSE FALSE
```
bei doppelter Nennung nur der erste Wert
```
> TRUE & c(TRUE, FALSE, FALSE)
[1]  TRUE
```
Die `&`-Operatoren werden dabei vor den `|`-Operatoren berechnet.

+ **`isTRUE(x)`** gibt `TRUE` aus, wenn x `TRUE` ist.
+ **`xor()`** Exclusive or. Nur T-F oder F-T gibt `TRUE`
+ **`which(x==y)`** Gibt die Indizes der TRUEs in einem Vektor an. (x==y gibt einen Vektor mit Bool-Werten aus.)
+ **`any(x)`** gibt TRUE zurück, wenn x mindestens ein TRUE enthält.
+ **`all(x)`** gibt TRUE zurück, wenn alle Teile von x TRUE sind.

#Funktionen
##Definition
Funktionen werden folgendermaßen definiert:
```
function_name <- function(arg1, arg2){
Manipuliere die Argumente
Gib einen Wert aus
}
```
Die Ausgabe der Funktion ist immer der Wert, der in der letzten Zeile berechnet wird.
Als Beispiel die my_mean-Funktion aus dem swirl-Kurs:
```
my_mean <- function(my_vector) {
  sum(my_vector)/length(my_vector)
}
```
my_mean gibt den Mittelwert des eingegebenen Vektors aus. Wenn gewünscht ist, dass eine unendliche Zahl an Argumenten übergeben werden kann, so setzt man statt eines Argumentnamens `...` ein. Wenn ein **Standardwert** definiert werden soll wird dieser in den Eingabewerten definiert.

```
addieren() <- function(number, incrementer = 1) {
  number + incrementer
}
```
Die Funktion addieren addiert nun bei der Eingabe einer Zahl `addieren(4)` die Zahl mit eins. Der Nutzer kann jedoch `addieren(4, incrementer = 4)` eingeben, die Zahl wird nun um vier erhöht.
Um einer Funktion eine andere Funktion zu übergeben wird diese in den Argumenten mit `func` vermerkt.
```
funktionsfunktion() <- function(func, input) {
  func(input)
}
```
Diese Funktion ist recht langweilig und unsinnig, denn alles was sie macht ist eine Funktion als Argument zu nehmen und den zweiten Input in die Funktion einzusetzen.

Um einem Programm eine On/Off-Funktion hinzuzufügen wird diese mit TRUE/FALSE in den Argumenten vermerkt. Um bspw. NAs aus dem verarbeiteten Datensatz zu entfernen schreibt man
```
mean <- function(x, removeNA=TRUE) {
  mean(x, na.rm = removeNA)
}
```

###Binäroperatoren definieren
Neben den bekannten Binäroperatoren (`+`, `-`, `/` und `*`) können in R auch eigene Binäroperatoren definiert werden. Macht aber nur Sinn, wenn diese auch sehr oft verwendet werden, sonst schränken sie die Lesbarkeit des Programms ein. Sie werden ähnlich wie Funktionen definiert:

```
"%Name%" <- function{arg1, arg2} {
  #Here is where the magic happens
}
```
Hier ist vor allem auf die Anführungszeichen um den Operatornamen zu achten. Aufgerufen wird der Operator mittels
```
4 %Name% 5
```

##Ellipsen
Bei der Definition einer Funktion kann auch eine unbestimmte Anzahl an Argumenten vorgesehen werden.
```
funktion <- function(argumtent1, ..., argument2=4) {
  #Hier passiert was
}
```
Dazu wird eine Ellippse `...` verwendet. Sie kann eine beliebige Zahl an Argumenten aufnehmen, um sie zu verarbeiten. Alle darauf folgenden Argumente müssen mit einem Standardwert versehen sein. Wenn dieser geändert werden soll, muss der Argumentname mit angegeben werden.
Die Ellipse wird in der Funktion in eine Liste übergeben und von dort aus einzelnen Argumenten zugewiesen.
```
funktion <- function(argument1, ..., argument2=4) {
  args <- list(...)
  arg1 <- args[1]
  etc. pp.
  später sinnvollerweise mit loop.
}
```
#Kontrollstrukturen

+ **`if/else`**
+ **`for`**
+ **`while`**
+ **`repeat`** wiederholt einen unendlichen Loop
+ **`break`** beendet die Wiederholung
+ **`next`** überspringt eine Wiederholung
+ **`return`** beendet die Funktion und gibt einen Wert aus (oder auch nicht)

##if/else
```
if(condition1) {
  #Code der ausgeführt wird, wenn condition1 == TRUE
}
elseif(condition2) {
  #Code der ausgeführt wird, wenn condition2 == TRUE
}
else {
  #Code der ausgeführt wird, wenn condition1 == FALSE && condition2 == FALSE
}
```
if kann auch für sich alleine stehen. Else ist nicht nötig. Die if-Funktion kann direkt einer Variable zugewiesen werden:
```
if(x<4) {
  y <- 5
}
else {
  y <- 10
}
```
ist das selbe wie
```
y <- if(x<4) {
  5
}
else {
  10
}
```
##for-Schleife
```
for(i in 1:10) {
  print i
}
```
Einfacher, und ohne `length(x)` gehts mit:
```
x <- c("a", "b", "c")

for(letter in x) {
  print(letter)
}
```
For-Schleifen sind auch in einer einzigen Zeile ohne geschweifte Klammern möglich, wenn er nur eine Zeile hat.
##while-Schleife
```
count <- 0
while(count < 10) {
  print(count)
  count <- count + 1
}
```
##repeat
```
repeat {
  #Was hier steht wird für immer wiederholt
  if(condition1) {
    #Außer man breakt.
    break
  }
}
```
repeat-Loops können prinzipiell für immer laufen und damit das Programm hängen lassen. Use with care.

##next & return
```
for (i in 1:100) {
  if (i<20) {
    #überspringt die ersten 19 Wiederholungen
    next
  }

}
```
return hat die prinzipiell gleiche Funktionalität, wird nur meist für Funktionen verwendet und kann einen Wert zurückgeben.
#Zeit und Datum

Zeit und Datum lassen sich mit Rechenoperatoren `+`, `-`, `*` und `/` verarbeiten. Format stimmt dann sogar noch.

+ **`Sys.date()`** gibt das aktuelle Datum aus
+ **`Sys.time()`** gibt die aktuelle Zeit aus
+ **`unclass()`** legt frei was behind the scenes passiert. `unclass(Sys.time)` gibt die Sekunden seit dem 1. Januar 1970 aus.
+ **`as.Date(YYYY-MM-DD)`** formatiert als Datum
+ **`strptime("October 17, 1986 08:24", , "%B %d, %Y %H:%M")`** nimmt einen String auf, der ein Datum enthält und formatiert es als Datumsformat. Input egal, weiter Flags siehe man-page.
+ **`weekdays(Sys.date())`** gibt den Wochentag aus, solange der input ein beliebiges Datumsformat ist.
+ **`months(Sys.time)`** gibt den Monat aus, solange der input ein beliebiges Datumsformat ist.
+ **`quarters(x)`** gibt das Quartal aus, solange der input ein beliebiges Datumsformat ist.
+ **`difftime(Sys.date, zeitVariable, units="days")`** gibt die Zeitdifferenz aus.

Das [lubridate-Paket](https://cran.r-project.org/web/packages/lubridate/vignettes/lubridate.html) von Hadley Wickham fügt mehr Funktionen für die Zeitverarbeitung hinzu. `base` hat aber auch schon einiges.

#Bereiche

+ **`environment()`** gibt den Arbeitsbereich aus, in dem die Variable definiert ist.
+ **``**

Wenn eine Befehl aufgerufen wird, sucht R in verschiedenen Bereichen nach dem Begriff:
```
[1] ".GlobalEnv"        "tools:rstudio"     "package:stats"     "package:graphics"
[5] "package:grDevices" "package:utils"     "package:datasets"  "package:methods"  
[9] "Autoloads"         "package:base"
```
Die obige Liste kann mit `search()` aufgerufen werden. Zuerst durchsucht R die globale Umgebung, also ob das Paket bereits definiert ist. Wenn nicht in absteigender Reihenfolge durch die jeweiligen Tools und Pakete. Wenn neue Pakete geladen werden, werden diese stets an die zweite Stelle gestellt. Man spricht hier vom **dynamischen Scoping**.
Dies kann sich zunutze gemacht werden, um Variablen Funktionseigenschaften zuzuweisen. Dazu wird eine Funktion definiert, die eine Funktion zurückgibt:
```
make.power <- function(n) {
  pow <- function(x) {
    x^n
  }
    pow
}
```
Wenn diese Funktion nun einer Variablen zugewiesen wird, wird der übergebene Wert `n` direkt an die Subfunktion weitergegeben, das `x` steht noch weiter zur Definition.
```
>cube <- make.power(3)
>square <- make.power(2)
>
>cube(3)
+[1] 27
>square(3)
+[1] 9
```
Die Funktion `make.power` versieht also die Variable mit der von ihr definierten Funktion.

#Loopfunktionen

Loopfunktionen werden vor allem in interaktiven Umgebungen benutzt, wenn es ungünstig ist einen Loop selbst zu schreiben.

+ **`lapply()`** loopt durch eine Liste und wendet eine Funktion auf jedes Element an.
+ **`sapply()`** loopt durch eine Liste und wendet eine Funktion auf jedes Element an. Vereinfacht das Ergebnis.
+ **`aplly(x, m, func)`** loopt durch ein mehrdimensionales Objekt `x` in Dimension `m` und führt dabei `func` aus.
+ **`tapply()`** loopt durch eine
+ **`mapply()`** loopt durch mehrere Listen und wendet eine Funktion auf jedes Element an.
+ **`split(x, x$Variablenname)`** teilt ein Objekt in Teilobjekte.

Loopfunktionen arbeiten häufig mit anonymen Funktionen, also Funktionen die keinen Namen haben. Sie werden direkt im Funktionsaufruf der `xapply()`-Funktion definiert.
```
>lapply(x, function(elt) elt[ ,1]) #extrahiert die erste Zeile eines Vektors
+$a
+[1] 1 3
+[1] 2 4 6
```

##apply()
Das Argument, das die Dimension beschreibt ist quasi als Auswahl zwischen Reihen und Spalten zu verstehen. `1` geht die einzelnen Reihen durch; `2` die einzelnen Spalten. Die Dimensionen trifft man auch in der Auswahl eines Elements aus einer Matrix matrix[1, 2] wieder.
Um die Summe oder den Mittelwert einer Reihe/Spalte zu berechnen gibt es eigene, optimierte Funktionen.

#Explorative Analyse eines Datensatzes

+ **`table(varname$colname)`** gibt die Anzahl verschiedener Objekte in einer Spalte aus.
+ **`str()`** gibt die Struktur eines Datensatzes zurück.
+ **`summary()`** gibt eine Zusammenfassung eines Datensatzes zurück.

#Simulation

Simulationen arbeiten sehr viel mit Zufallszahlen. Diese Zahlen sind aber nicht wirklich zufällig. Um den selben Satz an Zufallszahlen zu generieren muss mit der Funktion `set.seed(n)` der Seed auf die gleiche Zahl gesetzt werden.

+ **`sample(n:m, x)`** gibt x Zahlen aus dem Bereich n-m aus. Beispiel: Würfel. Gibt auch Vektoren in zufälliger Reihenfolge wieder aus.
+ **`rbinom(1, size = n, prob = m)`** gibt die Anzahl der geglückten Versuche von n Gesamtversuchen aus, bei denen das Ergebnis 1 mit der Wahrscheinlichkeit m eingetreten ist.
+ **`rnorm()`** gibt die Normalverteilung aus.
+ **`hist()`** gibt das Histogramm einer Verteilung aus.
+ **``**

Jede Funktion die mit der Normalverteilung zu tun hat hat 4 Geschmacksrichtungen:

+ **`d`** für die Dichte (density)
+ **`r`** für Zufallszahlengenerierung (random number generation)
+ **`p`** für kumulative Verteilungen (cumulative distribution)
+ **`q`** für die Quantilfunktion (quantile function)

Die Funktionen sind basically:

+ **`norm()`** Normalverteilung
+ **`pois()`** Poissonverteilung
+ **`binom`** Binomialverteilung
+ **``** Exponentialverteilung
+ **``** Gammaverteilung


##Linearmodelle simulieren
```
set.seed(1)
x <- rnorm(100) #100 Zufallswerte
#x <- rbinom(100, 1, 0.5) für binärwerte
e <- rnorm(100, 0, 2) #Noise
y <- 0.5 + 2 * x + e #Geradenfunktion
summary(y)
```

#Profiler

+ **`system.time()`** misst die Zeit, die vergeht um einen Befehl auszuführen. `user time` ist dabei die Zeit, die die CPU verbraucht. `Elapsed Time`, die Zeit die der Nutzer auf eine Ausgabe wartet.
+ **`Rprof()`** ruft den Profiler auf.
+ **`summaryRprof()`** gibt eine Zusammenfassung der Ergebnisse des Profilers aus. Dieses Programm kann mit dem `$by.total` und dem `$by.self` Argument ausgegeben werden. `by.total` zeigt absteigend an, wie viel Zeit in jeder Funktion verbraucht wurde, die aufgerufen wurde. Die ursprünglich aufgerufene Top-Level-Funktion hat dabei immer 100% und Rechenzeit die in Funktionen verbraucht wurde, die von einer Funktion in einer Funktion aufgerufen wurden, wird der übergeordneten Funktion zugerechnet. `by.self` führt dahingegen nur die Zeit auf, die eine Funktion tatsächlich verbraucht hat.
+ **``**
