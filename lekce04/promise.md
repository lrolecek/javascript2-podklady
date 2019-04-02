# Asynchronní kód a Promises

JavaScript je tzv. singlethreaded jazyk. To znamená, že v jednom okamžiku může vykonávat pouze jeden příkaz. Zjednodušeně - kód se čte řádek po řádku a vždy se čeká, až se daný příkaz dokončí, než začne další.

Opakem jsou tzv. multithreaded jazyky, kde můžeme mít několik *vláken*, která běží souběžně a v každém se nezávisle vykonává kód.

Některé úkony - typicky např. dotaz do databáze nebo dotaz na webové API - mohou trvat dlouho dobu. To může být problém, protože náš kód by se tak de facto zastavil, zatímco by čekal na výsledek. Aplikace nereaguje, uživatel neví, co se děje, apod.

## Asynchronní JavaScript

Proto vznikly mechanismy, které JavaScript dělají **asynchronním**. Asynchroní vykonávání kódu znamená, že například čekání na dlouhotrvající operaci (dotaz do internetu) se odloží někam bokem a JavaScript se k němu vrátí, až dostane ze serveru výsledek. JavaScript mezi tím vykonává dál hlavní program. Aplikace se tak "nezasekne" čekáním na místě, ale může mezitím vykonávat další důležité akce.

Jedním z asynchronních mechanismů jsou **promises**.

## Promise

**Promise** je zjednodušeně příslib, že výsledek operace bude dostupný někdy v budoucnu. Programátor může psát kód, který s tímto potenciálním budoucím výsledkem pracuje, ale kód se nevykoná ihned, ale **asynchronně* až ve chvíli, kdy je výsledek k dispozici. JavaScript se nezastavuje a nečeká na výsledek, vykonává mezitím další kód.

Promise může být v jednom ze tří stavů:
- **pending** - výchozí stav, čeká se na výsledek operace
- **fullfilled** - znamená, že operace proběhla úspěšně (vrací hodnotu jako výsledek prováděné operace)
- **rejected** - znamená, že operace selhala (vrací chybu, proč operace selhala)

Programátor může napsat kód, který se provede pří úspěchu a nebo při chybě.

Podrobnější informace najdeš např. v článku [Promise - basics](https://javascript.info/promise-basics) nebo v [dokumentaci promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) na MDN.


K obsluze každé promise slouží tzv. **konzumenti**. Nejpoužívanější je `.then()`.

### promise.then()

Ve chvíli, kdy promise vrátí buď úspěch nebo chybu, můžeme výsledek zpracovat pomocí `.then()`. Jako dva parametry se dovnitř předávají funkce - první pro zpracování úspěšné promise, druhá pro zpracování zamítnuté promise (tj. v případě chyby).

```javascript
promise.then(
  function(result) { /* funkce vykonaná v případě úspěchu */ },
  function(error) { /* funkce vykonaná v případě chyby */ },
);
```

Když uvedeme pouze jeden parametr, definujeme pouze funkci pro úspěšně splněnou promise. Chybu můžeme zachytit i jinak (viz catch() dále v textu).

Promises se často řetězí do sebe. Při dokončení jedné promise může jako výsledek kód vrátit další promise. Často pak můžeme vidět zřetězené zpracování výsledků:

```javascript
promise
  .then( function(result1) { ... } )
  .then( function(result2) { ... } )
  .then( function(result3) { ... } );
```

### promise.catch()

Ka zachycení chyb kdekoliv v řetězci promises můžeme použít `.catch()`.

```javascript
promise
  .then( function(result1) { ... } )
  .then( function(result2) { ... } )
  .catch( function(error) { /* zpracování chyby */ } );
```

### promise.finally()

Funkce uvnitř `.finally()` se vykoná vždy - ať už je promise splněná (fullfilled) nedo zamítnutá (rejected). Používá se pro akce, které chceme provést vždy, když dojde k dokončení asynchronní operace.

Když například spustíme načítání dat ze serverového API, můžeme předtím uživateli ukázat indikátor načítání (např. točící se kolečko).

Když ze serveru dostaneme výsledek - ať už požadovaná data nebo chybu, chceme v obou případech zastavit a skrýt indikátor.

```javascript
promise
  .then(function(result) { /* zpracování výsledku */ })
  .catch(function(error) { /* zpracování chyby */ })
  .finally(function() { /* toto se provede v obou případech */ });
```

