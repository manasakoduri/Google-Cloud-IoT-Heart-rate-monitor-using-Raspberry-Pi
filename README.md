# Google-Cloud-IoT-Heart-rate-monitor-using-Raspberry-Pi

## Introduction

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


## Raspberry Pi Setup

**Step 1:** Insert memory card into the computer/laptop. Install the "raspberry pi OS" into the SD card. Use raspberry pi imager to format and install OS. SD card must be formatted properly in order to boot the OS image. During this process, configure the ssh and WiFi connection details. The process will take around 15 minutes until it successfully writes and verifies OS. 

Follow the steps in the link [Install raspberry pi OS](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)


Once the image is installed on the sd card, enable the headless connection by creating a file in the boot folder.

Insert the SD card into the raspberry kit and switch on the device. Red light will be seen when the system is fully functional.

Connect the raspberry kit to a monitor and a heart rate sensor. 
After the raspberry pi kit boots up, connect to the kit using ssh or putty.

Verify the raspberry pi connection using ssh via putty or terminal. Below are the commands to verify the headless connection.

  ssh pi@raspberrypi.local
  
  and enter password when prompted.
* Clone heart rate receiver program on to the raspberry pi using below commands

  git clone https://github.com/googlecodelabs/iotcore-heartrate
  
  cd iotcore-heartrate
  
  ## Monitoring Heart rate
  
* Connect to the raspberry pi using the ssh terminal as per the steps provided in the "Raspberry Pi Setup" section above.
* Navigate to the directory of the heart rate program using below command

  cd /home/pi/iotcore-heartrate
  
* Start the heart rate script using below command. Project id, registry id and device id must match with the google cloud setup.
  
  python checkHeartRate.py --project_id=myproject --registry_id=myregistry --device_id=mydevice
  
* Terminal will show the echo messages which shows collecting heart rate data and making subscription. 

  

## Reading and Visualizing data

Data can be read from the BigQuery table and visualized using Google Sheets.

**Step 1:** Verify the heart rate data by accessing [BigQuery](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=rare-disk-306423&ws=!1m0)

**Step 2:** Navigate to BigQuery and query the table to see the recorded data.

**Step 3:** Export/save the table records into google sheets.

**Step 4:** Go to the "Insert" menu and insert the charts, to convert the data into charts.

## References

https://codelabs.developers.google.com/codelabs/iotcore-heartrate#8
https://cloud.google.com/iot/docs/how-tos/credentials/keys
https://www.raspberrypi.org/documentation/configuration/wireless/headless.md
https://www.raspberrypi.org/documentation/installation/installing-images/README.md
https://www.raspberrypi.org/documentation/remote-access/ssh/README.md

## Summary




