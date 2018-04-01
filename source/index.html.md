---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>admin@theregistrationsystem.com</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the myTRS API! You can use our API to create registrants, and grab information about users and registrants on your myTRS event.

We have language bindings in Shell. You can view code examples in the dark area to the right.


# Authentication

myTRS uses API keys to allow access to your data on the API. You can register a new myTRS API key by contact us at support@theregistrationsystem.com.

> To authorize, use this code:

```shell
# With shell via GET access_token
  curl https://app.my-trs.com/api/v1/registrations/1.json?access_token=<mytrs-api-key>

# With shell via HTTP Header
  curl -IH "Authorization: Token token=<mytrs-api-key>" "api_endpoint_here"

```

> Make sure to replace `<mytrs-api-key>` with your API key.

<aside class="warning">All requests without or with an invalid access_token will return an 402 Unauthorized error.</aside>

<aside class="success">
Your API key gives you access to all of your sites under myTRS.
</aside>



# Registrations

## Get All Registrations

```shell
curl "https://app.my-trs.com/api/v1/registrations.json"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns JSON structured like this:

````json
[
   {
      "id":99302,
      "registrant_type":null,
      "checked_in_at":null,
      "created_at":"03:45 PM on Tue, Feb 24th, 15",
      "site_id": 3,
      "client_id": 5,
      "background_check_result": "Eligible",
      "user":{
         "id":35727,
         "first_name":"Sarah",
         "last_name":"Gret",
         "custom_status": "Checked",
         "email":"test@example.com",
         "address":{
            "line1":"7929 Spooner Street",
            "line2":"",
            "city":"Indianapolis",
            "state":"IN",
            "zip_code":"46268",
            "country":"US",
            "phone":"317-444-9999",
            "company_name":null
         }
      },
      "custom_fields":[
         {
            "id": 5,
            "name":"T-Shirt Size",
            "value":"Small, Medium, Large, XLarge, XXLarge, XXXLarge"
         }
      ],
      "registration_items":[
         {
            "id":"t10016",
            "name":"06:00 PM on Thu, Apr 16th, 15 to 07:30 PM on Thu, Apr 16th, 15 - Volunteer Training - ",
            "registerable_type": "TimeSlot",
            "checked_out": true,
            "location": "Speedway", 
            "starts_at": "2018-04-01T16:02:13+03:00", # ISO 8601 string
            "ends_at": "2018-08-01T16:02:13+03:00",
            "activity_name": "Train the Trainer"
         },
         {
            "id":"t9651",
            "name":"Apr 25th, 2015 from 07:00 AM to 07:15 AM - Speedway Training ",
            "registerable_type": "Activity",
            "checked_out": false,
            "location": nil, # nil unless registerable_type is `TimeSlot`
            "starts_at": nil, # nil unless registerable_type is `TimeSlot`
            "ends_at": nil, # nil unless registerable_type is `TimeSlot`
            "activity_name": "Training Sessions v2"
         }
      ]
   }
]
...
````

```shell
curl "https://app.my-trs.com/api/v1/registrations.xml"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns XML structured like this:


````xml
<registrations type="array">
  <registration>
    <id type="integer">9950131231</id>
    <registrant-type nil="true"/>
    <checked-in-at nil="true"/>
    <created-at type="dateTime">2015-02-24T15:45:45Z</created-at>
    <user>
      <id type="integer">35727</id>
      <first-name>Sarah</first-name>
      <last-name>Gret</last-name>
      <email>test@example.com</email>
      <address>
        <line1>7929 N. Spooner Street</line1>
        <line2></line2>
        <city>Indianapolis</city>
        <state>IN</state>
        <zip-code>46268</zip-code>
        <country>US</country>
        <phone>317-888-1144</phone>
        <company-name nil="true"/>
      </address>
    </user>
    <custom-fields type="array">
      <custom-field>
        <name>T-Shirt Size</name>
        <value>Small, Medium, Large, XLarge, XXLarge, XXXLarge</value>
      </custom-field>
    </custom-fields>
    <registration-items type="array">
      <registration-item>
        <id>t10016</id>
        <name>06:00 PM on Thu, Apr 16th, 15 to 07:30 PM on Thu, Apr 16th, 15 - Volunteer Training - </name>
      </registration-item>
      <registration-item>
        <id>t9651</id>
        <name>Apr 25th, 2015 from 07:00 AM to 07:15 AM - Speedway Training - </name>
      </registration-item>
    </registration-items>
  </registration>
  ...
````

__HTTP REQUEST__

This resource supports JSON and XML responses.

JSON ````GET https://app.my-trs.com/api/v1/registrations.json````

XML ````GET https://app.my-trs.com/api/v1/registrations.xml````

__QUERY PARAMETERS__

|Parameters|Type|Description|Example|
|:------------- |:-------------:|:-----:|:-----:|
|site_id|optional|Filter results by a specific site | ````site_id=183````|
|email|optional|Filter results by a specific email address on the registration | ````email=test@my-trs.com````|
|starts_at|optional| Filter results by a date range. If you use this, you also have to use 'ends_at'|````starts_at=2015-02-1T12:00:00+00:00````|
|ends_at|optional| Filter results by a date range. If you use this, you also have to use 'starts_at'|````ends_at=2015-02-25T16:00:00+00:00````|
|updated_at_gteq|optional| Filter registrations by when they were last updated (start date). If you use this, you also have to use 'updated_at_lteq'|````updated_at_gteq=2015-02-1T12:00:00+00:00````|
|updated_at_lteq|optional| Filter registrations by when they were last updated (end date). If you use this, you also have to use 'updated_at_gteq'|````updated_at_lteq=2015-03-1T12:00:00+00:00````|


## Get a Specific Registration

```shell
curl "https://app.my-trs.com/api/v1/registrations/1.json"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns JSON structured like this:

```json
{  
   "id":1,
   "registrant_type":"Current TRS Clients",
   "checked_in_at": null,
   "site_id": 3,
   "client_id": 5,
   "background_check_result": "Eligible",
   "user":{  
      "id":22,
      "first_name":"Homer",
      "last_name":"Simpson",
      "custom_status": "Checked",
      "email":"hsimpson@thesimpsons.com",
      "address":{  
         "line1":"742 Evergreen Terrace",
         "line2":"Bldg B",
         "city":"Springfield",
         "state":"TX",
         "zip_code":"22111",
         "country":"US",
         "phone":null,
         "company_name":null
      }
   },
   "custom_fields":[  
      {  
         "id": 581,
         "name":"Organization/Company",
         "value":"The Simpsons"
      },
      {  
         "id": 582,
         "name":"TRS Client History",
         "value":"1 Year"
      },
      {  
         "id": 588,
         "name":"Registration Challenges",
         "value":"n/a"
      }
   ],
   "registration_items":[  
     {
        "id":"t10016",
        "name":"06:00 PM on Thu, Apr 16th, 15 to 07:30 PM on Thu, Apr 16th, 15 - Volunteer Training - ",
        "registerable_type": "TimeSlot",
        "checked_out": true,
        "location": "Speedway", 
        "starts_at": "2018-04-01T16:02:13+03:00", # ISO 8601 string
        "ends_at": "2018-08-01T16:02:13+03:00",
        "activity_name": "Train the Trainer"
     },
     {
        "id":"t9651",
        "name":"Apr 25th, 2015 from 07:00 AM to 07:15 AM - Speedway Training ",
        "registerable_type": "Activity",
        "checked_out": false,
        "location": nil, # nil unless registerable_type is `TimeSlot`
        "starts_at": nil, # nil unless registerable_type is `TimeSlot`
        "ends_at": nil, # nil unless registerable_type is `TimeSlot`
        "activity_name": "Training Sessions v2"
     }
   ]
}
```
> Custom fields are dynamically configured by the client and change depending on their site's configuration.

> The `background_check_result` field is only available for sites configured with Verified Volunteers Integration (https://www.verifiedvolunteers.com/)

### HTTP Request

`GET https://app.my-trs.com/api/v1/registrations/1.json`

### Query Parameters

Parameter | Description
--------- | -----------
id | The ID of the registration to retrieve

<aside class="success">
Remember — include '.json' at the end of your endpoint to ensure you get the right response back!
</aside>

## Find the Latest Registration Belonging to the Same User

Assuming you have two sites configured on your myTRS account, and the registrant you're requesting has signed up for both. This action will return the newest registration regardless of which registration ID is provided. The response will also include the "requested_id" parameter if the registration returned is not the same one as the registration requested.


```shell
curl "https://app.my-trs.com/api/v1/registrations/1.json/latest"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns JSON structured like this:

```json
{  
   "requested_id": 1,
   "id": 2,
   "registrant_type":"Current TRS Clients",
   "checked_in_at": null,
   "user":{  
      "id":522,
      "first_name":"Homer",
      "last_name":"Simpson",
      "custom_status": "Checked",
      "email":"homer@thesimpsons.com",
      "address":{  
         "line1":"742 Evergreen Terrace",
         "line2":"Bldg B",
         "city":"Springfield",
         "state":"TX",
         "zip_code":"22111",
         "country":"US",
         "phone":null,
         "company_name":null
      }
   },
   "custom_fields":[  
      {  
         "id": 581,
         "name":"Organization/Company",
         "value":"The Simpsons"
      },
      {  
         "id": 582,
         "name":"TRS Client History",
         "value":"1 Year"
      },
      {  
         "id": 588,
         "name":"Registration Challenges",
         "value":"n/a"
      }
   ],
   "registration_items":[  
     {
        "id":"t10016",
        "name":"06:00 PM on Thu, Apr 16th, 15 to 07:30 PM on Thu, Apr 16th, 15 - Volunteer Training - ",
        "registerable_type": "TimeSlot",
        "checked_out": true,
        "location": "Speedway", 
        "starts_at": "2018-04-01T16:02:13+03:00", # ISO 8601 string
        "ends_at": "2018-08-01T16:02:13+03:00",
        "activity_name": "Train the Trainer"
     },
     {
        "id":"t9651",
        "name":"Apr 25th, 2015 from 07:00 AM to 07:15 AM - Speedway Training ",
        "registerable_type": "Activity",
        "checked_out": false,
        "location": nil, # nil unless registerable_type is `TimeSlot`
        "starts_at": nil, # nil unless registerable_type is `TimeSlot`
        "ends_at": nil, # nil unless registerable_type is `TimeSlot`
        "activity_name": "Training Sessions v2"
     }
   ]
}
```

### HTTP Request

`GET https://app.my-trs.com/api/v1/registrations/1.json/latest`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the registration to retrieve


## Update Registrant's Check-In Time

This will update the checked_in_at field with the current datetime. Once the checked_in_at has been set for a registration, it cannot be changed. Consecutive requests will be ignored and return a 409 Conflict response code.


```shell
curl "https://app.my-trs.com/api/v1/registrations/1.json/check_in"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns JSON structured like this:

```json
{  
   "id":1,
   "registrant_type":"Current TRS Clients",
   "checked_in_at": "2014-10-01T13:55:54.000Z",
   "user":{  
   ...
```

### HTTP Request

`PUT https://app.my-trs.com/api/v1/registrations/1.json/check_in`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the registration to check in


## Create a User & Registration Combo

This endpoint allows you to create a combination of a user and registration. "Users" on myTRS are individuals that can sign up to multiple events under the same client. The benefits of being a user allow pre-population of address information when registering for an event. A "Registration" represents a single user sign up on a specific site. The registration includes activities and time slots that the user signed up for.

A site_id is required to ensure that both a user and registration can be created. The authenticated URL provided back allows you to redirect the user in a "logged in" state and send them directly to select their activities.


#### Custom Fields
myTRS clients can build custom fields as part of their site. They're often used to collect extra information from registrants on sign up.

If your myTRS site includes custom fields, you can pre-fill these values for registrants by passing in a "custom_fields" object where the key represents the *exact* field name, and the value is the field value you want to enter for this registrant.

#### Authenticated URLs
The "authenticated_url" parameter above provides a one-time use address that will log your newly created registrant in and allow them to select activities. If your token has expired, you can request a new one by re-POSTING to the above endpoint with an existing email address.

<aside class="warning">Authenticated URLs are one-time use and expire after a period of time. Please avoid storing authentication tokens!</aside>



```shell
curl -X POST -H "Content-Type: application/json" "https://app.my-trs.com/api/v1/registrations?access_token=<mytrs-api-key>" -d '{
     "create_user": "true",
     "registration": { 
       "site_id": 1, 
       "registrant_type_name": "Attendees" 
     },
     "user": {                                                                                                                         
       "email": "petergriffin@familyguy.com",    
       "first_name": "Peter",
       "last_name": "Griffin"                                                                                                                                               
     },
     "address": { 
        "line1": "123 Spooner Street",
        "city" : "Boston",
        "state": "MA",
        "country": "US", 
        "zip_code": "02314"
     },
     "custom_fields": {
        "T-Shirt Size": "Medium",
        "Hat Size": "X-Large"
     },
     "return_authenticated_url": "true"
}'
```

> The above command returns JSON structured like this:

```json
{
  "user": {
    "client_id": 1,
    "id": 34572,
    "email": "petergriffin@familyguy.com",
    "created_at": "2015-02-18T14:56:34.000Z",
    "updated_at": "2015-02-18T14:56:34.000Z",
    "first_name": "Peter",
    "last_name": "Griffin",
    "invitation_token": null,
    "invitation_created_at": null,
    "invitation_sent_at": null,
    "invitation_accepted_at": null,
    "invitation_limit": null,
    "invited_by_id": null,
    "invited_by_type": null,
    "invitations_count": 0,
    "group_leader": false
  },
  "authenticated_url": "https://test.my-trs.com/select_activities?auth_token=xszL4DjnrjfiFyeQAshn"
}

```

### HTTP Request

`POST https://app.my-trs.com/api/v1/registrations?access_token=<mytrs-api-key>`

### URL Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
create_user | Whether to create a user or not | Yes (must pass in true)
registration -> site_id | The TRS site ID to create this registration for | Yes
user -> email | User's email address | Yes
user -> first_name | User's first name | Yes
user -> last_name  | User's last name  | Yes
address -> line1   | User's street address 1 | site-dependent
address -> line2   | User's street address 2 | site-dependent
address -> city   | User's address city | site-dependent
address -> state   | User's address state code (ex: NY) | site-dependent
address -> country   | User's address country code (ex: US) | site-dependent
address -> zip_code   | User's address 5 digit zip code | site-dependent
custom_fields     | A key/value collection of custom fields and values for this registrant | No



# Sites

## Get All Sites for the Current Client

```shell
curl "https://app.my-trs.com/api/v1/sites.json"
  -H "Authorization: Token token=<mytrs-api-key>"
```

> The above command returns JSON structured like this:

````json
[
   {
      "id":5,
      "subdomain": "mytrswebinars",
      "client_id":1,
      "site_groups":[
        {
          "id": "5",
          "name": "Group A"
        },
        {
          "id": "7",
          "name": "Group B"
        }
      ]
   },
   {
      "id":8,
      "subdomain": "mytrs",
      "client_id":1,
      "site_groups": [
        {
          "id": "5",
          "name": "Group A"
        },
        {
          "id": "7",
          "name": "Group B"
        }
      ]
   }
]
````

__HTTP REQUEST__

This resource supports returning all sites and associated site groups belonging to the current client. The current client is determined based on your API token.

JSON ````GET https://app.my-trs.com/api/v1/sites.json````


__QUERY PARAMETERS__

n/a

