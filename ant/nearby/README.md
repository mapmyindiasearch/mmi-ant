# [Nearby API](#Nearby-API)

Nearby Places API, enables you to add discovery and search of nearby POIs by searching for a generic keyword used to describe a category of places or via the unique code assigned to that category.

 MapmyIndia Nearby API Platform provides following some advance features:

- Customized Radius*
- Custom Category Code
- POD
- Filter
- searchBy

## [Customized Radius](#Customized-Radius)

- The customized radius will be provisioned and managed by Anchor.
- Added **overrideRadiusLimit** claim. It takes radius value(number only) in                                     meters. The value must be greater than 249.
- The behavior works with custom datasets only, such as Honda.
- Customized Radius is min radius : 250m, max radius : 50 Km and by default : 10 Km

## [Custom Category Code](#Custom-Category-Code)
This will enable custom category code based nearby searching for customers(e.g. Honda, HDFC).The search can be performed on the basis of either custom category code or MMI category codes or keywords. The output contains standard fields and a richInfo object for client-specific data. The RichInfo can have dynamic response parameters as per customer requirement. This can be enabled on the basis of configuration provided at the time of onboarding customer data.

- Pass Custom Codes like Keywords.
- The custom code keywords like HNDAUT, HNDREP for searching near pois like Honda Stores.

## [POD](#POD)
Introducing "pod" parameter to search for villages. This parameter accepts "vlg", “CITY”, “LC”, “STATE”, “SLC” as value. The radius for village provides the range of distance. The radius for village search is 50 KM fixed.

## [Filter](#Filter)
The filter feature in Nearby API empowers the user a fine discovery of EV charging stations along with the existing keyword and category code lookups. It uses **key:value** pair(s).
(e.g. brandId:B420)

- Currently, filters are supported on brand id, connector type and car model.
- Each **key:value** pair is seperated by a seperator,
(e.g. filter= brandId:B420, plugType:IEC; model:Mahindra Electric).
- We can use two or more **values** for a **key** by putting either **OR(;)** or **AND($)** operator
(e.g. brandId:B420;B316, plugType:IEC&PN3; model:Mahindra Electric).
- By default key:value pairs are treated as **AND($)** case.

Suppose you want to search all electric vehical charging station of a particular brand(e.g. "Mahindra Electric" ) and of a particular plugType (e.g. "IEC") then you can use filter as:

(filter= brandId:B420, plugType:IEC)

where B420 is brandId for Mahindra Electric and IEC is plugType.

**Keys:** "brandId", "model", "plugType"

## [searchBy](#searchBy)

Search and Sort Nearby Places on the basis of either "Distance" or "Relevance/Importance".

- dist keyword is used to sort result in increasing order of distance, means nearest place related on top.
- imp will use the priority to give important or highest priority result on top.
- By Default it will use Distance

## [Operators](#Operators)

To send multiple keywords in a request, we’ve defined a couple of operators that can help the developers wrap their applications around this functionality. Below are the operators:

- The ; Operator: This operator is an **OR** operator. Defining multiple keywords separated with a ; would provide results that satisfies either of the keywords.\
- The **$** Operator: This operator is an **AND** operator. Defining multiple keywords separated with a $ would provide results that satisfy all the provided keywords. (default).
- The , operator: This operator is a seperator for using two or more **key:value** pairs and it has functionality of **AND($)**

To use these operators, simple just send in the keywords parameter like below:
&keywords=coffee;tea$sea food;alcohol
The above nearby search would yield in results that either provide coffee or tea but must provide either sea food or alcohol.

To use these operators, simple just send in the keywords parameter like below:
&keywords=coffee;tea$sea food;alcohol
The above nearby search would yield in results that either provide coffee or tea but must provide either sea food or alcohol.

**Please Note:** the spacing in the above example is of no relevance to the search result. It’s just there to provide better understanding.

## [Request Headers](#Request-Headers)

The Atlas API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

1. **Authorization:** “{token_type} {access_token}”.

## [Security Type](#Security-Type)
Atlas OAuth 2.0 based security using AES 256 and SHA-1.

## [Response Type](#Response-Type)
- JSON: if the user passed in “/json”. 
- XML: if the user passed in “/xml”

## [Response Messages (as HTTP response message)](#Response-Messages (as HTTP response message))
1. 200: Success. 
2. 204: No matches we’re found for the provided query. 
3. 400: Something’s just not right with the request. 
4. 401: Access Denied. 
5. 403: Services for this key has been suspended due to daily/hourly transactions limit. 
6. 500: Something went wrong. 
7. 503: Maintenance Break.

## [URL](#URL) 
https://atlas.mapmyindia.com/api/places/nearby/json?
## [Method](#Method)
GET 
## [Request Parameters](#Request-Parameters)
The parameters are colour coded based on their requirements. The **“Red”** one’s are mandatory, and the **“black”** one’s are optional and the **“green”** one’s are Claimbased.<br>
**Please Note:** The Restricted parameters are also optional.

a.	<span style="color: Orange">**Mandatory Parameters:** </span>

1.	<span style="color: red"> <b>keywords</b> </span> (string) e.g. FODCOF, Shoes, Coffee, Versace, Gucci, H&M, Adidas, Starbucks, B130 {POI, House Number, keyword, tag}
2.	<span style="color: red"> <b>refLocation</b> </span> {string (latitude[double],longitude[double])}: Provides the location around which the search will be performed. e.g. refLocation=28.454,77.435

b.	<span style="color: Orange"> **Optional Parameters:** </span>

3.	**page** (integer): provides number of the page to provide results from.
4.	**sort** (string): provides configured sorting operations for the client on cloud. Below are the available sorts:

    a) dist:asc & dist:desc - will sort data in order of distance from the passed location (default).

    b) name:asc & name:desc - will sort the data on alphabetically bases.

5.	**bounds** (x1,y1;x2,y2): Allows the developer to send in map bounds to provide a nearby search of the geobounds. where x1,y1 are the lat lng of.
6.	**region** (string): it takes in the country code. LKA, IND, BTN, BGD, NPL for Sri-Lanka, India, Bhutan, Bangladesh, Nepal respectively. Default is India (IND)
7.	**pod** (string): pod is search villages in 50 km radius and This parameter accepts vlg", “CITY”, “LC”, “STATE”, “SLC” as value.

c.	<span style="color: Orange"> **Internal Parameters:** </span>

8.	radius (integer): provides the range of distance to search over (default: 1000, min: 500, max: 10000).
9.	richdata (valueless): provides rich information like reviews, star count on demand e.g. {&richData}
10.	explain (valueless): provides explanation as to why did you receive the result that you’ve received.
11.	bounds (x1,y1;x2,y2): Allows the developer to send in map bounds to provide a nearby search of the geobounds. where x1,y1 are the lat lng of.
12.	Includes (string): Comma separated string that allows to restrict the search for the keyword on specific fields. Fields to search on are

    a)	keyword: the field containing keywords for all locations
    
    b)	brandName: the field containing names of brands that locations belong to.
    
    c)	locationName: the field containing the names of the locations.
    
    d)	popularName: the field containing the popular names of the locations.

## [Claim Request Parameters](#Claim-Request-Parameters)<br>

<table><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span><b>Claims Available</b></span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span><b>Remarks</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;" autocomplete="off"><p><span><b>Claimed Type</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>Possible Values</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>isPublic</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: red">keywords</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>e.g. FODCOF, Shoes, Coffee, Versace, Gucci, H&M, Adidas, Starbucks, B130 {POI, House Number, keyword, tag}</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span style = "color: red">refLocation</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Provides the location around which the search will be performed. e.g. refLocation=28.454,77.435</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span></span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span style = "color: green">overrideRadiusLimit</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>It just takes values in meters.
max 200 kms
</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">defaultEnabled</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>integer
This lets us enable / disable default ANT search when searchFor parameter is given and Contains two values 0, 1. By default, a user has access to MMI data in search. To prevent the user to access the MMI data, set the value of this claim to "0". Removing this claim or setting the value to 1 will allow users to access MMI data.
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>0,1</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">customCategoryCode</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>The custom category codes that should be supported for the particular client</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>HSPTMT,SMISST,HSPTST,HNDAUT,
CLIFVR,FODHNG,SMIBRN,TMPRSN,COVRSN,
HSPCOV,HNDREP,SMIDLR,HSPSCC,HOTNST</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isAllowedCategories*</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Used along with allowedCategories claim so that only limited category search is enabled.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">allowedCategories*</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Allow only given category codes to be search in nearBy</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>HSPTMT,HSPTST,HSPCOV,CLIFVR,HSPSCC,
FODHNG,HOTNST,TMPRSN</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>region</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>It will restrict the region in which the search is applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>lka,mmr,hindi,npl,btn,bgd,ind</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">searchFor</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>string<br>
For searching within specific datasets: like Honda or EV charging stations; depends on <b>defaultEnabled</b>
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>EV,COVID19,HONDA</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">autoExpand</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Allows search to auto expand radius when no result found
<b>overrideRadiusLimit</b> needs to be enabled for this to be used.
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>True, False</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>N</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">customDb</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div><p><span>Whether to search in master or custom index based on <b>searchFor</b> value.</span></p></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div><p><span>Y, N</span></p></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>N</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">Lang</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>to provide access of Indic response, currently supports Hindi only</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>hi</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">showTimings</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>To allow access open_close_hours.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">showAddressTokens</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>To allow access to address tokens.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">showContacts</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>This will show/hide the contact details in output.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isElocSearch</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Search can be done by passing a single eLoc and can be used to enable and disable eLoc based queries. By default, the eLoc based search is disabled for all the users.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">outputFieldsList[list]</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>claim can be provisioned from Anchor to control the output fields</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>addressTokens, distance, eLoc, email, entryLatitude, entryLongitude,
hourOfOperation, keywords, landlineNo, latitude, longitude,
mobileNo, orderIndex, placeAddress, placeName, type
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isPodSearch</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>A marker claim to enable the POD search. The parameter named isPodSearch is of data type LIST</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">pod[List]</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>This claim contains the list of admins to be searched.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>CITY, LC, STATE, SLC</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">itemCount(Number List)</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>The claim can be set to restrict the number of items in the result.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">noPagination</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>This is a marker claim to enable/disable pagination for a user. By default, pagination is enabled for all users.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isRestrictedCategories</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Allow user to search for restricted categories</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">restrictedCategories</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>This will restrict the user from access the categories in this list</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>CNTZON</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isPartnerSearch[list]</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>A marker claim to switch on/off the partner search for a user</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>maruti ev</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">partnerIds[List]</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>This claim can be used to set the partnerIds to be allowed to a user. The values in this claim can be selected from a pre-populated set of values.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr></table>

<table><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span><b>Claims Proposed</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span><b>Remarks</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;" autocomplete="off"><p><span><b>Claimed Type</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>Possible Values</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>isPublic</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>refLocation</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>String<br>
Provides the location around which the search will be performed. e.g. refLocation=28.454,77.435</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Not applicalbe</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Not applicalbe</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>page</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>integer<br>
It provides number of the page to provide results from.
</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>radius</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>integer<br>
radius of search
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Not applicable</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>region</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>string</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>lka,mmr,npl,btn,bgd,ind</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>bounds</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>bounds=lat1, lng1; lat2, lng2 (North West, South East) {e.g. bounds=28.598882, 77.212407; 28.467375, 77.353513}</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style>filter</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>String<br>
Takes in key value pair.<br>
filter= plugType:C2B
where categoryCode is a key<br>
Other keys:<br> 
" brandId:B420", "model", " plugType"
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>categoryCode, brandId,model, plugType</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>sortBy</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>string, possible values.
dist:asc(default)<br>
dist:desc<br>
imp
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>dist, imp</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr></table>

## [Response Parameters](#Response-Parameters)<br>

a.	suggestedLocations ([object])<br>


1.  addresstokens – <br>

    a)	houseNumber(string): The house number of the location.<br>
    b)	houseName(string): The house name of the location.<br>
    c)	poi(string): The name of the POI if the location is a place of interest     (POI).<br>
    d)	street(string): The name of the street of the location.<br>
    e)	subSubLocality(string): The name of the sub-sub-locality where the location exists.<br>
    f)	subLocality(string): The name of the sub-locality where the location exists.<br>
    g)	locality(string): The name of the locality where the location exists.<br>
    h)	village(string): The name of the village if the location exists in a village.<br>
    i)	subDistrict(string): The name of the sub-district in which the location exists.<br>
    j)	district(string): The name of the district in which the location exists.<br>
    k)	city(string): The name of the city in which the location exists.<br>
    l)	state(string): The name of the state in which the location exists.<br>
2.	distance (integer): provides the distance from the provided location bias in meters.<br>
3.	eLoc (string): Place Id of the location 6-char alphanumeric.<br>
4.	email (string): Email for contact.<br>
5.	entryLatitude (double): latitude of the entrance of the location.<br>
6.	entryLongitude (double): longitude of the entrance of the location.<br>
7.	keywords ( [ string ] ): provides an array of matched keywords or codes.<br>
8.	landlineNo (string): Email for contact.<br>
9.	latitude (double): Latitude of the location.<br>
10.	longitude (double): longitude of the location.<br>
11.	mobileNo : Phone number for contact.<br>
12.	orderIndex (integer): the order where this result should be placed<br>
13.	placeAddress (string): Address of the location.<br>
14.	placeName (string): Name of the location.<br>
15.	Richinfo: (string):<br>
    a)	for (string)<br>
    b)	eLoc (string)<br>
    c)	brandName (string)<br>
    d)	ownerType (string)<br>
    e)	privateVsPublic (string)<br>
    f)	buildingType (string)<br>
    g)	macVType (string)<br>
    h)	Active (string)<br>
    i)	oemName (string)<br>
    j)	macType (string)<br>
    k)	macPlugType (string)<br>
    l)	openOrClose (string)<br>
    m)	type (string)<br>

b.	suggestedSearches ([object])<br>


1. 	keyword (string): what the user typed in.<br>
2.	Identifier (string): what did the API use for it to qualify it as a suggested search request<br>
3.	location (string): the name of the location to which the nearby will run in context to.<br>
4.	hyperlink (string): the ready-made link for the nearby API pre-initialized with all default parameters and location with code to search for.<br>


## [Sample Response](#Sample-Response)<br>

<span style="color: Orange">**Input URL:** </span> https://atlasweb.mapmyindia.in/api/places/nearby/json? access_token=<>keywords=coffee&refLocation=28.535247, 77.270918&bridge=<br>

<span style="color: Orange">**Response:** </span><br>
{<br>
  "addresstokens": {<br>
    "houseNumber": "",<br>
    "houseName": "",<br>
    "poi": "Kaffa Cerrado The Roastery",<br>
    "street": "",<br>
    "subSubLocality": "",<br>
    "subLocality": "Block A",<br>
    "locality": "Okhla Industrial Estate Phase 2;Okhla Phase 2;Okhla Industrial Area Phase 2",<br>
    "village": "",<br>
    "subDistrict": "Kalkaji",<br>
    "district": "South East Delhi District",<br>
    "city": "New Delhi",<br>
    "state": "Delhi",<br>
    "pincode": "110020"<br>
  },<br>
  "distance": 419,<br>
  "eloc": "E95G6D",<br>
  "email": "support@kaffacerrado.com",<br>
  "entryLatitude": 28.5391550000001,<br>
  "entryLongitude": 77.2700790000001,<br>
  "hourOfOperation": "Mon-Sun 09:30-18:00",<br>
  "keywords": [<br>
    "FODCOF"<br>
  ],<br>
  "landlineNo": "+911141325350, +911141326705",<br>
  "latitude": 28.5389700000001,<br>
  "longitude": 77.2701960000001,<br>
  "mobileNo": "",<br>
  "orderIndex": 1,<br>
  "placeAddress": "A 77, Pocket D, Okhla Phase - 2, Opposite Intex Building, New Delhi, Delhi, 110020",<br>
  "placeName": "Kaffa Cerrado The Roastery",<br>
  "type": "POI "<br>
}<br>

## [Claim Sample Response](#Claim-Sample-Response)<br>

<span style="color: Orange">**Input URL:** </span> https://atlas.mapmyindia.com/api/places/nearby/json?access_token=<>&refLocation=28.628904,77.124870&keywords=TRNECS&filter=plugType:IEC&filter=brandId:B420&filter=model:Mahindra Electric<br>

<span style="color: Orange">**Response:** </span><br>
{<br>
  "addresstokens": {<br>
    "houseNumber": "",<br>
    "houseName": "",<br>
    "poi": "Mahindra Sri Durga Automobiles Charging Station",<br>
    "street": "",<br>
    "subSubLocality": "",<br>
    "subLocality": "Railway Line JJC Block B115",<br>
    "locality": "Mayapuri Industrial Area Phase 1",<br>
    "village": "",<br>
    "subDistrict": "Delhi Cantonment",<br>
    "district": "New Delhi District",<br>
    "city": "New Delhi",<br>
    "state": "Delhi",<br>
    "pincode": "110064"<br>
  },<br>
  "distance": 408,<br>
  "eloc": "CEORTY",<br>
  "email": "",<br>
  "entryLatitude": 28.625126,<br>
  "entryLongitude": 77.1233,<br>
  "hourOfOperation": null,<br>
  "keywords": [<br>
    "TRNECS"<br>
  ],<br>
  "landlineNo": null,<br>
  "latitude": 28.62542,<br>
  "longitude": 77.123551,<br>
  "mobileNo": "+919582599987",<br>
  "orderIndex": 1,<br>
  "placeAddress": "Mahindra Sri Durga Automobiles Service Centre, B84, Block         B, Mayapuri Industrial Area Phase 1, Mayapuri, New Delhi, Delhi, 110064",<br>
  "placeName": "Mahindra Sri Durga Automobiles Charging Station",<br>
  "richinfo": {<br>
    "for": "ev",<br>
    "eLoc": "CEORTY",<br>
    "brandName": "Mahindra Electric",<br>
    "ownerType": "OEM",<br>
    "privateVsPublic": "Controlled",<br>
    "buildingType": "Workshop",<br>
    "macVType": [<br>
      "Car"<br>
    ],<br>
    "Active": "Active",<br>
    "oemName": "Mahindra",<br>
    "macType": [<br>
      "AC",<br>
      "DC"<br>
    ],<br>
    "macPlugType": [<br>
      "IEC 60309",<br>
      "GBT"<br>
    ],<br>
    "openOrClose": "Close",<br>
    "type": "POI"<br>
  }<br>
}<br>

<p><span style = "color: green"><b>overrideRadiusLimit:</b></span> It overrides the radius limit in Nearby from 50 to max 200 kms.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json?access_toekn = <>&refLocation=28.550565, 77.268980&keywords=Fun N Food Village<br>

<span style="color: Orange"><b>Response:</b></span><br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "Fun N Food Village",<br>
                "street": "",<br>
                "subSubLocality": "",<br>
                "subLocality": "",<br>
                "locality": "Kapashera",<br>
                "village": "",<br>
                "subDistrict": "Vasant Vihar",<br>
                "district": "New Delhi District",<br>
                "city": "New Delhi",<br>
                "state": "Delhi",<br>
                "pincode": "110097"<br>
            },<br>
            "distance": 18227,<br>
            "eLoc": "E7436A",<br>
            "email": "marketing.delhi@funnfood.com",<br>
            "entryLatitude": 28.5249640000001,<br>
            "entryLongitude": 77.0842680000001,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "RCNAUS"<br>
            ],<br>
            "landlineNo": "+911143260000",<br>
            "latitude": 28.523809,<br>
            "longitude": 77.084887,<br>
            "mobileNo": "+919990006518, +919990006521, +919990006522",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Opposite Delhi Gurgaon Road, Kapashera, New Delhi, Delhi, 110097",<br>
            "placeName": "Fun N Food Village",<br>
            "type": "POI"<br>
        }

<p><span style = "color: green"><b>searchFor:</b></span> For searching within specific datasets: like Honda or EV charging stations, covid19, bajaj, partners; depends on defaultEnabled. degaultEnabled Contains two values 0 or 1. Here searchFor Parameter with <b>defaultEnabled</b> is 0.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.550566, 77.268980&keywords=Charging Station&searchFor=EV<br>

<span style="color: Orange"><b>Response:</b> </span><br>
{<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "CSC Electric Vehicle Charging Station",<br>
                "street": "",<br>
                "subSubLocality": "",<br>
                "subLocality": "",<br>
                "locality": "Okhla Industrial Estate Phase 3",<br>
                "village": "",<br>
                "subDistrict": "Kalkaji",<br>
                "district": "South East Delhi District",<br>
                "city": "New Delhi",<br>
                "state": "Delhi",<br>
                "pincode": "110020"<br>
            },<br>
            "distance": 43,<br>
            "eLoc": "D7JUOT",<br>
            "email": "",<br>
            "entryLatitude": 28.551061,<br>
            "entryLongitude": 77.269068,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "TRNECS"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.550945,<br>
            "longitude": 77.2691,<br>
            "mobileNo": "",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Parking, Plot No 238, Okhla Phase 3, New Delhi, Delhi, 110020",<br>
            "placeName": "CSC Electric Vehicle Charging Station",<br>
            "richInfo": {<br>
                "for": "ev",<br>
                "eLoc": "D7JUOT",<br>
                "brandName": "",<br>
                "ownerType": "Supplier",<br>
                "privateVsPublic": "Public",<br>
                "buildingType": "Business",<br>
                "macVType": [],<br>
                "Active": "Not Active",<br>
                "oemName": "",<br>
                "macType": [],<br>
                "macPlugType": [],<br>
                "openOrClose": ""<br>
            },<br>
            "type": "POI"<br>
        }<br>

<p><span style = "color: green"><b>searchFor:</b></span> Here <b>searchFor</b> Parameter with <b>defaultEnabled</b> is 1.</p>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>refLocation=28.550566, 77.268980&keywords=Honda<br>

<span style="color: Orange"><b>Response:</b> </span><br>
{<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "Honda Power Products",<br>
                "street": "",<br>
                "subSubLocality": "",<br>
                "subLocality": "Block A",<br>
                "locality": "Okhla Industrial Estate Phase 2",<br>
                "village": "",<br>
                "subDistrict": "Sarita Vihar",<br>
                "district": "South East Delhi District",<br>
                "city": "New Delhi",<br>
                "state": "Delhi",<br>
                "pincode": "110020"<br>
            },<br>
            "distance": 1428,<br>
            "eLoc": "7Z8HN9",<br>
            "email": "",<br>
            "entryLatitude": 28.5404770000001,<br>
            "entryLongitude": 77.2774870000001,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "RTSELC"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.5402050000001,<br>
            "longitude": 77.2776240000001,<br>
            "mobileNo": "",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Block A, Okhla Industrial Estate Phase 2, New Delhi, Delhi, 110020",<br>
            "placeName": "Honda Power Products",<br>
            "type": "POI"<br>
        }<br>

<p><span style = "color: green"><b>customCategoryCode:-</b></span> The custom category codes that should be supported for the particular client like HSPTMT,SMISST,HSPTST,HNDAUT,CLIFVR,FODHNG,SMIBRN,TMPRSN,COVRSN,HSPCOV,HNDREP,SMIDLR,HSPSCC,HOTNST.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.469664, 77.038592&keywords=HSPCOV<br>

<span style="color: Orange"><b>Response:</b> </span><br>
{<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "Kalyani Hospital Pvt Ltd",<br>
                "street": "Mehrauli Gurugram Road",<br>
                "subSubLocality": "",<br>
                "subLocality": "",<br>
                "locality": "Sector 14",<br>
                "village": "",<br>
                "subDistrict": "Gurgaon",<br>
                "district": "Gurugram District",<br>
                "city": "Gurugram",<br>
                "state": "Haryana",<br>
                "pincode": "122007"<br>
            },<br>
            "distance": 434,<br>
            "eLoc": "NJOX93",<br>
            "email": "",<br>
            "entryLatitude": 28.467566,<br>
            "entryLongitude": 77.042694,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "HLTHSP"<br>
            ],<br>
            "landlineNo": "+911242303101, +911244666999",<br>
            "latitude": 28.467788,<br>
            "longitude": 77.042491,<br>
            "mobileNo": "+919871150006",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Opposite Government Girls College, MG Road, Mehrauli-Gurgaon Road, Anamika Enclave, Sector 14, Gurugram, Haryana, 122007",<br>
            "placeName": "Kalyani Hospital Pvt Ltd",<br>
            "type": "POI"<br>
          }<br>

<p><span style = "color: green"><b>allowedCategories:-</b></span> **isAllowedCategories** is Used along with covidCategory claim to know that only limited category search is enabled. **allowedCategories** is allow only given category codes to be search in nearby like HSPTMT,HSPTST, HSPCOV,CLIFVR, HSPSCC,FODHNG, HOTNST,TMPRSN.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.469664, 77.038592&keywords=HOTNST<br>

<span style="color: Orange"><b>Response:</b> </span><br>
      {<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "Public Food & Night Shelter",<br>
                "street": "New Mata Road",<br>
                "subSubLocality": "",<br>
                "subLocality": "",<br>
                "locality": "Rajeev Nagar",<br>
                "village": "",<br>
                "subDistrict": "Gurgaon",<br>
                "district": "Gurugram District",<br>
                "city": "Gurugram",<br>
                "state": "Haryana",<br>
                "pincode": "122001"<br>
            },<br>
            "distance": 672,<br>
            "eLoc": "FJWB81",<br>
            "email": "",<br>
            "entryLatitude": 28.47568,<br>
            "entryLongitude": 77.038998,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "HOTNST"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.4757,<br>
            "longitude": 77.039,<br>
            "mobileNo": "+919899985124",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Mayor Office, Ward-7, Rajiv Nagar, Gurugram, Haryana, 122001",<br>
            "placeName": "Public Food & Night Shelter",<br>
            "type": "POI"<br>
        }

<p><span style = "color: green"><b>autoExpand:-</b></span> Allows search to auto expand radius when no result found.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.469664, 77.038592&keywords=the great india place&radius=2000000<br>

<span style="color: Orange"><b>Response:</b> </span><br>
{<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "The Great India Place Exit Gate No 10",<br>
                "street": "",<br>
                "subSubLocality": "",<br>
                "subLocality": "Entertainment City",<br>
                "locality": "Sector 38 A",<br>
                "village": "",<br>
                "subDistrict": "Dadri",<br>
                "district": "Gautam Buddha Nagar District",<br>
                "city": "Noida",<br>
                "state": "Uttar Pradesh",<br>
                "pincode": "201303"<br>
            },<br>
            "distance": 29828,<br>
            "eLoc": "9URZSD",<br>
            "email": "",<br>
            "entryLatitude": 28.5665020000001,<br>
            "entryLongitude": 77.3233060000001,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "GATEXT"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.566378,<br>
            "longitude": 77.323361,<br>
            "mobileNo": "",<br>
            "orderIndex": 1,<br>
            "placeAddress": "The Great India Place, Noida, Uttar Pradesh, 201303",<br>
            "placeName": "The Great India Place Exit Gate No 10",<br>
            "type": "POI"<br>
        }<br>

<p><span style = "color: green"><b>outputFieldsList:-</b></span> List of output fields to be displayed to the user like landlineNo, entryLongitude, entryLatitude, addressTokens, distance etc.</p><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>refLocation=28.478103, 77.026122&keywords=pizza<br>

<span style="color: Orange"><b>Response:</b> </span><BR>
{<br>
    "suggestedLocations": [<br>
        {<br>
            "distance": 593,<br>
            "eLoc": "JV8KD0",<br>
            "mobileNo": "+919582804682",<br>
            "placeName": "Pizza Hood"<br>
        }

<p><span style = "color: green"><b>POD:-</b></span> <b>isPodSearch</b> a marker claim to enable the <b>POD</b> search and <b>POD</b> claim contains the list of admins to be searched like CITY, LC, STATE, SLC.</P><br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json?refLocation=28.478103, 77.026122&keywords=school&access_token=<>&pod=LC<br>

<span style="color: Orange"><b>Response:</b> </span><BR>
{<BR>
    "suggestedLocations": [<BR>
        {<BR>
            "distance": 236,<BR>
            "eLoc": "9165VV",<BR>
            "placeName": "Amanpura",<BR>
            "district": "Gurugram District;Gurgaon District",<BR>
            "subDistrict": "Gurgaon",<BR>
            "state": "Haryana;HR",<BR>
            "pincode": "122006",<BR>
            "placeAddress": "Gurugram, Haryana, 122006",<BR>
            "type": "LOCALITY",<BR>
            "latitude": 28.4800250000001,<BR>
            "longitude": 77.0271500000001,<BR>
            "orderIndex": 1<BR>
        }<br>


<p><span style = "color: green"><b>showAddressTokens:-</b></span>To allow access to address tokens.</P><br>

<span style="color: Orange"><b>Input URL:</b> </span>https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.550565, 77.268980&keywords=Restaurant<br>

<span style="color: Orange"><b>Response:</b> </span><BR>

{<br>
    "suggestedLocations": [<br>
        {<br>
            "addressTokens": {<br>
                "houseNumber": "",<br>
                "houseName": "",<br>
                "poi": "Sonu Food Corner",<br>
                "street": "",<br>
                "subSubLocality": "",<br>
                "subLocality": "",<br>
                "locality": "Okhla Industrial Estate Phase 3",<br>
                "village": "",<br>
                "subDistrict": "Kalkaji",<br>
                "district": "South East Delhi District",<br>
                "city": "New Delhi",<br>
                "state": "Delhi",<br>
                "pincode": "110020"<br>
            },<br>
            "distance": 89,Map Interactions<br>
            "eLoc": "S8ZLTL",<br>
            "email": "",<br>
            "entryLatitude": 28.551223,<br>
            "entryLongitude": 77.2695860000001,<br>
            "hourOfOperation": "",<br>
            "keywords": [<br>
                "FODOTH"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.5511450000001,<br>
            "longitude": 77.2696120000001,<br>
            "mobileNo": "+919560372402, +919560372403",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Shop 47-48, Opposite Plot 239, Okhla Phase 3, New Delhi, Delhi, 110020",<br>
            "placeName": "Sonu Food Corner",<br>
            "type": "POI"<br>
        }<br>


<p><span style = "color: green"><b>partnerIds[List]:-</b></span> The parameter named <b>isPartnerSearch</b> is of data type LIST. This claim can be used to set the partnerIds to be allowed to a user. The values in this claim can be selected from a pre-populated set of values. For the example <b>PartnerIds</b> is 2. The list of PartnerIds is:</p><br>
-   1 : MMI<br>
-	2 : MSIL EV<br>
-	3 : Highway Delight<br>
-	4 : Web SDK<br>

<span style="color: Orange"><b>Input URL:</b> </span> https://atlas.mapmyindia.com/api/places/nearby/json? access_token=<>&refLocation=28.49728368,77.07214415&keywords=maruti ev<br>

<span style="color: Orange"><b>Response:</b> </span><BR>

   "suggestedLocations": [<br>
        {<br>
            "distance": 0,<br>
            "eLoc": "AGRTQV",<br>
            "email": "",<br>
            "entryLatitude": 0.0,<br>
            "entryLongitude": 0.0,<br>
            "keywords": [<br>
                "TRNECS"<br>
            ],<br>
            "landlineNo": "",<br>
            "latitude": 28.497283676540597,<br>
            "longitude": 77.07214415073395,<br>
            "mobileNo": "",<br>
            "orderIndex": 1,<br>
            "placeAddress": "Old Palam Gurgaon Road",<br>
            "placeName": "Ensto AC GUR0005",<br>
            "type": "POI"<br>
        }<br>
