# API

**API** je zkratka pro Application Programming Interface. Je to rozhraní, pomocí kterého mohou aplikace komunikovat mezi sebou. Je to soubor vlastností a pravidel uvnitř softwaru, který umožňuje interakci s jiným softwarem.

API může mít mnoho podob. Při webovém vývoji je důležité například **browser API**. To je rozhraní (metody, vlastnosti, události), které může programátor využít pro interakci s prohlížečem uživatele.

Může se jednat o manipulaci se stránkou (`document.querySelector`, `element.textContent`, `element.addEventListener`) nebo s dalším obsahem (audio/video, geolokace, obraz z kamery, apod.). Tyto věci nejsou přímo součásti programovacího jazyka JavaScript, ale JavaScript k nim má přístup a my je můžeme v našich programech využívat.

Existují i API třetích stran (nebo naše vlastní) vystavená do internetu, pomocí kterých můžeme využívat různé služby nebo přistupovat k informacím. Např. Facebook nebo Twitter poskytuje API, pomocí kterého můžete vložit příspěvek nebo tweet do vaší stránky. Google Maps poskytují API, pomocí kterého můžete do své stránky vložit mapu. Různé meteorologické služby poskytují API, přes které můžeme zjistit aktuální počasí.

Kombinací různých API můžeme bytvářet zajímavé aplikace. Například pomocí Geolocation API prohlížeče můžeme zjistit uživatelovu polohu a pomocí GoogleMaps API jeho polohu vykreslit v mapě a zároveň zobrazit turistické atrakce v jeho okolí.

Na MDN najdeš [seznam všech API](https://developer.mozilla.org/en-US/docs/Web/API), která jsou součástí prohlížeče a můžeš je v JavaScriptu použít. Jde o specifikaci, dostupnost a funkčnost v různých prohlížečích se může lišit.

## Geolokace - příklad API v prohlížeči

Moderní prohlížeče dávají programátorům k dispozici geolokační API (a spoustu dalších). Uživatel musí použití geolokačního API stránce povolit - prohlížeč se snaží chránit jeho soukromí.

Geolokační API umí vrátit souřadnice uživatele na zeměkouli (zeměpisná délka a šířka). Na některých zařízeních (mobily) se pro získání polohy používá přesné GPS, na jiných zařízeních (např. PC bez GPS) se používá odhad polohy pomocí známých Wi-Fi sítí v okolí nebo podle poskytovatele internetového připojení.

Ke geolokačnímu API se přistupuje pomocí objektu `navigator.geolocation`:

```javascript
// otestujeme, zda je geolokační API k dispozici
if ('geolocation' in navigator) {
  // geolokace JE dostupná
  // získáme souřadnice
  navigator.geolocation.getCurrentPosition(position => {
    console.log(position.coords.latitude, position.coords.longitude);
  });
} else {
  // geolokace NENÍ dostupná
  console.log('Smůla, nevím, kde jsi!');
}
```

V dokumentaci MDN najdeš podrobný [popis geolokačního API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API).


## Webové API

Pomocí API dostupných na internetu můžeme komunikovat s různými vzdálenými službami. Může se jednat o služby třetích stran (Google Maps, Facebook, přesný čas, počasí, apod.) nebo o naše vlastní API napsané speciálně pro naši aplikaci.

Tvorba vlastního API je mimo rámec tohoto kurzu, protože se nejedná o front-end programování v prohlížeči, ale o back-end programování na straně serveru.

Webové API si můžeš představit jako skupiny tzv. **koncových bodů (end point)** - to jsou URL adresy, na které když pošleš požadavek, dostaneš od serveru odpověď.

Velmi zjednodušeně řečeno, pro moderní webové aplikace slouží API jako rozhraní mezi klientem (prohlížečem) a databází na serveru. API umožňuje data číst, ale i je posílat zpět na server.

**API mohou být otevřená** - přistupovat na ně může kdokoliv bez ověření a číst libovolně data. Zcela otevřená API nejsou výjimečná, ale dnes už ani příliš obvyklá. Každý dotaz na server vyžaduje nějaký (i když malý) výkon serveru a kapacitu linky a u otevřených API hrozí, že počet požadavků od "internetové veřejnosti" přeroste serveru přes hlavu a nebude je zvládat odbavovat. Veřejná API jsou často limitována na maximální počet dotazů za den/hodinu/minutu nebo třeba na objem přenesených dat.

### API key

Většina volně dostupných API **vyžaduje alespoň nějakou formu autentifikace**. Ta obvykle spočívá v tom, že si u dané služby zřídíš účet a za odměnu dostaneš tzv. **API key** - klíč sestávající ze série znaků, který musí být součástí každého dotazu na API.


# Formát JSON

Webová API mohou vracet data v libovolných formátech. Většina moderních API však vrací data buď ve formátu XML nebo v dnes nejrozšířenějším formátu JSON.

**JSON** je zkratka pro JavaScript Object Notation. Je to způsob, jak zapsat JavaScriptový objekt v textové podobě, které se snadno přenáší uvnitř HTTP požadavků a odpovědí.

JSON na první pohled vypadá jako klasický JavaScriptový objekt, ale jsou zde drobné rozdíly. Hlavní je, že se v JSONu používají výhradně uvozovky a v uvozovkách musí být uzavřena i jména vlastností, nejen textové hodnoty.

Příklad formátu JSON:

```json
{
  "jmeno": "Jana",
  "prijmeni": "Nováková",
  "vek": 42,
  "svobodna": false,
  "zamestnani": {
    "firma": "První internetová, s.r.o.",
    "pozice": "programátorka"
  },
  "deti": [
    {
      "jmeno": "Alenka",
      "vek": 13
    },
    {
      "jmeno": "Pepík",
      "vek": 11
    }
  ]
}
```

Všimněte si, že jako hodnota vlastnosti může být uveden další objekt nebo pole (případně pole objektů).

JavaScritp má k dispozici metody:
- `JSON.parse()` pro převod formátu JSON na javascriptový objekt
- `JSON.stringify()` pro převod javascriptového objektu do formátu JSON
