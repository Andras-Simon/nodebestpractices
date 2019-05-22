# Kerüld a globális teszt adatokat, minden teszteset saját adatokkal dolgozzon  

<br/><br/>

### Rövid magyarázat

Kövessük a tesztelés aranyszabályát - a tesztesetek legyenek minél egyszerűbbek. Minden teszteset készítse el a saját teszt adatait és a teszt során csak ezeket használja. így elérhetőek a nem kívánt mellékhatások, és a teszt is könnyebben magyarázható. A valóságban ezt sajnos sokszor nem tartjuk be, gyakori eset, hogy a tesztek futtatása előtt töltjük fel az adatbázist (ún. ‘test fixture’), hogy a tesztek futását gyorsítsuk. A teszt futásideje valóban probéma lehet, azonban léteznek erre egyéb megoldások (pl. In-Memory adatbázissal, bővebben lásd a "Komponensek tesztelése" pontot) illetve a tesztek túlkomplikálása sokkal fájdalmasabb lehet, így tervezői döntéseinket ennek tudatában érdemes meghozni. Gyakorlatan arra kell figyelni, hogy minden tesztesetnek explicit létre kell hoznia az adatokat (Adatbázis rekordokat) amikre szüksége van, és a teszteset futása során csak ezeket szabad használni. Ha a teszt futásideje megkerülhetetlen tényező lesz, jó kompromisszum lehet, ha csak azokat az adatokat hozzuk létre teszteseten kívül, amiken módosítást nem végzünk a tesztek futása során (pl. adatlekérdezések).

<br/><br/>

### Példakód: minden teszteset saját adatokkal dolgozik
```javascript
it("When updating site name, get successful confirmation", async () => {
  //a teszt létrehozza az új rekordokat, és csak azokkal dolgozik
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });
  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");
  expect(updateNameResult).to.be(true);
});
```

<br/><br/>

### Példakód – Ellenpélda:  a tesztek nem függetlenek, és bizonyos, előre elkészített adatok meglétét feltételezik
```javascript
before(() => {
  // Kezdeti adatok hozzáadása az adatbázishoz. A teszt adatokat nem is látjuk, egy külső fájlban laknak
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Előre feltételezzük, hogy a "Portal" nevű oldal létezik - láttuk az adatfájlban
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Előre feltételezzük, hogy a "Portal" nevű oldal létezik - láttuk az adatfájlban
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Hiba! Az előző teszteset már megváltoztatta a nevet :(
});
```