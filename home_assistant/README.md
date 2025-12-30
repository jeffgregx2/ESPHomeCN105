# ESPHome - Home Assistant Support
Once you have the appropriate hardware to support the ESPHomeCN105 firmware, you need to setup the appropriate YAML files in ESPHome.  In my case this is attached to [Home Assistant](https://www.home-assistant.io) making it effortless to both interact as well as make other devices available such as temperature sensors.  While you may only have one (1) split-mini wall unit, once you have two (2) or more units setting up the configurations can result in lots of duplication, etc. between the various YAML files.  To help minimize this I have created a set of include files that hopefully make reuse across multiple device simple and straightforward.  

All of the configuration needed to use these include files is done via the substition command within ESPHome YAML files. This allows for high reusability of code within the devices being created which will hopefully reduce bugs and enable the devices to behave similarly.

Please note that these files are aligned to the hardware described in [PCB_assembly](/pcb_assembly/) and specifically the use of the ESP32-C6 dev kit.  If you are using different hardware slight tweaks will be required.

##  Overview
The functionality provided by the defined YAML files includes:
* Climate device for Mitsubishi CN105 split-mini
* LED status indicator: Red = not connected to CN105, Green = Connected : blinks every 1.5 seconds
* Home Assistant API integration
* Remote Temperature sensor definition and logic to update CN105 periodically to ensure split-mini internal sensor is not used if a valid remote sensor value is available.
* i2c bus initialization to allow i2c sensors to be installed and used
* Various diagnostic information reported to Home Assistant

There are multiple include files that break up the functionality allowing you to load those portions that you need.  These files are as follows:
* **mitsubishi_cn105_device_base.yaml** - Required - this is the core include file that you must always load containing all of the climate device definitions. 
* **mitsubishi_cn105_config.yaml** - Required - this contains the hardware module definitions, logging, web server definitions as well as home assistant integration.  Note that this file is aligned to the ESP32-c6 dev kit and would need modification to work with other boards.
* **One of the following:**
	* **mitsubishi_cn105_remote_temp.yaml** -  this connects to a home assistant device that will provide temperature sensor information that will be used to set the remote temperature in the climate device. 
	* **mitsubishi_cn105_remote_temp_dual.yaml** - a more sophisticated version of mitsubishi_cn105_remote_temp.yaml that support two (2) remote sensor devices that can be setup as either a primary/backup configuration or an average of the two.  This is useful in situations in which one of the sensors is not entirely accurate but you would prefer an external temperature vs the internal sensor from the split mini (which tends to not be accurate).
	* **mitsubishi_cn105_remote_temp_none.yaml** - indicates that no remote temperature device will be used.
* **One of the following:**
   Since WiFi is required, either the static or dynamic configuration must be included (but only one of them!).
	* **mitsubishi_cn105_wifi_dynamic.yaml** - This include file sets up DHCP provisioning of the network address.  In many situations this is the best option.  If you have a "flat" network (i.e., home router/wifi that everything directly connects to) this will work well.
	* **mitsubishi_cn105_wifi_static.yaml** - This include file sets up the use of static IP address for the device - DHCP is disabled!  If you have separated your ESPHome/IoT devices into a different network (VLAN, etc.) assigning static IP addresses is by far the best approach to ensure reliable connection via the ESPHome Builder.  It will require you recording the IP addresses you have assigned to ensure that two devices don't get the same IP address (this will break things).

While this looks like a lot, take a look at the examples which will demonstrate usage that is hopefully very straightforward.

## Installation
There are two ways you can use the include files in your Home Assistant configuration:
1. **REMOTE** - Referenced directly from the files stored in GitHub, nothing is installed locally except for the device's YAML file.  The primary advantage is nothing to install locally, just create the normal device YAML file and reference the GitHub include files.  Unless you plan on making local changes this is likely the best approach.
2. **LOCAL** - Installed directly in Home Assistant and locally referenced within a device's YAML file.  The examples in this README are using local copies of the files.  The primary advantage to using local files is the ability to make local changes to core files.  However it requires substantially more work to deploy new updates from GitHub should they occur since you need to merge the changes together.

### Installing locally
In order to reference the include files in your device YAML file, you need to place all of the files located at [home_assistant/common](/home_assistant/common/) into an appropriate location in Home Assistant using either the terminal or a tool such as the [File Editor Add-On](https://github.com/home-assistant/addons?tab=readme-ov-file).

It is recommended that you copy the files to homeassistant/esphome/common (creating the 'common' directory first).  Once you have uploaded the files you should see them as follows (this examples uses File Editor):

![File Editor example](/images/HA-File-editor.png)

## Simple Usage
In the simplest of cases, you can define a climate device with no remote sensors as follows:
### Remote include files
```
#
# Load the device configuration for Mitsubishi CN105 Controller.  This is a direct
# replacement for Mitsubishi Kumo Cloud Wifi Controller (Model PAC-USWHS002-WF-1/WF-2)
#
packages:
  - github://jeffgregx2/ESPHomeCN105/home_assistant/common/mitsubishi_cn105_config.yaml@v1.1
  - github://jeffgregx2/ESPHomeCN105/home_assistant/common/mitsubishi_cn105_wifi_dynamic.yaml@v1.1
  - github://jeffgregx2/ESPHomeCN105/home_assistant/common/mitsubishi_cn105_remote_temp_none.yaml@v1.1
  - github://jeffgregx2/ESPHomeCN105/home_assistant/common/mitsubishi_cn105_device_base.yaml@v1.1

# The packages have requirements regarding substitutions that need to be answered.
substitutions:
  name: midu-climate-guest-bedroom
  friendly_name: Mitsubishi Guest Bedroom
  
  # Wifi Setup - static configuration
  wifi_ssid: !secret wifi_iot_ssid
  wifi_password: !secret wifi_iot_password

  # Wifi Access Point Fallback
  wifi_ap_fallback_ssid: !secret fallback_ssid_midu_guest_bedroom
  wifi_ap_fallback_password: !secret fallback_password_midu_guest_bedroom

  # Various passwords
  api_key: !secret api_key_midu_guest_bedroom
  ota_key: !secret ota_key_midu_guest_bedroom

  # Setup web server authentication
  # To disable the web server add the following after the substitution section:
  #     web_server: !remove
  ws_username: !secret web_server_username
  ws_password: !secret web_server_password

 # Disable the web server component
web_server: !remove
```
Please note the '@v1.1' indicates that you only want version 1.1.  If you are not familiar with Git, this is a "tag" that was created to mark files at a specific point in time with a name (in this case "v1.1").  If you use "@main" then you would be using the latest version available in the repository.  By specifying a specific version you reduce the chances of breaking changes within the include files.  However you might miss an enhancement or a fix needed to maintain compatibility with the ESPHome and Home Assistant requiring manual intervention.

### Local include files
The only changes necessary to move to a local directory are in the packages definition:
```
packages:
  - !include common/mitsubishi_cn105_config.yaml
  - !include common/mitsubishi_cn105_wifi_dynamic.yaml
  - !include common/mitsubishi_cn105_remote_temp_none.yaml
  - !include common/mitsubishi_cn105_device_base.yaml
```
The directory specified must match the location you copied in the files in the [Installing Locally](#installing-locally) section.

## Detailed Examples
Click [HERE](/home_assistant/examples/) or more detailed examples
