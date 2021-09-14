---
description: >-
  If you need your values to have the same timestamp you can use the following
  format
---

# Batch Update of the Datastreams

{% api-method method="get" host="https://{server\_address}" path="/external/api/batch/update?token={token}&{pin1}={value1}&{pin2}={value2}" %}
{% api-method-summary %}
Batch update
{% endapi-method-summary %}

{% api-method-description %}
Updates multiple datastreams with one GET request. It could be used to save network bandwidth. Also, the batch update is required to show multiple datastreams in the map widget popup.  
  
**Example:**  
`https://blynk.cloud/external/api/batch/update?token=bFFtSHNCZZDWQ__Zs96cP5jLMhLoJofg&v1=33&v2=44`
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
Device AuthToken
{% endapi-method-parameter %}

{% api-method-parameter name="pin" type="string" required=true %}
Virtual Pin
{% endapi-method-parameter %}

{% api-method-parameter name="value" type="string" required=true %}
The desired value of the Datastream. Will be parsed based on the Datastream data type \(int, double, string\) and bounded with min / max values of datastream settings. In case value doesn't match the Datastream type error will be returned.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success
{% endapi-method-response-example-description %}

```text
OK
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Could not find a device token  
or  
Wrong pin format  
or  
Value doesn't match the Datastream data type
{% endapi-method-response-example-description %}

```text
{"error":{"message":"Invalid token."}}

or

{"error":{"message":"Wrong pin format."}}

or

{"error":{"message":"Value doesn't match the Datastream data type"}}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

