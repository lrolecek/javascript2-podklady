# Node.js

Node.js je velmi zjednodušeně JavaScript na příkazové řádce. Node.js umožňuje spouštět JavaScript mimo prohlížeč. Pro front-end vývoj slouží Node.js především jako systém, na které běží pomocné vývojářské nástroje, které usnadňují vývoj aplikací - například Babel a Webpack, které budeme používat v tomto kurzu.

## NPM

NPM je zkratka pro Node Package Manager - jedná se o správce javascriptových balíčků. Balíček může být právě buď nějaký nástroj, kterým si usnadňujeme vývoj nebo třeba i knihovna, kterou můžeme touto standardní cestou přidat do našeho projektu.

Výhoda systéu balíčků je, že když potřebujeme projekt přenést na jiný počítač nebo k jinému vývojáři, stačí poslat námi vytvořené zdrojové soubory. Nemusíme posílat soubory standardních knihoven nebo nástroje pro vývoj.

Na cílovém počítači jsme schopni jednoduchým příkazem `npm install` nainstalovat všechny **závislosti** (dependencies), které náš projekt potřebuje.

## Package.json

Soubor *package.json* obsahuje konfiguraci našeho projektu včetně všech závislostí - balíčků, které máme do projektu přidané.

## Startovní projekt

Pro příklady a domácí úkoly v kurzu budeme používat jako výchozí bod náš [Startovní projekt](https://czchts.cz/js2-start).

V popisu projektu na GitHubu je stručný návod, jak projekt inicializovat.

To nejdůležitější je, že po zkopírování projektu k sobě na disk provedeme instalaci balíčků příkazem `npm install` v terminálu.