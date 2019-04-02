# Git a GitHub

## Git

Git je systém pro správu verzí. To znamená, že je schopen zaznamenávat kompletní historii projektu - všechny změny v souborech, přidané nebo smazané soubory.

Uživatel se pak může kdykoliv vrátit v historii do minulosti a podívat se např. jak vypadal nějaký konkrétní soubor před změnou, případně obnovit smazaný soubor, apod.

Git také umožňuje vytvářet tzv. větve (branch). Vývojář si vytvoří v projektu samostatnou větev třeba pro vývoj nové funkce v aplikaci. Pracuje v této vývojové větvi, aniž by zasahoval do projektu, kde je stále aplikace ve funkčním a produkčním stavu.

Tj. i když vývojář dělá ve své větvi chyby, má rozepsaný a nefunkční kód apod, tak produkční verze aplikace zůstává netknutá. Teprve když je vývoj nové funkce hotový, lze vývojovou větev sloučit zpět do hlavní větve projektu. Větvím se nebudeme v rámci kurzu věnovat, ale je dobré o nich vědět.

**Git běží lokálně na počítači vývojáře** a sleduje změny v souborech.

### Inicializace repozitáře

Aby Git začal změny v projektu sledovat, musíš ho na projektu zapnout, neboli iniciovat (založit) tzv. repozitář.

### Commit

Ve chvíli, kdy chce vývojář uložit aktuální stav projektu jako bod v historii, musí provést tzv. **commit**. Každý commit má svůj název. V přehledu projektu je pak vidět, při kterém commitu byly konkrétní soubory změněny.

Důležité je pochopit, že Git neuchovává změny v souborech (historii) automaticky při každém uložení souboru. Vývojář sám musí commitem říci, že v tomto stavu chce projekt v historii uchovat.

### Kde je historie uložená

Všechny změny v projektu, které Git uchovává, se ukládají uvnitř projektu ve složce **.git**

Možná ve svém tuto složku nevidíš, protože máš operační systém nastavený tak, aby skryté složky neukazoval. To je v pořádku. Většinou ji nepotřebuješ vidět.

Ať už složku vidíš nebo ne, v žádném případě ji nemaž. Pokud složku smažeš, přijdeš o celou historii projektu a budeš mít pouze jeho aktuální verzi, která se právě nacházela ve složce projektu.


## GitHub

Jak už jsme si řekli, všechny změny Git uchovává lokálně na tvém počítači. GitHub je webová služba, která ti umožňuje uložit Git repozitář do internetu a sdílet ho tak s ostatními, nebo mít prostě zálohu pro vlastní použití.

GitHub (nebo podobné služby) je perfektní nástroj pro týmovou spolupráci.  Umožňuje totiž mnoha vývojářům pracovat na jednom projektu. Každý vývojář může pracovat na svém kousku a změny pak poslat do společného repozitáře, kde Git/GitHub změny sloučí.

GitHub je tzv. **vzdálený repozitář**.

## GitHub Desktop

Git se standardně ovládá z příkazové řádky a je to zcela regulérní magie (alespoň ty složitější úkony). Stane-li se z tebe vývojářka, bude dobré se příkazy pro ovládání Git na příkazové řádce naučit, ale v rámci tohoto kurzu se tím nebudeme zabývat.

Existuje spousta programů, které poskytují pro Git grafickou nadstavbu. Tj. lze v normálním programu klikat na tlačítka a dělat ty stejné věci, které bychom museli normálně psát na příkazové řádce.

Jednoduchým programem se základní sadou úkonů je [GitHub Desktop](https://desktop.github.com/), který slouží jak pro správu lokálního repozitáře, tak jeho posílání na GitHub do internetu nebo stahování změn z internetu zpět na lokální počítač.