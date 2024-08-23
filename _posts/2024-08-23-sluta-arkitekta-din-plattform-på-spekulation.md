# Sluta arkitekta din plattform på spekulation – Härled den från klienterna

Ibland finns det behov av en mjukvaruplattform. Lockelserna med en plattform kan vara stora och ibland kan en plattform vara motiverad, till exempel när den skulle skapa stora produktivitetsfördelar för team som ska utveckla klienter eller applikationer på plattformen, eller när alla klienter ska ha en liknande användarupplevelse.

Vår intuition som systemutvecklare och systemarkitekter säger oss att vi ska utveckla plattformen först, baserat på förväntade behov från klienter och applikationer. Det känns naturligt att lägga svårlösta och gemensamma funktioner på ett ställe där de sedan kan användas av flera olika klienter för att på så sätt spara utvecklingstid och underhållskostnader. Det brukar gå till så här: Vi identifierar de framtida kraven. Därefter utformar vi en plattform som klarar detta samt tar viss höjd för framtida behov. När en första version av plattformen är på plats kan klienter och applikationer börja använda den. Något annat arbetssätt vore oansvarigt och skulle troligen skapa dålig design och spagettikod.

Vi på Adaptiv menar att det här är feltänkt. Det här är ett av många exempel från mjukvaruvärlden när den intuitiva sanningen leder oss vilse.
Vi vill snarare argumentera för att en väl fungerande plattform måste definieras utifrån klienternas _verkliga_ behov. Men de behoven är inte tillräckligt kända förrän klientutvecklingen är i full gång! Vi måste därför låta klienternas kontinuerliga behov, som vi upptäcker under arbetet, få ett större inflytande på utformningen av plattformen.

> En mjukvaruplattform ska utformas genom refaktorisering.

Ett annat sätt att uttrycka den här ointuitiva lärdomen är att en mjukvaruplattform ska utformas genom refaktorisering. Så här går det till:

1. Den första klienten och backendtjänster utvecklas utan en tanke på plattform och återanvändning. Men… designen måste vara någorlunda väl genomtänkt och vältestad.
2. Den andra klienten och backendtjänster utvecklas. När vi ser att en liknande bastjänst behövs, extraherar vi och generaliserar den till en gemensam tjänst som båda klienterna använder. En hyfsad design och bra automatiserade tester skapar tillräcklig trygghet för att våga ändra designen.
3. När den tredje klienten och dess backendtjänster utvecklas gör vi på samma sätt. Flera gemensamma bastjänster identifieras och skapas. Vi börjar se en början på en plattform.
4. Detta sätt att arbeta fortsätter för varje ny typ av klient. Plattformen växer fram gradvis, precis efter de behov som finns.

Det finns uppenbara fördelar med detta sätt att utveckla en plattform:

- Plattformen utformas inte på spekulation utan erbjuder precis det som klienterna behöver. Det finns ingen överproduktion av kod eller överdesignad, svårbegriplig arkitektur.
- Klientutveckling behöver inte vänta på kravstudie, arkitektur och utveckling av en plattform. Här kan man ibland spara många månader eller till och med år.
- Klientutveckling får fria händer att utveckla det som de behöver, utan att behöva tänka på återanvändning och generalisering, vilket är betydligt snabbare. Om något saknas i plattformen kan de utveckla det själva, alternativt i samarbete med plattformsteamet, för inkludering i nästa version av plattformen.
- Vi kan när som helst trappa ner utvecklingen av plattformen med full realisering av värdet hittills.

Så nästa gång du ser behov av en mjukvaruplattform, jobba i små steg, med kvalitet, och härled plattformen från klienterna.

_av Joakim Manding Holm (Adaptiv, 2024)_
