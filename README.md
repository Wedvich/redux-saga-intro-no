Dette repoet inneholder eksempelkode og en presentasjon av [Redux-Saga](https://github.com/redux-saga/redux-saga) for de som ikke har vært borti det før.

# Introduksjon til Redux-Saga
**redux-saga** er et bibliotek som brukes sammen med **redux** for å håndtere sideeffekter. Det finnes flere andre alternativer, blant annet **redux-thunk**, **redux-promise** og **redux-observable**, men **redux-saga** løser det på sin egen måte. Det er definitivt tyngre å sette seg inn i enn f.eks. **redux-thunk**, men til gjengjeld har man mulighet til å uttrykke langt mer sofistikert logikk og synkronisering på tvers av prosesser som ellers vil kreve mye manuell kode.

## Hva er problemet med thunks?
I vanlig Redux har man ett immutable state-tre, som produseres av _reducers_. En reducer tar den eksisterende staten og kombinerer den med et _action_ som beskriver endringene som skal utføres, og produserer en ny state. Reducers i Redux skal være _pure_ (altså uten sideeffekter), slik at gitt samme input (state + action) vil en reducer alltid produsere samme output (ny state). Dette er det som gir Redux kraftig funksjonalitet som å reise frem og tilbake i tid ved å rulle actions tilbake/frem igjen.

Men sideeffekter er nøvdendige for de fleste applikasjoner for å gjøre ting som å lese data fra serveren eller skrive til local storage, så da må vi ha et annet sted å innkapsle denne logikken. Thunks er en vanlig måte å gjøre dette på. I stedet for å sende et action til Redux, sender man en asynkron funksjon som _produserer_ actions i stedet. Redux middleware som **redux-thunk** plukker ut disse action'ene og kjører funksjonen i stedet for å sende dem videre til reducerne.

Her er et eksempel på en vanlig måte å hente data fra et API med thunks:
```ts
const loadProducts = async () => {
  dispatch(actions.loadProductsRequest());
  try {
    const response = await fetch(productsUrl);
    dispatch(actions.loadProductsSuccess(await response.json()));
  } catch (error) {
    dispatch(actions.loadProductsFailure(error));
  }
}

```
Man dispatcher kun ett kall til `loadProducts()`, og så er selve logikken innkapslet i funksjonen. Det er en fin best practice å skille forretningslogikken fra koden som kaller på den.

For enkel logikk som eksempelet over fungerer det helt topp med thunks. Men det er spesielt to situasjoner som skaper problemer.

### Thunks kan ikke avbrytes
...

### Thunks kan ikke snakke med andre thunks
...

## Hvordan løser man det med sagas?
...
