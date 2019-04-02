# Rozdělení kódu na samostatné funkční celky, import/export

V programování obecně nechceme psát velké monolitické bloky kódu, ale chceme dělit kód na menší logické funkční celky (funkce, objekty, třídy). Snažíme se držet principu, že jedna funkce by měla mít pouze jednu zodpovědnost, dělat pouze jednu věc.

Tyto logické funkční celky je ideální rozdělit do samostatných souborů. V každém souboru pak máme relativně krátký kód, ve kterém se vyznáme, a vždy víme, kde ho najít.

Všechny tyto malé javascriptové soubory sice můžeme připojit do HTML a funkce v nich používat, ale má to spoustu nevýhod.

* musíme neustále myslet na to, co jsme zapomněli připojit
* spousta připojených *.js* souborů může zpomalit načítání stránky
* záleží na pořadí - my musíme myslet, v jakém pořadí soubory připojit, aby náš kód fungoval

## Moduly

Od specifikace ES2016 (ES6) - zjednodušeně "moderní JavaScript" - můžeme kód rozdělit na tzv. **moduly**, se kterými pracujeme pomocí příkazů `import` a `export`. Pomocí můžeme v kódu vytvářet vzájemné závislosti. Můžeme v jednom souboru *naimportovat* funkce z druhého souboru a tím říci, že náš kód je potřebuje, závisí na nich. Prohlížeč pak kód stahuje podle potřeby a tak, aby program fungoval.

O fungování ve staších prohlížečích se postará bundler - v našem případě Webpack. Bundler sestaví výsledný *.js* soubor, který se pak posílá do prohlížeče tak, aby obsahoval všechny funkce přidané do kódu pomocí `import`.

Pokud si vzpomenete např. na hru s panáčkem z kurzu JavaScript 1, měli jsme celou hru v jednom obrovském nepřehledném souboru a už to byl poměrně zmatek. Celou hru bychom mohli rozdělit do několika samostatných modulů:

* modul `panacek`, který by se staral o vykreslování a pohyb panáčka
* modul `mince`, který by se staral o náhodné generování mince na ploše
* modul `moucha`, který by měl na starosti pohyb nepřátelksé mouchy
* modul `score`, který by staral o počítání a vykreslování score
* hlavní modul `hra`, který by vše spojoval dohromady - volal by funkce z ostatních modulů pro zobrazení hrací plochy, mouchy, score; čekal by na stisk klávesy a volal příslušné funkce pro pohyb panáčky, apod.

### Import a export

Import a export jsou úzce provázané. Abychom mohli využít do svého kódu naimportovat funkce z jiného modulu, musíme ji v daném modulu vyexportovat. K neexportovaným funkcím nemá kód v jiných modulech přístup.

## Export

* lze exportovat funkce, objekty nebo hodnoty v proměnných
* dva typy exportu - pojmenovaný a defaultní

Defaultní export může být v modulu pouze jeden, počet pojmenovaných exportů je neomezený.

### Pojmenovaný export

* může jich být v modulu neomezený počet
* používáme, když chceme z modulu exportovat více věcí (konstanty, funkce, třídy)
* pojmenované exporty musíme v jiném modulu importovat stejným jménem, pod jakým jsme ho exportovali

```javascript
// export konstanty
export const cislo = 7;

// export funkce
export function secti(a, b) {
  return a + b;
}
```

Potřebné hodnoty/funkce můžeme z modulu vyexportovat také až nakonec dohromady jedním příkazem:

```javascript
const cislo = 7;

function secti(a, b) {
  return a + b;
}

export { cislo, secti };
```

### Defaultní export

* může být v modulu pouze jeden
* funkce/třída/hodnota, která je vyexportována jako default, může být do jiného modulu naimportována pod libovolným jménem (viz. dále)

```javascript
// export funkce
export default function() {
  // ...
}
```

```javascript
// export třídy
export default class {
  // ...
}
```


Další podrobnosti o `export` najdeš v [dokumentace MDN pro export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export).


## Import

Pomocí `import` můžeme do modulu naimportovat hodnoty/funkce/třídy z jiného modulu. Import lze provádět několika způsoby:

U importu je potřeby vždy uvést cestu k souboru s modulem relativně k souboru, do kterého importujeme.

### Import veškerého obsahu modulu

Naimportuje se vše, co je v modulu exportováno, a je to dostupné pod společným jménem udaném při importu.

```javascript
// exportujeme v souboru modul.js
export const hodnota = 42;
export function funkce() { ... }
```

```javascript
// potom import v hlavním souboru main.js
import * as mujModul from './modul.js';

// a následně používáme pod jménem mujModul
let cislo = mujModul.hodnota;
mujModul.funkce();
```

### Import jednoho nebo více pojmenovaných exportů z modulu

Z modulu můžeme naimportovat pouze konkrétní věci, které potřebujeme.

```javascript
// import pouze jednoho exportu z modulu
import { hodnota } from './modul.js';

// a následně používáme pod jménem, pod jakým se importovalo
// tj. v našem příkladu "hodnota"
let cislo = hodnota;
```

Lze importovat i více konkrétních exportů najednou:

```javascript
// import více pojmenovaných exportů z modulu
import { hodnota, funkce } from './modul.js';

// a následně používáme pod jmény, pod jakým se importovalo
// tj. v našem příkladu "hodnota" a "funkce"
let cislo = hodnota;
funkce();
```

Pokud se nám nehodí původní jména, můžeme je při importu přejmenovat:

```javascript
// přejmenování při exportu
import { hodnota as superCislo } from './modul.js';

// a následně používáme pod jménem uvedeným za as
// tj. v našem příkladu "superCislo"
let cislo = superCislo;
```

### Import defaultního exportu

Pokud importujeme defaultní export z modulu, použijeme tuto syntaxi:

```javascript
// import pouze jednoho exportu z modulu
import vychoziExport from './modul.js';

// a následně používáme pod uvedeným jménem způsobem
// podle toho, co se exportovalo (hodnota, funkce, třída, objekt, ...)

// v případě funkce
vychoziExport();

// v případě hodnoty
let cislo = vychoziExport;

// v případě objektu
vychoziExport.metoda();
```

Další podrobnosti o `import` najdeš v [dokumentace MDN pro expimportort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import).
