# Fetch API

Fetch API je relativně nové prohlížečové API, které slouží pro vytváření HTTP požadavků - tj. snadné načítání dat ze serveru nebo jejich odesílání na server.

## Metoda fetch()

Fetch funguje asynchronně, tj. JavaScript nečeká na výsledek operace, ale vrací se promise, která je splněná nebo odmítnutá ve chvíli, kdy ze serveru přijde odpověď.

Metoda `fetch()` má dva parametry:
- povinné URL - to je adresa, na kterou se požadavek odešle
- volitelný objekt s nastavením dalších vlastností požadavku

Více najdeš v dokumentace k fetch() na MDN


Jednoduchý příklad fetch v akci:

```javascript
fetch('https://swapi.co/api/people/1').then(
  response => {
    console.log(response);
  }
);
```

Do proměnné `response` se uloží objekt s odpovědí ze serveru. Ten obsahuje stavový kód a další hlavičky.

Promise je splněná ve chvíli, kdy ze serveru dorazí hlavičky. Tělo serverové odpovědi se mezitím dále asynchronně stahuje. K tělu serverové odpovědi můžeme přistoupit přes metodu `json()` nebo `text()` (nebo další) objektu `response`.

Tyto metody vrátí další promise, která je splněná ve chvíli, kdy se ze serveru stáhne kompletní obsah odpovědi. Abychom tedy mohli zpracovat skutečný obsah zprávy a ne jenom její hlavičky, musíme řetězit několik `.then()` za sebou:

```javascript
fetch('https://swapi.co/api/people/1')
  .then(response => response.json())
  .then(json => {
    console.log(json);
  }
);
```

Při komunikaci po síti bychom měli vždy myslet na to, že ne vše musí dopadnout podle našich představ, a ošetřit případné chyby.

```javascript
fetch('https://swapi.co/api/people/1')
  .then(response => response.json())
  .then(json => {
    console.log(json);
  }
  .catch(error => {
    console.log(error)
  });
);
```

Ze serveru ale může v pořádku přijít odpověď (tj. promise je splněná a vykoná se .then()), ale uvnitř odpovědi může být sdělení, že na serveru došlo při zpracování požadavku k chybě.

V ideálním případě tedy musíme proto počítat i s touto variantou:


```javascript
fetch('https://swapi.co/api/people/1')
  .then(response => {
    // ze serveru přišla odpověď
    if (response.ok) {
      // vše je ok, stáhneme zbytek zprávy jako JSON
      return response.json();
    } else {
      // dostali jsme odpověď, ale na serveru došlo k chybě
      throw Error('Něco je špatně');
    }
  })
  .then(json => {
    // vypsání výsledku
    console.log(json);
  })
  .catch(error => {
    // vypsání chyby
    console.log(error)
  });
```
