# Předávání parametrů hodnotou vs. odkazem

Když předáváme parametry do funkce nebo i když používáme jednoduché přiřazení hodnoty jedné proměnné do druhé, JavaScript některé parametry předává tzv. **hodnotou** a jiné **odkazem**. Abychom pochopili rozdíl, popišme si nejprve datové typy JavaScriptu.


## Datové typy

JavaScript má 5 základních datových typů: `Number`, `String`, `Boolean`, `null`, `undefined`. Těmto typům se říká **primitivní datové typy** (primitive data types). Tyto datové typy mohou obsahovat vždy pouze jednu hodnotu (číslo, textový řetězec, apod.).

JavaScript má ještě další speciální datový typ `Object`.

Objekty mohou uchovávat kolekce dat a složitější struktury. Do objektů patří pole `Array`, funkce `Function` a samozřejmě samotný `Object`. JavaScript všechny tři považuje za Object.

Existuje ještě další datový typ `Symbol`, který slouží pro vytváření jedinečných identifikátorů pro objekty. V tomto kurzu se jím nebudeme zabývat.


## Primitivní datové typy - předávání hodnotou

Když je primitivní datový typ přiřazený do proměnné, můžeme o tom přemýšlet tak, že proměnná skutečně *obsahuje* danou hodnotu.

```javascript
let a = 42;
let b = 'Alena';
let c = true;
```

V našem příkladu `a` *obsahuje hodnotu* `42`, `b` *obsahuje hodnotu* `'Alena'`, `c` *obsahuje hodnotu* `true`.

V paměti počítače tedy máme uloženo:

| Proměná | Hodnota |
| ------- | ------- |
| a       | 42      |
| b       | 'Alena' |
| c       | true    |

Když přiřadíme hodnotu z jedné proměnné primitivního typu do další proměnné, tak hodnotu **zkopírujeme** - nové proměnné jsou samostatné a zcela nezávislé na původních hodnotách.

Když k našemu kódu přidáme:

```javascript
let x = a;
let y = b;
let z = c;
```

Budeme v paměti počítače mít uchované tyto hodnoty:

| Proměná | Hodnota |
| ------- | ------- |
| a       | 42      |
| b       | 'Alena' |
| c       | true    |
| x       | 42      |
| y       | 'Alena' |
| z       | true    |

Když změníme jednu z hodnot, **nezmění** se druhá. Hodnoty jsou na sebě zcela nezávislé:

```javascript
a = 7;
b = 'Jana';
c = false;

console.log(a, b, c, x, y, z);

// vypíše se:
// 7, Jana, false, 42, Alena, true
```

Tento princip je zachován i v případě, že proměnnou předáváme do funkce jako parametr. Proměnná se **předává hodnotou**, tj. zkopíruje se do obsahu lokální proměnné ve funkci. Změna lokální proměnné nijak neovlivní hodnotu proměnné, kterou jsem do funkce předávali.



## Objekty - předávání odkazem (referencí)

Pokud do proměnné přiřadíme hodnotu neprimitivního typu (tj. objekt, pole, funkci), proměnná nebude skutečně obsahovat danou hodnotu, ale pouze **odkaz na ni**.  Můžeš si to představit třeba tak, že skutečná hodnota leží někde v paměti počítače a v proměnné je uložená pouze adresa, kde daná hodnota v paměti je. Říkáme, že se jedná o objekt **referenčního typu**.

Pokud tedy máme takovýto program:

```javascript
let pole = [1, 2, 3];
let objekt = { a: 1, b: 2};
```

V pyměti počítače se vytvořilo pole a objekt. Proměnné `pole` a `objekt` obsahují adresu, umístění tohoto pole nebo objektu v paměti.

Zkusme si to ukázat na příkladu:

```javascript
let pole = [];
```

Řekněme, že adresu v paměti počítače budeme uzavírat do ostrých závorek. V paměti počítače to bude vypadat nějak takto:

| Proměná | Hodnota |
| ------- | ------- |
| pole    | <#001>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | []            |

Přidejme do pole další prvek:

```javascript
let pole = [];

pole.push(1);
```

V paměti počítače bude vše vypadat následovně:

| Proměná | Hodnota |
| ------- | ------- |
| pole    | <#001>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | [1]           |

Všimni si, že *"hodnota"* pole se nezměnila. Pořád obsahuje odkaz na stejnou adresu v paměti počítače. Změnil se pouze obsah na dané adrese.

Když proměnnou neprimitivního typu přiřadíme do další proměnné, zkopírujeme do nové proměnné pouze adresu na stejné místo v paměti počítače:

```javascript
let novePole = pole;
```

Dostaneme:

| Proměná  | Hodnota |
| -------- | ------- |
| pole     | <#001>  |
| novePole | <#001>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | [1]           |


Když teď změníme obsah proměnné `novePole`, budeme měnit obsah objektu v paměti počítače, na který ukazují proměnné `pole` i `novePole`.

```javascript
let pole = [];
pole.push(1);
console.log(pole);
// výsledek: [1]

let novePole = pole;
novePole.push(2);
console.log(novePole);
// výsledek: [1, 2]

console.log(pole);
// výsledek: [1, 2]
// pole ukayuje na stejnou adresu, změna jednoho změní i druhé
```

V paměti počítače:

| Proměná  | Hodnota |
| -------- | ------- |
| pole     | <#001>  |
| novePole | <#001>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | [1, 2]        |


Vidíme že v paměti počítači je pouze jeden objekt, na který ukazují obě proměnné.

### Znovupřiřazení hodnoty

Když do proměnné referečního typu přiřadíme novou hodnotu, stará hodnota zůstane v paměti počítače.

```javascript
let pole = [1, 2, 3];
```
Dostaneme:

| Proměná | Hodnota |
| ------- | ------- |
| pole    | <#001>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | [1, 2, 3]     |

Když v kódu do `pole` přiřadíme novou hodnotu:

```javascript
let pole = [1, 2, 3];

// nová hodnota
pole = [7, 8, 9];
```
Dostaneme:

| Proměná | Hodnota |
| ------- | ------- |
| pole    | <#002>  |

| Adresa v paměti | Obsah objektu |
| --------------- | ------------- |
| <#001>          | [1, 2, 3]     |
| <#002>          | [7, 8, 9]     |


## Garbage collection

V příkladu vůše proměnná `pole` nyní ukazuje na `<#002>` a na původní `<#001>` neukazuje žádná jiná proměnná. Pokud přestanou existovat všechny odkazy na danou adresu, program ztratil možnost s danou adresou jakkoliv pracovat a JavaScript může provést tzv. **garbage collection**, tedy obsah bezpečně odstranit z paměti. V příkladu výše garbage collector z paměti odstraní pole `[1, 2, 3]`.


## Porovnávání referenčních typů (ojektů)

Když budeme porovnávat dvě proměnné referenčního typu, budou se rovnat pouze v případě, že odkazují na stejnou adresu. Nezáleží na tom, zda použijeme `==` nebo `===`.

```javascript
let pole1 = [1, 2, 3];
let pole2 = pole1;

console.log( pole1 === pole2 );
// výsledek: true
```

Pokud se ale jedna o dva samostatné objekty v paměti počítače, které pouze obsahují stejné hodnoty, nebude rovnost platit.

```javascript
let pole1 = [1, 2, 3];

// vytváříme nové pole, jen má náhodou stejné hodnoty
let pole2 = [1, 2, 3];

console.log( pole1 === pole2 );
// výsledek: false
```


## Parametry do funkcí

Stejně jako přiřazování hodnot do proměnných funguje i předávání parametrů do funkcí.

### Předávání parametru hodnotou (by value)

Předáme-li jako parametr do funkce primitivní hodnotu, zkopíruje se tato hodnota do lokální proměnné ve funkci. Jakmile program funkce skončí, lokální proměnná zanikne. I když uvnitř funkce změníme obsah proměnné, protože se jedná o zkopírovanou hodnotu, její změna nijak neovlivní obsah proměnné, kterou jsem zvenku předávali dovnitř funkce.

### Předávání parametru odkazem (by reference)

Předáváme-li do funkce neprimitivní hodnotu (referenční datový typ), umístí se do lokální proměnné pouze odkaz na data v paměti. Jakékoliv změny, které uvnitř funkce s proměnnou provedeme, se provedou na datech v paměti, kam ukazuje i vnější proměnná, kterou jsme do funkce posílali jako parametr.

Po ukončení funkce zanikne lokální proměnná - tj. přestane existovat odkaz na data v paměti uložený v lokální proměnné. Na stejná data ale stále ukazuje i proměnná z vnějšku funkce. Po ukončení funkce tedy původní proměnná obsahuje změny provedené uvnitř funkce.
