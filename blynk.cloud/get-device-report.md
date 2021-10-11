# Get Device History Data

{% swagger baseUrl="https://{server_address}" path="/external/api/data/get?token={token}&period={PERIOD}&granularityType={TYPE}&sourceType={SOURCE_TYPE}&tzName={tzName}&format={FORMAT}&output=FILE&pin={pin}" method="get" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="period" type="string" %}
Is 

`MONTH`

 by default. Other possible options: 

`HOUR`

, 

`DAY`

, 

`WEEK`

, 

`THREE_MONTHS`
{% endswagger-parameter %}

{% swagger-parameter in="path" name="granularityType" type="string" %}
Is 

`RAW_DATA`

 by default. ( 

`RAW_DATA`

 is not supported for the 

`THREE_MONTH`

 period! ). Other possible values: 

`MINUTE`

, 

`HOURLY`

, 

`DAILY`
{% endswagger-parameter %}

{% swagger-parameter in="path" name="sourceType" type="string" %}
Is 

`AVG`

 by default. Other possible values: 

`MIN`

, 

`MAX`

, 

`SUM`

, 

`COUNT`
{% endswagger-parameter %}

{% swagger-parameter in="path" name="tzName" type="string" %}
Is 

`UTC`

 by defult. Please specify timezones accordingly to 

`java.time.ZoneId`
{% endswagger-parameter %}

{% swagger-parameter in="path" name="format" type="string" %}
Is TS by default. Other possible values:

\


ISO_US "04/10/19 11:45:41 AM"

\


ISO_SIMPLE "2018-06-07 22:01:20"
{% endswagger-parameter %}

{% swagger-parameter in="path" name="sendEvents" type="string" %}
Is false by default
{% endswagger-parameter %}

{% swagger-parameter in="path" name="dataStreamId or pin" type="string" %}
Are optional parameteres, which are used to get data for the specific pin
{% endswagger-parameter %}

{% swagger-parameter in="path" name="output" type="string" %}
Is FILE by default. Other possible value: JSON
{% endswagger-parameter %}

{% swagger-response status="200" description="Success." %}
```
{"link":"https://server_address/device_data_2592_2021-04-13T02-27-11.zip"}
```
{% endswagger-response %}

{% swagger-response status="400" description="Could not find a device token
or
No device token was provided
or
Typo in parameter or it's value
or
Wrong pin format" %}
```
{"error":{"message":"Invalid token."}}

or

{"error":{"message":"No token provided."}}

or

{"error":{"message":"Request with incorrect parameters"}}

or

{"error":{"message":"Wrong pin format."}}
```
{% endswagger-response %}

{% swagger-response status="500" description="Wrong constant is used in parameter (specified in the end of the string)
or
There is no data for specified pin or datastream" %}
```
{"error":{"message":"No enum constant cc.blynk.server.core.model.widgets.outputs.graph.Period.YEAR"}}

or

{"error":{"message":"No data"}}

or

{"error":{"message":"Wrong pin format."}}
```
{% endswagger-response %}
{% endswagger %}

## **Use case example:**

You live in Sydney and have garage door opener and want to get an exact time you departed today in one file. The accuracy you need is up to 1 minute and it should be in "YYYY-MM-DD HH:MM:SS" format.\
Garage door opener is Blynked and it uses Datastream with ID 20 and virtual pin 6 for open/close commands. Also you want to get the list of all the events occured during this period. So API request for this case looks like:

`https://blynk.cloud/external/api/data/get?token=HjKjfij84050fege&period=DAY&granularityType=MINUTE&sourceType=AVG&tzName=America/New_York&format=ISO_SIMPLE&sendEvents=true&output=FILE&dataStreamId=20`

**JSON Output example:**

```
{
    "meta":
    [
        {
            "name": "data_stream_name",
            "type": "String"
        },
        {
            "name": "ts",
            "type": "UInt32"
        },
        {
            "name": "value",
            "type": "Float64"
        }
    ],

    "data":
    [
        {
            "data_stream_name": "",
            "ts": 2021-05-14 12:25:00,
            "value": 1.6100000000000003
        }
    ],

    "rows": 1,

    "rows_before_limit_at_least": 1
}
```
