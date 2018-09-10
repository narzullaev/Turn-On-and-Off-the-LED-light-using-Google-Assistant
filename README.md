# Turn On and Off the LED light using Google Assistant

## Introduction
In this tutorial we will go through how to do one-way (Google Assistant to NodeMcu) communication with NodeMcu using Google Assistant. At the end of this tutorial you will be able to turn off and turn on the LED light using Google Assistant.   

## Prerequisites
In order to complete this tutorial, you will need to have NodeMcu ESP8266 Wi-Fi boar, 1 LED light and basic knowledge in Arduino programming.

You will also need to perform the following tasks before you can start this guide:
- **Install [Google Assistant](https://itunes.apple.com/us/app/google-assistant/id1220976145?mt=8) if your are an _iPhone_ user**
- **Install [Arduino IDE](https://www.arduino.cc/en/Main/Software) together with [NodeMcu](https://github.com/nodemcu/nodemcu-devkit/tree/master/Drivers) driver**: We will be using Arduino IDE to write and deploy our code to NodeMcu board and for this you should have Arduino IDE installed in your machine together with NodeMcu driver.
- **Create an account at [IFTTT](https://ifttt.com/)**: If This Then That, also known as IFTTT, is a free web-based service to create chains of simple conditional statements, called applets.
- **Create an account at [Adafruit](https://io.adafruit.com/)**: Adafruit will help us to receive signals from IFTTT to NodeMcu board.

## Step One - configuration of Adafruit
First we will go to **[Adafruit](https://io.adafruit.com) > Dashboard** Click **Actions** and **Create A New Dashboard**. We can give whatever name we want.

![screenshot from 2018-09-10 17-32-24](https://user-images.githubusercontent.com/33327894/45289499-e2e3e580-b51f-11e8-88b2-538c2835a237.jpg)

After we created a dashboard open that dashboard and we should be able to see a blank dashboard. There are a few buttons on the top right corner. We should click **+** to add a new block (*I already have them as you can see from the photo below*).  

![screenshot from 2018-09-10 17-39-37](https://user-images.githubusercontent.com/33327894/45289790-a1a00580-b520-11e8-808b-e08815a2777c.jpg)

Next, we will choose our desired block. We need a toggle and it should be the first block in the list of shown blocks. We will add that block.  It should look something like this

![screenshot from 2018-09-10 17-44-03](https://user-images.githubusercontent.com/33327894/45290502-5850b580-b522-11e8-8d2e-650e8bd7f4c4.jpg)

When we choose a new block the new page will appear. We will enter the feed/block name in the field provided and click **Next Step**

![screenshot from 2018-09-10 17-54-09](https://user-images.githubusercontent.com/33327894/45291015-97cbd180-b523-11e8-8dae-62f2f7100f12.jpg)

The next step is the Block Settings. We only need to provide the Block Title, but we can also leave it blank as it is optional. Then, click **Create Block**

![screenshot from 2018-09-10 17-54-36](https://user-images.githubusercontent.com/33327894/45291312-63a4e080-b524-11e8-9b08-c9aaec5cc11b.jpg)

Now we need to create another block to save light status (ON/OFF). For this, follow the above steps, but instead of creating a toggle block choose **Text** block this time and name it as **LightStatus** (we can actually give any name we want, but we need this name as it is, as we will be using this exact same name in our coding later on). We can also change the font size there (Small, Medium, Large, Big, Huge).

## Step Two - Configuration of IFTT
We will start by opening the **[MyApplets](https://ifttt.com/my_applets) page of IFTTT**. We can see that there are no applets yet, so we will create two applets - one for turning on the light and the another for turning of the light. For this, click the **New Applet** button.

![screenshot from 2018-09-10 18-33-12](https://user-images.githubusercontent.com/33327894/45292529-1591dc00-b528-11e8-87e4-f92ab8ab2c81.jpg)

Next, we will create the *if this* part of our applet. You should be able to see the following page when you clicked **New Applet**. From here click on top of **+this**.

![screenshot from 2018-09-10 18-35-07](https://user-images.githubusercontent.com/33327894/45292773-c6987680-b528-11e8-868a-88c57ab5a7d2.jpg)

Then we should choose **Google Assistant** service from the list of the services provided. You can search for it in the field provided. Then, you should be able to see the following page and from there choose **Say a simple phrase**.

![screenshot from 2018-09-10 18-41-35](https://user-images.githubusercontent.com/33327894/45292916-3dce0a80-b529-11e8-8893-e5aa5da35bb4.jpg)

Next, you should complete the trigger fields. You can enter the word which triggers Google Assistant to do something and also you can choose the language from the list of languages provided. In our case the trigger fields are as follows:
- **What do you want to say**: Turn on the light
- **What's another way to say it? (optional**: Lights on (You can leave it blank if you want)
- **And another way? (optional)**: Turn on light
- **What do you want the Assistant to say in response?**: Okay. Turning on the light
- **Language**: English
After completion of those fields click **Create Trigger**.

Now we are done with **if this** part. Next, we will configure the **then that** part. For this click on top of **then that** in the following page.

![screenshot from 2018-09-10 19-04-48](https://user-images.githubusercontent.com/33327894/45294009-79b69f00-b52c-11e8-8db9-39615ffae422.jpg)

Then, from the list of the services we will search for Adafruit. When we found Adafruit we will click on it and we can see **Send data to Adafruit IO** applet there. Next, we will fill in the fields (if you did not connect your IFTTT to Adafruit IFTTT will ask you to connect to Adafruit first). You should be able to choose the **Feed name** from the list of feeds (which we have created earlier). Fill in the fields as follows and click on **Create Action**:

![screenshot from 2018-09-10 19-11-40](https://user-images.githubusercontent.com/33327894/45294307-7bcd2d80-b52d-11e8-8a00-618666f6b524.jpg)

After this step IFTTT will ask you to Review and Finish, click **Finish**. Now we are done with Turning On part.
Next we should create another applet to trigger Adafuit to turn off the light. To do this, follow the steps above and fill in the fields accordingly. This time our aim is to create another applet to turn off the light, thus we will change **What do you want to say**: *Turn on the light part* **to** *Turn off the light* and other changes as follows:
### **IF This** part
 -**What do you want the Assistant to say in response?**: Okay. Turning on the light **to** Okay. Turning off the light.
### **If That** part
- (Adafruit)**Data to save**: ON **to** OFF

Now we are done with configuration of Adafruit and IFTTT so lets move on to coding part.

## Step Three - Coding and Deploying
In this section we will deal with Coding and Deploying. The source code is already provided (Google Assistant Tutorial) and all you need to do is just change some fields in the source code, but before that we need to install required libraries.

### Installing the list of libraries to our Arduino IDE
There is a library manager in each Arduino IDE under **Sketch>Include Library>Manage Library** path. When you get there wait a minute for Arduino to update the list of libraries. Then, there is a search filed provided and you can search and instll the following libraries:
- _ESP8266WiFi_
- _Adafruit_MQTT_

**Example**

![screenshot from 2018-09-10 17-13-39](https://user-images.githubusercontent.com/33327894/45288712-e9715d80-b51d-11e8-80a1-7a139485eedf.jpg)

### Coding and Deploying
Next, download the source code and change the following parts:

1. Enter Wi-Fi SSID and Password to connect NodeMcu to internet.
```C++
#define WIFI_SSID "Your Wi-Fi SSID"         // enter your wifi SSID
#define WIFI_PASS "Your Wi-Fi Password"     // enter the Password
```
2. Enter your Adafruit AIO KEY to following line of codes
```C++
#define MQTT_NAME "your Adafruit username here"          // enter your Adafruit user name here
#define MQTT_PASS "your Adafruit AIO key here"        // you can get this from your Adafruit
```
To obtain username and AIO key go to your Adafruit Lights dashboard and click on **key** button on the top right corner then you should be able to see the following page.

![screenshot from 2018-09-10 21-20-57 1](https://user-images.githubusercontent.com/33327894/45300152-2e0df080-b540-11e8-8e79-d2a86686bd37.jpg)

Finally, upload the code to NodeMcu.
