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



## Oppgave 1

1. Få pre-koden til å kjøre
2. Legg til styling



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
