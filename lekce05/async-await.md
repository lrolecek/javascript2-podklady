# Async/await - synchronní vykonávání asynchronního kódu

Async/await je speciální nová syntaxe, která nám umožňuje pracovat s promises mnohem snadněji.

## Async

Klíčové slovo `async` může být umístěno před jakokoliv funkci. Když použijeme `async`, znamená to, že daná funkce vždy vrátí promise. I když se jedná o obyčejnou funkci, která vrací pouze hodnotu, je tato hodnota zabalena do okamžitě splněné (resolved) promise.

```javascript
async function mojeFunkce() {
  return 1;
}

mojeFunkce().then(alert); // ukáže 1
```

Takže `async` pouze zajišťuje, že funkce vždy vrátí promise. Vrací-li funkce občejnou hodnotu, `async` tuto hodnotu do promise zabalí.

## Await

Klíčové slovo `await` lze použít **pouze uvnitř `async` funkce**. `await` donutí JavaScript čekat, dokud není promise vyřešená (ať už splněná nebo zamítnutá).

```javascript
async function mojeFunkce() {
  let result = await promise;
  console.log(result)
}
```

Na řádku, kde je `await` se JavaScript zastaví a čeká, až bude daná promise vyřízená. JavaScript sice čeká, ale může mezitím spouštět další skripty, reagovat na události, apod.

Ukažme si to na praktickém příkladu s načítáním dat ze serveru pomocí fetch:

```javascript
async function getPerson(id) {
  // načteme údaje o postavě ze Star Wars s daným ID
  let response = await fetch(`https://swapi.co/api/people/${id}/`);

  // v proměnné response dostaneme odpověď ze serveru,
  // kterou pomocí funkce .json() převedeme na javascriptový
  // objekt. Funkce .json() opět vrací promise, takže na její
  // splnění můžeme znovu počkat pomocí await
  let json = await response.json();

  // vypíšeme výsledek
  console.log(json);
}

// zjistíme údaje o Luke Skywalkerovi
getPerson(1);
```

Protože `async` funkce vrací vždy promise, můžeme na ni normálně reagovat pomocí `.then()`.

```javascript
getPerson(1).then(() => {
    console.log('Luke je načtený!')
});
```

Protože ale veškeré čekání na odpověď zařizuje `await` uvnitř funkce, potřebujeme `.then()` pouze zřídkakdy.

Hezký popis **async/await** najdeš např. na [Javascript.info](https://javascript.info/async-await) nebo si prostuduj dokumentaci na MDN pro [async](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) a [await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await).


## Ošetření chyb pomocí try/catch

Pro ošetření případných chyb můžeme použít standardní javascriptové **try/catch**:

```javascript
try {
  // kód, ve kterém může dojít k chybě
} catch {
  // tento kód se provede v případě chyby
} finally {
  // tento blok lze vynechat
  // provede se v obou případech - buď po úspěšném
  // vykonání bloku try nebo v případě chyby po
  // skončení bloku catch
}
```

Tuto konstrukci můžeme použít i pro jednoduché zachycení chyb, které nastaly během `await`:

```javascript
async function getPerson(id) {
  try {
    let response = await fetch(`https://swapi.co/api/people/${id}/`);
  } catch {
    console.log('Došlo k chybě pro načítání ze serveru.');
  }
  let json = await response.json();
  console.log(json);
}
```

V bloku `try` můžeme mít i více řádků, pokud nám stačí vědět, že došlo k chybě, a nemusíme vědět, kde přesně.

```javascript
async function getPerson(id) {
  try {
    let response = await fetch(`https://swapi.co/api/people/${id}/`);
    let json = await response.json();
    console.log(json);
  } catch {
    console.log('Někde se něco nepovedlo.');
  }
}
```

