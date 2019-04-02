# Základy objektového programování v JavaScriptu, class

Základem objektového programování jsou tzv. třídy. Třída představuje něco jako šablonu pro tvorbu nových objektů v programu. Třída může obsahovat výchozí hodnoty pro vlastnosti objektu, stejně tak jako implementaci jeho chování - tj. funkce (metody), které pak budou mít objekty vytvořené pomocí této třídy.

Třída, neboli `class`, je novinka zavedená v ES2015 (tvz. moderní JavaScript). Jde o tzv. "syntactic sugar" - nepřináší žádnou novou funkčnost, která by v JavaScriptu nebyla už předtím, ale jde pouze o novou (hezčí) formu zápisu.

Třída obvykle obsahuje:

* vlastnosti (*properties*) - proměnné obsahující hodnoty
* metody (*methods*) - funkce, vykonávající nějakou činnost
* kontruktor (*contructor*) - speciální funkce pro incializaci objektu, která se zavolá při instancování třídy (vytvoření objektu na základě třídy)

Uvnitř třídy používáme objekt `this`, kterým se odkazujeme na konkrétní instanci objektu.

Třída obvykle zapouzdřuje nějakou funkcionalitu a bývá uložena v samostatném modulu.

Jako příklad třídy si můžeme představit objekty v naší hře s panáčkem, z kurzu JavaScript 1. Každý objekt měl vlastnosti - souřadnice x a y, šířku, výšku, obrázek. A mohl mít metody pro umístění objektu na obrazovce, test kolize s jiným objektem, apod.

## Syntaxe

Pro definování třídy používáme následující syntaxi:

```javascript
class Osoba {

  // konstruktor
  constructor(jmeno, prijmeni, vek) {
    // vlastnosti obvykle nastavujeme v konstruktoru
    this.jmeno = jmeno;
    this.prijmeni = prijmeni;
    this.vek = vek;
  }

  // metoda
  pozdrav() {
    console.log(`Ahoj, já jsem ${this.jmeno}.`);
  }
}
```

Když chceme vytvořit objekt, na základě těto třídy, musíme použít příkaz `new`:

```javascript
// vytvoříme instanci třídy Osoba a do konstruktoru
// předáme hodnoty, kterými se objekt inicializuje
let jana = new Osoba('Jana', 'Nováková', 23);

// následně se můžeme volat metody třídy
jana.pozdrav();

// nebo se ptát na vlastnosti
console.log(jana.vek);

// nebo je nastavovat
jana.vek = 24;

// nebo se ptát na getter - chová se jako vlastnost,
// ale není to přímo "proměnná" na objektu, ale funkce,
// která vrací hodnotu
console.log(jana.celeJmeno);
```