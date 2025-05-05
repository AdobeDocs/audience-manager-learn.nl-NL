---
title: De implementatie van de Audience Manager van uw site migreren van client-side DIL naar server-side door:sturen
description: Leer hoe te om de Audience Manager (AAM) implementatie van uw plaats van cliënt-kant DIL aan server-kant door:sturen te migreren. Deze zelfstudie is van toepassing als u zowel AAM als Adobe Analytics hebt, en u hits van de pagina naar AAM verzendt met DIL (Data Integration Library) code en u ook hits van de pagina naar Adobe Analytics verzendt.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
role: Developer, Data Engineer
level: Intermediate
exl-id: bcb968fb-4290-4f10-b1bb-e9f41f182115
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 0%

---

# De implementatie van de Audience Manager van uw site migreren van client-side DIL naar server-side door:sturen {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Deze zelfstudie is op u van toepassing als u zowel Adobe Audience Manager (AAM) als Adobe Analytics hebt en u momenteel een hit van de pagina naar AAM verzendt met DIL ([!DNL Data Integration Library]) en ook een hit van de pagina naar Adobe Analytics verzenden. Aangezien u beide oplossingen hebt, en aangezien zij allebei deel van Adobe Experience Cloud uitmaken, hebt u de kans om de beste praktijk te volgen om server-zij het door:sturen aan te zetten, die toelaat [!DNL Analytics] de servers van de gegevensinzameling om plaats analysegegevens in real time aan Audience Manager door:sturen, in plaats van het hebben van cliënt-zijcode verzendt een extra klap van de pagina naar AAM. Dit leerprogramma begeleidt u door de stappen om de schakelaar van de oudere cliënt-kant implementatie van DIL aan de nieuwere server-kant door:sturen methode te maken.

## Client-kant (DIL) versus server-kant {#client-side-dil-vs-server-side}

Bij het vergelijken en contrasteren van deze twee methoden om Adobe Analytics-gegevens in AAM te krijgen, kan het in de eerste plaats nuttig zijn om de verschillen in de volgende afbeelding te visualiseren:

![client-kant naar server-kant](assets/client-side_vs_server-side_aam_implementation.png)

### DIL-implementatie op de client {#client-side-dil-implementation}

Als u deze methode gebruikt om Adobe Analytics-gegevens in AAM te krijgen, hebt u twee hits op uw webpagina&#39;s: Eén gaat naar [!DNL Analytics]en één die naar AAM gaat (na het kopiëren van [!DNL Analytics] gegevens op de webpagina. [!UICONTROL Segments] worden teruggestuurd van AAM naar de pagina, waar ze kunnen worden gebruikt voor personalisatie, enzovoort. Dit wordt beschouwd als een oudere implementatie en wordt niet meer aanbevolen.

Afgezien van het feit dat dit niet de beste praktijken volgt, omvatten de nadelen om deze methode te gebruiken:

* Twee hits op de pagina in plaats van slechts één
* server-kant het door:sturen wordt vereist voor het delen in real time van AAM publiek aan [!DNL Analytics], zodat clientimplementaties deze functie (en mogelijk andere functies in de toekomst) niet toestaan

Men adviseert dat u zich aan een server-kant het door:sturen methode van AAM implementatie beweegt.

### Server-kant het door:sturen implementatie {#server-side-forwarding-implementation}

Zoals in bovenstaande afbeelding wordt getoond, komt een hit van de webpagina naar Adobe Analytics. [!DNL Analytics] die gegevens vervolgens doorsturen naar AAM in real time, en bezoekers worden geëvalueerd in AAM kenmerken en [!UICONTROL segments], net alsof de treffer rechtstreeks van de pagina afkomstig was.

[!UICONTROL Segments] worden geretourneerd op dezelfde real-time hit als [!DNL Analytics], die de reactie op de Web-pagina voor verpersoonlijking, etc. door:sturen.

Er is geen timing aan het bewegen naar server-kant door:sturen. Adobe raadt iedereen die zowel Audience Manager als [!DNL Analytics] gebruikt deze implementatiemethode.

## U hebt twee hoofdtaken {#you-have-two-main-tasks}

Er staat nogal wat informatie op deze pagina, en dat is natuurlijk allemaal belangrijk. Zij **alles komt neer op twee belangrijke dingen die u moet doen**:

1. Wijzig uw code van cliënt-kant DIL code in server-kant het door:sturen code
1. Draai de schakelaar in [!DNL Analytics] [!DNL Admin Console] om de daadwerkelijke doorzending van gegevens te starten (per [!UICONTROL report suite])

Als u één van beiden van deze taken overslaat, server-kant door:sturen zal niet correct werken. Er zijn stappen en aanvullende gegevens toegevoegd aan dit document, zodat u deze twee stappen correct kunt uitvoeren.

## Implementatieopties {#implementation-options}

Aangezien u zich van cliënt-kant aan server-kant het door:sturen beweegt, één van de taken u zult hebben verandert de code aan de nieuwe server-kant door:sturen code. Dit gebeurt op basis van een van de volgende opties:

* Adobe Experience Platform-tags - Adobe aanbevolen implementatieoptie voor webeigenschappen U zult zien dat dit een gemakkelijke taak is, aangezien Platform-tags al het harde werk voor u hebben gedaan.
* Op de pagina - U kunt de nieuwe SSF-code ook rechtstreeks in de `doPlugins` functie in uw `appMeasurement.js` bestand, als u (nog) geen Adobe Launch gebruikt
* Andere tagmanagers - Deze kunnen op dezelfde manier worden behandeld als de vorige optie (Op de pagina), aangezien u de SSF-code nog steeds in `doPlugins`, waar de andere tagmanager de [!DNL AppMeasurement] code

Hieronder vindt u een overzicht van de _De code bijwerken_ sectie.

## Uitvoeringsstappen {#implementation-steps}

In de volgende stappen wordt de implementatie beschreven.

### Stap 0: Vereiste: Experience Cloud ID-service (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

De belangrijkste voorwaarde voor de overgang naar server-kant door:sturen moet de Experience Cloud ID Service hebben uitgevoerd. Dit is het gemakkelijkst gedaan als u Experience Platform Launch gebruikt, in welk geval u eenvoudig de uitbreiding ECID installeert en het de rest zal doen.

Als u een niet-Adobe TMS of helemaal geen TMS gebruikt, moet u ECID implementeren om **voor** andere Adobe-oplossingen. Zie de [ECID-documentatie](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL) voor meer informatie . De enige andere voorwaarde is betreffende codeversies, zodat aangezien u eenvoudig de meest recente versies van de code in de volgende stappen toepast, zult u in orde zijn.

>[!NOTE]
>
>Lees dit gehele document voordat u het implementeert. De sectie &quot;Timing&quot; hieronder bevat belangrijke informatie over *wanneer* moet u elk onderdeel implementeren, inclusief ECID (als dit nog niet is geïmplementeerd).

### Stap 1: Momenteel gebruikte opties uit DIL-code opnemen {#step-record-currently-used-options-from-dil-code}

Aangezien u bereid wordt om zich van cliënt-kant DIL code aan server-kant door:sturen, is de eerste stap alles te identificeren dat u met DIL code doet, met inbegrip van douanemontages en gegevens die naar AAM worden verzonden. U kunt onder andere de volgende dingen opmerken en overwegen:

* Normaal [!DNL Analytics] variabelen, gebruiken `siteCatalyst.init` DIL module - U hoeft zich geen zorgen te maken over deze module, omdat het alleen gaat om het verzenden van de normale [!DNL Analytics] variabelen over, en dat gebeurt door eenvoudig te hebben server-zij toegelaten door:sturen.
* Subdomein van partner - in `DIL.create` functie, noteer de `partner` parameter. Dit is gekend als uw &quot;partner subdomain,&quot;of soms &quot;partner identiteitskaart,&quot;en zal nodig zijn wanneer u de nieuwe server-kant het door:sturen code plaatst.
* [!DNL Visitor Service Namespace] - Wordt ook wel &#39; &#39;[!DNL Org ID]&quot; of &quot;[!DNL IMS Org ID],&quot; hebt u dit ook nodig wanneer u de nieuwe servercode voor doorsturen instelt. Noteer dit.
* containerNSID, uuidCookie, en andere geavanceerde opties - maak een nota van om het even welke extra geavanceerde opties u gebruikt zodat u hen in de server-zij het door:sturen code kunt plaatsen eveneens.
* Aanvullende paginabariabelen - Als andere variabelen van de pagina naar AAM worden verzonden (naast de normale [!DNL Analytics] variabelen die door siteCatalyst.init worden behandeld), zult u nota van hen moeten maken zodat zij binnen via server-zij het door:sturen kunnen worden verzonden (spoiler waakzaam: via [!DNL contextData] variabelen).

### Stap 2: De code bijwerken {#step-updating-the-code}

In [Implementatieopties](#implementation-options) (hierboven), worden de veelvoudige opties gegeven betreffende hoe en waar u server-kant het door:sturen uitvoert. Om deze paragraaf doeltreffend te maken, moeten we ze in deze secties opsplitsen (met twee gecombineerd). Ga naar de methode van deze sectie die uw behoeften het best beschrijft.

#### Adobe Experience Platform-tags {#launch-by-adobe}

Bekijk de video hieronder om over het bewegen van implementatieopties van cliënt-kant DIL code in server-kant het door:sturen in Experience Platform Launch te leren.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### &quot;Op de pagina&quot; of niet-Adobe tagbeheer {#on-the-page-or-non-adobe-tag-manager}

Bekijk de video hieronder om te leren over het bewegen van implementatieopties van cliënt-kant DIL code in server-kant door:sturen binnen [!DNL AppMeasurement] code, die in een dossier of in een niet-Adobe systeem van het markeringsbeheer verblijft.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Stap 3: Het toelaten van het door:sturen (per [!UICONTROL Report Suite]) {#step-enabling-the-forwarding-per-report-suite}

Tot dusver in dit leerprogramma hebben wij al onze tijd besteed aan het schakelen van de code van cliënt-kant DIL code aan server-kant door:sturen. Dat is prima, want het is het moeilijkste. Hoewel u zult zien dat deze sectie bijzonder eenvoudig is, is deze net zo belangrijk als het bijwerken van de code. In deze video, zult u zien hoe te om de schakelaar te draaien die het daadwerkelijke door:sturen van gegevens van Analytics aan Audience Manager toelaat.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**OPMERKING:** Zoals verklaard in de video, herinner dat het tot 4 uren voor het toelaten van het door:sturen zal duren om volledig op de Experience Cloud backend worden uitgevoerd.

## Timing {#timing}

Als herinnering, zijn er twee hoofdtaken om zich over van cliënt-kant DIL aan server-kant door:sturen:

1. De code bijwerken
1. De schakelaar in [!DNL Analytics] [!DNL Admin Console]

Maar de vraag is: welke doe je eerst? Maakt het uit? Dat waren twee vragen. Maar de antwoorden zijn... het hangt af, en ja, het. *kan* van belang. Hoe is dat voor vaag? Laten we het splitsen. Maar eerst een extra vraag die kan komen als u een grote organisatie met talrijke plaatsen bent: Moet ik alles tegelijk doen? Dat is iets makkelijker. Nope. Je kunt het stuk voor stuk doen.

### Een beetje dieper duiken {#a-little-deeper-dive}

De reden waarom de timing en de orde belangrijk zijn omdat hoe door:sturen _echt_ werken, die in de volgende technische feiten kunnen worden samengevat:

* Als u de Experience Cloud ID Service (ECID) hebt geïmplementeerd, en de switch in de [!DNL Analytics] [!DNL Admin Console] (&quot;de schakelaar&quot;) is aan, gegevens ZULLEN van [!DNL Analytics] AAM, zelfs als u de code nog niet hebt bijgewerkt.
* Als u ECID niet hebt uitgevoerd, zullen de gegevens niet door:sturen, zelfs als u de schakelaar hebt, en de server-kant hebben door:sturen code.
* De server-kant het door:sturen code (of in de markeringen van het Platform of op de pagina) behandelt werkelijk de reactie en is noodzakelijk om de migratie te voltooien.
* Herinner dat de server-zij het door:sturen schakelaar door wordt toegelaten [!UICONTROL report suite], maar dat de code door het bezit in de markeringen van het Platform of door het [!DNL AppMeasurement] bestand als u geen Platform-tags gebruikt.

### Aanbevolen procedures {#best-practices}

Op basis van deze technische details zijn hier de aanbevelingen voor de timing van wat te doen en wanneer:

#### Als u ECID nog niet hebt geïmplementeerd {#if-you-do-not-have-ecid-yet-implemented}

1. De schakelaar omdraaien [!DNL Analytics] voor elke [!UICONTROL report suite] dat u voor server-kant het door:sturen zult toelaten.

   1. Het doorsturen begint nog niet omdat u geen ECID hebt.

1. Werk per site uw code bij van client-side DIL naar server-side door:sturen (dit kan in Platforms tags staan) of op de pagina, zoals in een andere sectie hierboven is beschreven).

   1. Als u nu stromen doorstuurt (zoals u ECID hebt toegevoegd), ontvangt u ook een juiste JSON-reactie op uw [!DNL Analytics] baken (zie de sectie van de Bevestiging en van het Oplossen van problemen hieronder voor meer details).

#### Als u ECID hebt geïmplementeerd {#if-you-do-have-ecid-implemented}

1. Bereid en plan voor zodat u bereid bent om uw code van DIL aan server-kant bij te werken door:sturen PER [!UICONTROL report suite] dat u voor server-kant het door:sturen zult toelaten:

   1. De schakelaar omdraaien [!DNL Analytics] om server-kant het door:sturen toe te laten.

      1. Het doorsturen begint omdat je ECID hebt ingeschakeld.
   1. Werk uw code zo snel mogelijk bij van client-side DIL naar single-side door:sturen (dit kan in Platform tags of op de pagina staan, zoals in een andere sectie hierboven is beschreven).

      1. U ontvangt een juiste JSON-reactie op uw [!DNL Analytics] baken (zie [Validatie en probleemoplossing](#validation-and-troubleshooting) voor meer informatie ).


>[!NOTE]
>
>Het is belangrijk om deze twee stappen zo dicht mogelijk bij elkaar te doen, omdat u tussen stap 1 en 2 hierboven dubbele gegevens hebt die naar AAM gaan. Met andere woorden, single-side door:sturen zal begonnen zijn met het verzenden van gegevens van [!DNL Analytics] AAM, en aangezien de code van de DIL nog op de pagina is, zal er ook een klap zijn die rechtstreeks van de pagina naar AAM gaat, waarbij de gegevens worden verdubbeld. Zodra u de code van DIL aan server-kant door:sturen bijwerkt, zal dit worden verlicht.

>[!NOTE]
>
>Als u liever een kleine discrepantie in gegevens hebt in plaats van een kleine duplicatie van gegevens, kunt u de volgorde van stap 1 en 2 hierboven wijzigen. Het bewegen van de code van DIL aan server-kant door:sturen zou de gegevensstroom in AAM tegenhouden tot u de schakelaar kon draaien om server-kant aan te zetten door:sturen voor server-kant aan te zetten [!UICONTROL report suite]. Meestal zouden klanten liever een kleine verdubbeling van gegevens hebben dan bezoekers de mogelijkheid te ontnemen om hun gegevens in te voeren en [!UICONTROL segments].

#### De timing van de migratie wanneer u vele plaatsen hebt en [!UICONTROL report suites] {#migration-timing-when-you-have-many-sites-and-report-suites}

Dit onderwerp wordt in eerdere paragrafen kort besproken, in die zin dat de hoofdstrategie als volgt kan worden samengevat:

Eén site/site migreren[!UICONTROL report suite] (of groep sites/[!UICONTROL report suites]) op een bepaald tijdstip.

Nochtans, kan dit een beetje lastig worden gebaseerd op een paar mogelijke scenario&#39;s:

* U hebt een site die verschillende specifieke [!UICONTROL report suites]
* U hebt een [!UICONTROL report suite] die meerdere sites bevat (zoals een globaal [!UICONTROL report suite])
* U gebruikt één eigenschap voor tags van Platforms om meerdere sites te bestrijken
* U hebt verschillende ontwikkelingsteams voor verschillende sites

Vanwege deze items kan het een beetje ingewikkeld worden. De beste dingen die ik kan voorstellen zijn:

* Neem wat tijd om een strategie te maken voor het migreren naar server-kant het door:sturen, die op de dingen wordt gebaseerd die hierboven zijn verklaard
* Gebaseerd op het feit dat één eigenschap in Platform-tags (of één eigenschap [!DNL AppMeasurement] bestand) wordt doorgaans toegewezen aan 1 of 2 verschillende [!UICONTROL report suites], zult u waarschijnlijk een plan kunnen maken dat aan deze verschillende groepen één voor één werkt, het bijwerken van uw onderneming aan server-kant door:sturen
* Als u met Adobe Consulting werkt, praat dan met hen over uw migratieplan, zodat zij waar nodig hulp kunnen bieden

## Validatie en probleemoplossing {#validation-and-troubleshooting}

De belangrijkste manier om te bevestigen dat de server-kant het door:sturen in werking is door de reactie op om het even welk van uw Adobe Analytics klappen te bekijken die uit app komen.

Als u server-zij niet het door:sturen van gegevens van doet [!DNL Analytics] Audience Manager, dan is er echt geen antwoord op de [!DNL Analytics] baken (behalve een 2 x 2 pixel). Nochtans, als u server-zij door:sturen doet, dan zijn er punten die u in kunt verifiëren [!DNL Analytics] verzoek en antwoord die u zullen laten weten dat [!DNL Analytics] communiceert correct met Audience Manager, door:sturen de klap, en het krijgen van een reactie.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

>[!WARNING]
>
>Let op de fout &quot;Succes&quot;. Als er een antwoord is, en alles lijkt te werken, zorg er dan voor dat u de `stuff` -object in de reactie. Als u dat niet doet, ziet u mogelijk een bericht dat `"status":"SUCCESS"`. Hoe gek dit ook klinkt, dit is eigenlijk een bewijs dat het NIET correct werkt.
>
>Als u dit ziet, betekent dit dat u de code hebt bijgewerkt in tags van Platforms of [!DNL AppMeasurement], maar dat het doorsturen van [!DNL Analytics] [!DNL Admin Console] nog niet voltooid. In dit geval moet u verifiëren dat u server-zij door:sturen in hebt toegelaten [!DNL Analytics] [!DNL Admin Console] voor uw [!UICONTROL report suite]. Als je wel, en dat is nog geen 4 uur, geduld hebt, omdat het zo lang kan duren om alle noodzakelijke veranderingen op de achtergrond te maken.


![vals succes](assets/falsesuccess.png)

Voor meer informatie over server-zij het door:sturen, gelieve te zien [documentatie](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=nl-NL).
