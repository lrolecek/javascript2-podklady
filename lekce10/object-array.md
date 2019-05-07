# Přístup k vlastnostem objektu jinak

Z našich lekcí jsme zvyklí, že k vlastnostem objektu přistupujeme tak, že název vlastnosti napíšeme za tečku, např. `osoba.jmeno`.

K vlastnostem objektu ale můžeme přistupovat i pomocí syntaxe se složenými závorkami, podobně jako přistupujeme k prvkům pole. (Nápověda: pole v JavaScriptu je objekt.)

Toto jsou dva zcela ekvivalentní zápisy:

```javascript
// pomocí tečkové konvence
osoba.jmeno = 'Lenka';

// nebo pomocí složených závorek
osoba['jmeno'] = 'Lenka';
```


...dopíšu