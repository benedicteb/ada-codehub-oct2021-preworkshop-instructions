# Codehub

### La oss bygge en chat!

```
https://codehub2021.benedicte.dev/slides
```

Nyttig å ha den åpen i en fane!

![QR kode som tar deg til slidene](/imgs/codehub_slides_qrcode.png)


<img src="/imgs/codehub_slides_qrcode.png" alt="QR kode som tar deg til slidene" width="70%" />



## Agenda

| ~ kl.    |                               |
|:-------------|:------------------------------|
| 16:30        | Introduksjon                  |
| 16:45        | Koding (alene eller i gruppe) |
| 17:45        | Lyntale (Zoom, Engelsk)       |
| 18:00        | Fortsette koding              |
| 18:45        | Oppsummering                  |

De som vil kan da vise frem det de har laget under oppsummeringen


![Demo av chatten vi skal bygge, to nettleservinduer som snakker med hverandre i en Messenger-lignende app](/gifs/working_chat_demo.gif)


## Lyntalen

> How we apply machine learning and data science to solve different problems at Schibsted

By Maria ([Zoom-link](https://NTNU.zoom.us/j/98421983257?pwd=UkQ1OVBMZEtWOUJrd1k0RjZrYlk1Zz09))



### Benedicte [@benedebr](https://twitter.com/benedebr)

<div style="display: flex; flex-direction: row; justify-content: flex-start; align-items: center">
   <img src="/imgs/benedicte_schibsted.jpg" alt="Benedicte står ved pulten sin på FINN-kontoret, fargerikt tastatur og en enhjørning som håndleddsstøtte" width="400px" />

   <ul style="margin-left: 80px;">
      <li>Utvikler, jobber med betalingsløsninger i FINN</li>
      <li>
         <p>Dataspill og tastaturbygging på fritiden</p>
         <img src="/imgs/building_keyboard.jpg" alt="Et halvferdig tastatur" width="200px" />
      </li>
      <li>Synger i kor</li>
   </ul>
</div>


### Siddise

  <ul style="margin-left: 80px;">
      <li>Utvikler, jobber med eiendomsannonser og bedriftsenter for eiendomsmeglere som bruker FINN</li>
      <li>Frivillig arbeid</li>
      <li>Bøker, film og musikk</li>
   </ul>


### Hvordan er det å jobbe i FINN?


![Bilde av plakatan fra FINN sin kampanje flytte fra gutterommet](/imgs/flytte_fra_gutterommet.jpeg)


![Skjermbilde fra Slack hvor kanalen er proppet full av feirende animerte gif memes av alle slag](/gifs/boom.gif)


![PuseFINN i regnponcho](/imgs/PuseFINN_regnoncho.jpg)


![Skjermbilde av nettsiden hvordan det er å jobbe i FINN](/imgs/working_in_finn.png)


![Skjermbilde av summer boost innlegget på jobb i FINN nettsidene](/imgs/alpaca_in_finn.png)


<!-- Empty slide for black screen -->
<!-- .slide: data-background="black" -->



## Sanntidsteknologi

(Real-time communication)

> Når noe skal skje **med en gang**


<img src="/imgs/messenger_screen.jpg" height="700px" alt="Skjermbilde fra en tilfeldig Facebook Messenger-app hvor meldingene er blurret ut" />
<!-- Image shamelessly stolen from: https://www.androidauthority.com/facebook-messenger-unsend-launch-925160/ -->


![En mobil spør en server om den har nye meldinger, serveren har ingen](/imgs/ingen_nye_meldinger.png)


![En mobil spør en server mange ganger om den har nye meldinger, til slutt får den ja](/imgs/ny_melding_til_slutt.png)


![En mobil abonnerer på meldinger fra en server ved å snakke til den](/imgs/abonner_meldinger.png)


## Server Sent Events

aka. SSE eller EventStream

* **En**-veiskommunikasjon
* Nettleseren har veldig god innebygget støtte via `EventSource`
* Bak kulissene veldig **enkel** og robust


## WebSockets

* Ligner veldig på SSE men har flere funksjoner
* Bak kulissene veldig avansert
* Lar **klienten** (brukeren, den som kobler seg til) sende data tilbake over samme kanal


![Animert gif som viser folk samarbeid om et Q4 report dokument i Google Docs Writer](/gifs/google-docs-live-edits.gif)
<!-- Image shamlessly stolen from: https://9to5google.com/2019/08/20/google-docs-live-edits/ -->



## La oss kode litt!



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
  "https://codehub-simple-chat-api.herokuapp.com/subscribe/1";

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
```


<img alt="Meldingene dukker opp etter hvert som de kommer inn" width="90%" src="/gifs/incoming_messages.gif" />



## Del 4

Men! Vi må da kunne sende meldinger også!

Vi legger til et **input-felt** for tekst og en
**knapp** for å sende melding


### 1: Legg til input-felt og knapp

```javascript
Fil: src/App.js
```

```javascript [8-11]
<main>
  <h1>CodehubCHAT!</h1>

  {messages.map((message) => (
    <p>{message.text}</p>
  ))}

  <form>
    <input type="text" id="chat-input-field" />
    <button type="submit">Send</button>
  </form>
</main>
```


![Lagt til input-felt og knapp](/imgs/added_form.png)


### 2: Håndter klikk

Når vi trykker på knappen må vi få tak i teksten som er skrevet inn

Vi kan skrive den til **konsollet** for å teste

```javascript
Fil: src/App.js
```

```javascript [3-11]
 <button
   type="submit"
   onClick={(event) => {
     event.preventDefault();

     const textInputField =
       document.getElementById("chat-input-field");
     const inputtedMessage = textInputField.value;

     console.log(inputtedMessage);
   }}
 >
```


![Teksten vises i konsollet når vi klikker på knappen](/imgs/add_click_handler.png)


### 3: Legg til URL

Akkurat som med subscribe-url'en så trenger vi
en egen url for å sende meldinger

```javascript
Fil: src/App.js
```

```javascript [3-4]
const SUBSCRIBE_URL =
  "https://codehub-simple-chat-api.herokuapp.com/subscribe/1";
const SEND_MESSAGE_URL =
  "https://codehub-simple-chat-api.herokuapp.com/sendMessage";
```


### 4: Send inn meldingen

Nå er vi klare for å sende inn!

**Pass på å fylle inn kallenavnet ditt**

```javascript
Fil: src/App.js
```

```javascript []
  const inputtedMessage = textInputField.value;

  fetch(SEND_MESSAGE_URL, {
    method: "POST",
    headers: {
      Authorization: "duerkul",
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      message: inputtedMessage,
      nick: "NAVNET DITT HER",
    }),
  });
```


![Meldingene blir sendt, og vi får de tilbake](/imgs/messages_are_sent.png)


### 5: Tøm tekstfeltet når meldingen er sendt

Ellers er det ikke så lett å vite at meldingen er sendt

```javascript
Fil: src/App.js
```

```javascript [13]
  fetch(SEND_MESSAGE_URL, {
    method: "POST",
    headers: {
      Authorization: "duerkul",
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      message: inputtedMessage,
      nick: "Your name",
    }),
  });

  textInputField.value = "";
```



## Del 5

La oss få det til å se litt kult ut!


### 1: Legg til styling på meldingene

```javascript
Fil: src/App.js
```

```javascript [3-4]
import "./App.css";
import { useEffect, useState } from "react";
import Chat from "./components/Chat";
import ChatMessage from "./components/ChatMessage";
```

```javascript []
<Chat>
 {messages.map((message) => {
   return (
     <ChatMessage
         avatarSrc={message.avatarUrl}
         name={message.sender}>
       {message.text}
     </ChatMessage>
   );
 })}
</Chat>
```


![Meldinger ser mye kulere ut med styling](/imgs/added_chat_styling.png)


### 2: Lag variabel for navnet ditt

Vi må gjenbruke navnet vårt, derfor er det fint å ha det i en variabel

```javascript
Fil: src/App.js
```

```javascript [6]
const SUBSCRIBE_URL =
  "https://codehub-simple-chat-api.herokuapp.com/subscribe/1";
const SEND_MESSAGE_URL =
  "https://codehub-simple-chat-api.herokuapp.com/sendMessage";

const NICK = "Benedicte";
```


### 2: Lag variabel for navnet ditt

```javascript
Fil: src/App.js
```

```javascript [9]
fetch(SEND_MESSAGE_URL, {
   method: "POST",
   headers: {
      Authorization: "duerkul",
      "Content-Type": "application/json",
   },
   body: JSON.stringify({
      message: inputtedMessage,
      nick: NICK,
   }),
});
```


### 3: Skil på dine egne meldinger

Nå kan vi bruke avsender/navnet på meldingen til å vite hva vi har sendt

```javascript
Fil: src/App.js
```

```javascript [5]
import "./App.css";
import { useEffect, useState } from "react";
import Chat from "./components/Chat";
import ChatMessage from "./components/ChatMessage";
import ChatMessageReply from "./components/ChatMessageReply";
```


### 3: Skil på dine egne meldinger

```javascript
Fil: src/App.js
```

```javascript [3-12]
<Chat>
 {messages.map((message) => {
   if (message.sender === NICK) {
     return (
       <ChatMessageReply
         avatarSrc={message.avatarUrl}
         name={message.sender}
       >
         {message.text}
       </ChatMessageReply>
     );
   }

   return (
```


![Nå ser meldingene fra deg selv annerledes ut enn fra de andre!](/imgs/added_blue_messages.png)


### 4: Legg på styling for input-feltet

> No har me juksa litt ...

Legg på to **CSS**-klasser jeg har laget for å få input-feltet og send-knappen til å se
litt kulere ut.

Du kan justere på disse selv i `src/App.css`


### 4: Legg på styling for input-feltet

```javascript
Fil: src/App.js
```

```javascript [1]
<main className="HeightAdjusted">
     <h1>CodehubCHAT!</h1>
```

```javascript [1]
<form className={"InputForm"}>
  <input type="text" id="chat-input-field" />
  <button
```


### 5: Chat-vinduet må scrolle av seg selv

Hvis ikke så ser vi ikke nye meldinger hvis de dukker opp utenfor skjermen

Merk at `[messages]` gjør at koden blir kjørt når `messages` endrer seg

```javascript
Fil: src/App.js
```

```javascript []
useEffect(() => {
 const chatlogRoot = document.getElementById("chatlog-root");

 chatlogRoot.scrollTo(0, chatlogRoot.scrollHeight);
}, [messages]);
```



## Utfordring 1

Legg til ditt eget profil-bilde. For at ikke bare du selv skal se det trenger du en `http`-lenke

#### Eksempel

1. Gå på Github-profilen din
2. Høyreklikk på profilbildet ditt og klikk "Kopier bildeadresse"


### Hint

`body`-argumentet der vi kaller `fetch` kan ha flere parametre

Ser du et relevant parameter vi bruker et annet sted?



## Utfordring 2

La brukeren skrive inn navnet sitt når de først åpner appen

Slik at de ikke må inn i koden for å endre det


### Hint 1

Du trenger en `useState` og `useEffect` til


### Hint 2

Du må bruke `if` og `return` for å returnere noe annet hvis brukernavnet ikke er satt


### Hint 3

Hvis du har fulgt hintene over så kan du kopiere mye av `<form>`



## Hva har vi lært?


* Sanntidsteknologi betyr at noe skjer **med en gang**
* Strategier for sanntids-kommunikasjon:
  * `Polling`
  * `Long-Polling`
  * `EventStream`/`SSE`
  * `Websockets`
  * (det finnes flere)
* I FINN/Schibsted får du jobbet med dette og **mer**
