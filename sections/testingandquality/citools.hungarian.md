# Gondosan válasszuk ki, hogy milyen CI platformot használunk

<br/><br/>

### Rövid magyarázat

A CI világban egykor választanunk kellett a [Jenkins rugalmassága](https://jenkins.io/) és a SaaS (felhő alapú) megoldások egyszerűsége között. Manapság már más a helyzet, bizonyos SaaS szolgáltatók, mint pl. a [CircleCI](https://circleci.com/) és a [Travis](https://travis-ci.org/) kellően robosztus szolgáltatásokat nyújtanak, többek között támogatják Docker konténerek használatát minimális konfigurációval. Eközben a Jenkins is próbálja magát vonzóbba tenni azok számára, akik egyszerű megoldást keresnek. Habár a felhő alapú megoldásokkal kellően sokszínű CI megoldások építhetőek, azonban ha minden  apró részletre kiterjedő kontrollt szeretnénk, még mindig a Jenkins az egyetlen jó választás. A választás leszűkíthető arra a kérdésre, hogy milyen mélyen szeretnénk testre szabni a CI folyamatot: a felhőszolgáltatások minimális (vagy akár semennyi) beállítást igényelnek, cserébe engedik shell parancsok futtatását, docker konténerek futtatását, a folyamat testreszabását, mátrix buildek futtatását. Ha azonban teljes egészében kontrollálni szeretnénk az infrastrukúrát, vagy saját magunk szeretnénk a CI logikát programozni valamilyen nyelven (pl. Java), akkor a Jenkins marad egyetlen választásunk. Minden más esetben fontoljuk meg, hogy egyszerű, konfigurálást nem igénylő felhőszolgáltatást használunk.

<br/><br/>

### Példakód – egy tipikus felhő alapú CI konfigurációs állománya. Egy egyszerű .yml fájl, és semmi más...

```javascript
version: 2
jobs:
  build:
    docker:
      - image: circleci/node:4.8.2
      - image: mongo:3.4.4
    steps:
      - checkout
      - run:
          name: Install npm wee
          command: npm install
  test:
    docker:
      - image: circleci/node:4.8.2
      - image: mongo:3.4.4
    steps:
      - checkout
      - run:
          name: Test
          command: npm test
      - run:
          name: Generate code coverage
          command: './node_modules/.bin/nyc report --reporter=text-lcov'      
      - store_artifacts:
          path: coverage
          prefix: coverage

```

### Circle CI - szinte semmi beállítást nem igénylő, felhő alapú CI

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/circleci.png "API error handling")

### Jenkins - szifisztikált és robosztus CI

![alt text](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/jenkins_dashboard.png "API error handling")

<br/><br/>
