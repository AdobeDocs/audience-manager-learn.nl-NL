---
title: Algemene validatie van apparaat-id
description: Leer over bevestiging van apparaat IDs die naar de globale gegevensbronnen voor juiste formattering wordt verzonden en over foutenmelding wanneer IDs verkeerd geformatteerd is.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Algemene validatie van apparaat-id {#global-device-id-validation}

Identificatienummers voor advertenties van apparaten (iDFA, GAID, Roku ID) hebben opmaakstandaarden die moeten worden nageleefd om te kunnen worden gebruikt in het ecosysteem voor digitale reclame. Vandaag, kunnen de klanten en de partners IDs aan onze Globale gegevensbronnen in om het even welk formaat uploaden zonder op de hoogte worden gebracht van of identiteitskaart behoorlijk geformatteerd is. Deze functie introduceert validatie van apparaat-id&#39;s die naar de algemene gegevensbronnen worden verzonden voor een correcte opmaak en geeft foutberichten wanneer id&#39;s onjuist zijn opgemaakt. We ondersteunen validatie voor [!DNL iDFA], [!DNL Google Advertising] en [!DNL Roku IDs] bij het opstarten.

## Overzicht van opmaakstandaarden {#overview-of-format-standards}

Hieronder vindt u de algemene advertenties-id-pools voor apparaten die momenteel worden herkend en ondersteund door AAM. Deze worden geïmplementeerd als gedeelde [!UICONTROL Data Sources] die door om het even welke klant of gegevenspartner kunnen worden gebruikt die met gegevens verbonden aan gebruikers van deze platforms werken.

<table>
  <tr>
   <td>Platform </td>
   <td>Gegevensbron-id AAM </td>
   <td>ID-indeling </td>
   <td>AAM PID </td>
   <td>Notities </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 hexadecimale getallen, in het algemeen weergegeven als 8-4-4-4-12<em>voorbeeld 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Deze id moet worden verzameld in een onbewerkte/ongewijzigde vorm Referentie - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 hexadecimale getallen, in het algemeen weergegeven als 8-4-4-4-12 <em>voorbeeld, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Deze id moet worden verzameld in een onbewerkte/ongewijzigde vorm Referentie - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 hexadecimale getallen, in het algemeen weergegeven als 8-4-4-4-12 <em>voorbeeld</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Deze id moet worden verzameld in een onbewerkte/ongewijzigde vorm Referentie - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>Microsoft-advertentie-ID (MAID)</td>
   <td>389146</td>
   <td>Numerieke tekenreeks</td>
   <td>14593</td>
   <td>Deze id moet worden verzameld in een onbewerkte/ongewijzigde vorm Referentie - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Voorbeeld van alfanumerieke tekenreeks, 7XCBNROQJQPYW</td>
   <td>15950</td>
   <td>Deze id moet worden verzameld in een onbewerkte/ongewijzigde vorm Referentie - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Een advertentie-id instellen in de app {#setting-an-advertising-identifier-in-the-app}

Het instellen van de adverteerder-id in de app is eigenlijk twee stappen: eerst de adverteerder-id ophalen en vervolgens naar de Experience Cloud sturen. Hieronder vindt u koppelingen voor het uitvoeren van deze stappen.

1. De id ophalen
   1. [!DNL Apple] informatie over de [!DNL advertising ID] kan worden gevonden [HIER](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Informatie over het instellen van de [!DNL advertiser ID] for [!DNL Android] ontwikkelaars kunt u vinden [HIER](http://android.cn-mirrors.com/google/play-services/id.html).
1. Verzend het in de Experience Cloud gebruikend [!DNL setAdvertisingIdentifier] in de SDK
   1. Informatie voor gebruik `setAdvertisingIdentifier` bevindt zich in de [documentatie](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) voor beide [!DNL iOS] en [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## DCS-foutbericht voor onjuiste id&#39;s  {#dcs-error-messaging-for-incorrect-ids}

Wanneer een onjuiste globale apparaat-id (IDFA, GAID, enz.) in realtime wordt verzonden naar de Audience Manager, wordt een foutcode geretourneerd bij de hit. Hieronder ziet u een voorbeeld van een geretourneerde fout omdat de id als een [!DNL Apple IDFA], die alleen hoofdletters mag bevatten, maar er staat een kleine letter &#39;x&#39; in de ID.

![foutafbeelding](assets/image_4_.png)

Zie de [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=nl-NL#api-and-sdk-code) voor de lijst met foutcodes.

## Algemene apparaat-id&#39;s aan boord {#onboarding-global-device-ids}

Naast realtime verzending van Global Device ID&#39;s kunt u ook &quot;[!DNL onboard]&quot;(upload) gegevens ook met de id&#39;s. Dit proces is het zelfde als wanneer u gegevens tegen uw klant IDs (typisch via sleutel/waardeparen) opneemt, maar u zou eenvoudig de juiste Gegevensbron IDs gebruiken, zodat de gegevens aan globale apparatenidentiteitskaart worden toegewezen. Documentatie over het instapproces vindt u in het [documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=nl-NL#implementation-integration-guides). Denk eraan dat u de globale gegevensbron-id wilt gebruiken, afhankelijk van het platform dat u gebruikt.

Als onjuiste globale apparaat-id&#39;s worden verzonden via het instapproces, worden de fouten weergegeven in het dialoogvenster [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=nl-NL#reporting).

Hieronder ziet u een voorbeeld van een fout die in dat rapport wordt vermeld:

![foutafbeelding](assets/image_5_.png)
