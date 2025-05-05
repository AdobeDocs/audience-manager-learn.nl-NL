---
title: Migreren van het volgen server aan rapport-reeks-vlakke server-kant door:sturen
description: Leer hoe te om server-zijhet door:sturen van de Gegevens van Adobe Analytics aan Audience Manager op rapport-reeks-niveau in plaats van op het volgen serverniveau toe te laten.
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
source-wordcount: '586'
ht-degree: 0%

---

# Migreren van het volgen server aan rapport-reeks-vlakke server-kant door:sturen {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Dit artikel en de video zullen u tonen hoe te om server-kant het door:sturen van toe te laten [!DNL Analytics] Gegevens naar Audience Manager op een [!UICONTROL report suite] niveau in plaats van op een [!UICONTROL tracking server] niveau.

## Inleiding {#introduction}

Als u Adobe Audience Manager EN Adobe Analytics hebt, kunt u server-side door:sturen van uitvoeren [!DNL Analytics] aan Audience Manager. Dit betekent dat er op uw pagina geen twee treffers worden verzonden (een naar [!DNL Analytics] en één naar Audience Manager), kan het een klap naar sturen [!DNL Analytics], en [!DNL Analytics] stuurt die gegevens door naar de Audience Manager.

Als u dit reeds hebt in werking gesteld, en als u het vóór Oktober 2017 had toegelaten/uitgevoerd, zou uw server-zij door:sturen op uw kunnen worden gebaseerd [!UICONTROL Tracking Server], die moest worden ingeschakeld door de klantenservice van Adobe of Adobe-consulting. Vanaf oktober 2017, kunt u server-kant nu vormen door:sturen zich, en het doen op een rapport-reeks-niveau (door:sturen per rapportreeks). Hieraan zijn aanzienlijke voordelen verbonden, die hieronder worden besproken.

## [!UICONTROL Tracking server] doorsturen {#tracking-server-forwarding}

Uw [!UICONTROL tracking server] is de locatie waarnaar u uw [!DNL Analytics] en ook het domein waarop de afbeeldingsaanvraag en het cookie worden geschreven. Het moet worden ingesteld in DTM of [!DNL Experience Platform Launch]of in de [!DNL AppMeasurement.js] en ziet er meestal als volgt uit: uw site of bedrijfsnaam vervangt &quot;mijnsite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Als server-zij het door:sturen opstelling is om bij door:sturen [!UICONTROL tracking server] niveau, elke treffer die naar deze [!UICONTROL tracking server] (ALS de Experience Cloud ID-service ook is ingeschakeld) wordt doorgestuurd naar de Audience Manager. Dit moest door de Adobe klantendienst of de Raadpleging van de Adobe worden toegelaten. Zij zijn ook degenen die het kunnen onbruikbaar maken NADAT u hebt overgegaan naar [!UICONTROL report suite] doorsturen, zoals hieronder beschreven.

Als u twijfelt of [!DNL tracking server forwarding] is ingeschakeld voor u, neemt u contact op met de klantenservice van de Adobe of met de Adobe. U kunt deze informatie dan ook altijd op de hoogte stellen.

## [!UICONTROL Report-suite]-Level server-side door:sturen {#report-suite-level-server-side-forwarding}

Een van de grootste voordelen van de overgang naar [!UICONTROL report suite] doorsturen van [!UICONTROL tracking server] het door:sturen is dat u &quot;Audience Analytics&quot;nu zult kunnen gebruiken, wat de capaciteit is om Audience Manager door:sturen [!UICONTROL segments] terug naar Adobe Analytics voor een gedetailleerde segmentanalyse. Deze geweldige functie wordt NIET ondersteund als u nog steeds actief bent [!UICONTROL tracking server] doorsturen en niet [!UICONTROL report suite] doorsturen. Meer informatie over Audience Analytics vindt u in de [documentatie](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html?lang=nl-NL).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Belangrijke tip {#additional-resources}

Zoals in de video hierboven is vermeld, hebt u alle [!UICONTROL report suites] om door te sturen dat u aan Audience Manager wilt door:sturen, zou u de Zorg van de Klant van de Adobe of van de Adobe moeten contacteren en hen hebben onbruikbaar maken [!UICONTROL tracking server] doorsturen. Het is geen noodgeval voor u om dit te doen, omdat u beide [!UICONTROL tracking server] doorsturen en [!UICONTROL report suite] het door:sturen resulteert niet in dubbele klappen. Het is echter de beste praktijk om alleen [!UICONTROL report suite] doorsturen.

Als u weggaat [!UICONTROL tracking server] door:sturen op, niet alleen zou het gegevens van door:sturen [!UICONTROL report suites] dat u niet door:sturen wilt, maar in de toekomst, nadat u (en iedereen bij uw bedrijf) is vergeten dat [!UICONTROL tracking server] het door:sturen is op, zou u kunnen denken dat het gegeven niet voor een specifiek door:sturen [!UICONTROL report suite]. De reden hiervoor is dat deze optie niet is ingeschakeld op het niveau van de rapportsuite, maar dat de gegevens toch worden doorgestuurd vanwege de [!UICONTROL tracking server]. Vervolgens verspilt u tijd en geld om uit te zoeken waarom het wordt doorgestuurd en betaalt u ook voor AAM serveraanroepen die u niet had verwacht. Het is daarom raadzaam deze optie uit te schakelen [!UICONTROL tracking server] doorsturen zodra u alle [!UICONTROL report suites] klaar zijn om die zin voor uw bedrijfsbehoeften door te sturen.
