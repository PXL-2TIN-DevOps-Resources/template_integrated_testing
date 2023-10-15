# Assignment 6 Integrated testing

Voor deze opdracht maak je opnieuw gebruik van de VM met daarin Jenkins uit de vorige lessen.

# Integratie testen (API)
## Kennismaking API
Er werdt een eenvoudige api gebouwd op [https://devops.d-ries.be/api](https://devops.d-ries.be/api) deze moet getest worden en deze tests willen we geïntegreerd zien in een Jenkins pipeline.

Om dit te doen gaan we gebruik maken van Postman en zijn CLI variant Newman. Installeer Postman alvorens te beginnen in je virtuele machine. Postman kan je downloaden op [https://www.postman.com/downloads/?utm_source=postman-home](https://www.postman.com/downloads/?utm_source=postman-home). 

_De API is beveiligd met een simpele authentication key, deze key is 2TINDEVOPS (in hoofdletters). De key moet meegegeven worden in de header met als naam ‘key’ zoals ook terug te vinden in de Swagger documentatie op de API zelf._

*   Ga aan de slag met de documentatie van de API (deze is te vinden op de api zelf onder de subdir /api). Zorg dat jullie vertrouwd raken met de werking van de API en zijn endpoints.
*   Zorg ervoor dat ieder lid van jullie groep zichzelf ook manueel toevoegt in de API. Dit doe je dus in deze fase handmatig met de tool postman.

## Integratietesten met postman 
*   Voorzie volgende stappen in een test collection (nog steeds in de tool Postman) en sla deze op onder de naam “api-testcollection-&lt;groepsnaam>”
    *   Geef een lijst weer van alle studenten in de API.
    *   Geef de specifieke details weer van een lid van jullie groep weer.
*   Sla de test collection op en exporteer deze in JSON format.

Bij bovenstaande requests doe je via de postman testen ook de nodige controle's of de request gelukt is en of de nodige data weldegelijk aanwezig is in de response. Hoe je dit doet is gezien tijdens de les. Zie ook [https://learning.postman.com/docs/writing-scripts/intro-to-scripts/](https://learning.postman.com/docs/writing-scripts/intro-to-scripts/)

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip")
_Toon aan met screenshots & uitleg onder **punt (a)** in oplossing.md hoe je het handmatig testen van de API aangepakt hebt. Toon ook de testen die je in Postman geschreven hebt._

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip")
_Voeg de geëxporteerde JSON files van je postman test suite toe aan deze repository._

# End to end testen
Binnen onze calculator app willen we ook graag enkele automatische e2e testen voorzien. Je gebruikt hiervoor de gedeployde applicatie uit de vorige opdracht &  **playwright**. Maak in deze repository een playwright test project aan met `npx playwright install`. Gebruik playwright om 2 testen te schrijven:

*   AppHasAddButton: Deze test check of er effectief een &lt;button> element op de webpagina aanwezig is met als inhoud "add". Indien niet moet deze test falen.
*   AppCanSubtract: Deze applicatie test de functionaliteit van de Applicatie, trekt 3 van 7 af en controleert dan of de uitkomst correct op de pagina staat. Indien niet, zal deze test falen.

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip")
_Toon met screenshots de verschillende stappen in je playwright scripts aan van de verschillende testen onder **punt (b)**._

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip")
_Sla het project op en voeg de playwright file(s) toe aan deze repository._

# Pipeline

Graag zouden we de testen ook willen zien runnen in een pipeline. Bouw een nieuwe pipeline die gebruik maakt van de `Jenkinsfile` uit deze repository die volgende stages heeft:

*   `Fetch code`: Deze stapt haalt het playwright test project & de postman `.json` files uit de repository van de opdracht (indien nodig).
*   `Install dependencies`: Deze stap installeert de nodige dependencies voor de playwright testen (`npm install`).
*   `Run e2e test`: Deze stap gebruikt playwright om de e2e testen te runnen in de pipeline. Zorg voor een gegenereerd rapport (JUNIT formaat). De nodige informatie hoe je dit doet kan je terugvinden in de slides.

    _Tip 1: Denk eraan dat je de browsers eerst handmatig moet installeren en configureren (zie slide 45). Je zal ook gebruik moeten maken van de nodeJS global tool configuration._
    
*   `Run integratie test`: Deze stap voert de postman testen uit a.d.h.v. newman en genereert ook een rapport (JUNIT formaat). Gebruik hiervoor de [newman](https://www.npmjs.com/package/newman) CLI omgeving.

    _Tip: Je kan newman ook opnemen in je global configuration tool._

*   `Archive artifact`: Deze stap maakt een artifact van alle gemaakte rapporten uit de vorige stappen.

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip")
_Sla het pipeline script op in de file "Jenkinsfile"._


# Deliverable
- Screenshots & beschrijvingen in oplossing.md
- een `.json` file export van de postman testen, toegevoegd aan deze repository
    - inclusief de test cases
- een playwright project met de e2e testen, toegevoegd aan deze repository
- een opgevulde Jenkinsfile die gebruik gemaakt van Newman en playwright om de testen uit te voeren
    - Een niet werkende (=syntax errors in het pipeline script) Jenkinsfile = -30% op het eindresultaat

