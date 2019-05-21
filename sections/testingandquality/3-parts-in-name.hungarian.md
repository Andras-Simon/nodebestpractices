# Minden teszt elnevezés 3 részből álljon

<br/><br/>

### Rövid magyarázat

Egy teszt eredménynek elég beszédesnek kell lennie ahhoz, hogy - a kódot nem feltétlenül ismerő - személyek (pl. DevOps, tester) is könnyedén értsék, hogy az alkalmazás megfelel-e a támasztott követelményeknek. Ez legkönnyebben úgy érhető el, hogy a tesztesetek jól definiáltak, és tartalmazzák a következőket:

(1) Mit tesztelünk? Pl.: ProductsService.addNewProduct metódus

(2) Milyen körülményeket vagy eseteket vizsgálunk? Pl.: "a metódust a price attribútum nélkül hívták meg"

(3) Mi az elvárt eredmény? Pl.: az új terméket nem fogadjuk el

<br/><br/>

### Példakód: 3 részes teszt elnevezés
```javascript
//1. mit tesztelünk?
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. körülmények 3. elvárt eredmény
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});
```

<br/><br/>

### Példakód: Ellenpélda - a teljes teszt kódját el kell olvasnunk, hogy megértsük milyen estre tesztelünk
```javascript
describe('Products Service', function() {
  describe('Add new product', function() {
    it('Should return the right status', ()=> {
        //hmm, vajon mit vizsgál a teszt? 
        //Mi volt a bemenet és mit várunk kimenetként?
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});
```

<br/><br/>

### "Így csináld jól: A teszt report hasonlítson a követelményleírásra"

 [Angol példák: "30 Node.js testing best practices"  Yoni Goldbergtől](https://medium.com/@me_37286/yoni-goldberg-javascript-nodejs-testing-best-practices-2b98924c9347)

 ![Teszt report példa](https://github.com/i0natan/nodebestpractices/blob/master/assets/images/test-report-like-requirements.jpeg "Teszt report példa")

<br/><br/>