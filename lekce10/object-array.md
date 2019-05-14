# Přístup k vlastnostem objektu jinak

Z našich lekcí jsme zvyklí, že k vlastnostem objektu přistupujeme tak, že název vlastnosti napíšeme za tečku, např. `osoba.jmeno`.

K vlastnostem objektu ale můžeme přistupovat i pomocí syntaxe se hranatými závorkami, do kterých uvedeme jako řetězec název vlasntosti objektu. Syntaxe vypadá podobně, jako když přistupujeme k prvkům pole. (Nápověda: pole v JavaScriptu je objekt.)

Toto jsou dva zcela ekvivalentní zápisy:

```javascript
// pomocí tečkové konvence
osoba.jmeno = 'Lenka';

// nebo pomocí složených závorek
osoba['jmeno'] = 'Lenka';
```

Toho můžeme využít ve chvíli, kdy například používáme objekt jako místo, kam si ukládáme stav naší aplikace a její data, aby k ní měli přístup všechny části aplikace.