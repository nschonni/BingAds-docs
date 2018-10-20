---
title: ResponsiveSearchAd Data Object - Campaign Management
ms.service: bing-ads-campaign-management-service
ms.topic: article
author: eric-urban
ms.author: eur
description: Reserved.
---
# ResponsiveSearchAd Data Object - Campaign Management
Reserved.

## Syntax
```xml
<xs:complexType name="ResponsiveSearchAd" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:complexContent mixed="false">
    <xs:extension base="tns:Ad">
      <xs:sequence>
        <xs:element minOccurs="0" name="Descriptions" nillable="true" type="tns:ArrayOfAssetLink" />
        <xs:element minOccurs="0" name="Domain" nillable="true" type="xs:string" />
        <xs:element minOccurs="0" name="Headlines" nillable="true" type="tns:ArrayOfAssetLink" />
        <xs:element minOccurs="0" name="Path1" nillable="true" type="xs:string" />
        <xs:element minOccurs="0" name="Path2" nillable="true" type="xs:string" />
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

## <a name="elements"></a>Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="descriptions"></a>Descriptions|Reserved.|[AssetLink](assetlink.md) array|
|<a name="domain"></a>Domain|Reserved.|**string**|
|<a name="headlines"></a>Headlines|Reserved.|[AssetLink](assetlink.md) array|
|<a name="path1"></a>Path1|Reserved.|**string**|
|<a name="path2"></a>Path2|Reserved.|**string**|

The [ResponsiveSearchAd](responsivesearchad.md) object has [Inherited Elements](#inheritedelements).

## <a name="inheritedelements"></a>Inherited Elements

### <a name="inheritedelementsad"></a>Inherited Elements from Ad
The [ResponsiveSearchAd](responsivesearchad.md) object derives from the [Ad](ad.md) object, and inherits the following elements. The descriptions below are specific to [ResponsiveSearchAd](responsivesearchad.md), and might not apply to other objects that inherit the same elements from the [Ad](ad.md) object.  

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="adformatpreference"></a>AdFormatPreference|Reserved.|**string**|
|<a name="devicepreference"></a>DevicePreference|Reserved.|**long**|
|<a name="editorialstatus"></a>EditorialStatus|Reserved.|[AdEditorialStatus](adeditorialstatus.md)|
|<a name="finalappurls"></a>FinalAppUrls|Reserved.|[AppUrl](appurl.md) array|
|<a name="finalmobileurls"></a>FinalMobileUrls|Reserved.|**string** array|
|<a name="finalurls"></a>FinalUrls|Reserved.|**string** array|
|<a name="forwardcompatibilitymap"></a>ForwardCompatibilityMap|Reserved.|[KeyValuePairOfstringstring](keyvaluepairofstringstring.md) array|
|<a name="id"></a>Id|Reserved.|**long**|
|<a name="status"></a>Status|Reserved.|[AdStatus](adstatus.md)|
|<a name="trackingurltemplate"></a>TrackingUrlTemplate|Reserved.|**string**|
|<a name="type"></a>Type|Reserved.|[AdType](adtype.md)|
|<a name="urlcustomparameters"></a>UrlCustomParameters|Reserved.|[CustomParameters](customparameters.md)|

## Requirements
Service: [CampaignManagementService.svc v12](https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v12/CampaignManagementService.svc)  
Namespace: https\://bingads.microsoft.com/CampaignManagement/v12  

