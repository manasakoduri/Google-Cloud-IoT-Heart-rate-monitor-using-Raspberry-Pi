# Google-Cloud-IoT-Heart-rate-monitor-using-Raspberry-Pi

## Introduction

Google cloud IoT is a fully managed service that provides secure connection to the devices and management. IoT Core, in combination with other services, such as Cloud Storage, Dataflow, Pub/Sub, BigQuery, will provide a complete solution for reading, streaming, analysing and visualization of data. In this project, we are going to build a data pipeline that reads heart rate from IoT device, publishes the data to google pub/sub subscription and saves it to BigQuery table. For this process, we used raspberry pi kit connected to a heart rate sensor and google cloud platform services (IoT Core, Cloud Storage, DataFlow, BigQuery and Pub/Sub). We can follow the below process to setup the google cloud, raspberry pi kit, generate and visualize the heart rate data.

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

* Insert memory card into the computer/laptop. Format and install the "raspberry pi OS" into the SD card using "raspberry pi imager". The process will take around 15 minutes until it successfully writes and verifies OS. During this process, configure the ssh and WiFi connection details.

![Picture1](https://user-images.githubusercontent.com/81333454/117594653-34473700-b104-11eb-9aa2-fb5045a97f89.png)

* To install raspberry pi OS image, follow the steps in the link [Install raspberry pi OS](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

* After installation, insert the SD card into the raspberry pi kit, connect the heart rate sensor and switch on the device. Red light will be seen when the system is fully functional.

![Picture2](https://user-images.githubusercontent.com/81333454/117594800-825c3a80-b104-11eb-9252-7be38427dc7d.png)

* After the raspberry pi kit boots up, connect to the kit using ssh or putty.

* Verify the raspberry pi connection using ssh via putty or terminal. 

* Below is the command to verify the headless connection:
  ```
  ssh pi@raspberrypi.local
  ```
 * When prompted, enter the password "raspberry"

 ### Install heart rate monitor software
 
 The software on the raspberry pi should be up to date.
 Use the below commands to update and install git and heart rate monitor programs
 ```
 sudo apt-get update
 sudo apt-get install git
 
 git clone https://github.com/googlecodelabs/iotcore-heartrate
 cd iotcore-heartrate
 ```
  
  ## Monitoring Heart rate
  
* Connect to the raspberry pi using the ssh terminal as per the steps provided in the "Raspberry Pi Setup" section above.

* Navigate to the directory of the heart rate program using below command
  ```
  cd /home/pi/iotcore-heartrate
  ```
* Start the heart rate script using below command. 
  Project id, registry id and device id must match with the google cloud setup.
  ```
  python checkHeartRate.py --project_id=myproject --registry_id=myregistry --device_id=mydevice
  ```
* Terminal will show the echo messages which shows collecting heart rate data and making subscription. 

* Now provide heart rate by holding the heart rate sensor.

* Data will be transmitted and published to the pub/sub subscription on the google cloud

![Screen Shot 2021-05-06 at 1 59 53 PM](https://user-images.githubusercontent.com/81333454/117594331-86d42380-b103-11eb-983a-e1b490ee315a.jpg)


## Reading and Visualizing data

Data can be read from the BigQuery table and visualized using Google Sheets.

**Step 1:** Verify the heart rate data by accessing [BigQuery](https://console.cloud.google.com/bigquery?utm_source=bqui&utm_medium=link&utm_campaign=classic&project=rare-disk-306423&ws=!1m0)

**Step 2:** Navigate to BigQuery and query the table to see the recorded data using below query.

```
SELECT * FROM `it432-iot-heartrate.heartratedata.heartRateDataTable`
```
<img width="350" alt="Screen Shot 2021-05-06 at 2 13 01 PM" src="https://user-images.githubusercontent.com/81333454/117594193-2d6bf480-b103-11eb-8f84-6488256e3cb2.png">

**Step 3:** Export/save the table records into google sheets. Click "save results" and select "google sheets" from the drop down list.

**Step 4:** Open this sheet on the google sheets account. Select the "time collected" and "heart rate" columns.

**Step 5:** Then go to the "Insert" menu, click on the "chart" option to convert the data into charts.

<img width="819" alt="Screen Shot 2021-05-06 at 2 14 29 PM" src="https://user-images.githubusercontent.com/81333454/117594090-0e6d6280-b103-11eb-9497-0218f6d6c4aa.png">


## References

[Using IoT Core to Stream Heart Rate Data](https://codelabs.developers.google.com/codelabs/iotcore-heartrate#0)

[Creating public/private key pairs](https://cloud.google.com/iot/docs/how-tos/credentials/keys)

[Setting up a Raspberry Pi headless](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)

[Installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)

[SSH (Secure Shell)](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md)


## Summary

This report gives an idea of how heart rate can be captured and published to google cloud platform using raspberry pi. We successfully created the required project with IoT core registry device which will be useful to establish connection to the raspberry pi kit. We also created the pub/sub subscription which will be used to publish heart rate data. And finally we created the dataflow job which is responsible for reading the data from the subscription and saving the data to big query table. We exported the data to google sheets and generated a chart to visualize the heart rate data. 

