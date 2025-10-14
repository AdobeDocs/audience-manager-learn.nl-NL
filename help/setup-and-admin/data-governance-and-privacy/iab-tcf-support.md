---
title: IAB TCF 2.2-ondersteuning
description: Meer informatie over de Audience Manager-plug-in naar IAB TCF en over de manier waarop deze werkt met het Adobe-aanmeldingsobject en de CMP-provider (Consent Management Provider).
feature: Data Governance & Privacy
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: f9708e705d95b43084ff11e342dc54ff11d6326c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# IAB TCF 2.2-ondersteuning in Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe biedt u de middelen om de privacykeuzes van uw gebruikers te beheren en door te geven via de aanmeldingsfunctionaliteit en via de Audience Manager-plug-in naar IAB Transparency and Consent Framework 2.2 (TCF 2.2) ondersteuning. Dit artikel werkt samen met de documentatie om u te helpen de Plug-in van Audience Manager aan IAB TCF begrijpen en hoe het samen met het Opt-in van Adobe voorwerp en uw Consent Management Provider (CMP) werkt. Om meer over IAB te leren, gelieve hun Website in [&#x200B; https://www.iabeurope.eu/ &#x200B;](https://www.iabeurope.eu/) te zien.

## Eerste stap: Inloggen met Experience Cloud-id {#first-step-understand-ecid-s-opt-in}

Als u wilt weten hoe u met IAB TCF werkt, moet u eerst de functionaliteit [!DNL Opt-in] begrijpen, die deel uitmaakt van de Experience Cloud ID Service-bibliotheek. Als u niet vertrouwd met hoe opt-in werken bent, te zien gelieve [&#x200B; dit nuttige artikel &#x200B;](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html?lang=nl-NL) eerst. U zou ook de Opt-in [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) moeten herzien. Als u deze bronnen hebt doorlopen, gaat u terug naar deze pagina en gaat u verder.

## De Audience Manager-insteekmodule voor IAB TCF {#the-audience-manager-plug-in-for-iab-tcf}

Nu u tenminste een basiskennis hebt van de werking van de Opt-in-service, kan Audience Manager er een laag op plaatsen [!DNL IAB Transparency and Consent Framework (TCF)] -ondersteuning, die via een plug-in in het Opt-in-object wordt uitgevoerd.

De Audience Manager-insteekmodule voor IAB TCF breidt de functionaliteit van Opt-in uit en biedt AAM-klanten de mogelijkheid om privacykeuzes van gebruikers te evalueren, te respecteren en door te sturen naar downstreampartners in overeenstemming met IAB TCF. Het verstrekt een norm dat de gegevenscontrolemechanismen (dat u als klant van Adobe) en verkopers (DMPs, DSPs, SSPs, Advertentieservers, etc.) kunnen gebruiken om toestemming over het toestemmingslandschap te begrijpen.

## IAB TCF inschakelen {#enabling-iab-tcf}

Het inschakelen van de Audience Manager-plug-in voor IAB TCF is eenvoudig als u Adobe Experience Platform Launch gebruikt, omdat dit een eenvoudig selectievakje is, zoals in de korte video hieronder wordt getoond:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Als u Launch niet gebruikt, kunt u `isIabContext=true` gebruiken om het in te schakelen wanneer u de Experience Cloud-bezoeker instantieert. Dit stelt de stroom IAB TCF in werking, d.w.z. voegt een andere stap aan toestemmingsinzameling toe, gebruikend IAB TCF om voor het koord te vragen IAB TC en het terug te verstrekken aan Opt-binnen, die dan dan met de oplossingen van Experience Cloud communiceert.

## IAB TC-tekenreeks {#iab-tcf-consent-string}

Een van de standaarden die IAB biedt, is een &quot;toestemmingstekenreeks&quot; (ook wel een &quot;DaisyBit&quot; genoemd), die eigenlijk twee lijsten zijn die worden samengesteld:

1. Doelstellingen: **wat** toestemming wordt gegeven om te doen?
1. Leveranciers: **Who** wordt toestemming gegeven aan?

### Doelstellingen {#purposes}

Met IAB TCF 2.2, zijn er tien &quot;doeleinden&quot;waarvoor om toestemming te verzamelen (wat de verkopers met de gegevens van de bezoeker kunnen doen). Adobe Audience Manager vereist niet alle tien, maar alleen toestemming voor de volgende doeleinden, naast toestemming van de leverancier:

* **Doel 1:** opslag en/of toegangsinformatie over een apparaat;
* **Doel 10:** ontwikkelt en verbetert producten;
* **Speciaal Doel 1:** verzekert veiligheid, verhindert fraude, en zuivert.

Dit is het eerste deel van de IAB TC-tekenreeks en wordt alleen opgenomen als &#39;1&#39; en &#39;0&#39;, en bepaalt of dat doel of die activiteit wordt goedgekeurd of niet.

>[!NOTE]
>
>Conform IAB-regels is Speciale doelstelling 1 (Beveiliging, Fraude voorkomen en fouten opsporen) altijd goedgekeurd en kunnen gebruikers er geen bezwaar tegen maken.

### Leveranciers {#vendors}

Een ander deel van de IAB TC-reeks bestaat uit een lange lijst met honderden leveranciers, zodat bezoekers een lijst kunnen krijgen met relevante leveranciers die tags op de site hebben en kunnen kiezen welke leveranciers u wilt gebruiken. Leveranciers behouden hun plaats in de lijst. Het Adobe Audience Manager-leveranciernummer in deze lijst is bijvoorbeeld 565. Als dat nummer in de lijst een &#39;1&#39; heeft, kan Audience Manager de goedgekeurde doeleinden uitvoeren vanaf de voorkant van de lijst. Als de plaats van de AAM &quot;0&quot;heeft, kan het niets met de gegevens doen.

**voor Audience Manager om een UI voor klanten te verstrekken om IAB TCF te gebruiken om deze doeleinden en verkopers te kiezen, of al activiteit goed te keuren/af te keuren, moet u een partner gebruiken CMP die met IAB TCF wordt geregistreerd of bouwt die IAB TCF steunt en met IAB TCF wordt geregistreerd.**

## Inschakelen: omzetten tussen IAB- en Adobe-toepassingen {#opt-in-translating-between-iab-and-adobe-solutions}

Een van de voordelen van het gebruik van de IAB TCF is dat de hierboven vermelde standaarddoeleinden de eindgebruiker waarschijnlijk meer een idee geven van wat zij goedkeuren dan een lijst van de oplossingen van Adobe. Eindgebruikers weten wellicht niet wat het betekent om Audience Manager of [!DNL Target] goed te keuren, maar &quot;Opslaan en/of toegang krijgen tot informatie op een apparaat&quot; of &quot;Producten ontwikkelen en verbeteren&quot; is voor hen waarschijnlijk eenvoudiger om te begrijpen en ermee in te stemmen.

Voor de goedkeuring van Audience Manager (d.w.z. Om ervoor te zorgen dat de IAB-doeleinden voor Opt-in worden vertaald en AAM &quot;ja&quot; kunnen stemmen, moeten de doelstellingen 1 en 10, zoals hierboven vermeld, door de eindgebruiker worden goedgekeurd. Als een van deze twee opties niet is goedgekeurd of als een finder niet is goedgekeurd, voert AAM geen pixelbranden uit of worden cookies ingesteld. Het is ook goed om te weten dat veel klanten er gewoon voor kiezen om de eindgebruiker een interface &quot;alles of niets&quot; te bieden, die natuurlijk het gebruik van Audience Manager (en de andere Experience Cloud-oplossingen) zou toestaan of weigeren.

Er is één of andere grote informatie in de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=nl-NL) over hoe de stop-binnen van Audience Manager voor de stroom van IAB TCF op zowel de Uitgever als Advertiser gebruiksgevallen van toepassing is.

## IAB: Verzendtoestemming verderop {#iab-sending-consent-downstream}

Wanneer de insteekmodule Audience Manager voor IAB TCF wordt gebruikt, zullen de de toestemmingskeuzen van de gebruiker ook naar platform-niveau (derde partij) de syncs van identiteitskaart voor partners worden verzonden die op de Globale Lijst van de Leverancier aanwezig zijn, zodat de partner de informatie van de gebruikerstoestemming heeft en op het kan ook handelen. Deze informatie wordt in twee variabelen verzonden:

* gdpr = 1
* gdpr_permission = [ gecodeerde toestemmingskoord ]

Het voorbehoud is dat als de gebruiker in de context van IAB is en geen toestemming (of negatieve toestemming verstrekt), dan Audience Manager niet het koord van IAB TC bij allen verzamelt, en als dusdanig de vraag laat vallen. Dus in dat geval... geen toestemming voorbij.

## Demo {#demo}

In de onderstaande video ziet u hoe cookies en bakens van ECID en oplossingen worden beïnvloed door de keuzeselecties van de IAB-gebruiker.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Voor meer gedetailleerde informatie over de stop-binnen van Audience Manager voor IAB TCF 2.2, met inbegrip van hoe te om uit te voeren en te testen, gebruiksgevallen, en werkschema, gelieve te zien de [&#x200B; documentatie &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=nl-NL).
