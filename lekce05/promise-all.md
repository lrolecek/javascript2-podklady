# Promise.all - když potřebujeme počkat na splnění více promise najednou

Když provádíme najednou několik asynchronních operace, jejichž výsledkem je promise, potřebujeme někdy vykonat další kód, teprve až jsou splněny všechny dílčí promise. Můžeme použít `Promise.all()` do nějž se jako parametr předává pole, kde každý prvek pole je promise. Výsledkem je pole hodnot vrácených z jednotlivých promise.

```javascript
let promise1 = ...;
let promise2 = ...;
let promise3 = ...;

Promise.all([promise1, promise2, promise3]).then(
  result => { console.log(result) }
);
```


## Příklad s fetch a async/await

Představme si jednoduchý kód pro stránku restaurace, který načítá zvlášť jídelní lístek a nápojový lístek. Oba lístky načítáme ze serveru pomocí `fetch` a abychom si zjednodušili zpracování promises, použijeme async/await.

```javascript
async function getMenu() {
  // jidelni listek
  let mealsResponse = await fetch('adresa jidelniho listku');
  let mealsJson = await mealsResponse.json();

  // napojovy listek
  let drinksResponse = await fetch('adresa napojoveho listku');
  let drinksJson = await drinksResponse.json();

  // vratime oba listky jako pole
  return [mealsJson, drinksJson];
  };
}

let menu = getMenu();
console.log(menu);
```

Daný příklad bude fungovat, ale má jeden velký nedostatek. Zbytečně zdržuje, protože čeká na jídelní lístek a teprve potom začíná s načítáním nápojového lístku. Pointou asynchronního JavaScriptu je, že může probíhat několik věcí najednou a my se pomocí promises dozvíme, až budou hotové. Ideálně přepíšeme program tak, aby se oba lístky stahovaly asynchronně každý zvlášť, a že máme oba načtené, zjistíme pomocí Promisse.all.


```javascript
async function getMeals() {
  // jidelni listek
  let mealsResponse = await fetch('adresa jidelniho listku');
  let mealsJson = await mealsResponse.json();
  return mealsJson;
}

async function getDrinks() {
  // napojovy listek
  let drinksResponse = await fetch('adresa napojoveho listku');
  let drinksJson = await drinksResponse.json();
  return drinksJson;
}

Promise.all([
  getMeals(),
  getDrinks()
]).then(
  result => { console.log(result) }
);
```

Výsledkem je program, který nečeká se stahováním nápojového lístku na dokončení stahování jídelního lístku. Stahuje oba zároveň a až jsou obě promise splněné, vypíše výsledek na obrazovku.
