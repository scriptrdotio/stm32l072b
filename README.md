# What is stm32l072b

Simple demo application that receives decrypted or encrypted data (temperature, humidity, pressure, battery level), sent by a LoRaWAN gateway on behalf of LoRaWAN enabled STM32L072B device.
The application persists the data and publishes latest and last 10 historical values to a dashboard.

# Pre-requisites

1. [Sign-up for a (free) scriptr.io account](https://www.scriptr.io/register)
2. Connect your scriptr.io account to Github using the instructions listed [here](https://github.com/scriptrdotio/howto/blob/master/teamwork/version_control.md#connecting-your-scriptr-account-to-github)

# How to install

Sign-in to your [scriptr.io workspace](https://www.scriptr.io/workspace)

Import the stm32l072b scripts into your workspace as follows:

- Click on the arrow near +New Script in the bottom-left corner of the screen and select Install module
- Click on Add Custom Module from GitHub, then fill the fields of the Modules dialog:
  - Owner: use scriptrdotio
  - Repository: set it to stm32l072b
  - Path: leave it empty
  - Branch: set it to master
  - Destination folder: set it to /stm32l072b

Click Install once done. This will import all the scripts to your workspace.

# How to configure the application

## Automatic configuration

- In the tree view on the left, open the /stm32l072b/config script
- Replace the value of the appsKey variable with the one used by the client application running on the stm32 device 
- Optionally, you can specify a sub-domain name for your scriptr.io account 
- In the tree view on the left, open the /stm32l072b/installer/install script then click Run. This will configure your account as needed

## Manual configuration

### Create the stm32l072b channel
This channel is used by the dashboard to obtain real-time updates, published by the ingest script
- Click on your username in the top-right corner of the workspace
- Select Settings then click on the Channels tab
- Click on +Add Channel
- Type stm32l072b in the channel name field
- Check Allow anonymous subscription
- Click on the check button to create the channel

### Create a sub-domain
- Click on your username in the top-right corner of the workspace
- Click on Account then on the Sub-domain tab
- Enter a sub-domain name
- Validate by clicking on the check button

### Schedule the /install/storekeeper script
This script cleans up the documents (records) that are created by the application
- In the tree view on the left, open the /stm32l072b/installer/storekeeper script
- In the toolbar, click on the Schedule button
- In the dialog, click on +Add Trigger, then click on Select then Every
- Click on Advanced and enter the following cron expression 0/5 * * * ? (will run every 5 minutes)
- Validate by clicking on the check button

# About the scripts

- ingest: receives data sent by the gateway. It can decrypt the data in case it is declared as encrypted
- latest: returns the latest recorded metrics (temperature, humidity, pressure, battery level)
- historical: returns the 10 latest records (temperature, humidity, pressure) with their creationDate
- dashboard: a simple dashboard that is automatically updated whenever data is received
- config: configuration script, mainly contains the appsKey to use to decrypt data (only if needed)

- /installer/install: utility script to automatically configure your account
- /installer/storekeeper: a script that is scheduled to run automatically at regular intervals to clean-up your data store and avoir bloating it with too many records 
 
