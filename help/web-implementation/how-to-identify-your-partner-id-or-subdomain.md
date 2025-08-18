---
title: Hoe te om uw partneridentiteitskaart of subdomain te identificeren
description: Leer hoe u uw partner-id of subdomein kunt identificeren wanneer u sommige Experience Cloud-functies implementeert, en over twee plaatsen kunt u deze id ophalen in de gebruikersinterface van Audience Manager.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer, Data Engineer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Hoe identificeert u uw Audience Manager Subdomain {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Wanneer u bepaalde Experience Cloud-functies implementeert, moet u weten wat de Audience Manager `Subdomain` is (ook wel `client ID` of `Partner ID` genoemd). In deze video tonen we u twee plaatsen waar u deze informatie kunt ophalen in de gebruikersinterface van Audience Manager.

## Het einde weggeven... {#giving-away-the-ending}

Als u liever gewoon naar binnen wilt springen en de video wilt zoeken zonder naar deze korte video te kijken, vindt u de `Partner Subdomain` op twee plaatsen in de gebruikersinterface:

1. Als u al een [!UICONTROL rule-based] -kenmerk hebt gemaakt, klikt u op **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] staat naast de eigenschap in de lijst met kenmerken in die map en de URL neemt het subdomein in de URL op.
1. Als u in de interface **[!UICONTROL Tools]** > **[!UICONTROL Tags]** gaat en **[!UICONTROL Get code]** voor uw container klikt, is subdomain tegen het eind van de lijn Akamai

Als u de video niet snel kunt vinden met deze snelle referenties, is de video een korte tijdsreferentie. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Er is een numerieke identiteitskaart die aan elke klant van Adobe Experience Cloud wordt toegewezen, en dit wordt vaak bedoeld als &quot;PID&quot;, of identiteitskaart van de Partner. Dit is niet de id waarover we het in dit artikel en video hebben. In plaats daarvan, is &quot;partnersubdomain&quot;, die soms als partneridentiteitskaart wordt bedoeld, gewoonlijk een versie van de cliëntnaam, en is subdomain van de server waarnaar de gegevens worden verzonden. Bijvoorbeeld, als uw bedrijf &quot;Knopen van Bob&quot;is (alle dingen kleven, natuurlijk, haha), dan is het waarschijnlijk dat uw partner subdomain &quot;knobs&quot;zou zijn, terwijl &quot;PID&quot;iets meer als &quot;12345&quot;zou zijn. Meestal hoeft u uw PID niet te kennen, maar het is belangrijk dat u het subdomein kent, zodat u uw Audience Manager-implementatie kunt configureren.
>
