# Használd az Asyn-Await-ot vagy Promiseokat az aszinkron hibakezeléshez

### Rövid magyarázat

A callbackek nem skálázhatóak jól mivel a legtöbb programozó nem ismeri őket. Megkövetelik a hibák vizsgálatát minden helyzetben és a sok szintű kódbeágyazás nehézkessé teszi a program futásának áttekintését. A Promise könyvárak, mint a BlueBird, async és Q egy egységes stílusban - a RETURN és THROW használatával - teszik lehetővé könnyen követhetően a program futásának kontrolálását. Lehetővé teszik a jól bevált try-catch hibakezelés használatát aszinkron környezetben, ami a program fő futási útvonalát megszabadítja a hibák vizsgálatától.

### Példakód – promise-ok használata kivételek elkapásához

```javascript
doWork()
 .then(doWork)
 .then(doOtherWork)
 .then((result) => doWork)
 .catch((error) => {throw error;})
 .then(verify);
```

### Kerülendő példa – hibakezelés callback stílusban

```javascript
getData(someParameter, function(err, result) {
    if(err !== null) {
        // az átadott callback hívása és a hiba átadása...
        getMoreData(a, function(err, result) {
            if(err !== null) {
                // az átadott callback hívása és a hiba átadása...
                getMoreData(b, function(c) {
                    getMoreData(d, function(e) {
                        if(err !== null ) {
                            // Érted már, mi a probléma? 
                        }
                    })
                });
            }
        });
    }
});
```

### Idézet: "Van egy baj a Promise-okkal"

 Idézet a pouchdb.com blogból:

 > ……tulajdonképpan a callbackek még ennél is baljósabb dolgot csinálnak: megfosztanak minket a call stacktől, amit általában adottnak tekintünk a többi nyelvben. Kód írása a call stack nélkül olyan, mint autót vezetni fékpedál nélkül: nem tudod, hogy mennyire fontos, amíg egyszer használnád, és nincs a helyén. A Promise-ok lényege, hogy visszaadják a nyelv azon alapjait, melyeket elvesztettünk az aszinkron kóddal: return, throw és a call stack. De ahhoz, hogy előnyt kovácsoljunk a Promise-okból, meg tanulni használni őket.

### Idézet: "A Promise-ok sokkal összetettebbek mint gondolnád"

 Idézet gosquared.com-ról:

  > ………A Promise-ok használata sokkal kompaktabb, átláthatóbb és gyorsabb. Ha egy hiba vagy kivétel ketletkezik bármelyik művelet közben egy egységes .catch() blokk fogja kezelni. Az ilyen egységes hibakezelés azt eredményezi, hogy nem kell minden egyes sor után vizsgálni a hibákat.

### Idézet: "A Promise megtalálható natívan az ES6 szabványban, használható generátorokkal"

 Idézet a StrongLoop blogról:

 > ………A callbackek hibakezelése meglehetősen rossz, a Promse-ok esetében ez sokkal jobban megoldható. Kombináld az Expressben beépített hibakezelést a Promise-okkal és máris drasztikusan csökkentetted a nem kezelt kivételek lehetőségét. A Promise megtalálható natívan az ES6 szabványban, használható generátorokkal és olyan fordítókkal mint a Babel, használható az ES7 szabványban leírt async/await-el.

### Idézet: "Az összes eddigi megoldás, amit eddig a program futásának szabályozására használtál teljesen rossz"

Idézet Benno blogjáról:

 > ……Az egyik 'legjobb' dolog a callback alapú, aszinkron programozásban, hogy az összes eddigi megoldás, amit eddig a program futásának szabályozására használtál teljesen rossz. Viszont, ami a legrosszabb az a hibák kezelése. A Javascript rendelkezik egy sokaknak ismerős try-catch megoldással a hibakezeléshez. A fő probléma a kivételekkel az, hogy nagyszerűen keresztül juttahatóak a call stacken, de teljesen haszontalanok, ha a hiba egy teljesen másik call stacken keltkezett.
