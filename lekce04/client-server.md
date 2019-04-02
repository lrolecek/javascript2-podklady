# Komunikace po síti

## Klient-server
Počítače na síti (např. na internetu) spolu na dálku komunikují a vyměňují si informace. Počítač, který si vyžádá informace se označuje jako **klient**. Počítač, který tyto informace na vyžádání poskytne se nazývá **server**.

Je asi nejjednodušší představovat si vazbu klient-server jako dva počítače, které si spolu povídají, ale ve skutečnosti nejde ani tak o tyto počítače jako spíše o software, který na nich běží. **Klient** je program, který běží na lokálním počítači (PC, mobil, apod.) a požaduje informace - např. webový prohlížeč. **Server** je program, který běží na vzdáleném počítači např. někde v datovém centru, a tyto informace poskytuje - např. webový server a webová aplikace na něm běžící.

Klient si data vyžádá pomocí požadavku - tzv. **request**. Server posílá odpověď - tzv. **response**.

![Komunikace klient-server](images/client-server.jpg)

Nejsnáze představitelná interakce klient-server je zobrazení webové stránky v prohlížeči. Při zadání url adresy do prohlížeče zadáváme požadavek na server, že chceme zobrazit webovou stránku. Server stáhne kopii webové stránky ze svého disku (nebo ji vytvoří dynamicky za běhu) a pošle ji klientovi (prohlížeči), který ji následně zobrazí.

Toto je velmi zjednodušený popis. Pokud by tě tématika zajímala více do hloubky, podívej se třeba na článek [How the Web Works](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works) na MDN.


## HTTP Request/Response

HTTP neboli Hyper-Text Tranfer Protocol je nejčastější (ale ne jediný) způsob, jakým spolu klient a server komunikují. Protokol si představ jako jazyk - klient i server ho musí oba znát, aby se spolu domluvili.

### Request (požadavek)

Každý **HTTP Request** se skládá ze tří částí:

- **požadavek (request line)** - jeden řádek, který obsahuje adresu, odkud vyžadujeme odpověď, způsob, jakým ji vyžadujeme, a protokol, kterým komunikujeme
- **hlavičky požadavku (request headers)** - slouží pro předávání dodatečných informací o požadavku. Může jít např. o jazyk, v jakém preferujeme odpověď, nebo třeba identifikační údaje, pokud cílový zdroj vyžadavku požaduje přihlášení, apod. Požadavek nemusí nutně žádné hlavičky obsahovat.
- **tělo požadavku (request body)** - je blok, kde můžeme serveru předat další data (requesty neslouží pouze k získávání dat, ale i k jejich posílání na server). Stejně jako u hlaviček nemusí být tělo v requestu vůbec obsaženo, pokud žádná data nepotřebujeme poslat.

Podrobnější popis HTTP požadavku najdeš např. [zde](https://www.toolsqa.com/client-server/http-request/)

### Response (odpověď)

Podobně jako u požadavku, každá **HTTP Response** se skládá ze tří částí:

- **stav odpovědi (status line)** - jeden řádek, který obsahuje protokol, jakým se komunikuje, stavový kód odpovědi a text s důvodem pro tento stavový kód
- **hlavičky odpovědi (response headers)** - stejně jako u požadavku, odpověď si nemusí nutně obsahovat žádné hlavičky, které poskytují dodatečné informace o odpovědi, ale většina odpovědí několik hlaviček má. Důležitou hlavičkou je např.:
  - *Content-Type* - obsahuje typ/formát dat, která jsou obsažena v tělě odpovědi
- **tělo odpovědi (response body)** - obsahuje data, která server posílá klientovi jako odpověď na jeho požadavek. Data mohou být v ruzných formátech, často se používá např. JSON nebo XML.

Podrobnější popis HTTP odpovědi najdeš např. [zde](https://www.toolsqa.com/client-server/http-response/)


## HTTP stavové kódy

Důležitou součástí každé HTTP odpovědi jsou tvz. **stavové kódy (status codes)**. Stavový kód je číslo, které podává informaci o tom, jak náš požadavek dopadl. Ke každému číslu stavového kódu existuje i textový popis, co který kód znamená.

Stavové kódy jsou rozdělené do skupin podle toho, na jakou číslici stavový kód začíná:

- **2xx** - Tyto chceme vidět nejčastěji. Kódy začínající dvojkou znamenají úspěšný požadavek. Nejčastěji se jedná o kód `200 OK`, který značí, že vše proběhlo v pořádku a v tělě odpovědi jsou požadovaná data (nebo v případě odesílání dat na server to znamená, že server data úspěšně přijal).
- **4xx** - kódy začínající čtyřkou znamenají, že chyba je na straně požadavku. Např. že jsme si vyžádali stránku (obrázek, data, ...), která neexistuje - to je nechvalně proslulá chyba `404 Not Found`. Nebo v případě `403 Not Authorized`, že jsme si vyžádali data, ke kterým nemáme povolený přístup.
- **5xx** - kódy začínající pětkou znamenají že požadavek byl v pořádku, ale došlo k chybě na straně serveru - např. ve skriptu, který nám měl poslat data, došlo k chybě, apod. Většinou dostaneme obecnou chybovou odpověd `500 Internal Server Error`, ale existují i další.

Chceš-li vědět víc, podívej se na MDN na [seznam stavových kódů a jejich význam](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) nebo na Dev.Opera na hezký [článek o status kódech](https://dev.opera.com/articles/http-response-codes/).

Stavové kódy jsou důležité, protože podle nich poznáme, zda byl náš požadavek úspěšný nebo ne. V našem kódu bychom měli minimálně testovat, zda odpověď ze serveru obsahuje kód `200 OK` a teprve potom můžeme předpokládat, že odpověď bude obsahovat i požadovaná data, a začít je zpracovávat.
