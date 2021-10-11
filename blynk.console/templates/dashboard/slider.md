# Slider

_**Note:**_ please remember that web and apps widgets are set up separately and may have same datastreams set to view the same data (excepts Map widgets – those two use different codebase now).\
\
Slider widget allows to send values to Virtual Pin of the selected Device. \
Usage examples: volume, brightness, RPM, flap position control, etc.

* Name the Slider widget by editing **Slider** inside top field; 
* **Choose Source** – select Datastream;
  * **Min** and **Max** – will be automatically taken from selected Datastream default value; 
    * **Send values on release only (optimal)** – we recommend to use this option to avoid misclick-like issues and decrease traffic to/from the Device (critical for GSM connection);  
* **Steps**  
  * **Step** – defines value change per one slider step, e.g. 20° per 1 slider move;
  * **Show fine controls** – adds - and + buttons to operate the slider;
    * **Fine Control Step** – defines value change per one fine control button click, e.g. 5° per click;
* **Value**  
  * **Value position** – left or right side to the Slider;
  * **Suffix** – type the unit you want to be viewed near the value.

![Slider widget setup demo](../../../.gitbook/assets/slider_setup.gif)
