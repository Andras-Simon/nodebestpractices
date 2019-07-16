# Kapd el a kezeletlen Promsie kivételeket

<br/><br/>

### Rövid magyarázat

Typically, most of modern Node.js/Express application code runs within promises – whether within the .then handler, a function callback or in a catch block. Surprisingly, unless a developer remembered to add a .catch clause, errors thrown at these places are not handled by the uncaughtException event-handler and disappear.  Recent versions of Node added a warning message when an unhandled rejection pops, though this might help to notice when things go wrong but it's obviously not a proper error handling method. The straightforward solution is to never forget adding .catch clauses within each promise chain call and redirect to a centralized error handler. However, building your error handling strategy only on developer’s discipline is somewhat fragile. Consequently, it’s highly recommended using a graceful fallback and subscribe to `process.on(‘unhandledRejection’, callback)` – this will ensure that any promise error, if not handled locally, will get its treatment.

Jellemzően, a legtöbb modern Node.js/Javsascript alkalmazás Promise-okban fut, vagy a .then-en belül, vagy egy catch blokkban, vagy egy callbackben. Meglepően, hacsak a fejlesztő nem felejtette el a .catch blokkot, az olyan kivételek amiket itt dobunk nem jutnak el az uncaughtException eseménykezelőig és felszívódnak. A Node újabb verziói már figyelmeztetnek ha ilyen történik, és ez segíthet is megtalálni ha valami balul sül el, de nem tekinthetőek rendes hibakezelésnek. Az egyértelmű megoldás, ha sosem felejtjük el a .catch blokkokat egyik Promise lánc esetében sem, és az itt keletkezett hibákat átadjuk egy központi hibakezelőnek. Viszont, csak a fejlesztői fegyelemre bízni a hibakezelési stratégiánkat nem egy életbiztosítás. Ezért erősen javasolt egy elegáns vésztervként a `process.on(‘unhandledRejection’, callback)` használata - ez bitzosítja, hogy a kezeletlen Promise kivételek is feldolgozásra kerülnek.

<br/><br/>

### Példakód: ezt a hibát nem fogja elkapni egyik hibakezelő sem (kivéve ha valahol használjuk az unhandledRejection-t)

```javascript
DAL.getUserById(1).then((johnSnow) => {
  // ez a hiba fel fog szívódni
  if(johnSnow.isAlive == false)
      throw new Error('ahhhh');
});

```

<br/><br/>

### Példakód: Feloldatlan és elutasított Promiseok elkapása

```javascript
process.on('unhandledRejection', (reason, p) => {
  // Épp elkapunk egy kezeletlen Promise elutasítást. Mivel már van egy eljárásunk a kezeletlen kivételek elkapására (ld. alul) ezért tovább dobjuk neki.
  throw reason;
});
process.on('uncaughtException', (error) => {
  // Épp elpatunk egy kezeletlen kivételt, itt az idő, hogy csináljunk vele valamit, és eldöntsük, hogy leállunk-e
  errorManagement.handler.handleError(error);
  if (!errorManagement.handler.isTrustedError(error))
    process.exit(1);
});

```

<br/><br/>

### Idézet: "Ha hibázhatsz, egyszer fogsz is"

 James Nelson blogjáról:

 > Teszteljük, hogy mennyire éred a hibakezelést. Az alábbiak közül melyik fog hibát írni a konzolra?

```javascript
Promise.resolve(‘promised value’).then(() => {
  throw new Error(‘error’);
});

Promise.reject(‘error value’).catch(() => {
  throw new Error(‘error’);
});

new Promise((resolve, reject) => {
  throw new Error(‘error’);
});
```

> Én személy szerint mindegyik esetében elvárnám, hogy a hiba kikerüljön a konzolra. A valóság ezzel szemben az, hogy számos modern JavaScript környezet nem fog hibát írni a konzolra egyik esetben sem. A probléma az emberekkel az, hogy, ha hibázhatnak, akkor egyszer fognak is. Ezt szem előtt tartva, nyilvánvaló, hogy a dolgokat úgy kell terveznünk, hogy hiba esetén a lehető legkisebb kárunk származzon belőle és ez azt jelenti, hogy hibákat kezelni kell nem pedig elfojtani.
