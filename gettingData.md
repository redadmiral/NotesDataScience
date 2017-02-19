#Getting and Cleaning Data
Es gibt verschiedene Wege an Daten zu kommen. Meistens werden sie zur Verfügung gestellt, manchmal müssen sie aber auch selbst gescraped werden. Was dann genau Rohdaten sind ist nicht leicht zu sagen und Frage der Perspektive. Für einen DNA-Sequenzer sind die Gewebeproben Rohdaten; die daraus erstellte Textdatei mit den sequenzierten Genomen verarbeitete Daten. Für den normalen Datenjournalisten ist die Textdatei ein Rohdat (es nervt keinen Singular für Daten zu haben.).

Für den Datenjournalisten ist es ein wichtiger Arbeitsschritt, die Rohdaten aufzubereiten, zu minen. Er sollte nachdem er die Daten aufzubereitet hat folgendes haben:

+ Die Rohdaten
+ Den sauberen Datensatz
+ Das Codebuch mit den Metadaten
+ Ein genaues Rezept, wie er von 1 nach 2,3 gekommen ist. Meistens R-Programme

###Codebuch
Das Codebuch sollte zum einen die Studie selbst und die Art und Methode des Datascrapings in der Tiefe beschreiben, zum anderen die einzelnen Werte im sauberen Datensatz genau beschreiben.

###Rezept
Das Rezept muss wirklich genau sein. Im Normalfall wird das R- oder Pythonprogramm dazu geliefert und die Parameter angegeben. Falls händisch etwas überarbeitet wurde muss das auch vermerkt werden. Reproduzierbarkeit ist wichtig.

##R zum Download

+ **`file.exists(x)`** überprüft, ob `x` im aktuellen Verzeichnis existiert. Nur für Dateien.
+ **`dir.create(x)`** erstellt das Verzeichnis `x`.
+ **`download.file("url")`** lädt eine Datei aus dem Netz
+ **`date()`** um das Datum des Ursprünglichen Downloads festzuhalten. Verhindert späteren Inkompatibilitätsshizzle.

##Lesen verschiedener Dateitypen
+ **`read.csv()`** um csv Dateien zu lesen.
+ **`read.table()`** praktisch das gleiche wie `read.csv()`, nur dass das `sep` und `header`-Argument manuell eingestellt werden müssen.
+ **`read.xlsx()`** ließt Excel-Dateien ein. Benötigt das Package `xlsx`.
+ **`read.xlsx2()`** ließt schneller, ist bei subsets aber instabil.
+ **`write.xlsx()`** schreibt Excel-Dateien.
###XML
+ **`xmlTreeParse()`** ließt eine XML-Datei ein. Setzt das `XML`-Paket voraus.
+ **`xmlRoot()`** speichert den Root-Node der XML-Datei ab. Der Root-Node ist die oberste Ebene des XML-Dokuments ähnlich dem `<html>`-Tag. Der Root-Node wird als `list` gespeichert. Zugriff über `[[]]`.
+ **`xmlName()`** gibt den Namen des Nodes aus.
+ **`xmlSApply(rootNode, xmlValue)`** gibt jeden `xmlValue` in der Variablen `rootNode` aus. Von Haus aus rekursiv. Unterstützt auch [XPath](https://www.w3schools.com/xml/xpath_intro.asp), eine Sprache um XML-Dateien auszulesen.
###JSON
+ **`fromJSON()`** ließt eine JSON-Datei ein. Benötigt das `jsonlite`-Paket.
+ **`names()`** gibt die Variablennamen des JSON-Objekts aus.
+ **`toJSON(dataset)`** schreibt einen Datensatz als JSON-Objekt.

##Data-Table
`Data.table` ist die ressourcenschonendere Variante des `data.frames`. Die Funktionsnamen sind die selben, `data.table` ist jedoch in C geschrieben weshalb es bedeutend schneller ist. Setzt das `data.table`-Paket voraus. Die Syntax sieht jedoch anders aus als bei `data.frames`.
**Datatables gibt es nur einmal. Wenn ein Datatable mehreren Variablen zugewiesen ist, betrifft eine Änderung alle Variablen weil sie auf den selben Datatable verweisen.**

+ **`tables()`** zeigt alle Tables im Speicher an.
+ **`setkey(columname)`** Setzt die Keyspalte
+ **`fread()`** ließt einen Datatable ein. 10x schneller als mit read.file.
Das Erstellen von Datatables funktioniert mit der selben Syntax wie Dataframes. Auch das Subsetten von Zeilen. Das Subsetten von Spalten hat jedoch eine andere Syntax:

```
DF:
>df[,c(2,3)]

DT:
>dt[,list(mean(z))]
```
Funktionen müssen stets als Listen übergeben werden. (not quite sure, though...)
Neue Spalte hinzufügen:
```
>dt[,w:=rnorm(2)] #Füllt eine neue Spalte w mit Zufallszahlen.
```
Es kann, wenn eine Spalte mit Binärwerten existiert, Operationen durchgeführt werden, die nur die Zeilen mit `TRUE` betreffen.
```
dt[,b=mean(x+w), by=a]
```
Dieser Befehl setzt in Spalte `b` in jeder Zeile in der `a==TRUE` ist, den Mittelwert aus den beiden Spalten `x` und `w`, für die Spalten in denen `a==TRUE` ist. In Spalten in denen `a!=TRUE` ist wird der Mittelwert aller `x` und `w` eingetragen in denen `a!=TRUE` ist. Siehe Skript data.table 1 S. 11.
Um die Anzahl eines bestimmten Eintrags in einer Spalte auszugeben gibt man
```
>dt <- data.table(x=sample(letters[1:3], 1E5, TRUE))
>dt[,.N, by=x]
   x     N
1: a 33387
2: b 33201
3: c 33412
```
Es können Keyspalten gesetzt werden um aus ihr Subsets zu generieren. Mit `setkey(dt, x)` wird die Spalte `x` im Datatable `dt` zur Keyspalte. Mit `dt["a"]` werden nur die Spalten ausgegeben in denen `x` den Wert `a` hat.

##MySQL
**Um Pakete zu installieren, die über RStudio nicht funktionieren (die meisten lassen sich nicht über RStudio installieren weil Fuck you) im Terminal `sudo apt install r-cran-paketname` eingeben. Läuft dann.**

Um mit dem `RMySQL`-Paket zu arbeiten ist es sehr hilfreich, die wichtigsten Befehle zu kennen. Eine Übersicht findet sich [hier](http://www.pantz.org/software/mysql/mysqlcommands.html). **Nur select als Kommando wählen. Dem Server nichts hinzufügen oder vom Server löschen!!! Srsly!**

Unterhalb steht Beispielcode um sich mit der Genomdatenbank der UCSC zu verbinden. In `ucscDb` werden die Zugangsdaten abgelegt. Das zweite Kommando connected die Datenbank, übergibt das MySQL-Kommando `show databases` und dbDisconnected wieder.
```
> ucscDb <- dbConnect(MySQL(), user="genome", host="genome-mysql.cse.ucsc.edu")
> result <- dbGetQuery(ucscDb, "show databases;"); dbDisconnect(ucscDb);
[1] TRUE
> head(result)
            Database
1 information_schema
2            ailMel1
3            allMis1
4            anoCar1
5            anoCar2
6            anoGam1
```
Aus den oben gewonnen Informationen können wir uns nun mit einer gewissen Datenbank verbinden, in diesem Fall die Datenbank `hg19`. Dies wird durch den `db`-Befehl in der ersten Zeile möglich gemacht.
```
> hg19 <- dbConnect(MySQL(), user="genome", db="hg19", host="genome-mysql.cse.ucsc.edu")
> allTables <- dbListTables(hg19)
> length(allTables)
[1] 11048
```
Die Dimensionen einer MySQL-Datenbank zu sehen ist etwas komplizierter:
```
> dbListFields(hg19, "affyU133Plus2")
 [1] "bin"         "matches"     "misMatches"  "repMatches"  "nCount"      "qNumInsert"
 [7] "qBaseInsert" "tNumInsert"  "tBaseInsert" "strand"      "qName"       "qSize"      
[13] "qStart"      "qEnd"        "tName"       "tSize"       "tStart"      "tEnd"       
[19] "blockCount"  "blockSizes"  "qStarts"     "tStarts"    
> dbGetQuery(hg19, "select count(*) from affyU133Plus2")
  count(*)
1    58463
```
Mit dem ersten Befehl `dbListFields` werden die Spaltennamen und damit auch die Anzahl abgefragt. Mit dem übermittelten Befehl `"select count(*) from affyU133Plus2"` werden die einzelnen Reihen in der Datenbank gezählt.
Um aus der Datenbank Inhalte abzufragen benutzt man folgendes Kommando:
```
> affyData <- dbReadTable(hg19, "affyU133Plus2")
> head(affyData)
  bin matches misMatches repMatches nCount qNumInsert qBaseInsert tNumInsert tBaseInsert
1 585     530          4          0     23          3          41          3         898
2 585    3355         17          0    109          9          67          9       11621
3 585    4156         14          0     83         16          18          2          93
4 585    4667          9          0     68         21          42          3        5743
5 585    5180         14          0    167         10          38          1          29
6 585     468          5          0     14          0           0          0           0
```
Die Datenbanken können sehr groß sein. Die obige hat über 1,2 Millionen Datenpunkte. Um direkt nur Subsets zu ziehen und so den Speicher zu entlasten passen wir das MySQL-Kommando an:
```
> query <- dbSendQuery(hg19, "select * from affyU133Plus2 where MisMatches between 1 and 3")
> affyMis <- fetch(query); quantile(affyMis$misMatches)
  0%  25%  50%  75% 100%
   1    1    2    2    3
```
Wenn man sich ohnehin nur den Head ansehen will, kann man dies direkt im Kommando einstellen und nur die oberen x Reihen holen:
```> affyMisSmall <- fetch(query, n=10); dbClearResult(query)
[1] TRUE
> dim(affyMisSmall)
[1] 10 22
```
`query` wurde im oberen Funktionsaufruf definiert. `dbClearResult` bricht die Anfrage ab, da der Server ansonsten erst aufhören würde, wenn alle Zeilen übermittelt sind.
Wenn man mit der Datenbankabfrage fertig ist muss die Connection geschlossen werden. Dies geschieht mittels `dbDisconnect(hg19)`, wobei hg19 die Credentials enthält.

##HDF5

HDF5 wurde entwickelt um große Datenmengen zusammen mit Metadaten abzuspeichern. Es wird von der [hdfgroup](http://www.hdfgroup.com) entwickelt.

Das R-Paket wird von Bioconductor herausgegeben und ist nicht über die normalen Paketquellen verfügbar. Es wird mittels
```
source("http://www.bioconductor.org/biolite.R")
biocLite("rhdf5")
library("rhdf5")
```
installiert.

###Erstellen und Schreiben

Mit folgendem Befehl können HDF5-Objekte erstellt werden.
```
> created = h5createFile("example.h5")
> created
[1] TRUE
```
Um dem noch leeren Objekt (Unter-)Gruppen hinzuzufügen folgende Befehle:
```
> created <- h5createGroup("example.h5", "foo")
> created <- h5createGroup("example.h5", "bar")
> created <- h5createGroup("example.h5", "/foo/foobar")
> h5ls("example.h5")
  group   name     otype dclass dim
0     /    bar H5I_GROUP           
1     /    foo H5I_GROUP           
2  /foo foobar H5I_GROUP
```
Um in den verschiedenen Gruppen Elemente, hier eine Matrix, abzulegen benutzt man den `h5write()`-Befehl.
```
> A <- matrix(1:10, nr=5, nc=2)
> h5write(A, "example.h5", "foo/A")
```
HDF5-Files können Metadaten zusammen mit den Daten abspeichern. Hier wird der Matrix die Einheit `liter` zugedacht.
```
> attr(A, "scale") <- "liter"
> h5ls("example.h5")
  group   name       otype  dclass   dim
0     /    bar   H5I_GROUP              
1     /    foo   H5I_GROUP              
2  /foo      A H5I_DATASET INTEGER 5 x 2
3  /foo foobar   H5I_GROUP   
```
###Lesen
HDF5-Files werden mit dem `hdfread()`-Befehl gelesen. Als erstes Argument wird die Datei übergeben, als zweites der Ort in dem das zu lesende Elemnt abgelegt wurde.
```
> h5read("example.h5", "/foo")
$A
     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10

$foobar
NULL
```
In HDF5-Files können Einträge an vom Nutzer spezifizierte Stellen geschrieben werden. Dazu wird an das `h5write`-Befehl das index-Argument übergeben, das ein `list`-Argument benötigt. Zuerst Reihen, dann Spalten.
```
> h5write(c(12, 13, 14), "example.h5", "/foo/A", index=list(1:3, 1))
> h5read("example.h5", "/foo/A")
     [,1] [,2]
[1,]   12    6
[2,]   13    7
[3,]   14    8
[4,]    4    9
[5,]    5   10
```
Für weitere Informationen gibt's auf der Bioconductor-Homepage ein [Tutorial](http://www.bioconductor.org/packages/release/bioc/vignettes/rhdf5/inst/doc/rhdf5.pdf).

##Webscraping und APIs

Das Webscraping (schließt auch die APIs mit ein), bezeichnet das strukturierte und automatisierte Auslesen von Daten aus Websites. Beim Scraping direkt aus dem HTML-Code, bei APIs über das jeweilige Format, dass die Schnittstelle bereitstellt.

###Webscraping
Die Daten werden mit dem `readLines()`-Statement ausgelesen.
```
> con <- url("https://scholar.google.com/citations?user=HI-I6C0AAAAJ")
> htmlCode <- readLines(con)
> close(con)
> htmlCode
[1] "<!doctype html><head><meta http-equiv=\"Content-Type\" content usw. usf.
```
`close(con)` schließt dabei wiederum die Verbindung, ähnlich wie es bei der Datenbank gemacht wurde.
Hier kann das Wissen aus der XML-Lektion angewendet werden. Mit dem `XML`-Paket können die relevanten Daten ausgelesen werden. mit der Kombination aus `htmlTreeParse()` und `xpathSapply()` können einzelne Tags ausgelesen werden.

Mit dem `httr`-Paket kann man auch auf Login-Bereiche zugreifen.
```
>  pg <- GET("https://httpbin.org/basic-auth/user/passwd", authenticate("user", "passwd"))
> pg
Response [https://httpbin.org/basic-auth/user/passwd]
  Date: 2017-02-17 17:20
  Status: 200
  Content-Type: application/json
  Size: 47 B
{
  "authenticated": true,
  "user": "user"
}
```
Ohne das `authenticate`-Token würde der Server nur einen 401 zurückschicken. Der `GET`-Befehl speichert auch noch weitere Informationen zum Zugriff auf. Diese lassen sich mit dem `names()`-Befehl oder `pg$xxx` abfragen.
Um sich nicht jedes mal neu authentifizieren zu müssen, nutzt das `httr`-Paket handles:
```
google <- handle(https://www.google.com)
pg <- GET(handle=google, path="search")
```
###APIS
Die Lektion dreht sich ausschließlich um die Twitter-API. Wenn man das brauchen sollte einfach nochmal anschauen.
Das `httr`-Paket erlaubt

+ **`GET`** ließt bestehende Inhalte.
+ **`POST`** erstellt neue Inhalte.
+ **`PUT`** updatet bereits bestehende Inhalte.
+ **`DELETE`** löscht Inhalte.

###Others
Es gibt für fast alle Arten von Daten ein eigenes R-Paket. Am einfachsten googlen. Auch für Bilddateien, andere Programmiersprachen, Ortsdaten, Musik,


##Subsetting

Mit den bekannten Operatoren `$`, `[]`, `[[]]` können Subsets gebildet werden. In diesen können auch logische Operatoren verwendet werden. `X[(X$var1 > 1 & X$var3 < 5), ]` gibt alle Zeilen von `X` aus in welchen `var1` größer als 1 und `var3` kleiner als 5 ist. Die logischen Operatoren sind `&` und `|` oder die selbstdefinierten `%name%`.

Durch die Verwendung des `which()`-Kommandos können `NA`s ausgeschlossen werden.

+ **`sort(X)`** gibt X in aufsteigender Reihenfolge aus.
+ **`X[order(X$var1, X$var2)]`** sortiert den `data.frame` in aufsteigender Reihenfolge von `var1`. Wenn mehr als ein Argument übergeben wird, so wird primär nach dem ersten Argument sortiert. Wenn zwei Variablen den selben Wert haben, so werden diese in aufsteigender Reihenfolge des zweiten Arguments sortiert.

Um einem Datensatz neue Spalten hinzuzufügen wird diese direkt bei der Zuweisung definiert:
```
> X <- data.frame(var1=c(1, 3, 4), var2=c(2, 4, 5))
> X
  var1 var2
1    1    2
2    3    4
3    4    5
> X$var3 <- c(6, 3, 5)
> X
  var1 var2 var3
1    1    2    6
2    3    4    3
3    4    5    5
```
Mit dem Befehl `cbind()` kann das gleiche Ergebnis erzielt werden. Weiter Infos gibt es im [LectureScript](http://biostat.jhsph.edu/~ajaffe/lec_winterR/Lecture%202.pdf).


###plyr-Paket
Das `plyr`-Paket macht das Sortieren etwas leichter:

+ **`arrange(X, var1)`** sortiert `X` in Reihenfolge von `var1`.

###dplyr-Paket
Die fünf Hauptverben des dplyr-Pakets sind `select`, `filter`, `arrange`, `mutate` und `summarize:`

+ **`select(dataset, var1, var2)`** gibt nur `var1` und `var2` aus dem Datensatz aus.
+ **`filter(dataset, var1 == "bla", var2 <= 3.4)`** gibt die Zeilen aus, in denen alle Bedingungen zutreffen. Geht auch mit `|`-Operator.
+ **`arrange(X, var1)`** sortiert `X` in Reihenfolge von `var1`.
+ **`arrange(X, desc(var1))`** sortiert `X` in absteigender Reihenfolge von `var1`.
+ **`mutate(df, x = y*2)`** fügt `df` eine neue Spalte `x` hinzu. Diese hat den doppelten Wert von `y`.
+ **`summarize(dataset, name = var1*2)`** stellt eine Zusammenfassung des Datensatzes anhand einer Zeile dar.

Neben den fünf Hauptfunktionen gibt es noch weitere Funktionen in `dplyr`:
+ **`group_by(database, var1)`** gruppiert den frame nach `var1`. Alle Aktionen werden jetzt auf Basis der Gruppierten Spalte gemacht.
+ **`n()`** ist eine komische Funktion. Sie kann nur innerhalb der `summarize()`-Funktion aufgerufen werden und zählt, wie oft ein Element pro Gruppe vorkommt.
+ **`n_distinct(var)`** zählt wie viele verschiedene Einträge es in `var` gibt.   
+ **`%>%`** wird als "then" ausgesprochen. Wird benutzt um in einem Skript verschiedene Programmaufrufe hintereinander zu stellen ohne das Programm schwer lesbar Verschachteln zu müssen.

##Summarizing Data
+ **`head()`**
+ **`tail()`**
+ **`summary()`**
+ **`str()`**
+ **`quantile()`** Errechnet das [Quanitl](https://de.wikipedia.org/wiki/Quantil_(Wahrscheinlichkeitstheorie)) einer Funktion.
+ **`table()`** gibt einzelne Spalten als Tabelle aus. Um die `NA`s miteinzubeziehen, das Argument `useNA="ifany"` übergeben. Mit zwei übergebenen Spalten gibt `table()` eine Kreuztabelle aus.
+ **`any(logischesArgument)`** gibt `TRUE` zurück, wenn ein beliebiges der übergebenen Argumente `TRUE` ist.
+ **`all(logischesArgument)`** gibt `TRUE` zurück, wenn alle der übergebenen Argumente `TRUE` sind.
+ **`colSums()`** gibt die Summe einer Spalte zurück. Besonders hilfreich in Verbindung mit `is.na()`.
+ **`rowSums()`** gibt die Summe einer Zeile zurück. Besonders hilfreich in Verbindung mit `is.na()`.
+ **`X[X$var1 %in% c(1, 2, 3)]`** gibt die Reihen zurück in denen `var1` eine Teilmenge von c ist.
+ **`xtabs(var1 ~ var2 + var3, data=dataframe)`** erstellt eine Kreuztabelle aus den beiden Variablen.
+ **`ftable(xtabs())`** vereinfacht den Output von `xtabs()`.
