# Csoportosítsd a komponenseid

<br/><br/>

### Rövid magyarázat

Közpes méretűnél nagyobb alkalmazások esetén a monolit architektúra rossz döntés - egy hatalmas alkalmazásról, amely rendszerint rengeteg függőséggel rendelkezik nehezen tudunk érvelni és rendszerint spagetti kódhoz vezet. Még a tapasztalt Achitectek - akik kellően felkészültek, és modularizálják a kódot - is rengeteg időt töltenek tervezéssel, és minden változtatásra alaposan mérlegelik, hogy az milyen hatással lesz a többi függőségre. A helyes megoldás az, ha kis szoftvereket fejlesztünk: a teljes alkalmazást daraboljuk fel kis, önmagukban is értelmes komponensekre, melyek a többi komponenstől függetlenül léteznek (pl. API, szolgáltatások , adatelérés, teszt stb.) és jól meghatározható a feladatuk. Egyesek ezt 'microservice' architektúrának is nevezik -  de fontos hogy leszögezzük, a mocrosrvicek nem egy specifikáció amit követned kell, hanem inkább  elvek gyűjteménye. A tervezőn múlik, hogy minden elvet szem előtt tart-e, vagy csak pár számára fontosat. Mindkét döntés megállja a helyét, mindaddig, amíg a szoftver komplexitását alacsonyan tartjuk. A minimum, ami elvárható, hogy a komponensek között egy finom határvonalat húzunk és minden business komponenst egy saját dedikált mappájában fejlesztünk a projektkönyvtáron belül - fontos, hogy ezeket az elkülönített komponenseket a többi komponens csak a külvilág felé nyújtot, jól definiált API-n keresztül használhatja. Ez a megközelítés alapfeltétele annak, hogy a komponenseink egyszerűek maradjanak, elkerüljük a 'dependency hell'-t és, hogy a jövőben ha alkalmazáunk tovább növekszik, könnyedén adaptáljuk a teljes microservice architektúrát.

### Idézet egy blogból: "Egy komponens felskálázása pedig magával vonja a teljes alkalmazás felskálázását"

 A MartinFowler.com blogból

> A monolit alkalmazások is lehetnek jók, de egyre több ember érez frusztrációt velük kapcsolatban - különösen mióta egyre több telepítenek a felhőbe. A valtozásperiódusok a monolit esetén összefüggenek - egy apró változás az alkalmazás egy részében a teljes alkalmazás újrafordítását és telepítését vonja magával. Idővel pedig egyre nehezebb lesz megtartani egy jól működő moduláris struktúrát, ami megnehezíti olyan módosítások véghezvitelét ami az alkalmazás egy kis részét érinti csak. Egy komponens felskálázása pedig magával vonja a teljes alkalmazás felskálázását, ahelyett, hogy csak a terheltebb komponenseket skálázzuk.

<br/><br/>

### Idézet egy blogból: "Mit árul el rólad az alkalmazásod felépítése?"

  [uncle-bob](https://8thlight.com/blog/uncle-bob/2011/09/30/Screaming-Architecture.html) blogjából
> ...ha egy könyvtár felépítését nézzük, akkor elvárjuk, hogy legyen egy nagy központi bejárat, olvasótermek, kisebb konferencia termek, és rengeteg galéria, ahol a könyvtár könyvei számára polcok találhatóak. Az épület felépítése elárulja: ez egy könyvtár.
Szóval mit árul el rólad az alkalmazásod felépítése? Mit látsz ha megnézed a főkönyvtárat és az ott található fájlokat? Elárulják, hogy éppen egy egészségügyi alkalmazást látsz, vagy egy könyvelő alkalmazást vagy esetleg egy raktárkészletezőt alkalmazást? Vagy csakt azt árulják el, hogy az alkalmazás miben iródott: Rails, vagy Spring/Hibernate, esetleg ASP?

<br/><br/>

### Jó példa: Struktúráld projekted önálló komponensekbe (angol nyelvű)

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/structurebycomponents.PNG "Struktúráld projekted önálló komponensekbe")

<br/><br/>

### Rossz példa: Csoportosítsd fájljaidat szerepük alapján (angol nyelvű)

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/structurebyroles.PNG "Csoportosítsd fájljaidat szerepük alapjén")
