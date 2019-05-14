# Data store a uchování stavu aplikace

Při programování téměř jakékoliv aplikace narazíme na problém, že potřebujeme uchovat stav aplikace, anglicky tzv. **state**.


## Stav aplikace (state)

Co je to stav (state)? Zjednodušeně si to můžeme představit jako *"výsledek všech akcí, které se na stránce staly (ať už automaticky nebo zásahem uživatele) os načtení stránky"*.

Představme si třeba hudební přehrávač, který je vždy v nějakém stavu:
- *loading* - přehrávač načítá hudnu a ještě není připravený
- *ready* - přehrávač je načtený a připravený, ale zatím nehraje
- *playing* - přehrávač hraje hudbu (stáv po stisknutí tlačítka Play)
- *paused* - přehrávání hudby je pozastaveno (po stisknutí tlačítka Play/Pause)
- *stopped* - hudba zcela zastavená

Aplikace může reagovat na různé stavy, ve kterých se nachází. Např. ukazuje progress bar, zatímco se stahuje hudba. Jakmile je hudba načtená, přehrávač se přepne do stavu *ready* a zobrazí ovládácí tlačítka a seznam skladeb. Po stisknutí tlačítka Play se přepne do stavu *playing*, na který aplikace zareaguje tak, že místo tlačítka Play zobrazí tlačítko Pause a ukazuje pozici ve skladbě.

Po stisknutí tlačítka Pause se aplikace přepne do stavu *paused*, kde se z tlačítka Pause opět stane tlačítko Play, zastaví se hudba, apod. - asi si dovedeš představit, jak to celé zjednodušeně funguje a k čemu jsou stavy aplikace dobré.


## Jeden stav vládne všem

Stav aplikace není nic složitého a ve svých programech ho používáš zcela běžně - stačí nastavit libovolnou proměnnou, na kterou se pak ptáš v podmínce. I to je stav v té nejjednodušší podobě.

Pod uchováním stavu se ale většinou myslí nějaký ucelený koncept a datový model, který se stará o správu stavu pro celou aplikaci. Většinou se jedná o jeden objekt nebo pole, do kterého přidáváme další prvky pole nebo vlastnosti podle potřeby.

*Poznámka: Na běžné operace uvnitř funkcí samozřejmě stále používáme obyčejné proměnné. Nechápej to tak, že proměnné jsou něco špatného a state management je něco, čím bys je měla nahradit.*

V nejprimitivnější podobě může stav aplikace být doslova pole nebo objekt. Představme si náš přehrávač hudby:

```javascript
// vytvoříme objekt pro stav
const playerState = {};

// zde např. načteme seznam hudby, kterou chceme mít v přehrávači
playerState.state = "loading";

// jakmile je sezna načtený...
playerState.playlist = seznamHudbyzApi;
playerState.state = "ready";

// tato funkce se volá po kliknutí na tlačítko Play
function play(song) {
  // spustíme přehrávání písničky
  if (playerState.state === "ready") {
    song.play();

    // a nastavíme stav aplikace
    playerState.state = "playing";
    playerState.currentSong = song;
  }
}
```

Nehledej v kódu žádný vyšší smysl, jde jen o smyšlený příklad, kde je vidět, že stav může být obyčejný objekt, kterému nastavujeme vlastnosti.


## Jednoduchý modul pro správu stavu

Výhodou správy stavu je, že celá aplikace využívá jeden datový sklad a můžeme tak jednoduše sdílet data mezi jednotlivými moduly. Do stavu aplikace si můžeme ukládat např. i načtená data, odkud je mohou ostatní moduly číst, apod.

Celou věc zabalíme do samostatného modulu, který pak mohou ostatní moduly naimportovat a používat:

```javascript
// soubor state.js
const _data = {};

const DataStore = {
  set: (key, value) => _data[key] = value;
  get: (key) => _data[key];
};

Object.freeze(DataStore);

export default DataStore;
```

A v aplikaci použijeme následovně:

```javascript
// soubor cokoliv.js
import DataStore from './state.js';

// naše aplikace něco dělá a potřebuje nastavit stav
DataStore.set('playlist', poleObsahujiciPlaylist);
DataStore.set('state', 'ready');

// později potřebujeme někde jinde v aplikaci vypsat seznam skladeb
if (DataStore.get('state') === 'ready') {

  DataStore.forEach(song => {
    console.log(song.name);
  })
}
```

Objekt datového skladu samozřejmě může mít spoustu dalších metod a vlastností podle potřeby naší aplikace.


### Datový sklad pomocí třídy

Možná je i implementace pomocí JavaScriptové třídy:

```javascript
class Store {

  constructor() {
    this._data = {};
  }

  set(key, value) {
    this._data['key']  = value;
  }

  get(key) {
    return this._data['key'];
  }
}

// na základě výše deklarované třídy ihned vytvoříme objekt
const DataStore = new Store();

// zamrzneme ho - tj. nepůjde měnit jeho vlastnosti
Object.freeze(Data.store);

// a tento objekt vyexportujeme z modulu ven
export default DataStore;
```

Při použití třídy je důležité si uvědomit, že musíme z modulu ven neexportujeme samotnou třídu, ale že na jejím základě vytvoříme ihned nový objekt (instanci třídy) a ten vyexportujeme.

Kdybychom vyexportovali z modulu třídu, každý jiný modul, který by ji chtěl použít, by si musel vytvořit její novou instanci - tj. vždy separátní objekt, nezávislý na ostatních. Něco nastavené v jedné instanci by se neprojevilo v ostatních a sdílení dat by pak nebylo možné.

Výše uvedený modul pak v naší aplikaci použijeme stejně, jako dříve:

```javascript
// soubor cokoliv.js
import DataStore from './state.js';

// nastavíme
DataStore.set('state', 'playing');
DataStore.set('playlist', [
  { artist: 'Beatles', song: 'Yesterday', year: 1965 },
  { artist: 'Beyoncé', song: 'Halo', year: 2008 }
]);

// přečteme
if (DataStore.get('state') === 'playing') {
  ...
};
```

Takovýto datový sklad samozřejmě neumí stav naší aplikace uchovat i při obnovení a znovunačtení stránky, ale v rámci jedné stránky běžící aplikace můžeme sklad naimportovat do libovolného počtu dalších modulů a sdílet společný stav mezi nimi.