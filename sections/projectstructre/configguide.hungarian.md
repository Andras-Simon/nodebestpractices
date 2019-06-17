# Használj környezeti változó kompatibilis, biztonságos és hierarchikus konfigurációt

<br/><br/>

### Rövid magyarázat

Ha konfigurációs fájlokkal van dolgunk, sok dolog nehezítheti meg, vagy lassíthatja munkánkat:

1. Környezeti változók segítségével beállítani alkalmazásunkat könnyen nehézkessé válhat ha több 100 változót kell kezelnünk (ahelyett, hogy egyszerűen  beállítanánk őket egy konfigurációs fájlban, amit aztán kommitolunk), azonban ha csak a fájlokra hagyatkoznánk elvennénk a lehetőséget a DevOps tagoktól, hogy a kód átírása nélkül változtassák az alkalmazás viselkedését. Éppen ezek miatt, egy megbízható konfigurációs megoldás a fájlok mellett kezeli a környezeti változókkal való felülírást is.

2. Ha minden beállítás egy lapos JSON fájlban található, nehézkes lesz megtalálni a fájlban a keresett változókat ha abból túl sok van. Egy hierarchikus JSON file, ami csoportosítja a változókat megoldja ezt a problémát ill. számos osztálykönyvtár létezik, ami külön fájlokból tudja összefésülni a végső konfigurációt. Példákat ld. később.

3. Érzékeny adatok (pl. adatbázis jelszavak) tárolása konfigurációs fájlokban kifejezetten nem ajánlott, de sajnos nincs gyors és egyszerű módszer ennek kiküszöbölésére. Egyes konfiguráció kezelő megoldások lehetővé teszik a konfig fájlok titkosítását, mások csak a változó értékét titkosítják GIT kommit előtt, vagy szimplán nem is tárolják ezeket az érzékeny adatokat, hanem telepítés során helyettesítik be az értékeket, környezeti változókból.

4. Egyes összetettebb esetek megkívánják, hogy a konfigurációt parancssori argumantumokkal (vargs) vagy központi cacheből betöltve (pl. Redisben tárolt beállítások, hogy több párhuzamosan telepített szerver ugyanazzal a konfigurációval fusson) adjuk meg.

Léteznek osztálykönyvtárak, melyek a fenti problémákra mind nyújtanak megoldást, ráadásul ingyenesen elérhetőek. Példák amik mind megfelelnek a fent állított követelményeknek: [rc](https://www.npmjs.com/package/rc), [nconf](https://www.npmjs.com/package/nconf) és [config](https://www.npmjs.com/package/config).

<br/><br/>

### Példakód – a hierarchikus konfiguráció segít a fájl átláthatóbbá tételében, és a hatalmas lonfogurációs fájlok is jól karbantarthatóak maradnak

```js
{
  // Customer modul konfiguráció
  "Customer": {
    "dbConfig": {
      "host": "localhost",
      "port": 5984,
      "dbName": "customers"
    },
    "credit": {
      "initialLimit": 100,
      // Állítsd ezt alacsonyra ha tesztelsz
      "initialDays": 1
    }
  }
}
```

<br/><br/>
