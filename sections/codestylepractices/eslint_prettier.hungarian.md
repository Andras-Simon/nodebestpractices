# Használj ESLint-et és Prettier-t


### ESLint és Prettier összehasonlítás

Ha a lenti kódrészletet ESLinttel formázod, figyelmeztetést kapsz, hogy a sorok túl hosszúak (ez függ a `max-len` értékétől is). A Prettier automatikusan a megfelelő hosszúra tördeli a sorokat.

```javascript
foo(reallyLongArg(), omgSoManyParameters(), IShouldRefactorThis(), isThereSeriouslyAnotherOne(), noWayYouGottaBeKiddingMe());
```

```javascript
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne(),
  noWayYouGottaBeKiddingMe()
);
```

Forrás: [https://github.com/prettier/prettier-eslint/issues/101](https://github.com/prettier/prettier-eslint/issues/101)

### Az ESLint és Prettier integrálása

Az ESLint és Prettier kód formázó funkcionalitásában ugyan vannak átfedések, de könnyedén megférnek egymás mellet, ha használjuk a következő csomagok valamelyikét:
 [prettier-eslint](https://github.com/prettier/prettier-eslint), [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier), és [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier). Ha több információra van szükséged, vagy mélyebb összehasonlítást keresel, kattints [ide (angol nyelvű)](https://stackoverflow.com/questions/44690308/whats-the-difference-between-prettier-eslint-eslint-plugin-prettier-and-eslint).
