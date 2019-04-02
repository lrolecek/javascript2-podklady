# Ošetření chyb pomocí try/catch

Pro ošetření případných chyb v programu můžeme použít konstrukci **try/catch/finally**:

```javascript
try {
  // kód, ve kterém může dojít k chybě
} catch {
  // tento kód se provede v případě chyby
} finally {
  // tento blok lze vynechat
  // provede se v obou případech - buď po úspěšném
  // vykonání bloku try nebo v případě chyby po
  // skončení bloku catch
}
```

Tuto konstrukci můžeme použít i pro jednoduché zachycení chyb, které nastaly během `await`:

```javascript
async function getPerson(id) {
  try {
    let response = await fetch(`https://swapi.co/api/people/${id}/`);
  } catch {
    console.log('Došlo k chybě pro načítání ze serveru.');
  }
  let json = await response.json();
  console.log(json);
}
```

V bloku `try` můžeme mít i více řádků, pokud nám stačí vědět, že došlo k chybě, a nemusíme vědět, kde přesně.

```javascript
async function getPerson(id) {
  try {
    let response = await fetch(`https://swapi.co/api/people/${id}/`);
    let json = await response.json();
    console.log(json);
  } catch {
    console.log('Někde se něco nepovedlo.');
  }
}
```
