# Dědičnost

Třída (class) v JavaScriptu může rozšiřovat jinou třídu. Může z ní vycházet, sdílet společné vlastnosti a metody, a zároveň přidávat metody vlastnosti nebo přepisovat (tzv. přetěžovat) metody existující.

Představme si jednoduchou třídu pro zvířátko. Každé zvířátko má jako vlastnosti jméno a rychlost a metodu `run()`, která do konzole prohlížeče vypíše, jak rychle zvířátko běží:

```javascript
class Animal {

  // konstruktor
  constructor(name, speed) {
    // vlastnosti
    this.name = name;
    this.speed = speed;
  }

  // metoda
  run() {
    console.log(`${this.name} běží rychlostí ${this.speed} km/h.`);
  }
}
```

Třídu můžeme použít následujícím způsobem:

```javascript
let alik = new Animal('Alík', 10);
alik.run();
// do konzole se vypíše: Alík běží rychlostí 10 km/h.
```

Naše třída Animal obsahuje vlastnosti a metody společné pro všechna zvířátka. Ma bychom ale chtěli, aby náš Alík uměl i štěkat. Nedává ale smysl, přidávat metodu pro štěkání do obecné třídy Animal, protože ne všechna zvířátka štěkají.

Vytvoříme tedy dřídu Dog, která bude orzšiřovat třídu `Animal` (bude z ní dědit). K tomu se používá klíčové slovo `extends`:

```javascript
class Dog extends Animal {

  // konstruktor
  constructor(name, speed, sound) {
    // zavoláme konstruktor nadražené supertřídy
    // a předáme mu potřebné parametry
    super(name, speed);

    // a můžeme nastavit i vlastnosti specifické pro třídu Dog
    this.sound = sound;
  }

  // metoda
  bark() {
    console.log(`${this.name} štěká: ${this.sound}.`);
  }
}
```

Použijeme následovně:

```javascript
let alik = new Dog('Alík', 10, 'Haf, haf, haf');
alik.run();
alik.bark();
// do konzole se vypíše:
// Alík běží rychlostí 10 km/h.
// Alík štěká: Haf, haf, haf.
```

Vydíme, že třída Dog má zároveň vlastnosti `name` a `speed` a metodu `run()` z nadřazené třídy Animal, tak svoji vlastní vlastnost `sound` a metodu `bark()`.

V kontruktoru vždy voláme metodu `super()`, která zavolá kontruktor nadřazené třídy.
