---
title: Bijwerken naar Adobe Audience Manager DIL versie 8.0 (of hoger)
description: In dit artikel worden de stappen en aanbevelingen beschreven voor het bijwerken van Adobe Audience Manager (AAM) Data Integration Library (DIL)-code naar versie 8.0 of hoger. Dit heeft betrekking op "client-side" DIL-implementatie, niet op het doorsturen van Adobe Analytics-gegevens aan de serverzijde, en geldt voor DTM, Launch by Adobe en implementaties zonder oplossing voor Adobe tagbeheer.
feature: dil implementation
topics: null
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
translation-type: tm+mt
source-git-commit: dfd549508cc223714bdb07ac6fd2aa31e6ca5586
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 0%

---


# Bijwerken naar Adobe Audience Manager DIL versie 8.0 (of hoger) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

In dit artikel worden de stappen en aanbevelingen beschreven voor het bijwerken van Adobe Audience Manager-code (AAM) [!DNL Data Integration Library] (DIL) naar versie 8.0 of hoger. Dit heeft betrekking op &quot;client-side&quot; DIL-implementatie, niet op het doorsturen van Adobe Analytics-gegevens aan de serverzijde, en geldt voor DTM, Launch by Adobe en implementaties zonder oplossing voor Adobe tagbeheer.

## Overzicht {#overview}

De code van de Audience Manager [!DNL Data Integration Library] (DIL) staat u toe om AAM op uw Website* uit te voeren. Bij het uitvoeren van vorige versies van DIL, werd het niet vereist om de Dienst van identiteitskaart van de Experience Cloud van Adobe te hebben ook (ECID) wordt uitgevoerd (hoewel het een zeer goed idee was). Vanaf DIL versie 8.0 is er een sterke afhankelijkheid van ECID versie 3.3 of hoger. Als u DIL 8.0 of later zonder ECID 3.3 of met een vroegere versie implementeert, krijgt u een fout en werkt deze niet. Aangezien er meerdere manieren zijn waarop u AAM kunt implementeren, hebben we deze pagina gemaakt om u enkele stappen te geven die u moet doorlopen, en enkele aanbevelingen. Hieronder vindt u deze stappen en aanbevelingen, uitgesplitst naar platform/implementatiemethode. Meer informatie over DIL is beschikbaar in de [documentatie](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html).

* Zoals vermeld in de beschrijving van deze pagina, zal dit slechts &quot;cliënt-kant&quot;DIL implementaties omvatten, die door AAM klanten worden gebruikt die geen Adobe Analytics hebben. Als u Adobe Analytics hebt, zou u de server-kant het door:sturen methode moeten gebruiken om AAM uit te voeren. Deze methode wordt beschreven in de [documentatie](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html).

## Elementen en methoden dupliceren en afgekeurd {#duplicate-and-deprecated-elements-and-methods}

In eerdere versies van DIL en ECID waren er dubbele methoden (methoden die dezelfde functie in zowel DIL als ECID hebben), die verwarring veroorzaakten over welke methode moet worden gebruikt. Typisch, moest u beide gebruiken en hen aanpassen omhoog, en dat bericht werd niet goed meegedeeld aan onze klanten. Vanaf DIL 8.0 zijn deze dubbele methoden en elementen afgekeurd in DIL en het wordt aanbevolen de ECID-versie te gebruiken.

Bijvoorbeeld:

* Bij gebruik [!DNL DIL.create]zijn een aantal elementen afgekeurd en moet u in plaats daarvan de ECID-elementen gebruiken. Deze elementen worden genoemd in de [[!DNL DIL.create] documentatie](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html).
* De methode op [!DNL idSync] instantieniveau is ook afgekeurd, zoals wordt aangeroepen in de [documentatie](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_idsync.html)van de methode.

## ID synchroniseren met een klant-id {#id-syncing-with-a-customer-id}

In AAM kunt u uw UUID (anonieme unieke gebruikersnaam) op de computer synchroniseren met een klant-id, zodat u offlinegegevens over die klant kunt uploaden en deze kunt koppelen aan hun onlinegedrag om een beter inzicht te krijgen in uw klanten. In het verleden is dit op twee manieren gebeurd:

* De methode op [!DNL idSync] instantieniveau
* Het [!DNL declaredId] element in [!DNL DIL.create]

Als u een van deze oudere methoden hebt gebruikt om te synchroniseren met een klant-id, wordt u ten zeerste aangeraden een update uit te voeren naar de [!DNL setCustomerIDs] methode, die deel uitmaakt van de ECID-service. Meer informatie over [!DNL setCustomerIDs] is beschikbaar in de [documentatie](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)van de methode.

**Snelle tip:** Wanneer eerder het gebruiken van één van beide methodes hierboven, u van verwijzingen ging het AAM [!UICONTROL Data Source] met [!UICONTROL Data Source] identiteitskaart (AKA de &quot;DPID&quot;). Wanneer u een update uitvoert naar [!DNL setCustomerIDs], moet u in plaats daarvan de [!UICONTROL Data Source]&#39;[!UICONTROL Integration Code]&#39; van de AAM gebruiken. Het verwijst nog steeds naar hetzelfde [!UICONTROL Data Source] maar is slechts een andere id. Dit wordt weergegeven in de onderstaande video.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

In de volgende secties vindt u stappen en aanbevelingen voor het bijwerken naar DIL 8.0 op basis van uw implementatiemethode:

## Bijwerken naar DIL 8.0 in Adobe Experience Platform Launch {#updating-to-dil-in-experience-platform-launch}

Basisstappen voor het bijwerken naar DIL 8.0

1. Als u pre-8.0 DIL gebruikt, alvorens u bevordert, ga in de configuratie van de DIL in de AAM uitbreiding, en neem nota van om het even welke geavanceerde opties die u gebruikt (in een verdere stap moet worden gebruikt)
1. Werk uw AAM extensie bij naar versie 8.0 of hoger
1. Controleer of uw Experience Cloud ID Service-extensie versie 3.3.0 of hoger is
1. Schakel de ECID-methoden in de ECID-extensie in voor alle vervangen methoden/elementen (zoals &quot;[!DNL disableIDSyncs]&quot;) die zich in de extensie voor 8.0 AAM of in de aangepaste code voor DIL bevonden.

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs
   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs
   1. (DIL) iframeAkamaiHTTPS -> (ECID) dSyncSSLUseAkamai
   1. (DIL) declareerdeId -> (ECID) setCustomerID&#39;s

1. Wijzigingen publiceren

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Bijwerken naar DIL 8.0 in Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Werk het AAM bij naar versie 8.0 of hoger. Deze versie-instelling bevindt zich onder de sectie Algemeen van het AAM.
1. Voor afgekeurde methoden/elementen (zoals &quot;disableIDSyncs&quot;) die zich in de aangepaste code van het gereedschap AAM 8.0 voor DIL bevonden, noteert u deze (zodat u ze aan het gereedschap ECID kunt toevoegen) en verwijdert u ze uit de aangepaste code [!DNL DIL code] in het gereedschap AAM.
1. Werk uw Experience Cloud ID-serviceverlenging bij naar versie 3.3.0 of hoger
1. Voeg de geavanceerde opties toe aan het gereedschap ECID die u uit de aangepaste code van het gereedschap AAM hebt verwijderd.
1. Wijzigingen publiceren

## Bijwerken naar DIL 8.0 zonder oplossing voor beheer van Adobe-tags {#additional-resources}

Als u de code rechtstreeks op de pagina bijwerkt, kunt u alleen oudere items vervangen door nieuwere items, behalve wanneer u methoden/elementen moet verplaatsen van DIL naar ECID, zoals hierboven beschreven. In dat geval vervangt u gewoon de oude methode/het oude element op de locatie DIL door de ECID-methode/het ECID-element op de locatie ECID.

Hetzelfde geldt voor niet-Adobe-tagmanagers. overal waar u de oude versies in die oplossing van het markeringsbeheer hebt, vervang het met de nieuwe code zoals die in de volgende stappen wordt beschreven.

1. Werk uw DIL-bibliotheek bij naar de nieuwste versie (8.0 of hoger) - U moet de nieuwste DIL-code ophalen van Adobe Consulting of Adobe Customer Care, omdat deze momenteel niet beschikbaar is op een openbare locatie. Vervang vervolgens gewoon de oude bibliotheekcode van de DIL door de nieuwe bibliotheekcode van de DIL en ga naar de volgende stap (stop nu niet of u gaat problemen krijgen, ha).
1. Installeer [!DNL ECID Service] of werk uw bestaande versie bij aan 3.3.0 of hoger. U kunt de recentste versie van de Dienst van identiteitskaart van Experience Cloud downloaden [van onze pagina](https://github.com/Adobe-Marketing-Cloud/id-service/releases)GitHub. Raadpleeg de [documentatie](https://marketing.adobe.com/resources/help/en_US/mcvid/) of neem contact op met een Adobe Consultant als u hier hulp bij nodig hebt.

1. Controleer of afgekeurde methoden of elementen in de aangepaste code voor DIL naar de ECID-methoden worden verplaatst:

   1. (DIL) disableDestinationPublishingIframe -> (ECID) disableIdSyncs

      [Documentatie](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) disableIDSyncs -> (ECID) disableIdSyncs

      [Documentatie](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-disableidsync.html)

   1. (DIL) iframeAkamaiHTTPS -> (ECID) idSyncSSLUseAkamai

      [Documentatie](https://marketing.adobe.com/resources/help/en_US/aam/r_dil_create.html)

   1. (DIL) declareerdeId -> (ECID) setCustomerID&#39;s

      [Documentatie](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid_setcustomerids.html)