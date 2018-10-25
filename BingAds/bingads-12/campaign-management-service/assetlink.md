---
title: AssetLink Data Object - Campaign Management
ms.service: bing-ads-campaign-management-service
ms.topic: article
author: eric-urban
ms.author: eur
description: Defines the relationship of an asset to an ad.
---
# AssetLink Data Object - Campaign Management
Defines the relationship of an asset to an ad.

For example, within a [ResponsiveSearchAd](responsivesearchad.md) there is an array of asset links that each contain a [TextAsset](textasset.md). 

> [!NOTE]
> Not everyone has this feature yet. If you don't, don't worry. It's coming soon. 

## Syntax
```xml
<xs:complexType name="AssetLink" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:sequence>
    <xs:element minOccurs="0" name="Asset" nillable="true" type="tns:Asset" />
    <xs:element minOccurs="0" name="AssetPerformanceLabel" nillable="true" type="xs:string" />
    <xs:element minOccurs="0" name="EditorialStatus" nillable="true" type="tns:AssetLinkEditorialStatus" />
    <xs:element minOccurs="0" name="PinnedField" nillable="true" type="xs:string" />
  </xs:sequence>
</xs:complexType>
```

## <a name="elements"></a>Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="asset"></a>Asset|Reserved.|[Asset](asset.md)|
|<a name="assetperformancelabel"></a>AssetPerformanceLabel|Reserved.|**string**|
|<a name="editorialstatus"></a>EditorialStatus|Reserved.|[AssetLinkEditorialStatus](assetlinkeditorialstatus.md)|
|<a name="pinnedfield"></a>PinnedField|Reserved.|**string**|

## Requirements
Service: [CampaignManagementService.svc v12](https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v12/CampaignManagementService.svc)  
Namespace: https\://bingads.microsoft.com/CampaignManagement/v12  

## Used By
[ResponsiveSearchAd](responsivesearchad.md)  
