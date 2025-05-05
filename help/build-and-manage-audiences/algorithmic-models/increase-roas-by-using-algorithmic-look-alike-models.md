---
title: ROAS verhogen door Algorithmic (look-Alike) Models te gebruiken
description: De echte kracht van look-alike Modeling van de Audience Manager komt wanneer u probeert uw basislijnpubliek tegen een kwaliteit uit te breiden, gloednieuwe reeks gebruikers van de tweede en derde gegevensbronnen. Leer in deze zelfstudie de stappen om een model te maken van deze gegevens.
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
source-wordcount: '909'
ht-degree: 0%

---

# ROAS verhogen door de Modellen van Algorithmic (kijkt-Alike) in Audience Manager te gebruiken {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

De echte kracht van Audience Manager&#39;s look-alike [!UICONTROL Modeling] komt wanneer u probeert om uw basislijnpubliek tegen een kwaliteit uit te breiden, gloednieuwe reeks gebruikers van tweede - en derdegegevensbronnen. Leer in deze zelfstudie de stappen die nodig zijn om een model te maken van deze gegevens.

## Gegevensstromen van derden of derden inschakelen vanuit de Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Als u gegevens van derden en derden wilt gebruiken in een look-alike-model, moeten we deze gegevens eerst inschakelen in de interface van de Audience Manager. Adobe heeft een groot aantal secundaire en externe gegevensproviders waaruit u kunt kiezen. Deze zijn beschikbaar voor u in een zelf-serverinterface in AAM, via de Audience Marketplace. Navigeer naar de Audience Marketplace en blader door de mogelijkheden. In de volgende video ziet u hoe u dit kunt doen, inclusief hoe u gratis streams kunt inschakelen voordat u deze koopt, zodat u zich op de gegevens kunt aanmelden die het nuttigst zijn voor uw organisatie voordat u de prijs van de gegevensaanbieder doorvoert.

Om u te helpen zoeken en te beslissen welke gegevensleverancier u moet gebruiken, is een groot middel [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identificeer of creeer een ideaal gebruiker (omzetting) bezit of segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Wat probeert u mensen op uw site te laten doen? Wat is uw conversiegebeurtenis? Natuurlijk, zijn er vele verschillende antwoorden op deze vraag, afhankelijk van uw plaatstype/verticaal en uw organisatorische doelstellingen. In ieder geval is het in AAM om een kenmerk te creëren voor bezoekers die aan deze criteria hebben voldaan.

In de onderstaande video zal ik u laten zien hoe u een conversiekenmerk maakt dat u wilt gebruiken terwijl u doorgaat met deze zelfstudie en een model maakt dat lijkt op het model.

Wanneer u Adobe Analytics-gebeurtenissen gebruikt om kenmerken te maken, moet u ook rekening houden met een grote gotcha, zodat u niet meer gebruikers verzamelt dan u zou moeten doen. Bekijk de volgende video voor de grote openbaring. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OPMERKING:** In de video hierboven gaat het voorbeeld dat ik toon ervan uit dat je Adobe Analytics hebt. Dat is natuurlijk niet het geval. Als u Google Analytics (GA) hebt, hebben wij een module die u kunt gebruiken om gegevens naar AAM te verzenden (zie [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=nl-NL)) en als uw conversieactiviteiten op uw site naar AAM worden verzonden door GA, kunt u de conversietekenmerken daarvan maken. Als u een andere analytische oplossing hebt (of geen analytische oplossing), kunt u nog steeds gegevens naar AAM sturen via onze DIL code en de `submit` functie, enz. (zie de [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=nl-NL)). Maak vervolgens de conversietekenmerken op basis van de gegevens die worden verzonden wanneer de conversieactiviteit op de site wordt uitgevoerd.

## Een model met een visuele gelijkenis maken op basis van gegevens van derden of derden {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Na het voltooien van de bovenstaande stappen zijn we nu klaar om een Algorithmic (Look-alike)-model te maken. Terwijl wij het model opzetten, zullen wij de omzettingseigenschap als ons basisbezit (zeer belangrijke bezoekers gebruiken die wij willen dupliceren), en wij zullen de toegelaten derdegegevensstroom als onze pool van mensen gebruiken om uit te trekken.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Belangrijke beste praktijken {#an-important-best-practice}

Bij het maken van het algoritmische model in de Audience Manager willen we natuurlijk dat het model zo effectief mogelijk is. Aangezien in het model alle kenmerken in aanmerking worden genomen waarvan de leden van het basiskenmerk/segment deel uitmaken, is het niet nuttig om het model te gebruiken als ALLE personen zich in een kenmerk/segment bevinden. Daarom als u om het even welke supergenerische eigenschappen hebt (zoals iedereen die naar uw plaats ging, of iedereen die om het even welke advertentie van u, enz. heeft ontvangen), zorg ervoor dat de gegevensbron die zij tot behoren NIET inbegrepen in de gegevensbronnen in uw model is. In het gebruiksgeval van dit artikel is het onwaarschijnlijk dat u dit doet, omdat we ons richten op het bekijken van gegevens van derden voor onze nieuwe look-alies, maar het is de moeite van het vermelden waard, en het is van toepassing op ALLE van uw algoritmische modellen.

## Een [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

Nu moeten we een  [!UICONTROL Algorithmic Trait], zodat de resultaten van het model kunnen worden gebruikt. Zonder een eigenschap te creëren, is het model nutteloos. Zorg er dus voor dat u, nadat het model is uitgevoerd, het dialoogvenster Handtekening opent en een [!UICONTROL Algorithmic Trait]. De volgende video doorloopt het en toont een paar uiteinden.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Maak een segment van de modelgegevens en verzend het naar DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Als u eenmaal een [!UICONTROL Algorithmic Trait], kunt u een nieuw segment maken om het in te zetten, zodat u de gegevens kunt activeren (u kunt een eigenschap niet activeren, maar een nieuw segment met één kenmerk maken met de [!UICONTROL Algorithmic Trait] zodat u het segment kunt activeren (gebruiken).

Als u een segment hebt gemaakt op basis van deze algoritmische eigenschap, hebt u een publiek van potentiële klanten die eruitzien als mensen die al op uw site zijn geconverteerd. Nu kunt u dit segment aan om het even welk van uw DSP bestemmingen in Audience Manager in kaart brengen. U kunt uw marketing richten aan die blik-alikes, die eerder op uw plaats dan enkel het normale publiek zullen omzetten, die uw Terugkeer op Advertentie verhogen.
