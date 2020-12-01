  
  

![MapmyIndia APIs](https://www.mapmyindia.com/api/img/mapmyindia-api.png)
# Nearby API

Nearby Places API, enables you to add discovery and search of nearby POIs by searching for a generic keyword used to describe a category of places or via the unique code assigned to that category.

 MapmyIndia Nearby API Platform provides following some advance features:

- Customized Radius*
- Custom Category Code
- POD
- Filter
- searchBy

## Customized Radius

- The customized radius will be provisioned and managed by Anchor.
- Added **overrideRadiusLimit** claim. It takes radius value(number only) in                                     meters. The value must be greater than 249.
- The behavior works with custom datasets only, such as Honda.
- Customized Radius is min radius : 250m, max radius : 50 Km and by default : 10 Km

## Custom Category Code
This will enable custom category code based nearby searching for customers(e.g. Honda, HDFC).The search can be performed on the basis of either custom category code or MMI category codes or keywords. The output contains standard fields and a richInfo object for client-specific data. The RichInfo can have dynamic response parameters as per customer requirement. This can be enabled on the basis of configuration provided at the time of onboarding customer data.

- Pass Custom Codes like Keywords.
- The custom code keywords like HNDAUT, HNDREP for searching near pois like Honda Stores.

## POD
Introducing "pod" parameter to search for villages. This parameter accepts "vlg", “CITY”, “LC”, “STATE”, “SLC” as value. The radius for village provides the range of distance. The radius for village search is 50 KM fixed.

## Filter
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

## searchBy

Search and Sort Nearby Places on the basis of either "Distance" or "Relevance/Importance".

- dist keyword is used to sort result in increasing order of distance, means nearest place related on top.
- imp will use the priority to give important or highest priority result on top.
- By Default it will use Distance

## Operators

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

## Request Headers

The Atlas API leverages OAuth 2.0 based security. Hence, the developer would need to send a request for access token using their client_id and client_secret to the OAuth API. Once validated from the OAuth API, the access_token and the token_type need to be sent as Authorization header with the value: “{token_type} {access_token}”.

1. **Authorization:** “{token_type} {access_token}”.

## Security Type
Atlas OAuth 2.0 based security using AES 256 and SHA-1.

## Response Type 
- JSON: if the user passed in “/json”. 
- XML: if the user passed in “/xml”

## Response Messages (as HTTP response message)
1. 200: Success. 
2. 204: No matches we’re found for the provided query. 
3. 400: Something’s just not right with the request. 
4. 401: Access Denied. 
5. 403: Services for this key has been suspended due to daily/hourly transactions limit. 
6. 500: Something went wrong. 
7. 503: Maintenance Break.

## URL 
**https://atlas.mapmyindia.com/api/places/nearby/json?**
## Method
GET 
## Request Parameters
The parameters are colour coded based on their requirements. The **“Red”** one’s are mandatory, and the **“black”** one’s are optional and the **“green”** one’s are Claimbased.
**Please Note:** The Restricted parameters are also optional.

a.	<span style="color: Orange">**Mandatory Parameters:** </span>

1.	<span style="color: red"> keywords </span> (string) e.g. FODCOF, Shoes, Coffee, Versace, Gucci, H&M, Adidas, Starbucks, B130 {POI, House Number, keyword, tag}
2.	<span style="color: red"> keywords </span> {string (latitude[double],longitude[double])}: Provides the location around which the search will be performed. e.g. refLocation=28.454,77.435

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

## Claim Request Parameters

<table><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><span><b>Claims Available<td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span><b>Remarks</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;" autocomplete="off"><p><span><b>Claimed Type</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>Possible Values</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span><b>isPublic</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: red">keywords</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>e.g. FODCOF, Shoes, Coffee, Versace, Gucci, H&M, Adidas, Starbucks, B130 {POI, House Number, keyword, tag}</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div class="" contenteditable="false" style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span style = "color: red">refLocation</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Provides the location around which the search will be performed. e.g. refLocation=28.454,77.435</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span></span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Y</span></p></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span style = "color: green">overrideRadiusLimit</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>It just takes values in meters.
max 200 kms
</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Not applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">defaultEnabled</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>integer
This lets us enable / disable default ANT search when searchFor parameter is given and Contains two values 0, 1. By default, a user has access to MMI data in search. To prevent the user to access the MMI data, set the value of this claim to "0". Removing this claim or setting the value to 1 will allow users to access MMI data.
</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>Valued</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>0,1</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>N</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">customCategoryCode</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>The custom category codes that should be supported for the particular client</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>HSPTMT,SMISST,HSPTST,HNDAUT,
CLIFVR,FODHNG,SMIBRN,TMPRSN,COVRSN,
HSPCOV,HNDREP,SMIDLR,HSPSCC,HOTNST</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">isAllowedCategories*</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Used along with allowedCategories claim so that only limited category search is enabled.</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valueless</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span></span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span style = "color: green">allowedCategories*</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Allow only given category codes to be search in nearBy</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"><p><span>HSPTMT,HSPTST,HSPCOV,CLIFVR,HSPSCC,
FODHNG,HOTNST,TMPRSN</span></p></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>region</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>It will restrict the region in which the search is applicable</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Valued</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>lka,mmr,hindi,npl,btn,bgd,ind</span></p></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div><p><span>Y</span></p></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr><tr><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td><td class="border_l border_r border_t border_b selected"><div class="wrap"><div style="margin: 10px 5px;"></div></div></td></tr></table>


