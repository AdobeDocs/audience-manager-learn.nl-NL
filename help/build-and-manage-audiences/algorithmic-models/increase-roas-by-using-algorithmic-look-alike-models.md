---
title: ROAS verhogen door Algorithmic (look-Alike) Models te gebruiken
description: De echte kracht van Audience Manager Look-alike Modeling wordt geleverd wanneer u uw basispubliek wilt uitbreiden in vergelijking met een kwalitatief hoogstaande, gloednieuwe set gebruikers uit gegevensbronnen van derden en derden. Leer in deze zelfstudie de stappen om een model te maken van deze gegevens.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# ROAS verhogen door algoritmische (look-Alike) modellen in Audience Manager te gebruiken {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

De echte kracht van Audience Manager-look-alike [!UICONTROL Modeling] is wanneer u uw basislijnpubliek wilt uitbreiden in vergelijking met een gloednieuwe reeks gebruikers van externe en externe gegevensbronnen van kwaliteit. Leer in deze zelfstudie de stappen die nodig zijn om een model te maken van deze gegevens.

## Gegevensstromen van derden of derden inschakelen vanuit de Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Als u tweedehands gegevens en gegevens van derden wilt gebruiken in een model dat lijkt op het uiterlijk, moeten we deze gegevens eerst inschakelen in uw Audience Manager-interface. Adobe heeft een groot aantal secundaire en externe gegevensproviders waaruit u kunt kiezen. Deze zijn beschikbaar voor u in een zelfserverinterface in AAM, via de Audience Marketplace. Navigeer naar de Audience Marketplace en blader door de mogelijkheden. In de volgende video ziet u hoe u dit kunt doen, inclusief hoe u gratis streams kunt inschakelen voordat u deze koopt, zodat u zich op de gegevens kunt aanmelden die het nuttigst zijn voor uw organisatie voordat u de prijs van de gegevensaanbieder doorvoert.

Ook, om u te helpen onderzoeken en beslissen over welke gegevensleverancier te gebruiken, is een groot middel [[!DNL Adobe Audience Finder] ](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identificeer of creeer een ideaal gebruiker (omzetting) bezit of segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Wat probeert u mensen op uw site te laten doen? Wat is uw conversiegebeurtenis? Natuurlijk, zijn er vele verschillende antwoorden op deze vraag, afhankelijk van uw plaatstype/verticaal en uw organisatorische doelstellingen. In ieder geval is het in AAM gebruikelijk om een kenmerk te creëren voor bezoekers die aan deze criteria voldoen.

In de onderstaande video zal ik u laten zien hoe u een conversiekenmerk maakt dat u wilt gebruiken terwijl u doorgaat met deze zelfstudie en een model maakt dat lijkt op het model.

Wanneer u Adobe Analytics-gebeurtenissen gebruikt om kenmerken te maken, moet u ook rekening houden met een grote gotcha, zodat u niet meer gebruikers verzamelt dan u zou moeten doen. Bekijk de volgende video voor de grote openbaring. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**NOTA:** in de video hierboven, het voorbeeld dat ik toon veronderstelt dat u Adobe Analytics hebt. Dat is natuurlijk niet het geval. Als u Google Analytics (GA) hebt, hebben wij een module die u kunt gebruiken om gegevens naar AAM (zie de [ documentatie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)) te verzenden, en als uw omzettingsactiviteit op uw plaats door GA naar AAM wordt verzonden, dan kunt u uw omzettingseigenschap van dat tot stand brengen. Als u een andere analyseoplossing hebt (of geen analyseoplossing), kunt u nog steeds gegevens naar AAM verzenden via onze DIL-code en de `submit` -functie, enzovoort. (zie de [ documentatie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). Maak vervolgens de conversietekenmerken op basis van de gegevens die worden verzonden wanneer de conversieactiviteit op de site wordt uitgevoerd.

## Maak een model dat er uitziet van gegevens van derden of derden {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Na het voltooien van de bovenstaande stappen zijn we nu klaar om een Algorithmic (Look-alike)-model te maken. Terwijl wij het model opzetten, zullen wij de omzettingseigenschap als ons basisbezit (zeer belangrijke bezoekers gebruiken die wij willen dupliceren), en wij zullen de toegelaten derdegegevensstroom als onze pool van mensen gebruiken om uit te trekken.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Belangrijke beste praktijken {#an-important-best-practice}

Bij het maken van het algoritmische model in Audience Manager willen we natuurlijk dat het model zo effectief mogelijk is. Aangezien in het model alle kenmerken in aanmerking worden genomen waarvan de leden van het basiskenmerk/segment deel uitmaken, is het niet nuttig om het model te gebruiken als ALLE personen zich in een kenmerk/segment bevinden. Daarom als u om het even welke supergenerische eigenschappen hebt (zoals iedereen die naar uw plaats ging, of iedereen die om het even welke advertentie van u, enz. heeft ontvangen), zorg ervoor dat de gegevensbron die zij tot behoren NIET inbegrepen in de gegevensbronnen in uw model is. In het gebruiksgeval van dit artikel is het onwaarschijnlijk dat u dit doet, omdat we ons richten op het bekijken van gegevens van derden voor onze nieuwe look-alies, maar het is de moeite van het vermelden waard, en het is van toepassing op ALLE van uw algoritmische modellen.

## Een [!UICONTROL Algorithmic Trait] maken {#creating-an-algorithmic-trait}

Vervolgens moeten we een [!UICONTROL Algorithmic Trait] maken, zodat de resultaten van het model kunnen worden gebruikt. Zonder een eigenschap te creëren, is het model nutteloos. Nadat het model is uitgevoerd, moet u dus het dialoogvenster Handtekening openen en een [!UICONTROL Algorithmic Trait] maken. De volgende video doorloopt het en toont een paar uiteinden.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Creeer een segment van de modelgegevens en verzend het naar DSPs {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Nadat u een [!UICONTROL Algorithmic Trait] hebt gemaakt, kunt u een nieuw segment maken om het in te zetten, zodat u de gegevens kunt activeren (u kunt een eigenschap niet activeren, maar u moet er een nieuw segment met één kenmerk maken met de [!UICONTROL Algorithmic Trait] erin, zodat u het segment kunt activeren (gebruiken).

Als u een segment hebt gemaakt op basis van deze algoritmische eigenschap, hebt u een publiek van potentiële klanten die eruitzien als mensen die al op uw site zijn geconverteerd. Nu kunt u dit segment toewijzen aan al uw DSP-doelen in Audience Manager. U kunt uw marketing richten aan die blik-alikes, die eerder op uw plaats dan enkel het normale publiek zullen omzetten, die uw Terugkeer op Advertentie verhogen.
