# Turn On and Off the LED light using Google Assistant 

## Introduction 
In this tutotrial we will go through how to do one-way (Google Assistant to NodeMcu) communication with NodeMcu using Google Assistant. At the end of this tutorial you will be able to turn off and turn on the LED light using Google Assistant.  

## Prerequisites
In order to complete this tutorial, you will need to have NodeMcu ESP8266 Wi-Fi boar and 1 LED light.

You will also need to perform the following tasks before you can start this guide:
- **Install [Google Assistant](https://itunes.apple.com/us/app/google-assistant/id1220976145?mt=8) if your are an _iPhone_ user**
- **Install [Arduino IDE](https://www.arduino.cc/en/Main/Software) together with [NodeMcu](https://github.com/nodemcu/nodemcu-devkit/tree/master/Drivers) driver**: We will be using Arduino IDE to write and deploy our code to NodeMcu board and for this you should have Arduino IDE installed in your machine tgether with NodeMcu driver. 
- **Create an account at [IFTT](https://ifttt.com/)**: If This Then That, also known as IFTTT, is a free web-based service to create chains of simple conditional statements, called applets.
- **Create an account at [Adafruit](https://io.adafruit.com/)**: Adafruit will help us to recieve signals from IFTT to NodeMcu board. 

## Step One - Installing list of libraries to our Arduino IDE
There is a library manager in each Arduino IDE under **Sketch>Include Library>Manage Library** path. When you get there there wait a minute for Arduino to update the list of libraries. There is a search bar provided and you can search and instll the following libraries: 
- _ESP8266WiFi_
- _Adafruit_MQTT_

**Example**

![screenshot from 2018-09-10 17-13-39](https://user-images.githubusercontent.com/33327894/45288712-e9715d80-b51d-11e8-80a1-7a139485eedf.jpg)

## Step Two - Configuration of Adafruit.  
First we will go to **[Adafruit](https://io.adafruit.com) > Dashboard** Click **Actions** and **Create A New Dashboard**. We can give whatever name we want.

![screenshot from 2018-09-10 17-32-24](https://user-images.githubusercontent.com/33327894/45289499-e2e3e580-b51f-11e8-88b2-538c2835a237.jpg)

After we created a dashboard open that dashboard and we should be able to see a blank dashboard. There are a few buttons on the top right corner. We should click **+** to add a newblock (*I already have them*).  

![screenshot from 2018-09-10 17-39-37](https://user-images.githubusercontent.com/33327894/45289790-a1a00580-b520-11e8-808b-e08815a2777c.jpg)

Next, we will choose our desired block. We need a toggle and it should be the first block in the list of shown blocks. We will add that block.  It should look something like this

![screenshot from 2018-09-10 17-44-03](https://user-images.githubusercontent.com/33327894/45290502-5850b580-b522-11e8-8d2e-650e8bd7f4c4.jpg)

When we choose a new block the new page will appear. We will enter the feed/block name in the space provided and click **Next Step**

![screenshot from 2018-09-10 17-54-09](https://user-images.githubusercontent.com/33327894/45291015-97cbd180-b523-11e8-8dae-62f2f7100f12.jpg)

The next step is the Block Settings. We only need to provide the Block Title, but we can also leave it blank as it is optional. Then, click **Create Block**

![screenshot from 2018-09-10 17-54-36](https://user-images.githubusercontent.com/33327894/45291312-63a4e080-b524-11e8-9b08-c9aaec5cc11b.jpg)

Now we need to create another block to save light status (ON/OFF). For this, follow the above steps, but instead of creating a toggle block choose **Text** block this time and name it as **LightStatus** (we can actually give any name we want, but we need this name as it is as we will be using this exact same name in our coding later on). We can also change the font size there (Small, Medium, Large, Big, Huge). 

## Step Three - Configuration of IFTT 
We will start by opennig the **[MyApplets](https://ifttt.com/my_applets) page of IFTT**. We can see that there are no applets yet, so we will create two applets - one for turning on the light and the another for turnning of the light. For this, click the **New Applet** button. 

![screenshot from 2018-09-10 18-33-12](https://user-images.githubusercontent.com/33327894/45292529-1591dc00-b528-11e8-87e4-f92ab8ab2c81.jpg)

Next, we will create the *if this* part of our applet. You should be able to see the following page when you clicked **New Applet**. From here click on top of **+this**. 

![screenshot from 2018-09-10 18-35-07](https://user-images.githubusercontent.com/33327894/45292773-c6987680-b528-11e8-868a-88c57ab5a7d2.jpg)

Then we should choose **Google Assitant** service from the list of the services provided. You can search for it in the space provided. Then, you should be able to see the followng page and from there choose **Say a simple phrase**. 

![screenshot from 2018-09-10 18-41-35](https://user-images.githubusercontent.com/33327894/45292916-3dce0a80-b529-11e8-8893-e5aa5da35bb4.jpg)



