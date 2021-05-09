# Google-Cloud-IoT-Heart-rate-monitor-using-Raspberry-Pi

## Hardware/Software Requirements
* Raspberry Pi kit
* 8GB SD memory card with usb card reader
* Power supply
* Heartrate sensor
* Wifi connection
* Google cloud platform account

## Google Cloud Setup

**Step 1:** Create an account on google cloud platform or sign in to existing google cloud console at [Google Cloud Console](https://console.cloud.google.com)

**Step 2:** Create a new project with a unique name on the cloud console.

**Step 3:** Enable Pub/Sub API's from console menu "APIs & Services". This API's must be enabled in order to use dataflow, IoT Core.

**Step 4:** Create BigQuery table to hold all the heart rate data. This can be done by creating a dataset from "BigQuery" menu on the cloud console. Add a new table to the dataset. This table will hold all the heart rate data that is received from the raspberry pi.

**Step 5:** Create a Pub/Sub subscription which is responsible for handling the incoming IoT messages. To create a subscription, navigate to cloud console and select "Pub/Sub" and create a "new topic". From submenu of the topic, create a subscription with delivery type pull.

**Step 6:** Create a bucket using "cloud storage" option on the cloud console. This storage will be used as a temporary location by the dataflow template.

**Step 7:** Create a dataflow template using "Dataflow" option on the cloud console. Dataflow job is responsible for monitoring the incoming messages on the Pub/Sub subscription and move the data to BigQuery. 

**Step 8:** Create google cloud IoT registry which allows you to easily and securely connect, manage, and ingest data from external devices. Registry can be created using "IoT Core" option on the cloud console.

**Step 9:** Create an IoT core registry and add a device to the registry. Then generate the public key in ES256 format. For device authentication, either choose upload and upload the key from the computer, or choose manual and copy/paste the key from the key file to the the public key box.


##Raspberry Pi Setup

**Step 1:** Install the raspberry pi OS into the SD card. 
Insert memory card into the computer/laptop. 
For MacOS users, download Raspberry pi imager to format

