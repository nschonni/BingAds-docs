---
title: BidMultiplier Data Object - Campaign Management
ms.service: bing-ads-campaign-management-service
ms.topic: "article"
ms.date: 11/1/2017
author: eric-urban
ms.author: eur
description: Defines the multiplier by which to adjust your base bid for the corresponding criterion.
---
# BidMultiplier Data Object - Campaign Management
Defines the multiplier by which to adjust your base bid for the corresponding criterion.

## Syntax
```xml
<xs:complexType name="BidMultiplier" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:complexContent mixed="false">
    <xs:extension base="tns:CriterionBid">
      <xs:sequence>
        <xs:element minOccurs="0" name="Multiplier" type="xs:double" />
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

## <a name="elements"></a>Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="multiplier"></a>Multiplier|The percentage amount that you want to adjust the bid for the corresponding criterion. <br/><br/>For most criterion types the valid bid multiplier range is -90.00 through 900.00. For exceptions, see [DeviceCriterion Usage](#devicecriterion) and [LocationIntentCriterion Usage](#locationintentcriterion) below.<br/><br/>**Add:** Required<br/>**Update:** Required|**double**|

The [BidMultiplier](bidmultiplier.md) object has [Inherited Elements](#inheritedelements).

## <a name="inheritedelements"></a>Inherited Elements

### <a name="inheritedelementscriterionbid"></a>Inherited Elements from CriterionBid
The [BidMultiplier](bidmultiplier.md) object derives from the [CriterionBid](criterionbid.md) object, and inherits the following elements. The descriptions below are specific to [BidMultiplier](bidmultiplier.md), and might not apply to other objects that inherit the same elements from the [CriterionBid](criterionbid.md) object.  

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="type"></a>Type|The type of the criterion bid. This value is *BidMultiplier* when you retrieve a bid multiplier. For more information about criterion types, see the [CriterionBid Data Object Remarks](../campaign-management-service/criterionbid.md#remarks).<br/><br/>**Add:** Read-only<br/>**Update:** Read-only|**string**|

## <a name="remarks"></a>Remarks
### <a name="devicecriterion"></a>DeviceCriterion Usage
If the *Criterion* property of the [BiddableCampaignCriterion](../campaign-management-service/biddablecampaigncriterion.md) or [BiddableAdGroupCriterion](../campaign-management-service/biddableadgroupcriterion.md) object is a [DeviceCriterion](../campaign-management-service/devicecriterion.md), please note the following usage of *BidMultiplier* properties.

#### <a name="devicecriterion_multiplier"></a>Multiplier
Supported values are -100 (negative one hundred) through positive 900 (nine hundred) percent. Setting the bid adjustment to -100 percent will result in the exclusion of the corresponding *DeviceName* for the [DeviceCriterion](../campaign-management-service/devicecriterion.md). 

### <a name="locationintentcriterion"></a>LocationIntentCriterion Usage
If the *Criterion* property of the [BiddableCampaignCriterion](../campaign-management-service/biddablecampaigncriterion.md) or [BiddableAdGroupCriterion](../campaign-management-service/biddableadgroupcriterion.md) object is a [LocationIntentCriterion](../campaign-management-service/locationintentcriterion.md), please note the following usage of *BidMultiplier* properties.

#### <a name="locationintentcriterion_multiplier"></a>Multiplier
You cannot bid on a location intent criterion. The service will ignore the multiplier without returning any error.

## Requirements
Service: [CampaignManagementService.svc v11](https://campaign.api.bingads.microsoft.com/Api/Advertiser/CampaignManagement/v11/CampaignManagementService.svc)  
Namespace: https://bingads.microsoft.com/CampaignManagement/v11  
