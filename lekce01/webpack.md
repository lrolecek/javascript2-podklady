# Babel

**Kompilátor** moderní syntaxe JavaScriptu (ES2015 a novější) do "starého javascriptu", který funguje bez problémů ve všech prohlížečích.

# Webpack

Tzv. **bundler** - dokáže spojovat více souborů JavaScriptu do jednoho cílového souboru, který pak připojíme do naší webové stránky.

Naše aplikace chceme psát modulárně. Chceme kód rozdělit do malých **modulů**, které pak budeme importovat do našeho programu dle potřeby. Naše aplikace tak bude přehledná dobře udržovatelná.

# Jak spouštět

babel i Webpack máme v našem startovním projektu nakonfigurované. Vždy, když budeme chtít sestavit naši aplikaci, použijeme v terminálu příkaz:

`npm run build`

Součástí Webpacku je i lokální webový server, který nám umožňuje spouštět naše aplikace stejně, jako by běžely na opravdovém serveru. *Nechceme* spouštět naši aplikaci tak, že budeme klikat na HTML soubor.

`npm run serve`

Tímto příkazem spustíme webový server, který přímo otevře naši aplikaci a zároveň provádí tzv. **live reload** - každou změna v kódu se okamžitě promítne v prohlížeči.
