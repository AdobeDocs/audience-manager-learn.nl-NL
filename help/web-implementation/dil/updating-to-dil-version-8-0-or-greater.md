---
title: Bijwerken naar Adobe Audience Manager DIL versie 8.0 (of hoger)
description: In dit artikel worden de stappen en aanbevelingen beschreven voor het bijwerken van de Adobe Audience Manager (AAM) Data Integration Library (DIL)-code naar versie 8.0 of hoger. Dit heeft betrekking op DIL-implementatie aan de clientzijde, niet op het doorsturen van Adobe Analytics-gegevens aan de serverzijde. DTM, Launch door Adobe en implementaties worden behandeld zonder Adobe-oplossing voor tagbeheer.
feature: DIL Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer, Data Engineer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Bijwerken naar DIL versie 8.0 (of hoger) van Adobe Audience Manager {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

In dit artikel worden de stappen en aanbevelingen beschreven voor het bijwerken van Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL)-code naar versie 8.0 of hoger. Dit heeft betrekking op DIL-implementatie aan de clientzijde, niet op het doorsturen van Adobe Analytics-gegevens aan de serverzijde. DTM, Launch door Adobe en implementaties worden behandeld zonder Adobe-oplossing voor tagbeheer.

## Overzicht {#overview}

Met Audience Manager [!DNL Data Integration Library] (DIL)-code kunt u AAM implementeren op uw website*. Bij de implementatie van eerdere versies van DIL was het niet nodig om ook de Experience Cloud ID Service (ECID) van Adobe te laten uitvoeren (hoewel dit een zeer goed idee was). Vanaf DIL versie 8.0 is er een sterke afhankelijkheid van ECID versie 3.3 of hoger. Als u DIL 8.0 of hoger implementeert zonder ECID 3.3 of met een eerdere versie, krijgt u een fout en werkt deze niet. Aangezien er meerdere manieren zijn waarop u AAM kunt implementeren, hebben we deze pagina gemaakt om u enkele stappen te geven die u moet doorlopen, en enkele aanbevelingen. Hieronder vindt u deze stappen en aanbevelingen, uitgesplitst naar platform/implementatiemethode. Meer informatie over DIL is beschikbaar in de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=nl-NL).

* Zoals vermeld in de beschrijving van deze pagina, zal dit slechts &quot;cliënt-kant&quot;DIL implementaties omvatten, die door klanten van AAM worden gebruikt die geen Adobe Analytics hebben. Als u Adobe Analytics hebt, zou u de server-kant het door:sturen methode moeten gebruiken om AAM uit te voeren. Deze methode wordt beschreven in de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=nl-NL).

## Elementen en methoden dupliceren en vervangen {#duplicate-and-deprecated-elements-and-methods}

In eerdere versies van DIL en ECID waren er dubbele methoden (methoden die dezelfde functie in zowel DIL als ECID hebben), die verwarring veroorzaakten over welke methode moet worden gebruikt. Typisch, moest u beide gebruiken en hen aanpassen omhoog, en dat bericht werd niet goed meegedeeld aan onze klanten. Vanaf DIL 8.0 zijn deze dubbele methoden en elementen afgekeurd in DIL. U wordt aangeraden de ECID-versie te gebruiken.

Bijvoorbeeld:

* Bij het gebruik van [!DNL DIL.create] zijn een aantal elementen vervangen en moet u in plaats daarvan de ECID-elementen gebruiken. Deze elementen worden geroepen uit in de [[!DNL DIL.create]  documentatie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=nl-NL).
* De [!DNL idSync] instantie-vlakke methode is ook afgekeurd, zoals die in de 1&rbrace; documentatie van de methode [&#x200B; wordt geroepen.](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html?lang=nl-NL)

## ID synchroniseren met een klant-id {#id-syncing-with-a-customer-id}

In AAM kunt u uw UUID (anonieme unieke gebruikersnaam) op de computer synchroniseren met een klant-id, zodat u offlinegegevens over die klant kunt uploaden en deze kunt koppelen aan hun onlinegedrag voor een beter inzicht in uw klanten. In het verleden is dit op twee manieren gebeurd:

* De methode op instantieniveau [!DNL idSync]
* Het element [!DNL declaredId] in [!DNL DIL.create]

Als u een van deze oudere methoden hebt gebruikt om te synchroniseren met een klant-id, is het raadzaam een update uit te voeren naar de methode [!DNL setCustomerIDs] , die deel uitmaakt van de ECID-service. Meer informatie over [!DNL setCustomerIDs] is beschikbaar in de 1&rbrace; documentatie van de methode [.](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=nl-NL)

**Snelle Uiteinde:** wanneer eerder het gebruiken van één van beiden van de methodes hierboven, u AAM [!UICONTROL Data Source] met [!UICONTROL Data Source] identiteitskaart (AKA &quot;DPID&quot;) van verwijzingen voorzien. Wanneer u een update uitvoert naar [!DNL setCustomerIDs] , moet u in plaats daarvan de instructies &quot; [!UICONTROL Data Source]&quot; van [!UICONTROL Integration Code] AAM gebruiken. Het verwijst nog steeds naar hetzelfde [!UICONTROL Data Source] , maar het is slechts een andere id. Dit wordt weergegeven in de onderstaande video.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

In de volgende secties vindt u stappen en aanbevelingen voor het bijwerken naar DIL 8.0 op basis van uw implementatiemethode:

## DIL 8.0 bijwerken in Adobe Experience Platform-tags {#updating-to-dil-in-experience-platform-launch}

Basisstappen voor het bijwerken naar DIL 8.0

1. Als u pre-8.0 DIL gebruikt, alvorens u bevordert, ga in de configuratie van DIL in de uitbreiding van AAM, en neem nota van om het even welke geavanceerde opties die u gebruikt (in een verdere stap).
1. Werk uw AAM-extensie bij naar versie 8.0 of hoger.
1. Controleer of uw Experience Cloud ID Service-extensie versie 3.3.0 of hoger is.
1. Schakel de ECID-methoden in de ECID-extensie in voor alle vervangen methoden/elementen (zoals `disableIDSyncs` ) die zich in de AAM-extensie vóór 8.0 of in de aangepaste code voor DIL bevonden.

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`
   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`
   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `dSyncSSLUseAkamai`
   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

1. Publiceer de wijzigingen.

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Bijwerken naar DIL 8.0 in Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Werk de AAM-tool bij naar versie 8.0 of hoger. Deze versie-instelling bevindt zich onder de sectie Algemeen van het gereedschap AAM.
1. Voor afgekeurde methoden/elementen (zoals `disableIDSyncs` ) die zich in de aangepaste code van AAM voor DIL van vóór 8.0 bevonden, noteert u deze (zodat u ze aan het gereedschap ECID kunt toevoegen) en verwijdert u ze uit de aangepaste [!DNL DIL code] in het gereedschap AAM.
1. De Experience Cloud ID Service-extensie bijwerken naar versie 3.3.0 of hoger
1. Voeg de geavanceerde opties toe aan het gereedschap ECID die u uit de aangepaste code van het gereedschap AAM hebt verwijderd.
1. Wijzigingen publiceren

## Bijwerken naar DIL 8.0 zonder Adobe Tag Management-oplossing {#additional-resources}

Als u de code rechtstreeks op de pagina bijwerkt, kunt u alleen oudere items vervangen door nieuwere items, behalve wanneer u methoden/elementen van DIL naar ECID moet verplaatsen, zoals hierboven is beschreven. In dat geval vervangt u gewoon de oude methode/het oude element op de DIL-locatie door de ECID-methode/het ECID-element op de ECID-locatie.

Hetzelfde geldt voor niet-Adobe-tagmanagers. overal waar u de oude versies in die oplossing van het markeringsbeheer hebt, vervang het met de nieuwe code zoals die in de volgende stappen wordt beschreven.

1. Werk uw DIL-bibliotheek bij naar de nieuwste versie (8.0 of hoger) - U moet de nieuwste DIL-code ophalen van Adobe Consulting of Adobe Customer Care, omdat deze momenteel niet beschikbaar is op een openbare locatie. Vervang vervolgens gewoon de oude DIL-bibliotheekcode door de nieuwe DIL-bibliotheekcode en ga naar de volgende stap (stop nu niet of u gaat problemen ondervinden, ha).
1. Installeer [!DNL ECID Service] of werk de bestaande versie bij naar versie 3.3.0 of hoger. U kunt de recentste versie van de Dienst van Experience Cloud identiteitskaart [&#x200B; van onze pagina van GitHub &#x200B;](https://github.com/Adobe-Marketing-Cloud/id-service/releases) downloaden. Als u hulp met dit nodig hebt, zie de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=nl-NL) of praat met een Consultant van Adobe.

1. Controleer of afgekeurde methoden of elementen in de aangepaste code voor DIL naar de ECID-methoden worden verplaatst:

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`

      [&#x200B; Documentatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=nl-NL)

   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`

      [&#x200B; Documentatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=nl-NL)

   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `idSyncSSLUseAkamai`

      [&#x200B; Documentatie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=nl-NL)

   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

      [&#x200B; Documentatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=nl-NL)
