# Csomagold a gyakran használt segédeszközöket npm csomagokba

<br/><br/>

### Rövid magyarázat

Amint az alkalmazásod növekedni kezd és lesznek különböző komponensei különböző szervereken amik hasonló segédfüggvényeket használnak, el kell kezdened menedzselni a függőségeid - hogyan tudsz egyetlen példányt karbantartani a segédfüggvény kódjából amit az azt használó komponensek használni és telepíteni tudják? Nos, erre van megoldás, melyet NPM-nek hívnak... Kezdetnek burkold a 3. féltől származó segédeszközöket saját burkoló függvényeid mögé (hogy később könnyen cserélhető legyen) és a saját kódoból készíts egy privát NPM csomagot. Innentől, a teljes kódbázisod importálni tudja ezt a csomagot, és ki tudja használni az NPM adottságait. Lehetséges NPM csomagot saját privát használatra készíteni, anélkül, hogy bárki mással megosztanánk: [privát modulok](https://docs.npmjs.com/private-modules/intro), [privát registry](https://npme.npmjs.com/docs/tutorials/npm-enterprise-with-nexus.html) or [lokális npm csomagok](https://medium.com/@arnaudrinquin/build-modular-application-with-npm-local-modules-dfc5ff047bcc)

<br/><br/>

### Gyakran használt saját segédeszközök megosztása különböző futtatási környezetek és komponensek között

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/Privatenpm.png "A projekt komponensekre bontása")
