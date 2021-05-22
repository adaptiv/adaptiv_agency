---
layout: post
title:  "Klimatavtrycket av din egenutvecklade molntjänst"
author: Måns Sandström & Johan Dewe
---

<img class="img-responsive" src="/assets/images/trees-for-compensation.png" alt="Illustration av antal fullstora träd som behövs för att kompensera för nuvarande CPU-energiförbrukning" title="44 fullstora träd behövs för att kompensera nuvarande CPU-energiförbrukning">

Vi på Adaptiv har nyligen beräknat [vårt eget klimatavtryck](https://adaptiv.se/2021/05/21/klimatrapporter-publicerade/). Man kan summera det med att avtrycket är ringa och att våra ansträngningar att sänka det ytterligare troligen inte är det viktigaste vi kan göra för klimatet.

För att kunna göra större skillnad har vi börjat fundera på hur vi kan hjälpa våra kunder att bli medvetna om hur de kan sänka sina avtryck. Som ett led i det arbetet har vi börjat hjälpa vår kund PostNord att synliggöra klimatavtrycket för de IT-tjänster som de driftsatt i form av molntjänster.

Under en av PostNords återkommande innovationsdagar tog vi tillfället i akt och började undersöka möjligheten att visualisera klimatavtrycket för PostNords egenutvecklade molnbaserade tjänster – i realtid.

Eftersom vi hade begränsad tid avgränsade vi oss till att endast titta på klimatavtrycket som uppstår på grund av energiförbrukningen kopplad till CPU-användning. Uträkningen är i grunden väldigt enkel:

```text
Klimatavtryck =  Antal förbrukade wattimmar * Koldioxidutsläppen för en wattimme  
```

Men för att komma dit behöver man ha koll på ett par saker. Man behöver såklart veta hur många CPU-sekunder man förbrukat under en given tidsperiod och man behöver veta hur mycket energi en sådan CPU-sekund förbrukar. Sedan behöver man ha koll på hur energimixen ser ut i den eller de regioner där man förbrukar energin. Exempelvis varierar resultatet beroende på vilken region molntjänsten är placerad i; det är stor skillnad mellan Norden eller centraleuropa.

För oss handlade det om en utomnordisk, europeisk region. Vi lyckades hitta information om mängden [CO₂ som regionens energimix hade som utsläpp per kilowattimme](https://www.eea.europa.eu/data-and-maps/daviz/co2-emission-intensity-6#tab-googlechartid_googlechartid_chart_111_filters=%7B%22rowFilters%22%3A%7B%7D%3B%22columnFilters%22%3A%7B%22pre_config_date%22%3A%5B2018%5D%7D%3B%22sortFilter%22%3A%5B%22ugeo%22%5D%7D).

Vi identifierade vilken CPU-hårdvara vi använde och tog reda på hur många watt den drevs av (220 W) och delade det med antalet kärnor per CPU (8). Vi avrundade resultatet uppåt till 30 W. Vi antog en modest “avrunda uppåt”-strategi mest för att inte kunna kritiseras för att försöka sopa undan utsläppen som vi försöker mäta. Här kan det bli lite struligt om man har många olika typer av hårdvara med radikalt olika energiförbrukning, så var det dock inte för oss.

Nu vet vi att:

* En CPU under användning drar 30 W och att en CPU-kärnetimme alltså konsumerar 30 Wh.
* Vi kunde också konstatera att 1 Wh gav upphov till 0.425 gram CO₂ i utsläpp.
* Antalet CPU-sekunder per applikation i vårt Kubernetes-kluster kan vi läsa ur vår Prometheus-instans.

**Där är vi framme. Vi kunde se hur mycket CPU-tid vi förbrukade och hur mycket energi det motsvarade, och vi hade hittat hur mycket CO₂ den energimängden motsvarade i utsläpp för den region förbrukningen gäller.**

Vi kunde dessutom dela upp avtrycket på våra olika Kubernetes-kluster och namespace för att ge teamen ytterligare information om var de kan hitta lågt hängande frukter för att sänka utsläppen.

Utöver detta tillkommer såklart energiförbrukning för lagring, nätverk, RAM-användning och tredjepartstjänster som databaser och meddelandehanterare, samt serverhallar och kylning. Därför ska detta experiment mest betraktas som ett spårljus. Vi har lyst upp möjligheten att mäta och visat att det är möjligt.  

När vi väl fått vårt svar blev det i form av CO₂ för ett givet tidsintervall. Vi resonerade kring hur man kan få bättre förståelse för vad det innebär. Känslan för CO₂ är ju oftast kopplat till hur långt en bil kan köra, men det är en ganska dålig referens eftersom utsläppen från fossildrivna bilar är väldigt hög.

**Därför bestämde vi oss för att mäta i antal fullstora träd som skulle behöva finnas, utöver de träd som redan fanns innan tjänsterna var utvecklade, för att deras kontinuerliga bindande av CO₂ skulle kompensera för vår verksamhet.** Ett fullvuxet träd absorberar [ungefär 21 kilo CO₂ under ett år](https://www.viessmann.co.uk/heating-advice/how-much-co2-does-tree-absorb). Med den informationen kunde vi ge en lite mer konkret känsla för hur stora våra utsläpp var kopplat till naturens egna verktyg.

En helt annan strategi som vi funderat lite över för att beräkna klimatavtrycket är att abstrahera och förenkla avtrycksberäkningen med en [Fermi-uppskattning](https://en.wikipedia.org/wiki/Fermi_problem). Vi vet att de löpande kostnaderna för molntjänster till stor del utgörs av energikostnader. Alltså skulle man kunna ta sina totala kostnader för molntjänsterna multiplicera med en rimlig faktor under 1 (de tjänar ju även pengar på oss) och sedan ta reda på hur många kilowattimmar regionens energipris gör gällande att man rimligen konsumerat. Tillsammans med regionens energimix kan det möjligen ge en fullgod uppskattning av klimatavtrycket. Nackdelen med den strategin är att man riskerar att få längre återkopplingstider på de förändringar man gör för att minska kostnader/avtryck.

Så här kan en förenklad uppskattning inspirerad av [Fermi](https://en.wikipedia.org/wiki/Fermi_problem) se ut:

```text
Molnkostnad * 0.75 = Mk  
Energikostnad per kWh på den lokala marknaden = Ek  
Energimix CO₂/kWh = avtryckstimme  

Uppskattning = Mk/Ek * avtryckstimme
```
