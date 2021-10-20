# Codehub

### La oss bygge en chat!



## Agenda



## Lightning talk



## About FINN


## Benedicte


## Siddise



## Sanntidsteknologi

(Real-time communication)

> Når noe skal skje samtidig


## EventSource



## Del 1


### I Start prosjektet

Pass på at du har vært gjennom [pre-workshop instruksjonene](https://codehub2021.benedicte.dev/)
aller først

1. Last ned [pre-koden](https://github.com/benedicteb/simple-chat/archive/refs/heads/main.zip)
2. Åpne mappen i Visual Studio Code
3. Installer avhengigheter
   ```shell
   $ npm install
   ```
4. Start
   ```shell
   $ npm start
   ```


### II Legg til tekst

La oss sjekke at vi kan legge til ting på skjermen

```
Fil: src/App.js
```

```javascript [9]
function App() {
  return (
    <div className="App">
      <main>
        <h1>CodehubCHAT!</h1>

        <p>Du er nå klar for workshop.</p>

        <p>Dette er en ny setning.</p>
      </main>
    </div>
  );
}
```


![Dette er en ny setning](/imgs/added_sentence.png)


### III Legg til styling

Vi kan bruke CSS for å endre på utseende

```javascript
Fil: src/index.css
```

```css [9]
body {
  font-family: -apple-system, BlinkMacSystemFont,
  'Segoe UI', 'Roboto', 'Oxygen',
  'Ubuntu', 'Cantarell', 'Fira Sans',
  'Droid Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  background-color: #1b91ff;
}
```


![Endret bakgrunnsfargen](/imgs/changed_backgroundcolor.png)


## Oppgave 2

Bruk EventSource til å laste ned og vise
chat-meldinger som allerede er sendt


```js [1|3-5]
const eventStream = new EventSource('/api/v1/sse');

eventStream.addEventListener("messageReceived", function(e) {
  console.log(e.data)
})
```



## Oppgave 3

Legg til tekst-boks og knapp for å sende inn
nye meldinger



## Oppgave 4

Legg til animasjoner
