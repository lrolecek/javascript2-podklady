# Getter a setter

Někdy potřebujeme u třídy skrýt interní implementaci a nechceme, aby programátor přímo četl nebo nastavoval interní vlastnosti třídy. Do třídy můžeme přidat tzv. gettery a settery, které slouží pro čtení a nastavování tzv. kalkulovaných vlastností.

Představme si např. třídu pro osobu, která má lřestní jméno a příjmení. My ale chceme, aby třída navenek nabízela možnost číst nebo nastavit pouze celé jméno.

```javascript
class Person {

  // konstruktor
  constructor(name, surname) {
    // nastavíme interní vlastnosti předané kontruktoru
    this._name = name;
    this._surname = surname;
  }

  // přidáme možnost číct/nastavovat kalkulovanou
  // vlastnost pro celé jméno

  // getter pro celé jméno
  get fullName() {
    return this.name + ' ' + this.surname;
  }

  // setter pro celé jméno
  set fullName(newName) {
    let names = newName.split(' ');
    this._name = names[0];
    this._surname = names[1];
  }
}
```

**Getter** je funkce, která se stará o čtení hodnoty z třídy. Před metodu přidáme klíčové slovo `get`. **Setter** funguje obdobně, ale je to funkce, která má jeden parametr a můžeme pomocí ní nastavit kalkulovanou vlastnost třídy.

Naše třídy `Person` z příkladu výše se chová, jako by obsahovala vlastnost `fullName`, kterou můžeme číst i nastavovat, i když ve skutečnosti třída interně pracuje pouze s vlastnostmi `name` a `surname` pro jméno a příjmení.

Třídu můžeme použít následovně:

```javascript
// vytvoříme instanci třídy a předáme výchozí vlastnosti
let osoba = new Person('Jana', 'Nováková');

// vypíšeme celé jméno
console.log(osoba.fullName);

// nebo ho můžeme i nastavit,
// jako by se jednalo o opravdovou vlastnost
osoba.fullName = 'Lenka Svobodová';
```