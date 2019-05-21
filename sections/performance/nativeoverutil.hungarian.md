# Részesítsd előnyben a natív JS metódusokat a harmadik fejlesztő(k)től származó könyvtárakkal szemben


<br/><br/>

### Rövid magyarázat

Néha a natív metódusok használata jobb megoldás, mint pl. a `lodash` vagy `underscore` használata, hiszen ezek használata lassíthatja a végrehajtási sebességet ill. a szükségesnél több tárhely felhasználásával járhat. Natív metódusok használata hozzávetőlegesen [ ~50% teljesítménynövekedéssel](https://github.com/Berkmann18/NativeVsUtils/blob/master/analysis.xlsx) járhat, többek között az alábbi metódusok esetén: `Array.concat`, `Array.fill`, `Array.filter`, `Array.map`, `(Array|String).indexOf`, `Object.find`, ...

<!-- comp here: https://gist.github.com/Berkmann18/3a99f308d58535ab0719ac8fc3c3b8bb-->

<br/><br/>

### Példa: Lodash vs V8 (natív) összehasonlítás
A lenti diagrammon [számos Lodash metódus átlagos végrehajtási ideje látható](https://github.com/Berkmann18/NativeVsUtils/blob/master/nativeVsLodash.ods). A Lodash metódusoknak átlagosan 146.23%-kal tovább tart elvégezni egy adott feladatot, mint a metódusok natív megfelelőinek. 

![meanDiag](../../assets/images/sampleMeanDiag.png)

### Példakód – A `_.concat`/`Array.concat` metódus benchmarkja
```javascript
const _ = require('lodash'),
  __ = require('underscore'),
  Suite = require('benchmark').Suite,
  opts = require('./utils'); //cf. https://github.com/Berkmann18/NativeVsUtils/blob/master/utils.js

const concatSuite = new Suite('concat', opts);
const array = [0, 1, 2];

concatSuite.add('lodash', () => _.concat(array, 3, 4, 5))
  .add('underscore', () => __.concat(array, 3, 4, 5))
  .add('native', () => array.concat(3, 4, 5))
  .run({ 'async': true });
```

A fenti kód eredménye:

![output](../../assets/images/concat-benchmark.png)

További tesztek [itt találhatóak](https://github.com/Berkmann18/NativeVsUtils/blob/master/index.txt) vagy [ez a teszt](https://github.com/Berkmann18/NativeVsUtils/blob/master/index.js) is használható, utóbbi színezett eredményekkel szolgál.

### Blog Idézet: "(Lehet, hogy) Nincs szükséged Lodash-re/Underscore-ra"

Egy, a [Lodash és Underscore teljesítményére fókuszálló GitHub repositroyból](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore).

 > A Lodash és az Underscore kiváló, modern JavaScript könyvtárak, és széles körben elterjedtek a Front-end fejlesztők körében. Viszont, ha modern böngészőkre fejlesztünk, gyakran szembesülünk a ténnyel, hogy rengeteg metódus az említett könyvtárakból már eleve rendelkezésre áll natív módon, az ECMAScript5 [ES5] és ECMAScript2015 [ES6] szabványoknak köszönhetően. Ha szeretnéd a projekt függőségeit alacsonyan tartani, és tisztában vagy a megcélzott böngészőkkel, nincs szükséged a Lodash-re/Underscore-ra.

### Példa: nem natív segédfüggvények használatlának automatikus észlelése
Létezik egy [ESLint plugin](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore) ami felimseri, ha olyan külső könyvtárat használunk, amire nincs feltétlen van szükség (ld. az alábbi példát).
Használatához adjuk a következő sorokat az ESLint konfigurációs fájlhoz:
```json
{
  "extends": [
    "plugin:you-dont-need-lodash-underscore/compatible"
  ]
}
```

Vegyük az alábbi példát:
```js
const _ = require('lodash');
// az ESLint jelezni fog a fenti sorra
console.log(_.map([0, 1, 2, 4, 8, 16], x => `d${x}`));
```
Az ESLint az alábbi kimentet fogja produkálni, ha a YDNLU plugint használjuk:
![output](../../assets/images/ydnlu.png)

Persze a fenti példa nem feltétlenül valószerű, de szemléltetésnek tökéletes.
