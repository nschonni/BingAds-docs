---
title: GetBidOpportunities Service Operation
ms.service: bing-ads-ad-insight
ms.topic: article
author: eric-urban
ms.author: eur
---
# GetBidOpportunities Service Operation
Gets the keyword bid opportunities of the specified ad group.

> [!NOTE]
> Currently bid opportunities are only available in the United States. It is not recommended to use this service operation for accounts in other markets.

## <a name="request"></a>Request Elements
The *GetBidOpportunitiesRequest* object defines the [body](#request-body) and [header](#request-header) elements of the service operation request. The elements must be in the same order as shown in the [Request SOAP](#request-soap). 

### <a name="request-body"></a>Request Body Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="adgroupid"></a>AdGroupId|The identifier of the ad group for which you want to determine keyword bid opportunities.<br /><br />If this element is nil or empty, the operation will return all bid opportunities for the specified campaign.|**long**|
|<a name="campaignid"></a>CampaignId|The identifier of the campaign that owns the ad group specified in the *AdGroupId* element.<br /><br />If this element is nil or empty, then the *AdGroupId* must also be nil or empty, and the operation will return all bid opportunities for the account.|**long**|
|<a name="opportunitytype"></a>OpportunityType|Determines the type or types of bid opportunities corresponding to your ad position goals.<br /><br />**Note:** The operation will only return opportunities if there?s a suggested increase within 100% of your current bid that will help you achieve the specified goal.|[BidOpportunityType](bidopportunitytype.md)|

### <a name="request-header"></a>Request Header Elements
[!INCLUDE[request-header](./includes/request-header.md)]

## <a name="response"></a>Response Elements
The *GetBidOpportunitiesResponse* object defines the [body](#response-body) and [header](#response-header) elements of the service operation response. The elements are returned in the same order as shown in the [Response SOAP](#response-soap).

### <a name="response-body"></a>Response Body Elements

|Element|Description|Data Type|
|-----------|---------------|-------------|
|<a name="opportunities"></a>Opportunities|An array of *BidOpportunity* objects that identifies the keywords whose clicks and impressions may increase if you were to apply the suggested match-type bid value.<br /><br />Up to 500 opportunities of each *OpportunityType* will be returned for the account.|[BidOpportunity](bidopportunity.md) array|

### <a name="response-header"></a>Response Header Elements
[!INCLUDE[response-header](./includes/response-header.md)]

## <a name="request-soap"></a>Request SOAP
The following template shows the order of the [body](#request-body) and [header](#request-header) elements for the SOAP request.

```xml
<s:Envelope xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header xmlns="Microsoft.Advertiser.AdInsight.Api.Service.V11">
    <Action mustUnderstand="1">GetBidOpportunities</Action>
    <ApplicationToken i:nil="false">ValueHere</ApplicationToken>
    <AuthenticationToken i:nil="false">ValueHere</AuthenticationToken>
    <CustomerAccountId i:nil="false">ValueHere</CustomerAccountId>
    <CustomerId i:nil="false">ValueHere</CustomerId>
    <DeveloperToken i:nil="false">ValueHere</DeveloperToken>
    <Password i:nil="false">ValueHere</Password>
    <UserName i:nil="false">ValueHere</UserName>
  </s:Header>
  <s:Body>
    <GetBidOpportunitiesRequest xmlns="Microsoft.Advertiser.AdInsight.Api.Service.V11">
      <AdGroupId i:nil="false">ValueHere</AdGroupId>
      <CampaignId i:nil="false">ValueHere</CampaignId>
      <OpportunityType>ValueHere</OpportunityType>
    </GetBidOpportunitiesRequest>
  </s:Body>
</s:Envelope>
```

## <a name="response-soap"></a>Response SOAP
The following template shows the order of the [body](#response-body) and [header](#response-header) elements for the SOAP response.

```xml
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Header xmlns="Microsoft.Advertiser.AdInsight.Api.Service.V11">
    <TrackingId d3p1:nil="false" xmlns:d3p1="http://www.w3.org/2001/XMLSchema-instance">ValueHere</TrackingId>
  </s:Header>
  <s:Body>
    <GetBidOpportunitiesResponse xmlns="Microsoft.Advertiser.AdInsight.Api.Service.V11">
      <Opportunities xmlns:e469="http://schemas.datacontract.org/2004/07/Microsoft.BingAds.Advertiser.AdInsight.Api.DataContract.V11.Entity" d4p1:nil="false" xmlns:d4p1="http://www.w3.org/2001/XMLSchema-instance">
        <e469:BidOpportunity>
          <e469:AdGroupId>ValueHere</e469:AdGroupId>
          <e469:CampaignId>ValueHere</e469:CampaignId>
          <e469:CurrentBid>ValueHere</e469:CurrentBid>
          <e469:EstimatedIncreaseInClicks>ValueHere</e469:EstimatedIncreaseInClicks>
          <e469:EstimatedIncreaseInCost>ValueHere</e469:EstimatedIncreaseInCost>
          <e469:EstimatedIncreaseInImpressions>ValueHere</e469:EstimatedIncreaseInImpressions>
          <e469:KeywordId>ValueHere</e469:KeywordId>
          <e469:MatchType d4p1:nil="false">ValueHere</e469:MatchType>
          <e469:SuggestedBid>ValueHere</e469:SuggestedBid>
        </e469:BidOpportunity>
      </Opportunities>
    </GetBidOpportunitiesResponse>
  </s:Body>
</s:Envelope>
```

## <a name="example"></a>Code Syntax
```csharp
protected async Task<GetBidOpportunitiesResponse> GetBidOpportunitiesAsync(
	long adGroupId,
	long campaignId,
	BidOpportunityType opportunityType)
{
	var request = new GetBidOpportunitiesRequest
	{
		AdGroupId = adGroupId,
		CampaignId = campaignId,
		OpportunityType = opportunityType
	};

	return (await AdInsight.CallAsync((s, r) => s.GetBidOpportunitiesAsync(r), request));
}
```
```java
static GetBidOpportunitiesResponse getBidOpportunities(
	long adGroupId,
	long campaignId,
	BidOpportunityType opportunityType)
{
	GetBidOpportunitiesRequest request = new GetBidOpportunitiesRequest();

	request.setAdGroupId(adGroupId);
	request.setCampaignId(campaignId);
	request.setOpportunityType(opportunityType);

	return AdInsight.getService().getBidOpportunities(request);
}
```
```php
static function GetBidOpportunities(
	$adGroupId,
	$campaignId,
	$opportunityType)

	$getBidOpportunitiesRequest = new GetBidOpportunitiesRequest();

	$request->AdGroupId = $adGroupId;
	$request->CampaignId = $campaignId;
	$request->OpportunityType = $opportunityType;

	return $AdInsightProxy->GetService()->GetBidOpportunities($request);
}
```
```python
response=adinsight.GetBidOpportunities(
	AdGroupId=AdGroupIdHere,
	CampaignId=CampaignIdHere,
	OpportunityType=OpportunityTypeHere
)
```

## Requirements
Service: [AdInsightService.svc v11](https://adinsight.api.bingads.microsoft.com/Api/Advertiser/AdInsight/v11/AdInsightService.svc)  
Namespace: Microsoft.Advertiser.AdInsight.Api.Service.V11  
