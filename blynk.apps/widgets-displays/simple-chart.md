# Simple Chart

![](../../.gitbook/assets/simple-chart-widget-newsletter.png)

Visualize live and historical data in a chart from a **single** datastream. Applications include sensor data and binary event logging. Choose from data aggregation options of average and sum. The Y-axis scaling can be customized.  Scrolling is an option, and you can connect missing data points.

See also the [SuperChart widget](superchart.md) that can handle multiple datastreams, shows the Y axis values, and supports the chart types of line, step, area, bar, state.

Simple Chart features:

* line, stepped line, or bar chart types
* plotting data resolutions: 1 min, 1 hour, or 1 day
* plotting time ranges from 6 hours to 1 year
* auto-scaled or fixed data axis
* highlighted min/max values
* easily reveal individual points via tap-n-hold
* scrollable time axis
* numerous styling settings
* full-screen mode

### Datastream

Select or create a datastream of [data type](https://docs.blynk.io/en/blynk.console/templates/datastreams/datastreams-common-settings/data-type) integer or double.



### Widget Controls

The widget has the following controls:

1. **Time Ranges**: tap to select a time range. These are configurable under the widget settings.
2. **Full Screen**: when enabled, the full screen icon will be displayed at the lower right of the widget. Tap to zoom the chart to the full screen.

### **Widget Settings**

The widget has extensive charting display options that are easily explored interactively with the preview. Chart types of line, step, area, bar, and binary are configurable for each datastream assigned.

#### **Data**

![](../../.gitbook/assets/simple-chart-widget-data-settings.png)

Select a datastream which has numerical (i.e. of Int or Double) data type and comes from the device. Data that the app sends to the device is not registered. Simple Chart widget shows data from a single datastream. If you need to plot multiple datastreams in a single chart, check the Super Chart widget. By default the chart shows the average value (AVG) for each point on the chart, but you can change aggregation to (SUM) total of the incoming data. The time period covered by each point on the chart is defined by the selected Time Range/Resolution (see below).

#### Chart Style

![](../../.gitbook/assets/simple-chart-widget-style.png)

Choose chart type (Line, Bar, or Step line) and its visual properties, like line width, color or gradient, axes style, etc. Note: when the gradient option is used, its color distribution is based on min/max properties of the selected datastream.

#### Time Ranges / Resolution

![](../../.gitbook/assets/simple-chart-widget-time-ranges.png)

Select up to 7 time ranges you want to be able to switch between in the widget. Each time range button you select specifies its resolution - that is a period of time covered by each single point on a chart. Whenever there are multiple actual data writings coming from the device within the resolution period, that data is aggregated into one point (calculating average or total depending on the selection made in the Data section (see above).

#### Y-Axis Scaling

![](../../.gitbook/assets/simple-chart-widget-y-axis-scaling.png)

There are a number of ways to define the range of values to be shown on a chart. Select option t&#x6F;**:**

* use datastream min/max (available for AVG aggregation, not available for SUM aggregation)
* auto scale the visual range to always fit all the data
* 0-Auto: auto-scale but always start from zero
* define fixed min and max of the visual range
* define delta: chart is auto-scaled, but its range never gets less than the delta set

#### Summary

![](../../.gitbook/assets/simple-chart-widget-value-summary.png)

Turn on Summary to show the average or total of all values presented on the chart in the top right corner. Note: summary style settings also define the style of selected value during tap-n-hold.

#### Other Settings

![](../../.gitbook/assets/simple-chart-widget-settings.png)

* Show or hide a button at the bottom right to go to full-screen mode
* Allow chart scrolling along the time axis. On scrolling, the chart and the summary are updated according to the new time range
* Whether the line chart should connect missing points - that is all available points are connected in a line. Turn it off to visualize points without neighbours

### How to send data from device to Simple Chart widget

Usually, just make sure that the data coming from the device is numerical. See more details on sending data [here](https://docs.blynk.io/en/getting-started/how-to-display-any-sensor-data-in-blynk-app).

```
float sensorData = readSensor(); 
Blynk.virtualWrite(V5, sensorData);
```

#### Reading the widget value(s)

You can read the latest values from the datastreams assigned to the widget. For datastream V1 of data type double:

```cpp
BLYNK_WRITE(V1) {
// Called when the datastream V1 value changes

double pinValue = param.asDouble();
Serial.print(“V1: “);
Serial.println(pinValue, 3);

}
```

To get the latest datastream value assigned to V1:

```
https://{server_address}/external/api/get/?token={your 32 char token}&V1
```

To get the historical values assigned to datastream V1:

```
https://{server_address}/external/api/data/get/?token={your 32 char token}&period={PERIOD}&granularityType={TYPE}&sourceType={SOURCE_TYPE}&tzName={tzName}&format={FORMAT}&output=FILE&pin={pin}

https://{server_address}/external/api/data/get/?token={your 32 char token}&period=WEEK&granularityType=RAW_DATA&sourceType=MAX&tzName=America/New_York&format=ISO_SIMPLE&sendEvents=true&output=FILE&pin=V1
```

#### Changing the datastream value(s)

You can change the value of the datastream assigned to the widget with the hardware or HTTP API. The widget works best with historical data sent on a constant interval.

For a datastream V1 assigned the data type of double.

**Hardware:**

```cpp
Blynk.virtualWrite(V1, 3.14159);
```

**HTTP API:**

```
https://{server_address}/external/api/update/?token={your 32 char token}&V1=3.14159
```

{% hint style="danger" %}
Don't put **`Blynk.virtualWrite()`**&#x69;nto the **`void loop()`** as it can cause a flood of messages and your hardware will be disconnected. Send such updates only when necessary, use flags, or [timers](../../blynk.edgent-firmware-api/blynk-timer.md).
{% endhint %}



Sketch:[ Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

Sketch:[ ](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)[Set Property](https://github.com/blynkkk/blynk-library/blob/master/examples/More/SetProperty/SetProperty_SingleValue/SetProperty_SingleValue.ino)

Sketch:[ ](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)[VirtualPinWrite](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/VirtualPinWrite/VirtualPinWrite.ino)

Sketch: [VirtualPinRead](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/VirtualPinRead/VirtualPinRead.ino)



### Change Widget Properties

You can change certain properties of the Widget from your hardware. For that, use this command:&#x20;

```cpp
Blynk.setProperty(vPin, "widgetProperty", "propertyValue"); 
```

Where:&#x20;

* `vPin` is: virtual pin number the widget is assigned to
* `widgetProperty`: property you want to change
* `propertyValue`: value of the property you want to change

{% hint style="danger" %}
Don't put **`Blynk.setProperty()`**&#x69;nto the **`void loop()`** as it can cause a flood of messages and your hardware will be disconnected. Send such updates only when necessary, or use timers.
{% endhint %}



### Properties you can change

You can change the properties _label_, _color_, _isDisabled_, _isHidden_ of the widget from your hardware, or via an [HTTP API](broken-reference). The URL must be encoded, so spaces in labels must be replaced with %20, and color hexadecimal values in the HTTP API URL must include the hash # character urlencoded as %23.

#### **Change Widget Label**

```cpp
Blynk.setProperty(V1, "label", "Air temperature");
```

#### **Set Color**

'Color' property changes title color if the title is set and is visible.

```cpp
//#D3435C - Blynk RED 
Blynk.setProperty(V1, "color", "#D3435C");
```

#### **Disable/Enable**

Widget will be greyed out on UI and users won't be able to tap on it.

```cpp
Blynk.setProperty(V1, "isDisabled", true);
```

#### **Show/Hide**

Widget will be hidden from dashboard. Design your UI so that it doesn't look weird when there is no widget.

```cpp
Blynk.setProperty(V1, "isHidden", true);
```



### Change widget properties via HTTPs API

## Updates the Datastream Property and all assigned Widgets

<mark style="color:blue;">`GET`</mark> `https://{server_address}/external/api/update/property?token={your 32 char token}&pin={your vPin}&{property}={value}`

The endpoint allows you to update the Datastream Property value via GET request. All widgets (both web and mobile) that are assigned to this datastream will inherit this property. The Datastream Property is persistent and will be stored forever until you change it with another value. In order to clear the property you need to clear the device data in device actions menu.

**Example:**\
`https://blynk.cloud/external/api/update/property?token=GVki9IC70vb3IqvsV0YD3el4y0OpneL1&pin=V2&label=My%20Label`

`https://blynk.cloud/external/api/update/property?token=GVki9IC70vb3IqvsV0YD3el4y0OpneL1&pin=V1&color=%23D3435C`

`https://blynk.cloud/external/api/update/property?token=GVki9IC70vb3IqvsV0YD3el4y0OpneL1&pin=V1&isDisabled=true`

#### Path Parameters

| Name                                               | Type   | Description                                                                                                                 |
| -------------------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| {server address}<mark style="color:red;">\*</mark> | string | Get from the bottom right of your Blynk console. [More information](../../blynk.cloud/device-https-api/troubleshooting.md). |

#### Query Parameters

| Name                                    | Type   | Description                                                                                                                                |
| --------------------------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| token<mark style="color:red;">\*</mark> | string | Device [auth token](../../concepts/device.md#authtoken) from Device info                                                                   |
| pin<mark style="color:red;">\*</mark>   | string | The datastream [virtual pin](../../blynk.console/templates/datastreams/virtual-pin.md) (should start with "v")                             |
| {property}                              | string | The property of the widget you want to update: `label`, `color`, `isDisabled`, `isHidden`                                                  |
| label                                   | string | the text used as widget label                                                                                                              |
| color                                   | string | hexadecimal, must include the hash # character urlencoded as %23. 'Color' property changes title color if the title is set and is visible. |
| isDisabled                              | string | true or false                                                                                                                              |
| isHidden                                | string | true or false                                                                                                                              |

{% tabs %}
{% tab title="200 Success" %}
```
```
{% endtab %}

{% tab title="400 Could not find a device token" %}
```
{"error":{"message":"Invalid token."}}
```
{% endtab %}
{% endtabs %}

### **Sync to the latest known state**&#x20;

You can update your hardware to the latest datastream value from Blynk.Cloud after your hardware went offline, and then came online again. Use `Blynk.syncVirtual()` to update a single virtual pin, or `Blynk.syncAll()` to update all virtual pins. See [State Syncing](../../blynk.edgent-firmware-api/state-syncing.md) for more details.

```cpp
BLYNK_CONNECTED() { 
  // Called when hardware is connected to Blynk.Cloud  

  // get the latest value for V1
  Blynk.syncVirtual(V1); 

  // Request Blynk server to re-send latest values for all pins
  Blynk.syncAll()
}
```
