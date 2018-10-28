---
title: "Responsive Search Ad Record - Bulk"
ms.service: bing-ads-bulk-service
ms.topic: "article"
author: "eric-urban"
ms.author: "eur"
description: Describes the Responsive Search Ad fields in a Bulk file.
dev_langs:
  - csharp
---
# Responsive Search Ad Record - Bulk
Defines a responsive search ad format for text ads in the Search network that can be downloaded and uploaded in a bulk file.

> [!NOTE]
> Not everyone has this feature yet. If you don't, don't worry. It's coming soon. 

> [!WARNING]
> As of November 1st, 2018 responsive search ads are only available via the Bing Ads API. You cannot yet view or manage responsive search ads via the Bing Ads web application. 
> 
> When you create responsive search ads the [Description](#description) and [Headline](#headline) lists are stored as text assets that can be shared by any responsive search ad within the account. For example if *Seemless Integration* is a text asset, it will have the same asset identifier across all ads in the same Bing Ads account. Even after you delete all ads that use (are linked to) *Seemless Integration*, the text asset will remain in your account with a unique system identifier. The next time you use *Seemless Integration* in an ad, it will retain the original Bing Ads system identifier. Currently Bing Ads does not support retrieval or deletion of account assets. 

Responsive search ads allow you to set between 3-15 unique ad headlines (a.k.a. "titles") and 2-4 ad descriptions within a single ad. From there, Bing will select the most relevant headline and description combination for each given query and corresponding search user. By allowing Bing AI to select the most relevant headloine and description for each query, we ensure that the right message lands for each of your potential customers, at the right time, across all possible intent signals. 

The responsive ads shown to users appear identical to expanded text ads i.e., up to 3 headlines (title parts via expanded text ads) and 2 descriptions (text parts via expanded text ads). Two headlines and one description will always be shown in the ad. However, depending on the screen size, your ad may show without the third headline or second description.

This ad format works seamlessly on mobile, tablet and desktop devices so you can focus more on crafting your longer ad copy and optimizing your ad text to better engage your customers before they click your ad. 

## <a name="entitydata"></a>Attribute Fields in the Bulk File
For a *Responsive Search Ad* record, the following attribute fields are available in the [Bulk File Schema](bulk-file-schema.md). The combination of the Description, Headline, Final Url, Path 1, and Path 2 fields make the responsive search ad unique.  

- [Ad Format Preference](#adformatpreference)
- [Ad Group](#adgroup)
- [Campaign](#campaign)
- [Client Id](#clientid)
- [Custom Parameter](#customparameter)
- [Description](#description)
- [Domain](#domain)
- [Editorial Appeal Status](#editorialappealstatus)
- [Editorial Location](#editoriallocation)
- [Editorial Reason Code](#editorialreasoncode)
- [Editorial Status](#editorialstatus)
- [Editorial Term](#editorialterm)
- [Final Url](#finalurl)
- [Headline](#headline)
- [Id](#id)
- [Mobile Final Url](#mobilefinalurl)
- [Modified Time](#modifiedtime)
- [Parent Id](#parentid)
- [Path 1](#path1)
- [Path 2](#path2)
- [Publisher Countries](#publishercountries)
- [Status](#status)
- [Tracking Template](#trackingtemplate)

You can download all fields of the *Responsive Search Ad* record by including the [DownloadEntity](downloadentity.md) value of *ResponsiveSearchAds* in the [DownloadCampaignsByAccountIds](downloadcampaignsbyaccountids.md) or [DownloadCampaignsByCampaignIds](downloadcampaignsbycampaignids.md) service request. Additionally the download request must include the [DataScope](datascope.md) value of *EntityData*. For more information, see [Bulk Download and Upload](../guides/bulk-download-upload.md).

The following Bulk CSV example would add a new responsive search ad given a valid ad group ID (*Parent Id*). 

```csv
Type,Status,Id,Parent Id,Campaign,Ad Group,Client Id,Modified Time,Ad Format Preference,Name,App Platform,App Id,Final Url,Mobile Final Url,Tracking Template,Custom Parameter,Description,Path 1,Path 2,Domain,Headline
Format Version,,,,,,,,,6,,,,,,,,,,,
Responsive Search Ad,Active,,-1111,ParentCampaignNameGoesHere,AdGroupNameHere,ClientIdGoesHere,,False,,,,http://www.contoso.com/womenshoesale,http://mobile.contoso.com/womenshoesale,,{_promoCode}=PROMO1; {_season}=summer,"[{""id"":null,""text"":""Find New Customers & Increase Sales!"",""pinnedField"":""Description1"",""editorialStatus"":null},{""id"":null,""text"":""Start Advertising on Contoso Today."",""pinnedField"":""Description2"",""editorialStatus"":null}]",seattle,shoe sale,,"[{""id"":null,""text"":""Contoso"",""pinnedField"":""Headline1"",""editorialStatus"":null},{""id"":null,""text"":""Quick & Easy Setup"",""pinnedField"":null,""editorialStatus"":null},{""id"":null,""text"":""Seemless Integration"",""pinnedField"":null,""editorialStatus"":null}]"
```

If you are using the [Bing Ads SDKs](../guides/client-libraries.md) for .NET, Java, or Python, you can save time using the *BulkServiceManager* to upload and download the *BulkResponsiveSearchAd* class (coming soon), instead of calling the service operations directly and writing custom code to parse each field in the bulk file. 


```csharp
var uploadEntities = new List<BulkEntity>();

// Map properties in the Bulk file to the BulkResponsiveSearchAd
var bulkResponsiveSearchAd = new BulkResponsiveSearchAd
{
    // 'Parent Id' column header in the Bulk file
    AdGroupId = adGroupIdKey,
    // 'Ad Group' column header in the Bulk file
    AdGroupName = "AdGroupNameHere",
    // 'Campaign' column header in the Bulk file
    CampaignName = "ParentCampaignNameGoesHere",
    // 'Client Id' column header in the Bulk file
    ClientId = "ClientIdGoesHere",

    // Map properties in the Bulk file to the 
    // ResponsiveSearchAd object of the Campaign Management service.
    ResponsiveSearchAd = new ResponsiveSearchAd
    {
        // 'Ad Format Preference' column header in the Bulk file
        AdFormatPreference = "All",
        // 'Description' column header in the Bulk file
        Descriptions = new AssetLink[]
        {
            // Each AssetLink is represented as a JSON list item in the Bulk file.
            new AssetLink
            {
                Asset = new TextAsset
                {
                    Id = null,
                    Text = "Find New Customers & Increase Sales!"
                },
                PinnedField = "Description1"
            },
            new AssetLink
            {
                Asset = new TextAsset
                {
                    Id = null,
                    Text = "Start Advertising on Contoso Today."
                },
                PinnedField = "Description2"
            },
        },
        // 'Mobile Final Url' column header in the Bulk file
        FinalMobileUrls = new[] {
            // Each Url is delimited by a semicolon (;) in the Bulk file
            "http://mobile.contoso.com/womenshoesale"
        },
        // 'Final Url' column header in the Bulk file
        FinalUrls = new[] {
            // Each Url is delimited by a semicolon (;) in the Bulk file
            "http://www.contoso.com/womenshoesale"
        },
        // 'Headline' column header in the Bulk file
        Headlines = new AssetLink[]
        {
            // Each AssetLink is represented as a JSON list item in the Bulk file.
            new AssetLink
            {
                Asset = new TextAsset
                {
                    Id = null,
                    Text = "Contoso"
                },
                PinnedField = "Headline1"
            },
            new AssetLink
            {
                Asset = new TextAsset
                {
                    Id = null,
                    Text = "Quick & Easy Setup"
                },
                PinnedField = null
            },
            new AssetLink
            {
                Asset = new TextAsset
                {
                    Id = null,
                    Text = "Seemless Integration"
                },
                PinnedField = null
            },
        },
        // 'Id' column header in the Bulk file
        Id = responsiveSearchAdIdKey,
        // 'Path 1' column header in the Bulk file
        Path1 = "seattle",
        // 'Path 2' column header in the Bulk file
        Path2 = "shoe sale",
        // 'Status' column header in the Bulk file
        Status = AdStatus.Active,
        // 'Tracking Template' column header in the Bulk file
        TrackingUrlTemplate = null,
        // 'Custom Parameter' column header in the Bulk file
        UrlCustomParameters = new CustomParameters
        {
            // Each custom parameter is delimited by a semicolon (;) in the Bulk file
            Parameters = new[] {
                new CustomParameter(){
                    Key = "promoCode",
                    Value = "PROMO1"
                },
                new CustomParameter(){
                    Key = "season",
                    Value = "summer"
                },
            }
        },
    },
};

uploadEntities.Add(bulkResponsiveSearchAd);

var entityUploadParameters = new EntityUploadParameters
{
    Entities = uploadEntities,
    ResponseMode = ResponseMode.ErrorsAndResults,
    ResultFileDirectory = FileDirectory,
    ResultFileName = DownloadFileName,
    OverwriteResultFile = true,
};

var uploadResultEntities = (await BulkService.UploadEntitiesAsync(entityUploadParameters)).ToList();
```

### <a name="adformatpreference"></a>Ad Format Preference
The *Ad Format Preference* field is used to indicate whether or not you prefer the ad copy to be shown to users as a search or audience ad. Search ads tend to be written as a call to action, whereas audience ads should be written in more of an informational style. While you have the option to use responsive search ads as audience ads, designating an ad as Audience ads preferred format allows you to optimize its messaging for native delivery. 

> [!IMPORTANT]
> You must define at least one responsive search ad per ad group that does not prefer audience ads, otherwise the ad copy of all responsive search ads will be eligible for both search and audience ads. 

Possible values are *Audience Ad* and *All*. If set to *All*, the ad will be eligible for both search and audience ad formats. If set to *Audience Ad*, the ad will only be eligible for the audience ad format.

**Add:** Optional. If you do not set this field when creating a responsive search ad, by default the ad format preference will be set to *All*.  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed. If you set this field to *delete_value* when updating a responsive search ad, the ad format preference will be set to the default value i.e. *All*.    
**Delete:** Read-only  

### <a name="adgroup"></a>Ad Group
The name of the ad group that contains the ad.

**Add:** Read-only and Required  
**Update:** Read-only and Required  
**Delete:** Read-only and Required  

> [!NOTE]
> For add, update, and delete, you must specify either the *Parent Id* or *Ad Group* field.

### <a name="campaign"></a>Campaign
The name of the campaign that contains the ad group and ad.

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="clientid"></a>Client Id
Used to associate records in the bulk upload file with records in the results file. The value of this field is not used or stored by the server; it is simply copied from the uploaded record to the corresponding result record. It may be any valid string to up 100 in length.

**Add:** Optional  
**Update:** Optional    
**Delete:** Read-only  

### <a name="customparameter"></a>Custom Parameter
Your custom collection of key and value parameters for URL tracking.

In a bulk file, the list of custom parameters are formatted as follows.

- Format each custom parameter pair as Key=Value, for example {_promoCode}=PROMO1.

- You may include up to 3 custom parameter key and value pairs. Each key and value pair are delimited by a semicolon and space ("; "), for example {_promoCode}=PROMO1; {_season}=summer.

- A Key cannot contain a semicolon. If a Value contains a semicolon it must be escaped as '\;'. Additionally if the Value contains a backslash it must also be escaped as '\\'.

- The Key cannot exceed 16 UTF-8 bytes, and the Value cannot exceed 200 UTF-8 bytes. The maximum size of the Key does not include the braces and underscore i.e., '{', '_', and '}'. 

    > [!NOTE] 
    > With the Bulk service the Key must be formatted with surrounding braces and a leading underscore, for example if the Key is promoCode, it must be formatted as {_promoCode}. With the Campaign Management service you cannot specify the surrounding braces and underscore.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed. To remove all custom parameters, set this field to *delete_value*. The *delete_value* keyword removes the previous setting. To remove a subset of custom parameters, specify the custom parameters that you want to keep and omit any that you do not want to keep. The new set of custom parameters will replace any previous custom parameter set.    
**Delete:** Read-only  

### <a name="description"></a>Description
The list of descriptions that Bing can use to optimize the ad layout.

Unless you pin one of the descriptions to a specific position, Bing will optimize the ad layout dynamically with the best headlines and descriptions for the user's search query. 

From a data model perspective the descriptions are stored as text assets. The same asset can be used by multiple ads. For example if *Seemless Integration* is a text asset, it will have the same asset identifier across all ads in the same Bing Ads account. 

You must set between 2-4 descriptions. Each description is represented in the bulk file as a JSON string. Two descriptions are included in the example JSON below, and both are pinned to specific positions. The `id` and `text` are properties of the asset, whereas the `editorialStatus` and `pinnedField` are properties of the asset link i.e., the relationship between the asset and the ad. For more details see [editorialStatus](#description-editorialstatus), [id](#description-id), [pinnedField](#description-pinnedfield), and [text](#description-text) below.

```json
[{
	"id": null,
	"text": "Find New Customers & Increase Sales!",
	"pinnedField": "Description1",
	"editorialStatus": null
},
{
	"id": null,
	"text": "Start Advertising on Contoso Today.",
	"pinnedField": "Description2",
	"editorialStatus": null
}]
```

> [!NOTE]
> In the comma separated bulk file you'll need to surround the list of asset links and each attribute with an extra set of double quotes e.g., the above JSON string would be written as *"[{""id"":null,""text"":""Find New Customers & Increase Sales!"",""pinnedField"":""Description1"",""editorialStatus"":null},{""id"":null,""text"":""Start Advertising on Contoso Today."",""pinnedField"":""Description2"",""editorialStatus"":null}]"*.

#### <a name="description-editorialstatus"></a>editorialStatus
The `editorialStatus` attribute is read-only when you download the responsive search ad. Possible values are described in the table below.  

|Value|Description|
|-----------|---------------|
|Active|The asset passed editorial review.|
|ActiveLimited|The asset passed editorial review in one or more markets, and one or more elements of The asset is undergoing editorial review in another market. For example The asset passed editorial review for Canada and is still pending review in the United States.|
|Disapproved|The asset failed editorial review.|
|Inactive|One or more elements of The asset is undergoing editorial review.|
|Unknown|Reserved for future use.|

#### <a name="description-id"></a>id
The `id` attribute is a unique Bing Ads identifier for the asset in a Bing Ads account. 

The same asset can be used by multiple ads. For example if *Seemless Integration* is a text asset, it will have the same asset identifier across all ads in the same Bing Ads account. After you upload a text asset the result file will include the asset identifier e.g., `""id:""123`, whether the asset is new or already existed in the account's asset library. 

#### <a name="description-pinnedfield"></a>pinnedField
To pin an asset to a specific description position, set the `pinnedField` attribute to either *Description1* or *Description2*. 

#### <a name="description-text"></a>text
The maximum input length of each `text` attribute is 1,000 characters including dynamic text strings, and of those 1,000 no more than 90 final characters are allowed after substitution. For languages with double-width characters e.g. Traditional Chinese the maximum input length is 500 characters including dynamic text strings, and of those 500 no more than 45 final characters are allowed after substitution.

The text can contain a countdown function. Regardless of the total length of all unsubstituted countdown parameters, the final displayed countdown will always use 8 characters out of the total characters available. For more details see [Countdown Customizers](../guides/countdown-customizers.md). 

The text can contain dynamic text strings such as {keyword}. For more information, see the Bing Ads help article [Automatically customize your ads with dynamic text parameters](http://help.bingads.microsoft.com/#apex/3/en/50811/1).

The maximum input length is 1,000 characters including dynamic text strings, and of those 1,000 no more than 90 final characters are allowed after substitution. The ad will fail to display if the length exceeds 90 characters after dynamic text substitution occurs.

For languages with double-width characters e.g. Traditional Chinese the maximum input length is 500 characters including dynamic text strings, and of those 500 no more than 45 final characters are allowed after substitution. The ad will fail to display if the length exceeds 45 characters after dynamic text substitution occurs. The double-width characters are determined by the characters you use instead of the character set of the campaign or ad group language settings. Double-width characters include Korean, Japanese and Chinese languages characters as well as Emojis.

The text cannot contain the newline (\n) character.

**Add:** Required. The list of 3-15 descriptions is required. Only the [pinnedField](#description-pinnedfield) and [text](#description-text) are honored. Even if the asset already exists in your account, the [id](#description-id) and [editorialStatus](#description-editorialstatus) will be ignored if you include them. 
**Update:** Optional. To retain all of the existing asset links, set or leave this field empty. If you set this field, any descriptions that were previously linked to this ad will be replaced. If you specify this field, a list of 3-15 descriptions is required. Only the [pinnedField](#description-pinnedfield) and [text](#description-text) are honored. Even if the asset already exists in your account, the [id](#description-id) and [editorialStatus](#description-editorialstatus) will be ignored if you include them.   
**Delete:** Read-only  

### <a name="domain"></a>Domain
The URL that will be displayed instead of the final URL. The final URL will still be used for the landing page URL.

Reserved for limited pilot usage e.g. pharmaceutical customers.

The domain portion of the URL in combination with the path 1 and path 2 strings cannot exceed 67 characters.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.     
**Delete:** Read-only 

### <a name="editorialappealstatus"></a>Editorial Appeal Status
Determines whether you can appeal the issues found by the editorial review.

Possible values include *Appealable*, *AppealPending*, and *NotAppealable*. For more details, see [AppealStatus Value Set](../campaign-management-service/appealstatus.md).

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="editoriallocation"></a>Editorial Location
The component or property of the ad that failed editorial review. 

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="editorialreasoncode"></a>Editorial Reason Code
A code that identifies the reason for the failure. For a list of possible reason codes, see [Editorial Reason Codes](../guides/editorial-failure-reason-codes.md). 

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="editorialstatus"></a>Editorial Status
The editorial status of the ad.

Possible values include *Active*, *ActiveLimited*, *Disapproved*, and *Inactive*. For more details, see [AdEditorialStatus Value Set](../campaign-management-service/adeditorialstatus.md).

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="editorialterm"></a>Editorial Term
The term that failed editorial review.

This field will not be set if a combination of terms caused the failure or if the failure was based on a policy violation.

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="finalurl"></a>Final Url
The landing page URL.

The domain portion of the URL in combination with the path 1 and path 2 strings cannot exceed 67 characters.

The following validation rules apply to Final URLs and Final Mobile URLs.

- The length of the URL is limited to 2,048 characters. The HTTP or HTTPS protocol string does count towards the 2,048 character limit.

- You may specify up to 10 items for both Final URLs and Final Mobile URLs; however, only the first item in each list is used for delivery. The service allows up to 10 for potential forward compatibility.

- Each URL is delimited by a semicolon and space ("; ").

- Usage of '{' and '}' is only allowed to delineate tags, for example "{lpurl}".

- Each URL must be a well-formed URL starting with either http:// or https://.

- If you specify Final Mobile URLs, you must also specify Final Url.

Also note that  if the *Tracking Template* or *Custom Parameter* fields are set, then at least one Final URL is required.

> [!NOTE]
> This URL is used only if the keyword does not specify a final URL.

**Add:** Optional  
**Update:** Optional    
**Delete:** Read-only  

### <a name="headline"></a>Headline
The list of ad titles that Bing can use to optimize the ad layout.

Unless you pin one of the headlines to a specific position, Bing will optimize the ad layout dynamically with the best headlines and descriptions for the user's search query. 

From a data model perspective the headlines are stored as text assets. The same asset can be used by multiple ads. For example if *Seemless Integration* is a text asset, it will have the same asset identifier across all ads in the same Bing Ads account. 

You must set between 3-15 headlines. Each headline is represented in the bulk file as a JSON string. Three headlines are included in the example JSON below, and only the first headline is pinned to specific position. The `id` and `text` are properties of the asset, whereas the `editorialStatus` and `pinnedField` are properties of the asset link i.e., the relationship between the asset and the ad. For more details see [editorialStatus](#headline-editorialstatus), [id](#headline-id), [pinnedField](#headline-pinnedfield), and [text](#headline-text) below.

```json
[{
	"id": null,
	"text": "Contoso",
	"pinnedField": "Headline1",
	"editorialStatus": null
},
{
	"id": null,
	"text": "Quick & Easy Setup",
	"pinnedField": null,
	"editorialStatus": null
},
{
	"id": null,
	"text": "Seemless Integration",
	"pinnedField": null,
	"editorialStatus": null
}]
```

> [!NOTE]
> In the comma separated bulk file you'll need to surround the list of asset links and each attribute with an extra set of double quotes e.g., the above JSON string would be written as *"[{""id"":null,""text"":""Contoso"",""pinnedField"":""Headline1"",""editorialStatus"":null},{""id"":null,""text"":""Quick & Easy Setup"",""pinnedField"":null,""editorialStatus"":null},{""id"":null,""text"":""Seemless Integration"",""pinnedField"":null,""editorialStatus"":null}]"*.

#### <a name="headline-editorialstatus"></a>editorialStatus
The `editorialStatus` attribute is read-only when you download the responsive search ad. Possible values are described in the table below.  

|Value|Description|
|-----------|---------------|
|Active|The asset passed editorial review.|
|ActiveLimited|The asset passed editorial review in one or more markets, and one or more elements of The asset is undergoing editorial review in another market. For example The asset passed editorial review for Canada and is still pending review in the United States.|
|Disapproved|The asset failed editorial review.|
|Inactive|One or more elements of The asset is undergoing editorial review.|
|Unknown|Reserved for future use.|

#### <a name="headline-id"></a>id
The `id` attribute is a unique Bing Ads identifier for the asset in a Bing Ads account. 

The same asset can be used by multiple ads. For example if *Seemless Integration* is a text asset, it will have the same asset identifier across all ads in the same Bing Ads account. After you upload a text asset the result file will include the asset identifier e.g., `""id:""123`, whether the asset is new or already existed in the account's asset library. 

#### <a name="headline-pinnedfield"></a>pinnedField
To pin an asset to a specific headline position, set the `pinnedField` attribute to either *Headline1*, *Headline2*, or *Headline3*.

#### <a name="headline-text"></a>text
The maximum input length of each `text` attribute is 1,000 characters including dynamic text strings, and of those 1,000 no more than 90 final characters are allowed after substitution. For languages with double-width characters e.g. Traditional Chinese the maximum input length is 500 characters including dynamic text strings, and of those 500 no more than 45 final characters are allowed after substitution.

The text can contain a countdown function. Regardless of the total length of all unsubstituted countdown parameters, the final displayed countdown will always use 8 characters out of the total characters available. For more details see [Countdown Customizers](../guides/countdown-customizers.md). 

The text can contain dynamic text strings such as {keyword}. For more information, see the Bing Ads help article [Automatically customize your ads with dynamic text parameters](http://help.bingads.microsoft.com/#apex/3/en/50811/1).

The maximum input length is 1,000 characters including dynamic text strings, and of those 1,000 no more than 90 final characters are allowed after substitution. The ad will fail to display if the length exceeds 90 characters after dynamic text substitution occurs.

For languages with double-width characters e.g. Traditional Chinese the maximum input length is 500 characters including dynamic text strings, and of those 500 no more than 45 final characters are allowed after substitution. The ad will fail to display if the length exceeds 45 characters after dynamic text substitution occurs. The double-width characters are determined by the characters you use instead of the character set of the campaign or ad group language settings. Double-width characters include Korean, Japanese and Chinese languages characters as well as Emojis.

The text cannot contain the newline (\n) character.

**Add:** Required. The list of 2-4 headlines is required. Only the [pinnedField](#headline-pinnedfield) and [text](#headline-text) are honored. Even if the asset already exists in your account, the [id](#headline-id) and [editorialStatus](#headline-editorialstatus) will be ignored if you include them. 
**Update:** Optional. To retain all of the existing asset links, set or leave this field empty. If you set this field, any descriptions that were previously linked to this ad will be replaced. If you specify this field, a list of 2-4 headlines is required. Only the [pinnedField](#headline-pinnedfield) and [text](#headline-text) are honored. Even if the asset already exists in your account, the [id](#headline-id) and [editorialStatus](#headline-editorialstatus) will be ignored if you include them.   
**Delete:** Read-only  


### <a name="id"></a>Id
The system generated identifier of the ad.

**Add:** Read-only  
**Update:** Read-only and Required  
**Delete:** Read-only and Required  

### <a name="mobilefinalurl"></a>Mobile Final Url
The mobile landing page URL.

The following validation rules apply to Final URLs and Final Mobile URLs.

- The length of the URL is limited to 2,048 characters. The HTTP or HTTPS protocol string does count towards the 2,048 character limit.

- You may specify up to 10 items for both Final URLs and Final Mobile URLs; however, only the first item in each list is used for delivery. The service allows up to 10 for potential forward compatibility.

- Each URL is delimited by a semicolon and space ("; ").

- Usage of '{' and '}' is only allowed to delineate tags, for example "{lpurl}".

- Each URL must be a well-formed URL starting with either http:// or https://.

- If you specify Final Mobile URLs, you must also specify Final Url.

> [!NOTE]
> This URL is used only if the keyword does not specify a *Mobile Final Url*.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.    
**Delete:** Read-only  

### <a name="modifiedtime"></a>Modified Time
The date and time that the entity was last updated. The value is in Coordinated Universal Time (UTC).

> [!NOTE]
> The date and time value reflects the date and time at the server, not the client. For information about the format of the date and time, see the dateTime entry in [Primitive XML Data Types](https://go.microsoft.com/fwlink/?linkid=859198).

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="parentid"></a>Parent Id
The system generated identifier of the ad group that contains the ad.

This bulk field maps to the *Id* field of the [Ad Group](ad-group.md) record.

**Add:** Read-only and Required. You must either specify an existing ad group identifier, or specify a negative identifier that is equal to the *Id* field of the parent [Ad Group](ad-group.md) record. This is recommended if you are adding new ads to a new ad group in the same Bulk file. For more information, see [Bulk File Schema Reference Keys](../bulk-service/bulk-file-schema.md#referencekeys).  
**Update:** Read-only  
**Delete:** Read-only  

> [!NOTE]
> For add, update, and delete, you must specify either the *Parent Id* or *Ad Group* field.

### <a name="path1"></a>Path 1
The first part of the optional path that will be appended to the domain portion of your display URL. The domain portion of your display URL e.g. *http://www.contoso.com* will be generated from the domain of your Final URL (*Final Url* field).  Then if you have specified a value for *Path 1* it will be appended to the display URL. If you have also specified a value for *Path 2*, then it will also be appended to the display URL after *Path 1*. For example if your *Final Url* contains *http://www.contoso.com*, *Path 1* is set to *subdirectory1*, and *Path 2* is set to *subdirectory2*, then the URL displayed will be *http://www.contoso.com/subdirectory1/subdirectory2*.

The path can contain a countdown function. Regardless of the total length of all unsubstituted countdown parameters, the final displayed countdown will always use 8 characters out of the total characters available. For more details see [Countdown Customizers](../guides/countdown-customizers.md). 

The path can contain dynamic parameters such as {MatchType}. For a list of supported parameters, see the Bing Ads help article [What tracking or URL parameters can I use?](https://help.bingads.microsoft.com/#apex/3/en/56799/2).

The maximum input length is 50 characters including dynamic text strings, and of those 50 no more than 15 final characters are allowed after substitution. The ad will fail to display if the length exceeds 15 characters after dynamic text substitution occurs. 

For languages with double-width characters e.g. Traditional Chinese the maximum input length is 25 characters including dynamic text strings, and of those 25 no more than 7 final characters are allowed after substitution. The ad will fail to display if the length exceeds 7 characters after dynamic text substitution occurs. The double-width characters are determined by the characters you use instead of the character set of the campaign or ad group language settings. Double-width characters include Korean, Japanese and Chinese languages characters as well as Emojis.

The path cannot contain the forward slash (/) or newline (\n) characters.

If the path includes a space, it will be replaced with an underscore (_) when the ad is shown.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.    
**Delete:** Read-only  

### <a name="path2"></a>Path 2
The second part of the optional path that will be appended to the domain portion of your display URL. The domain portion of your display URL e.g. *http://www.contoso.com* will be generated from the domain of your Final URL (*Final Url* field).  Then if you have specified a value for *Path 1* it will be appended to the display URL. If you have also specified a value for *Path 2*, then it will also be appended to the display URL after *Path 1*. For example if your *Final Url* contains *http://www.contoso.com*, *Path 1* is set to *subdirectory1*, and *Path 2* is set to *subdirectory2*, then the URL displayed will be *http://www.contoso.com/subdirectory1/subdirectory2*.

You can only specify *Path 2* if *Path 1* is also set.

The path can contain a countdown function. Regardless of the total length of all unsubstituted countdown parameters, the final displayed countdown will always use 8 characters out of the total characters available. For more details see [Countdown Customizers](../guides/countdown-customizers.md). 
	
The path can contain dynamic parameters such as {MatchType}. For a list of supported parameters, see the Bing Ads help article [What tracking or URL parameters can I use?](https://help.bingads.microsoft.com/#apex/3/en/56799/2).

The maximum input length is 50 characters including dynamic text strings, and of those 50 no more than 15 final characters are allowed after substitution. The ad will fail to display if the length exceeds 15 characters after dynamic text substitution occurs. 

For languages with double-width characters e.g. Traditional Chinese the maximum input length is 25 characters including dynamic text strings, and of those 25 no more than 7 final characters are allowed after substitution. The ad will fail to display if the length exceeds 7 characters after dynamic text substitution occurs. The double-width characters are determined by the characters you use instead of the character set of the campaign or ad group language settings. Double-width characters include Korean, Japanese and Chinese languages characters as well as Emojis.

The path cannot contain the forward slash (/) or newline (\n) characters.
	
If the path includes a space, it will be replaced with an underscore (_) when the ad is shown.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.    
**Delete:** Read-only  

### <a name="publishercountries"></a>Publisher Countries
The list of publisher countries whose editorial guidelines do not allow the specified [term](#editorialterm).

In a bulk file, the list of publisher countries are delimited with a semicolon (;).

**Add:** Read-only  
**Update:** Read-only  
**Delete:** Read-only  

### <a name="status"></a>Status
The status of the ad.

Possible values are *Active*, *Paused*, or *Deleted*. 

**Add:** Optional. The default value is *Active*.  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.    
**Delete:** Required. The Status must be set to *Deleted*.

### <a name="trackingtemplate"></a>Tracking Template
The tracking template to use as a default for the URL specified with FinalUrls.

The following validation rules apply to tracking templates. For more details about supported templates and parameters, see the Bing Ads help article [What tracking or URL parameters can I use?](https://help.bingads.microsoft.com/#apex/3/en/56799/2)

- Tracking templates defined for lower level entities e.g. ads override those set for higher level entities e.g. campaign. For more information, see [Entity Hierarchy and Limits](../guides/entity-hierarchy-limits.md).

- The length of the tracking template is limited to 2,048 characters. The HTTP or HTTPS protocol string does count towards the 2,048 character limit.

- The tracking template must be a well-formed URL beginning with one of the following: *http://*, *https://*, *{lpurl}*, or *{unescapedlpurl}*. 

- Bing Ads does not validate whether custom parameters exist. If you use custom parameters in your tracking template and they do not exist, then the landing page URL will include the key and value placeholders of your custom parameters without substitution. For example, if your tracking template is *http://tracker.example.com/?season={_season}&promocode={_promocode}&u={lpurl}*, and neither *{_season}* or *{_promocode}* are defined at the campaign, ad group, criterion, keyword, or ad level, then the landing page URL will be the same.

**Add:** Optional  
**Update:** Optional. If no value is specified on update, this Bing Ads setting is not changed.    
**Delete:** Read-only  
