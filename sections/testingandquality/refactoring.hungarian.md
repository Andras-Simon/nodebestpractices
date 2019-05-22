# Refaktorálás

<br/><br/>

### Rövid magyarázat

A refaktorálás egy fontos lépése az interatív fejlszetési folyamatnak. Az ún. "Code Smell"-ek (szagos kód - rossz programozási gyakorlatok, mint pl. a kódduplikcáió, tól hosszú metódusok, túl sok paraméter) eltávolítása javítani fogja a kóf minőségét és könnyen karbantartható kódot eredményez. Bizonyos statikus analízis eszközök segítenek megtalálni ezeket a "Code Smell"-eket, és segítségükkel a refaktorálás is egy folyamat részévé tehető. Ha ezeket az eszközöket a CI build egy lépéseként alkalmazzuk, automatizálhatjuk a minőségellenőrzés folyamatát. Ha a CI megoldásunk integrálható olyan eszközökkel, mint pl. a Sonar vagy a Code Climate, a build folyamat megszakítható ha a forráskódban "Code Smell" található, és egyúttal a kód szerzője tanácsokat is kap arra, hogy miként javítsa a hiányosságot. Ezek a statikus ellenörző eszközök jól kiegészítik az automatikus formázó eszközöket pl. az ESlint-et. Amíg ezek a formázó eszközök a kódolás formázását ellnőrzik, mint pl. helyes indentáció és a pontosvesszők megléte (habár néhány "Code Smell" így is megtalálható, pl. a túl hosszú metódusok) addig a statikus kód analízis akár komplex (duplikált kód, komplexitás analízis) és több forrásfájlon átívelő "Code Smell"-t is megtalál.

<br/><br/>


### Martin Fowler - Vezető Kutató a ThoughtWorksnél

 Idézet a "Refactoring - Improving the Design of Existing Code" című könyvből (saját frodítás)

 > A refaktorálás egy kontrollált technika a meglévő kódbázisunk modelljének javítására.

<br/><br/>

### Evan Burchard - Webfejlsztés Tanácsadó és Író

 Idézet a "Refactoring JavaScript: Turning Bad Code into Good Code" című könyből (saját frodítás)

 > Mindegy, hogy milyen keretrendszert vagy "JS-re-fordított" nyelvet használsz, hibák és teljesítménybeli problémák mindig előfordulnak, ha a mögöttes JavaScript kód minősége nem megfelelő.

<br/><br/>

 ### Példa (angol): Komplex metódusok elemzése CodeClimate segítségével (kereskedelmi szoftver)

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/codeanalysis-climate-complex-methods.PNG " Komplex metódusok elemzése")

### Példa (angol): Kód analízis trendek és előzmények CodeClimateben (kereskedelmi szoftver)

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/codeanalysis-climate-history.PNG "Kód analízis trendek és előzmények")

### Példa (angol): Kód analízis összesítés és trendek SonarQube-ban (kereskedelmi szoftver)

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/codeanalysis-sonarqube-dashboard.PNG "Kód analízis összesítés és trendek")


<br/><br/>
