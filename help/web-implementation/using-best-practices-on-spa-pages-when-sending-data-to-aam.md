---
title: Gebruik best practices op SPA-pagina's wanneer u gegevens naar AAM verzendt
description: Leer beste praktijken voor het verzenden van gegevens van enig-paginatoepassingen (SPA) aan Adobe Audience Manager (AAM). Dit artikel richt zich op het gebruik van Experience Platform-tags, de aanbevolen implementatiemethode.
feature: Implementation Basics
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: Developer, Data Engineer
level: Experienced
exl-id: 99ec723a-dd56-4355-a29f-bd6d2356b402
source-git-commit: d4874d9f6d7a36bb81ac183eb8b853d893822ae0
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Gebruik best practices op SPA-pagina&#39;s wanneer u gegevens naar AAM verzendt {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

Dit document beschrijft verscheidene beste praktijken voor het verzenden van gegevens van enig-paginatoepassingen (SPA) aan Adobe Audience Manager (AAM). Dit artikel richt zich op het gebruik van [!UICONTROL Experience Platform tags] , de aanbevolen implementatiemethode.

## Eerste aantekeningen

* In de onderstaande items wordt ervan uitgegaan dat u de tags Platform gebruikt om te implementeren op uw site. De overwegingen bestaan nog als u geen markeringen van het Platform gebruikt, maar u zou hen aan uw implementatiemethode moeten aanpassen.
* Alle SPAs zijn verschillend, zodat zou u sommige volgende punten kunnen moeten aanpassen om aan uw vereisten het best te voldoen, maar Adobe wil sommige beste praktijken delen die u moet nadenken aangezien u gegevens van de pagina&#39;s van het KUUROORD naar Audience Manager verzendt.

## Eenvoudig diagram van het werken met SPAs en AAM in de markeringen van Experience Platform (vroeger, Lancering){#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![ SPA voor naam in markeringen ](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Zoals verklaard, is dit een vereenvoudigd diagram van hoe de pagina&#39;s van het KUUROORD in een implementatie van Adobe Audience Manager (zonder Adobe Analytics) gebruikend de markeringen van het Platform worden behandeld. Zoals u kunt zien, is het vrij recht-voorwaarts, met het grote besluit is hoe u een meningsverandering (of een actie) aan de markeringen van het Platform gaat meedelen.

## Tags uit de SPA-pagina triggeren {#triggering-launch-from-the-spa-page}

Twee van de gemeenschappelijkere methodes om een regel in de markeringen van het Platform (en daarom het verzenden van gegevens naar Audience Manager) teweeg te brengen, zijn:

* Het plaatsen van de douanegebeurtenissen van JavaScript (zie voorbeeld [ HER ](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) met Adobe Analytics)
* Een [!UICONTROL Direct Call Rule] gebruiken

In dit Audience Manager-voorbeeld gebruikt u een [!UICONTROL Direct Call rule] in Platform-tag om de hit te activeren naar Audience Manager. Zoals u in de volgende secties zult zien, wordt dit handig door de [!UICONTROL Data Layer] in te stellen op een nieuwe waarde, zodat deze kan worden opgepakt door de [!UICONTROL Data Element] in de tags Platform.

## Demopagina {#demo-page}

Hier is een kleine pagina die het veranderen van een waarde in de gegevenslaag en het verzenden van het in Audience Manager aantoont, aangezien u op een pagina van het KUUROORD kunt doen. Deze functionaliteit kan worden gemodelleerd voor uitgebreidere wijzigingen die nodig zijn. U kunt deze demopagina [ HER ](https://aam.enablementadobe.com/SPA-Launch.html) vinden.

## De gegevenslaag instellen {#setting-the-data-layer}

Zoals vermeld, wanneer nieuwe inhoud op de pagina wordt geladen of wanneer iemand een actie op de plaats uitvoert, moet de gegevenslaag dynamisch in het hoofd van de pagina worden geplaatst VOORDAT de markeringen van het Platform worden geroepen en [!UICONTROL rules] in werking stellen, zodat de markeringen van het Platform de nieuwe waarden van de gegevenslaag kunnen opvangen en hen in Audience Manager duwen.

Als u naar de hierboven vermelde demosite gaat en naar de paginabron kijkt, ziet u:

* De gegevenslaag bevindt zich in de kop van de pagina, vóór de aanroep van de tags Platform
* De JavaScript in de gesimuleerde SPA-koppeling wijzigt de [!UICONTROL Data Layer] en roept vervolgens de tags Platform aan (de `_satellite.track()` -aanroep). Als u aangepaste JavaScript-gebeurtenissen gebruikte in plaats van deze [!UICONTROL Direct Call Rule] , is de les hetzelfde. Wijzig eerst de [!DNL data layer] -tags en roep vervolgens de tags Platform aan.

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Aanvullende bronnen {#additional-resources}

* [ bespreking van het KUUROORD op de forums van Adobe ](https://forums.adobe.com/thread/2451022)
* [ de plaatsen van de Architectuur van de Verwijzing om te tonen hoe te om KUUROORD in de markeringen van het Platform uit te voeren ](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [ Gebruikend beste praktijken wanneer het volgen van KUUROORD in Adobe Analytics ](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [ plaats van de Demo die voor dit artikel wordt gebruikt ](https://aam.enablementadobe.com/SPA-Launch.html)
