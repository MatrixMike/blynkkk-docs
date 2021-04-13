# Template Quick Setup

Device Template is a set of configurations inherited by devices of a similar type. 

Think about smart home switches. They all perform a similar function and it's safe to assume that they should have the same data model, GPIOs, firmware code, etc. If you would need to introduce changes to all of these devices, instead of editing each of them you could just edit a Device Template and all devices will be updated.

## Tutorial Overview

Device Template has a lot of settings, but in this tutorial, we will focus only on the most important things you can set up quickly.

At the end of this tutorial, you will have your first working device which will:

* send random values to the web and mobile dashboard in intervals
* receive user input from the web or mobile dashboard 

{% hint style="info" %}
You would need a development board \(e.g. Node MCU, Arduino\). List of supported boards can be found here.
{% endhint %}

Full documentation on all of the Template settings can be found [here](../../web-dashboard/products/porducts-management.md):

{% page-ref page="../../web-dashboard/products/porducts-management.md" %}

## 1. Edit/Create Template

Open the Templates section in the left menu and click **+ New Template** button**.** If you already have a template - click to open it and press **Edit** button.

![](../../.gitbook/assets/open-templates.gif)



## 2. **Basic** Settings

Give your new template a name,  specify the hardware and connectivity you will be using.

{% hint style="info" %}
 If you can't find your hardware in the list choose **Generic Board**
{% endhint %}

![](../../.gitbook/assets/create_new_template_modal.png)

## 3. Find **Template ID**

A new Template was created. On this screen notice **Template ID** and **Firmware Configuration** sections. You will need these details later in your sketch.  

![](../../.gitbook/assets/image%20%2820%29.png)



## 5. **Set Up Mobile Dashboard**

## Link mobile dashboard with your product:

1. Open [Blynk.App](../../mobile-applications/overview.md)
2. Log In to your account
3. Switch to [Developer Mode](../developer-mode.md)
4. Add a new Template 
5. Link it to your Product 
6. Add the widgets you need and assign them Datastreams
7. Publish the changes 

## Configure your board:

1. Open Dynamic Provisioning Template: - [ESP8266 ](https://github.com/blynkkk/blynk-library/tree/master/examples/Blynk.Inject/Template_ESP8266)- [ESP32 ](https://github.com/blynkkk/blynk-library/tree/master/examples/Blynk.Inject/Template_ESP32)- [MKR1000 ](https://github.com/blynkkk/blynk-library/tree/master/examples/Blynk.Inject/Template_MKR1000)- [MKR1010](https://github.com/blynkkk/blynk-library/tree/master/examples/Blynk.Inject/Template_MKR1010) 
2. Specify [TMPLID](https://docs.blynk.io/en/web-dashboard/for-developers/products/info/template-ids), [SSID WiFi](../../web-dashboard/products/info/hotspot-prefix.md) and Board Name in the [sketch](../activating-devices/)
3. Flash this template to your board

### Congratulations, you have configured your Product and it is ready to use!

Now all that remains is to [add your test board using Blynk.App](../../mobile-applications/device-management/add-new-device.md), make sure it works as you expect, and integrate your code.

 


