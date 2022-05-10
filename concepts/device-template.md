# Device Template

Device Template is a set of configurations inherited by devices of a similar type.

Imagine smart home switches. They all perform a similar function and we can assume they should have the same data model, GPIOs, firmware code, etc. If you would need to introduce changes to all these devices, instead of editing each of them you could just edit a Device Template and all devices will be updated.

Every Device Template has a **Template ID** – \_\*\*\_a unique template identifier that helps Blynk to recognize the type of added device and attach all other template elements:

**General Settings:** general settings of the device

**Metadata**: a table of `key:value` data attached to every device. `Keys` are static, and `values` are related for each device. For example Serial Number field can belong to every device, but the actual value is different.

**Datastreams:** channels for any time-stamped data that flows in and out from the device to the cloud. For example sensor data should go through a Datastream. If you used the first version of Blynk platform, these are Virtual Pins.

**Events:** important events in the life of the device that should be logged and, if needed, used for notifications. Events can be triggered from the device itself or externally using HTTP API

Template also includes two dashboards:

![Template](https://user-images.githubusercontent.com/72824404/119498209-0a317e00-bd6e-11eb-84d1-ae6565dfb7d3.png)

**Web Dashboard:** a set of UI elements (widgets) to visualize the data from the device accessible for the users in Blynk.Console – a web-based application.

**Mobile Dashboard:** a set of UI elements (widgets) to visualize the data in Blynk mobile apps for iOS and Android. Mobile apps also contain a template of how device is represented in the list of devices (tiles)

## Related Articles

{% content-ref url="../getting-started/template-quick-setup/" %}
[template-quick-setup](../getting-started/template-quick-setup/)
{% endcontent-ref %}

{% content-ref url="device-template.md" %}
[device-template.md](device-template.md)
{% endcontent-ref %}

\*\*\*\*
