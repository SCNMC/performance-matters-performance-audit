> _Fork_ deze leertaak en ga aan de slag. Onderstaande outline ga je gedurende deze taak in jouw eigen GitHub omgeving uitwerken. De instructie vind je in: [docs/INSTRUCTIONS.md](docs/INSTRUCTIONS.md)

## 🔬 Performance audit onderzoek 25-4-22

Voor deze opdracht heb ik een performance audit gedaan op de site van [Pathe!](https://www.pathe.nl/). Ik heb een performance audit gedaan om te kijken welke verbeteringen gedaan kunnen worden op deze website. Mijn bevindingen heb ik gedocumenteerd in deze wiki.

### Resultaat performance audit:
<img width="700" alt="Schermafbeelding 2022-04-25 om 12 21 35" src="https://user-images.githubusercontent.com/90189750/165070788-d703ab13-a2bf-4166-b227-29878b90d20e.png">

Uit de performance audit is gekomen dat website van pathe op de volgende punten laag gescoord heeft:

- FCP (First Contentful Paint)
- SI ( Speed index)
- LCP (Largest Contentful Paint)

Punten waar de site wel goed op scoort:



- TTI (Time to Interactive)
- TBT (Total Blocking Time)
- CLS (Cumulative Layout Shift)

## Verbeteringen

### FCP

<img width="186" alt="Schermafbeelding 2022-04-26 om 21 37 06" src="https://user-images.githubusercontent.com/90189750/165378745-f9c2e268-b789-4d71-a656-1d956f09117a.png">

FCP meet hoe lang het duurt voor de browser om het eerste deel van de DOM content te renderen nadat een een gebruiker navigeert naar jou pagina. Images, non-white `<canvas>` elements, and SVGs worden gezien als DOM content. Met een tijd van 1.9 sec kan dit vele malen sneller. 
De volgende dingen kunnen gedaan worden om dit te verbeten:
- Reduce unused CSS 

  Verminder ongebruikte CSS om bytes te verminderen die worden consumed bij de network activity.

- Eliminate render-blocking resources
  
  Bepaalde resources blokkeren de first paint van deze pagina. Het gaat om een paar CSS bestanden en JS bestanden. Wanneer je de critical code heb geïdentificeerd kan je de code van de render blokkende url verplaatsen naar een inline script tag in de HTML pagina. Non critical code kan in de URL blijven maar het is handig om de url met een `defer` of `async` te marken.

### SI

<img width="186" alt="Schermafbeelding 2022-04-26 om 22 30 58" src="https://user-images.githubusercontent.com/90189750/165386999-87b12969-6f86-4154-b925-93b3e70a083b.png">


SI oftewel speed index meet hoe snel de content visueel zichtbaar is tijdens de page loading. De speed index word gemeten met de volgende info:

Speed Index
(in seconds)	Color-coding

0–3.4	Green (fast)

3.4–5.8	Orange (moderate)

Over 5.8	Red (slow)

Met een oranje kleur is de content niet snel maar ook niet langzaam zichtbaar. Om ervoor te zorgen dat de speed index een groene kleur krijgt is het belangrijk dat ongebruikte CSS verwijderd word om bytes te verminderen die worden consumed bij de network activity.

### LCP
 
<img width="191" alt="Schermafbeelding 2022-04-26 om 22 48 26" src="https://user-images.githubusercontent.com/90189750/165389659-70659c02-6eaf-467f-b83f-b3b6f17a8557.png">

Largest Contentful Paint marks the time at which the largest text or image is painted. Larges Contentful Paint meet de tijd wanneer de grootste text of image zichtbaar is. Met een score van 4.4s is dit aan de lage kant en kan hier veel verbeterd op worden. Het volgende kan gedaan worden:

- Reduce unused CSS 

  Verminder ongebruikte CSS om bytes te verminderen die worden consumed bij de network activity. Hierdoor kan er wel 0.32 s bespaard worden. Deze oplossing geldt ook voor de FCP.

- Eliminate render-blocking resources
  
  Net zoals bij de LCP is het belangrijk om render blocking resources te elimineren. Door dit te doen kan er wel 1.94 s bespaard worden. 
 
- Ensure text remains visible during webfont load

  Fonts zijn over het algemeen grote bestanden waarbij het een tijdje kan duren voordat deze ingeladen zijn. Sommige browsers verbergen de 
 tekst totdat de font is ingeladen waardoor er een FOIT (flash of invisible text) ontstaat. 
 Een manier om dit op te lossen is om tijdelijk een system font te weergeven. Door font-display: swap te includeren in de @font-face style kan 
 dit voorkomen worden in de meeste moderne browsers. Hierdoor word een system font eerst in geladen, wanneer de custom font geladen is zal 
 deze de system font vervangen. 

  Een andere manier is door een preload te gebruiken op fonts. Door `<link rel="preload" as="font"> ` gebruiken zullen de font files eerder 
 gefetcht worden.

  Door dit aan te passen bespaar je 200 ms. 



## Bronnen

## Licentie

![GNU GPL V3](https://www.gnu.org/graphics/gplv3-127x51.png)

This work is licensed under [GNU GPLv3](./LICENSE).
