# Figyeld a az alkalmazás hibáit és a leállásokat APM megoldásokkal


### Rövid magyarázat

Exception != Error. A tradícionális hibakezelés feltételezi a kivételek (Excpetion) jelenlétét, de az alkalmazás hibái még számos különboző formát ölthetnek: lassú kód, API leállás, számítási kapacitás hiánya stb... Ez az a pont ahol jól jöhetnek az APM (Application Performance Management) megoldások, melyek lehetővé teszik a nehezen fellelhető problémák megtalálását minimális erőfeszítéssel. Többek között képesek figyelmeztetni ha a HTTP API hibával tér vissza, felfedezik ha az API válaszidő átlép egy határértéket, felfedezik az ún. 'code smell'-eket, monitorozzák az erőforrások kihasználtságát és egy összesített dashboardot nyújtanak a fontos üzleti metrikák egyszerű áttekintéséhez. A legtöbb ilyen szolgálatás alap verziója ingyen is ingénybe vehető.

### A Wikipedia bejegyzése az APM-ről 

Az információs technológiában és a rendszerfelügyeletben az APM (Application Performance Management) a szoftver termékek műküdésének és teljesítményének menedzselését és monitorozását jelenti. Az APM detektálja és diagnosztizálja a komplex alkalmazások teljesítményproblémáit, hogy a megfelelő szintű rendelkezésreállás biztosítható legyen. Az APM a "IT metrikiák üzleti értelemmel való felruházása (pl. értékek)".

### Az APM piac áttekintése

A különböző APM megoldások 3 nagy ágra bonthatóak:

1. Weboldal és API monitorozás - külső szolgáltatások, amelyek rendszeresen monitorozzák a rendszer elérhetőségét és válaszidejét HTTP kérésekkel. Akár pár perc alatt is beállítható egy ilyen rendszer. Pár szolgáltató: [Pingdom](https://www.pingdom.com/), [Uptime Robot](https://uptimerobot.com/) és [New Relic](https://newrelic.com/application-monitoring)

2. Code instrumentáció - az apm egy olyan ága, ami egy ágens beágyazását követeli meg és képes detektálni többek között a lassú végrehajtási útvonalakat, statisztikát vezetni a keletkező kivételekről és telejesítménymérésre. Pár szolgáltató: New Relic, App Dynamics.

3. Üzleti intelligencia felület - ezek a termékek arra fókuszálnak, hogy az üzemeltető csapatot ellássák a megfelelő metrikákkal és válogatott tartalmakkal, melyek segítenek az alkalmazások teljesítményének könnyű áttekintésében. Ez általában magában foglalja különböző információk aggregálását (alkalmazás logok, adatbázis logok, szerver logok stb.) és felület előzetes beállítását. Pár szolgáltató: [Datadog](https://www.datadoghq.com/), [Splunk](https://www.splunk.com/), [Zabbix](https://www.zabbix.com/)

 ### Példa UpTimeRobot.Com – Weboldal monitorozás
![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/uptimerobot.jpg "Weboldal monitorozás")

 ### Példa: AppDynamics.Com – teljeskörű monitorozás instrumentációval kombinálva
![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/app-dynamics-dashboard.png "teljeskörű monitorozás instrumentációval kombinálva")
