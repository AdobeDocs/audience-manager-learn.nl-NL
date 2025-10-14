---
title: Migreren van het volgen server aan rapport-reeks-vlakke server-kant door:sturen
description: Leer hoe u het doorsturen van Adobe Analytics Data naar Audience Manager op de server mogelijk maakt op rapportniveau in plaats van op trackingserverniveau.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Migreren van het volgen server aan rapport-reeks-vlakke server-kant door:sturen {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

In dit artikel en in deze video ziet u hoe u het doorsturen van [!DNL Analytics] gegevens naar Audience Manager op [!UICONTROL report suite] -niveau in plaats van op [!UICONTROL tracking server] -niveau kunt inschakelen.

## Inleiding {#introduction}

Als u Adobe Audience Manager AND Adobe Analytics hebt, kunt u server-side het door:sturen van de [!DNL Analytics] gegevens aan Audience Manager uitvoeren. Dit betekent dat in plaats van dat uw pagina twee hits (een naar [!DNL Analytics] en een naar Audience Manager) verzendt, er een hit naar [!DNL Analytics] kan worden verzonden en dat [!DNL Analytics] die gegevens doorstuurt naar Audience Manager.

Als u dit al hebt gedaan en deze vóór oktober 2017 hebt ingeschakeld/geïmplementeerd, is het mogelijk dat het doorsturen aan de serverzijde is gebaseerd op uw [!UICONTROL Tracking Server] , die door Adobe Customer Care of Adobe Consulting moest worden ingeschakeld. Vanaf oktober 2017, kunt u server-kant nu vormen door:sturen zich, en het doen op een rapport-reeks-niveau (door:sturen per rapportreeks). Hieraan zijn aanzienlijke voordelen verbonden, die hieronder worden besproken.

## [!UICONTROL Tracking server] doorsturen {#tracking-server-forwarding}

Uw [!UICONTROL tracking server] is de locatie waarnaar u de [!DNL Analytics] -gegevens verzendt en ook het domein waar de afbeeldingsaanvraag en het cookie worden geschreven. Deze moet worden ingesteld in DTM of [!DNL Experience Platform Launch] of in het [!DNL AppMeasurement.js] -bestand en ziet er doorgaans als volgt uit: uw site of bedrijfsnaam vervangt &quot;mijnsite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Als server-side het door:sturen op het [!UICONTROL tracking server] niveau wordt opgezet door:sturen, zal om het even welke klap die naar dit [!UICONTROL tracking server] wordt verzonden (ALS de Dienst van Experience Cloud ID ook wordt toegelaten) door:sturen aan Audience Manager. Dit moest worden ingeschakeld door Adobe Customer Care of Adobe Consulting. Zij zijn ook degenen die het kunnen onbruikbaar maken, NADAT u op [!UICONTROL report suite] het door:sturen hebt overgegaan, zoals hieronder beschreven.

Als u niet zeker weet of [!DNL tracking server forwarding] voor u is ingeschakeld, neemt u contact op met de klantenservice van Adobe of Adobe Consulting en kunt u dit op de hoogte stellen.

## [!UICONTROL Report-suite] op server-niveau door:sturen {#report-suite-level-server-side-forwarding}

Een van de grootste voordelen van de overgang naar [!UICONTROL report suite] forward van [!UICONTROL tracking server] door:sturen is dat u nu &quot;Audience Analytics&quot; kunt gebruiken, namelijk de mogelijkheid om Audience Manager [!UICONTROL segments] terug naar Adobe Analytics te sturen voor gedetailleerde segmentanalyse. Deze fantastische functie wordt NIET ondersteund als u [!UICONTROL tracking server] door:sturen gebruikt en [!UICONTROL report suite] niet. Zie meer informatie over Audience Analytics in de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=nl-NL).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Belangrijke tip {#additional-resources}

Zoals in de video hierboven is vermeld, dient u, zodra u alle [!UICONTROL report suites] hebt ingesteld om door te sturen naar Audience Manager, contact op te nemen met de klantenservice van Adobe of Adobe Consulting en ervoor te zorgen dat deze het [!UICONTROL tracking server] doorsturen uitschakelen. Het is geen noodgeval voor u dit te doen, omdat het hebben van zowel [!UICONTROL tracking server] door:sturen als [!UICONTROL report suite] door:sturen niet in dubbele klappen resulteert. Het is echter aan te raden [!UICONTROL report suite] alleen door te sturen.

Als u [!UICONTROL tracking server] het door:sturen op verlaat, niet alleen zou het gegevens van [!UICONTROL report suites] door:sturen die u niet wilt door:sturen, maar in de toekomst, nadat u (en iedereen bij uw bedrijf) is vergeten dat [!UICONTROL tracking server] het door:sturen is, zou u kunnen denken dat de gegevens niet voor een specifieke [!UICONTROL report suite] door:sturen. De reden hiervoor is dat deze functie niet is ingeschakeld op het niveau van de rapportsuite, maar dat de gegevens toch worden doorgestuurd vanwege de [!UICONTROL tracking server] . Vervolgens verspilt u tijd en geld om uit te zoeken waarom het wordt doorgestuurd en betaalt u ook voor AAM-serveroproepen die u niet had verwacht. Het is daarom raadzaam [!UICONTROL tracking server] doorsturen uit te schakelen zodra u over alle [!UICONTROL report suites] beschikt die u nodig hebt om aan uw bedrijfsbehoeften te voldoen.
