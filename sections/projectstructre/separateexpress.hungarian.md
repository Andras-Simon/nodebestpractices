# Válaszd szét az Express 'app' és 'server' objektumait

<br/><br/>

### Rövid magyarázat

A legutóbbi Express generátor bevezet egy új gyakorlatot, amit érdemes a továbbiakban is tartani - az API deklaráció külön van választva a hálózatspecifikus beállításoktól (port, protokoll stb). Ez lehetővé teszi, hogy az API-t processzen belül teszteljük, nem szükséges hálózati hívásokat intézni. Ennek eredményeként a tesztelési folyamat felgyorsul és a kódról is egyszerűbb coverage metrikákat gyűjteni. Ez azt is lehetővé teszi, hogy ugyanazt az API-t könnyedén használjuk más hálózati környezetben. Bónusz: tisztább kód és a szerepek jobb elkülönülése.

<br/><br/>

### Példakód: Az API deklaráció az app.js-be tartozik

```javascript
var app = express();
app.use(bodyParser.json());
app.use("/api/events", events.API);
app.use("/api/forms", forms);
```

<br/><br/>

### Példakód: A szerver hálózati beállításai a /bin/www-be tartoznak

```javascript
var app = require('../app');
var http = require('http');

/**
 * Port kiolvasása a környzeti változóból, és eltárolása Express-ben.
 */

var port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * HTTP szerver létrehozás
 */

var server = http.createServer(app);
```

### Példa: teszteld az API-t folyamaton belül supertesttel (népszerű teszt rendszer)

```javascript
const app = express();

app.get('/user', function(req, res) {
  res.status(200).json({ name: 'tobi' });
});

request(app)
  .get('/user')
  .expect('Content-Type', /json/)
  .expect('Content-Length', '15')
  .expect(200)
  .end(function(err, res) {
    if (err) throw err;
  });
````
