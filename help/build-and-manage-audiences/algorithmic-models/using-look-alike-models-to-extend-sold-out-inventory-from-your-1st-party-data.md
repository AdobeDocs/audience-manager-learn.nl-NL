---
title: Use look-alike modellen to extend sales voorraad from first-party data
description: In deze zelfstudie doorlopen we de stappen die u moet uitvoeren om modellen op te zetten en te gebruiken die op look-alike lijken, zodat u een nieuw soort publiek kunt maken en deze als een uitbreiding op uw conversiesegment kunt verkopen.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Use look-alike modellen to extend sales voorraad from first-party data {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

In deze zelfstudie doorlopen we de stappen die u moet uitvoeren voor het instellen en gebruiken van Look-Alike [!UICONTROL Models], zodat u nieuwe look-alike soorten publiek kunt maken en deze kunt verkopen als een uitbreiding op uw conversiesegment.

## Details van hoofdletters/kleine letters gebruiken {#use-case-details}

U bent een uitgever van inhoud. Als u al voorraad voor converters op uw site hebt verkocht, kunt u denken dat uw kans daar eindigt. Ga de look-Alike van AAM in [!UICONTROL Models]. Met deze functie kunt u de verkochte voorraad verder uitbreiden en ook het publiek verkopen van mensen die misschien nog niet zijn omgezet, maar die er net zo uitzien als mensen die zijn omgezet. Dit publiekssegment wordt doorgaans voor minder dan de werkelijke converters verkocht, maar u kunt desondanks aan uw bedrijfsresultaten toevoegen door een extra publieksoptie te bieden aan adverteerders die advertenties op uw site willen plaatsen. Het extra voordeel van dit gebruiksscenario is dat het uitvoeren van dit model op de gegevens van de eerste partij niets kost.

De stappen in deze zelfstudie zijn als volgt:

1. Identificeer/creeer een ideale gebruiker (omzetting) bezit of segment
1. Een model maken met deze conversietaak/dit segment als basisitem
1. Kies [!UICONTROL First party] gegevensbron(nen) in het model en voer het model uit
1. Een [!UICONTROL Algorithmic Trait] uit de modelresultaten en voeg de eigenschap toe aan een segment
1. Het segment aanbieden aan geïnteresseerde adverteerders om de verkoop van het conversiesegment uit te breiden

## Identificeer of creeer een ideaal gebruiker (omzetting) bezit of segment {#identify-create-an-ideal-user-conversion-trait-or-segment}

Wat probeert u mensen op uw site te laten doen? Wat is uw conversiegebeurtenis? Natuurlijk, zijn er vele verschillende antwoorden op deze vraag, afhankelijk van uw plaatstype/verticaal en uw organisatorische doelstellingen. In ieder geval is het in AAM om een kenmerk te creëren voor bezoekers die aan deze criteria hebben voldaan.

In dit geval wordt dit al verondersteld, omdat u de voorraad hebt verkocht voor mensen die converters zijn. In het kader van deze zelfstudie is het echter een goede zaak om deze voor de rest van de gebruikszaak te bespreken.

Ook, wanneer het gebruiken van gebeurtenissen om eigenschappen tot stand te brengen, is er een belangrijk gotcha dat u in mening moet houden, zodat u niet meer gebruikers verzamelt dan u in het bezit zou moeten. Bekijk de volgende video voor de grote openbaring. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**OPMERKING:** In de video hierboven gaat het voorbeeld dat ik toon ervan uit dat je Adobe Analytics hebt. Dat is natuurlijk niet het geval. Als u Google Analytics (GA) hebt, hebben wij een module die u kunt gebruiken om gegevens naar AAM te verzenden (zie [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=nl-NL)) en als uw conversieactiviteiten op uw site naar AAM worden verzonden door GA, kunt u de conversietekenmerken daarvan maken. Als u een andere analytische oplossing hebt (of geen analytische oplossing), kunt u nog steeds gegevens naar AAM sturen via onze DIL code en de `submit` functie, enz. (zie de [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=nl-NL)). Maak vervolgens opnieuw de conversietekenmerken op basis van de gegevens die worden verzonden wanneer de conversieactiviteit op de site wordt uitgevoerd.

## Creeer een blik-gelijkaardig model van eerste-partijgegevens {#creating-a-look-alike-model-from-first-party-data}

In deze stap gaan we een [!UICONTROL First Party] Kijk-naar-model. Dit betekent dat wij niet alleen een eerstepartijomzettingseigenschap/segment voor ons basisbezit/segment (dit zou voor de meeste modellen hoe dan ook normaal zijn) gaan gebruiken, maar wij zullen ook slechts in de pool van eerstepartijgegevens voor meer mensen kijken die als de converters kijken. We zullen niet naar gegevens van derden of derden kijken.

In dit gebruiksgeval is dit belangrijk, omdat we proberen een segment van gebruikers op onze site te maken die er als converters uitzien maar nog niet zijn omgezet, zodat we dit look-alike segment aan geïnteresseerde adverteerders kunnen verkopen.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Een algoritmische eigenschap maken {#creating-an-algorithmic-trait}

Nu moeten we een [!UICONTROL Algorithmic Trait], zodat de resultaten van het model kunnen worden gebruikt. Zonder een eigenschap te creëren, is het model nutteloos. Zorg er dus voor dat u, nadat het model is uitgevoerd, het dialoogvenster Handtekening opent en een [!UICONTROL Algorithmic Trait]. De volgende video doorloopt het en toont een paar uiteinden.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## De [!UICONTROL Algorithmic Segment] aan adverteerders {#offering-the-algorithmic-segment-to-advertisers}

Als u eenmaal een [!UICONTROL Algorithmic Trait], kunt u een nieuw segment maken om het in te zetten, zodat u de gegevens kunt activeren (u kunt een eigenschap niet activeren, maar een nieuw segment met één kenmerk maken met de [!UICONTROL Algorithmic Trait] zodat u het segment kunt activeren (gebruiken).

Nadat u een segment hebt gemaakt van bezoekers van de eerste partij die een score hebben behaald in het model dat lijkt op een look-alike (die er dus uitziet als converters maar nog niet is omgezet), kunt u dit segment aanbieden aan adverteerders op uw site, zelfs nadat u al uw voorraad van de werkelijke converters op uw site hebt verkocht. Dit is een grote manier om dit publiek uit te breiden en extra opbrengst te blijven zien door te gebruiken kijkt-Alike [!UICONTROL Models] in de Audience Manager.
