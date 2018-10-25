---
title: TextAsset Data Object - Campaign Management
ms.service: bing-ads-campaign-management-service
ms.topic: article
author: eric-urban
ms.author: eur
description: A text asset with a unique Bing Ads identifier that can be reused across multiple ads.
---
# TextAsset Data Object - Campaign Management
A text asset with a unique Bing Ads identifier that can be reused across multiple ads. For example, see responsive search ad [Descriptions](responsivesearchad.md#descriptions) and [Headlines](responsivesearchad.md#headlines).

> [!NOTE]
> Not everyone has this feature yet. If you don't, don't worry. It's coming soon. 

## Syntax
```xml
<xs:complexType name="TextAsset" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:complexContent mixed="false">
    <xs:extension base="tns:Asset">
      <xs:sequence>
        <xs:element minOccurs="0" name="Text" nillable="true" type="xs:string" />
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

## <a name="elements"></a>Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="text"></a>Text|The meaning and business rules for the text asset vary depending on where it is used. For example, see responsive search ad [Descriptions](responsivesearchad.md#descriptions) and [Headlines](responsivesearchad.md#headlines).<br/><br/>**Add:** Required<br/>**Update:** Required|**string**|

The [TextAsset](textasset.md) object has [Inherited Elements](#inheritedelements).

## <a name="inheritedelements"></a>Inherited Elements

### <a name="inheritedelementsasset"></a>Inherited Elements from Asset
The [TextAsset](textasset.md) object derives from the [Asset](asset.md) object, and inherits the following elements. The descriptions below are specific to [TextAsset](textasset.md), and might not apply to other objects that inherit the same elements from the [Asset](asset.md) object.  

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="id"></a>Id|The unique Bing Ads identifier for the asset.<br/><br/>**Add:** Read-only<br/>**Update:** Read-only|**long**|
|<a name="name"></a>Name|The asset name.<br/><br/>The case-sensitive asset name can be between 1 to 80 characters in length, and must be unique across all assets in the account.<br/><br/>**Add:** Optional<br/>**Update:** Optional|**string**|
|<a name="type"></a>Type|The type of the asset. This value is *TextAsset* when you retrieve a text asset. For more information about asset types, see the [Asset Data Object Remarks](asset.md#remarks).<br/><br/>**Add:** Read-only<br/>**Update:** Read-only|**string**|

## Requirements
Service: [CampaignManagementService.svc v12](https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v12/CampaignManagementService.svc)  
Namespace: https\://bingads.microsoft.com/CampaignManagement/v12  

