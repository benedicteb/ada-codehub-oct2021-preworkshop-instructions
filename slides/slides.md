# Codehub

### La oss bygge en chat!



## Agenda


## Lyntalen



## Om oss (og om FINN)


## Benedicte


## Siddise



## Sanntidsteknologi

(Real-time communication)

> Når noe skal skje samtidig


## EventSource



## Del 1

Vi sjekker at vi får startet prosjektet

At vi får lagt til ting på skjermen

Og at får endret på farger og styling


### 1: Start prosjektet

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


### 2: Legg til tekst

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


### 3: Legg til styling

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



## Del 2

Ting må dukke opp på skjermen når variabler oppdaterer seg

Vi jobber med **state management**


### 1: Liste for å lagre meldinger

Siden må **oppdatere seg** når vi får nye meldinger

```javascript
Fil: src/App.js
```

```javascript [2,5]
import "./App.css";
import { useState } from "react";

function App() {
  const [messages, setMessages] = useState([]);

  return (
    <div className="App">
      <main>
        <h1>CodehubCHAT!</h1>
```


### 2: Vis frem alle meldinger på skjermen

```javascript
Fil: src/App.js
```

```javascript [6-8]
  return (
    <div className="App">
      <main>
        <h1>CodehubCHAT!</h1>

        {messages.map((message) => (
          <p>{message.text}</p>
        ))}
      </main>
    </div>
  );
```


### 3: Legg til en test-melding

Vi trenger å se at den dukker opp på skjermen

```javascript
Fil: src/App.js
```

```javascript [2,7-13]
import "./App.css";
import { useEffect, useState } from "react";

function App() {
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    const testMessage = {
      text: "Hello!",
    };

    setMessages([testMessage]);
  }, []);
```


![La til en test-melding som dukker opp på skjermen](/imgs/added_test_chat.png)



## Del 3

Nå skal vi endelig ta imot ting fra internett!

Vi legger til selve lytteren

Og viser nye meldinger på skjermen etter hvert som de kommer inn


### 1: Legg til en lytter

Vi må gjøre dette i flere steg

```javascript
Fil: src/App.js
```

```javascript [1-2,8]
const SUBSCRIBE_URL =
  "https://codehub-simple-chat-api.herokuapp.com/subscribe";

function App() {
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    const eventSource = new EventSource(SUBSCRIBE_URL);
  }, []);

  return (
    <div className="App">
      <main>
        <h1>CodehubCHAT!</h1>
```


### 2: Håndter innkommende meldinger

Vi kan printe de ut til **konsollet** for å sjekke at alt virker (`Ctrl+Shift+i`)

```javascript
Fil: src/App.js
```

```javascript [4-8]
useEffect(() => {
 const eventSource = new EventSource(SUBSCRIBE_URL);

 eventSource.addEventListener("messageReceived", (event) => {
   const message = JSON.parse(event.data);

   console.log(message.text);
 });
}, []);

return (
 <div className="App">
   <main>
     <h1>CodehubCHAT!</h1>
```


![Meldinger dukker opp i konsollet](/imgs/print_incoming_to_console.png)


### 3: Vis meldingene på skjermen

Vi har allerede gjort den tunge løftingen her!

```javascript
Fil: src/App.js
```

```javascript [7-9]
useEffect(() => {
 const eventSource = new EventSource(SUBSCRIBE_URL);

 eventSource.addEventListener("messageReceived", (event) => {
   const message = JSON.parse(event.data);

   setMessages((currentMessages) =>
       [...currentMessages, message]);
   });
}, []);

return (
 <div className="App">
   <main>
     <h1>CodehubCHAT!</h1>
```


<img alt="Meldingene dukker opp etter hvert som de kommer inn" width="90%" src="/gifs/incoming_messages.gif" />
