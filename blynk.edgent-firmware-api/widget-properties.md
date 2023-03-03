# Widget Properties

Changing some of the widget properties from hardware side is also supported.\
For example, you can change the color of LED widget based on a condition:

```
//change LED color
Blynk.setProperty(V0, "color", "#D3435C");

//change LED label
Blynk.setProperty(V0, "label", "My New Widget Label");

//change MENU labels
Blynk.setProperty(V0, "labels", "Menu Item 1", "Menu Item 2", "Menu Item 3");
```

[Set Property for single value field](https://github.com/blynkkk/blynk-library/blob/master/examples/More/SetProperty/SetProperty\_SingleValue/SetProperty\_SingleValue.ino)

[Set Property for multi value field](https://github.com/blynkkk/blynk-library/blob/master/examples/More/SetProperty/SetProperty\_MultiValue/SetProperty\_MultiValue.ino)

**NOTE :** Changing these parameters work **only** for widgets attached to Virtual pins (analog/digital pins won't work).

`color`, `label` widget properties are supported for all widgets :

`label` is string for label of all widgets.

`color` is string in [HEX](http://www.w3schools.com/html/html\_colors.asp) format (in the form: #RRGGBB, where RR (red), GG (green) and BB (blue) are hexadecimal values between 00 and FF). For example :

```
#define BLYNK_GREEN     "#23C48E"
#define BLYNK_BLUE      "#04C0F8"
#define BLYNK_YELLOW    "#ED9D00"
#define BLYNK_RED       "#D3435C"
#define BLYNK_DARK_BLUE "#5F7CD8"
```

On firmware side, widget objects also support `setLabel()` and `setColor()` functions.

Widget specific properties:

**Button**

`onLabel` / `offLabel` is string for ON/OFF label of button;

**Styled Button**

`onLabel` / `offLabel` is string for ON/OFF label of button;

`onColor` / `offColor` is string in HEX format for ON/OFF colors of the button;

`onBackColor` / `offBackColor` is string in HEX format for ON/OFF colors of the button background.

**Music Player**

`isOnPlay` is boolean accepts true/false.

```
Blynk.setProperty(V0, "isOnPlay", "true");
```

**Menu**

`labels` is list of strings for Menu widget selections;

```
Blynk.setProperty(V0, "labels", "label 1", "label 2", "label 3");
```

**Video Streaming**

```cpp
Blynk.setProperty(V1, "url", "http://my_new_video_url");
```

**Step**

```cpp
Blynk.setProperty(V1, "step", 10);
```

**Image**

```cpp
Blynk.setProperty(V1, "opacity", 50); // 0-100%
```

```cpp
Blynk.setProperty(V1, "scale", 30); // 0-100%
```

```cpp
Blynk.setProperty(V1, "rotation", 10); //0-360 degrees
```

also, you can fully replace the list of images from the hardware:

```cpp
Blynk.setProperty(V1, "urls", "https://image1.jpg", "https://image2.jpg");
```

or you can change individual image by it index:

```cpp
Blynk.setProperty(V1, "url", 1, "https://image1.jpg");
```

You can also change widget properties via [HTTP API](https://docs.blynk.io/en/blynk.cloud/https-api-overview).

**Alarm and Sound**

```cpp
Blynk.setProperty(V1, "isMuted", "true");
```
