# Rapport för kurs 1DV449 projekt 
## - FoodGen


[Länk till projektet](http://janinaeb.se/FoodGen)

(OBS: Måste logga in med facebook för att få tillgång till all funktionalitet)


### Inledning
Nästan varje dag ställs jag inför ett jobbigt beslut - vad ska jag äta idag? Därför har jag alltid önskat ha någon som kan bestämma åt mig, helst någon som vet vad jag är sugen på. Men eftersom tekniken inte gått så pass långt än, så får det duga med en applikation man kan tala om vad man tycker om och inte för.

Min applikation tar recept från [säsongsmat.nu] och visar ett slumpat för användaren. Användaren kan därefter välja att dela receptet på facebook, favorisera receptet så det sparas i en lista på användarens profil, rata receptet så det inte tas med i slumpningen igen, eller slumpa fram ett nytt recept. På användarens profil kan favoriserade och ratade recept visas och hanteras, och användaren kan även ställa in en kostinställning om denne är vegetarian, vegan eller allätare.

(Screencap med beskrivning av funktionaliteten)


### Serversida - cachning, felhantering
#### Språk
PHP, databas: MySQLi 

#### Funktionalitet och felhantering
Används för att hämta och skriva data om användare och recept till databasen. Data hämtas med ajax-anrop som JSON, eller text vid saknaden av objekt att returnera. Try/catch-satser används för att hantera fel gällande databasen.

#### Cachning
Går inte att cacha filer på serversidan, då de främst används till att generera fram recept ur en lista. Om filerna cachas hämtas samma recept hela tiden.


### Klientsida
#### Språk
HTML, CSS, Javascript. 

#### Ramverk
Bootstrap och jQuery

#### APIer
Facebook api för inloggning och delning av recept. Receptinformationen från säsongsmat skrapas från deras hemsida. De har ett api för att hämta recept, men hur jag än gjorde fick jag ändå inte ut all information jag behövde från det. Dessutom skulle jag behövt göra 2-3 förfrågningar till deras api per recept, och eftersom det finns ganska många recept tyckte jag att skrapning kändes bättre. Det var inte lätt att skrapa deras hemsida eftersom den är helt ostrukturerad, och efter mycket krångel finns det fortfarande information som inte kommer med på några recept. 

#### Cachning
Jag har satt, i .htaccess-filen, att javascript och css cachas i 30 dagar efter att filen senast blev ändrad. Bilder är satta till 90 dagar. HTML och text bör inte cachas då HTML-sidan ändras dynamiskt hela tiden, speciellt när man genererar recept. En text-fil används för att lagra senaste datum recept-databasen uppdaterades, så därför kan inte den cachas då den ändras varje dag någon besöker hemsidan.

#### Felhantering
Fel från serversidan hanteras via strängar, vilket skapar många strängberoenden som inte är speciellt bra men som fungerar i applikationen som den ser ut nu. Efter ett serveranrop kontrolleras utdatan om den är fel, och annars tas den omhand som ett objekt som är förväntat av applikationen. Generella fel- och rättmeddelanden visas efter utförd funktion via bootstraps alert-rutor.


### Egen reflektion
Jag har haft väldigt mycket problem med att få ut information om recepten. De första veckorna i projektet spenderades i maildiskussion med skaparen för att få reda på hur man använder deras api för att få ut recept. Till slut bestämde jag mig för att strunta i apiet och skrapa deras receptsidor istället, och efter det har nästan allt flytit på. 


Jag har även haft problem med text-formatet vid skrapning av information, då det på vissa recept funnits konstiga tecken, vilket John hjälpte mig med på handledningen.


Jag skulle ha velat hunnit klart tidigare än jag gjort, för då skulle jag ha gett mig på att lägga in funktionalitet för att lägga till egna recept till säsongsmat från min applikation. Det är något jag skulle tänka mig lägga till i framtiden.


### Risker med applikationen
Att alla recept inte är fullständiga. Om man hittar ett recept man verkligen vill göra sen finns knappa instruktioner. Användare skulle antingen bli besvikna på min applikation, eller lämna den och gå till originalsidan istället.


En risk är om säsongsmat skulle ändra strukturen på deras receptsidor. I så fall skulle kanske min skrapningsfunktionalitet inte fungera som planerat och receptinformationen kan blir helt fel.


Jag valde att använda säsongsmat för recept-hämtning från första början eftersom de delar med sig av all information och släpper den fritt, vilket är riktigt bra. Etiskt finns ingen risk med att använda deras data.
