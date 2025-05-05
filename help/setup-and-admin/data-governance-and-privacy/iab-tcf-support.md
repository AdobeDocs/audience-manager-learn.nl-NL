---
title: IAB TCF 2.2-ondersteuning
description: Meer informatie over de plug-in Audience Manager in IAB TCF en over de manier waarop deze werkt met het aanmeldingsobject van de Adobe en de CMP (Consent Management Provider).
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

De Adobe voorziet u van de middelen om de privacykeuzen van uw gebruikers te beheren en mee te delen door de Opt-in functionaliteit en door de Plug-in van de Audience Manager aan de Transparantie van IAB en de Steun van het Kader 2.2 van de Goedkeuring (TCF 2.2). Dit artikel werkt samen met de documentatie om u te helpen de Plug-in van de Audience Manager aan IAB TCF begrijpen en hoe het samen met het Opt-in voorwerp van de Adobe en uw Consent Management Provider (CMP) werkt. Om meer over IAB te leren, gelieve hun Website in [ https://www.iabeurope.eu/ ](https://www.iabeurope.eu/) te zien.

## Eerste stap: Inloggen met Experience Cloud-id {#first-step-understand-ecid-s-opt-in}

Als u wilt weten hoe u met IAB TCF werkt, moet u eerst de functionaliteit [!DNL Opt-in] begrijpen. Deze functionaliteit maakt deel uit van de ECID-bibliotheek (Experience Cloud ID Service). Als u niet vertrouwd met hoe opt-in werken bent, te zien gelieve [ dit nuttige artikel ](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html?lang=nl-NL) eerst. U zou ook de Opt-in [ documentatie ](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=nl-NL) moeten herzien. Als u deze bronnen hebt doorlopen, gaat u terug naar deze pagina en gaat u verder.

## De plug-in Audience Manager voor IAB TCF {#the-audience-manager-plug-in-for-iab-tcf}

Nu u tenminste een basiskennis hebt van de werking van de Opt-in-service, kunt u de Audience Manager erop plaatsen met ondersteuning voor [!DNL IAB Transparency and Consent Framework (TCF)] . Dit gebeurt via een plug-in in het Opt-in-object.

De insteekmodule van de Audience Manager voor IAB TCF breidt de functionaliteit van toe Opt-binnen uit, en laat AAM klanten toe om, de keuzen van de gebruikersprivacy aan stroomafwaartse partners in overeenstemming met IAB TCF te evalueren, te respecteren en door:sturen. Het verstrekt een norm dat de gegevenscontrolemechanismen (dat u als klant van de Adobe) en verkopers (DMPs, DSP, SSPs, Advertentieservers, enz. is) kan worden gebruikt om instemming in het hele toestemmingslandschap te begrijpen.

## IAB TCF inschakelen {#enabling-iab-tcf}

Het inschakelen van de plug-in Audience Manager voor IAB TCF is eenvoudig als u Adobe Experience Platform Launch gebruikt, omdat dit een eenvoudig selectievakje is, zoals in de korte video hieronder wordt getoond:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Als u Launch niet gebruikt, kunt u `isIabContext=true` gebruiken om het in te schakelen wanneer u de Bezoeker van het Experience Cloud instantieert. Dit stelt de stroom IAB TCF in werking, d.w.z. voegt een andere stap aan toestemmingsinzameling toe, gebruikend IAB TCF om voor het koord te vragen IAB TC en het terug te verstrekken aan Opt-binnen, die dan dan met de oplossingen van het Experience Cloud communiceert.

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

Een ander deel van de IAB TC-reeks bestaat uit een lange lijst met honderden leveranciers, zodat bezoekers een lijst kunnen krijgen met relevante leveranciers die tags op de site hebben en kunnen kiezen welke leveranciers u wilt gebruiken. Leveranciers behouden hun plaats in de lijst. Het Adobe Audience Manager-leveranciernummer in deze lijst is bijvoorbeeld 565. Als dat nummer in de lijst een &#39;1&#39; heeft, kan de Audience Manager de goedgekeurde doeleinden uitvoeren vanaf de voorkant van de lijst. Als AAM vlek &quot;0&quot;heeft, kan het niets met de gegevens doen.

**voor Audience Manager om een UI voor klanten te verstrekken om IAB TCF te gebruiken om deze doeleinden en verkopers te kiezen, of al activiteit goed te keuren/af te keuren, moet u een partner gebruiken CMP die met IAB TCF wordt geregistreerd of bouwt die IAB TCF steunt en met IAB TCF wordt geregistreerd.**

## Inschakelen: omzetten tussen IAB- en Adobe-toepassingen {#opt-in-translating-between-iab-and-adobe-solutions}

Een van de voordelen van het gebruik van IAB TCF is dat de hierboven vermelde standaarddoeleinden de eindgebruiker waarschijnlijk meer van een idee van geven wat zij dan een lijst van Adobe oplossingen goedkeuren. Eindgebruikers weten wellicht niet wat het betekent om Audience Manager of [!DNL Target] goed te keuren, maar &quot;Opslaan en/of toegang krijgen tot informatie over een apparaat&quot; of &quot;Producten ontwikkelen en verbeteren&quot; is voor hen waarschijnlijk eenvoudiger om te begrijpen en ermee in te stemmen.

Voor de goedkeuring van de Audience Manager (d.w.z. Om ervoor te zorgen dat de vertaling van IAB-doeleinden voor Opt-in AAM &quot;ja&quot;-stem), moet de eindgebruiker instemmen met de hierboven vermelde doelstellingen 1 en 10. Als een van deze twee opties niet is goedgekeurd of als een finder niet is goedgekeurd, worden AAM geen pixelbranden uitgevoerd of cookies ingesteld. Het is ook goed om te weten dat vele klanten eenvoudig verkiezen om de eindgebruiker van &quot;alles of niets&quot;UI te voorzien, die, natuurlijk, het gebruik van Audience Manager (en de andere oplossingen van het Experience Cloud) zou toestaan of verwerpen.

Er is wat grote informatie in de [ documentatie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=nl-NL) over hoe de Audience Manager elektrisch-binnen voor de stroom IAB TCF op zowel de Uitgever als Advertiser gebruiksgevallen van toepassing is.

## IAB: Verzendtoestemming verderop {#iab-sending-consent-downstream}

Wanneer de insteekmodule van de Audience Manager voor IAB TCF wordt gebruikt, zullen de de toestemmingskeuzen van de gebruiker ook naar platform-niveau (derde partij) de syncs van identiteitskaart voor partners worden verzonden die op de Globale Lijst van de Leverancier aanwezig zijn, zodat de partner de informatie van de gebruikerstoestemming heeft en op het kan ook handelen. Deze informatie wordt in twee variabelen verzonden:

* gdpr = 1
* gdpr_permission = [ gecodeerde toestemmingskoord ]

Het voorbehoud is dat als de gebruiker in IAB context is en geen toestemming verleent (of negatieve toestemming verleent), dan de Audience Manager niet het koord van IAB TC bij allen verzamelt, en als dusdanig de vraag laat vallen. Dus in dat geval... geen toestemming voorbij.

## Demo {#demo}

In de onderstaande video ziet u hoe cookies en bakens van ECID en oplossingen worden beïnvloed door de keuzeselecties van de IAB-gebruiker.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Voor meer gedetailleerde informatie over de stop-binnen van de Audience Manager voor IAB TCF 2.2, met inbegrip van hoe te om uit te voeren en te testen, gebruiksgevallen, en werkschema, gelieve te zien de [ documentatie ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=nl-NL).
