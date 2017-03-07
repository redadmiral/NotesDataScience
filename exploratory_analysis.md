#Exploratory Data Analysis

Das plotten von Daten folgt einigen simplen Grundprinzipien:

1. Schaffe eine Vergleichsmöglichkeit
2. Liefere eine Erklärung für die Funktionsweise der Daten.
3. Aussagekräftige Datensätze haben mehr als zwei Variablen
4. Nutze mehr als eine Darstellungsform: Kombiniere Wort, Zahlen, Bilder und Diagramme.
5. Content is King!

+ **`boxplot(df)`** erstellt einen Boxplot aus `df`.
+ **`boxplot(var1 ~ var2, data = df)`** plottet `var1` im Verhältnis zu `var2` aus dem Datensatz `df`.
+ **`abline(h=x)`** zieht eine vertikale Linie bei `x` im aktuellen `boxplot`.
+ **`hist(df)`** erstellt ein Histogramm aus `df`.
+ **`rug(df)`** erstellt einen eindimensionalen Plot mit einem Strich pro Wert in `df`.
