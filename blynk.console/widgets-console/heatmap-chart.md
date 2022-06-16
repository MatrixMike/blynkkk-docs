# Heatmap Chart

Available only for PRO users

Heatmap Chart is a two-dimensional visual representation of data, where X-axis is time, and Y-axis is a value visualized with color intensity.&#x20;

![](<../../.gitbook/assets/image (35) (1) (1).png>)

An example of use could be a chart of temperature change depicted in color, but it can also be used to visualize on/off or mode states.&#x20;





### Datastream

It's possible to plot up to 5 datastreams in one widget. Only INT, DOUBLE, and ENUM datastreams are supported.

When using ENUM type, colors will be taken from Datastream settings, for others you can set your own color mapping.



### Data aggregation

How data will be aggregated:&#x20;

* **AVG** will plot average value per minute;
* **Raw** will plot using all the data available (PRO plan only)
* **MIN** will plot the minimum value per minute;
* **MAX** will plot the maximum value per minute;

{% hint style="info" %}
ENUM will only work with **Raw** aggregation type
{% endhint %}



### Color

Set the color scale to color the incoming values.

When using ENUM datastream, colors will be taken from datastream settings, for others you can set your own colors.





## How to send data from the device&#x20;



### Send data using Blynk library

To send data to the chart, use standard command:

```cpp
Blynk.virtualWrite(vPin, value);
```

where `vPin` is a number, and `value` is the actual value you want to send.&#x20;

{% hint style="danger" %}
Don't put **`Blynk.virtualWrite()`**into the **`void loop()`**as it can cause a flood of messages and your hardware will be disconnected from the server for spam. Send such updates only when necessary, or use timers as described below.
{% endhint %}



Here is a C++ code example to update the chart using timer. You can find a full code example for your hardware [here](https://examples.blynk.cc/?board=ESP8266\&shield=ESP8266%20WiFi\&example=GettingStarted%2FPushData).

```cpp
// Declaring a global variable to for sensor data
int sensorVal; 

// This function creates the timer object. It's part of Blynk library 
BlynkTimer timer; 

void heatmapchartTimer() 
{
  // Writing sensor value to datastream V5
  Blynk.virtualWrite(V5, sensorVal);  
}

void setup()
{
  //Connecting to Blynk Cloud
  Blynk.begin(auth, ssid, pass); 
  
  // Setting interval to send data to Blynk Cloud to 1000ms. 
  // It means that data will be sent every second
  timer.setInterval(1000L, heatmapchartTimer); 
}

void loop()
{
  // Reading sensor from hardware analog pin A0
  sensorVal = analogRead(0); 
  
  // Runs all Blynk stuff
  Blynk.run(); 
  
  // runs BlynkTimer
  timer.run(); 
}
```



### Send data using HTTP API

You can also use HTTPs API to send data. Check the articles below:&#x20;

{% content-ref url="../../blynk.cloud/update-datastream-value.md" %}
[update-datastream-value.md](../../blynk.cloud/update-datastream-value.md)
{% endcontent-ref %}

{% content-ref url="../../blynk.cloud/upload-set-of-data-with-timestamps-api.md" %}
[upload-set-of-data-with-timestamps-api.md](../../blynk.cloud/upload-set-of-data-with-timestamps-api.md)
{% endcontent-ref %}



