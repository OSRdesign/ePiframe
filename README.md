<img align="right" src="https://github.com/MikeGawi/ePiframe/blob/master/assets/logo.png">


# ePiframe

Python 3 e-Paper Raspberry Pi Photo Frame with Google Photos, weather information, Telegram Bot, Web User Interface and API.


## Table of Contents
<!--ts-->
   * [Main features](#main-features)
      * [New features](#new-features-)
   * [Hardware required](#hardware-required)
      * [Frame](#frame)
   * [Advantages](#advantages)
   * [Installation](#installation)
      * [Automatic](#automatic)
      * [Manual](#manual)
      * [Next steps](#next-steps)
      	* [Weather Stamp](#weather-stamp)
      	* [Telegram Bot](#telegram-bot)
      	* [Web User Interface](#web-user-interface)
			* [WebUI Users](#webui-users)
			* [API](#api)
   * [Update](#update)
      * [Update Automatically](#update-automatically)
      * [Update Manually](#update-manually)
   * [Uninstalling](#uninstalling)
      * [Automatic](#automatic-1)
      * [Manual](#manual-1)
      * [Next steps](#next-steps-1)
   * [Configuration](#configuration)
   * [Command line](#command-line)
   * [Debugging](#debugging)
   * [Performance](#performance) 
   * [Service control](#service-control)
   * [Flow](#flow)
   * [Future plans](#future-plans)
   * [Resources](#resources)
   * [This is not what I'm looking for](#this-is-not-what-im-looking-for)
<!--te-->


## Main features

* Pulls photos (videos are ignored) from one or more albums in Google Photos and automatically prepares them for attached e-Paper display
* Non-HDMI e-Paper Waveshare SPI displays supported
* No additional storage or 3rd party software is required as only one and current photo is downloaded and processed per frame update
* Updating after time interval with option to change time per photo (by *hot word* in photo description)
* Off hours per different days
* Photo filtering (by creation date, number of images)
* Showing randomly, descendingly or ascendingly by creation date
* Automatic conversion to black-and-white with 6 different presets, color inversion and various background colors 
* For vertical or horizontal frame position
* Even for Raspberry Pi Zero W + Raspberry Pi OS Lite
* Low power consumption

![](https://github.com/MikeGawi/ePiframe/blob/master/assets/frame.gif)

### New features 🎉

* (06.10.2021 since [ePiframe v0.9.3 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.3-beta)) Weather stamp (optional) - subtly showing current weather icon and temperature in defined display corner, size and color. Taken from free API of [OpenWeather](https://openweathermap.org/api) according to [Maps.ie](https://www.maps.ie/coordinates.html) coordinates - [#3](https://github.com/MikeGawi/ePiframe/issues/3)
* (14.10.2021 since [ePiframe v0.9.4 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.4-beta)) Telegram Bot (optional) - control the ePiframe with few commands from Telegram IM - [#5](https://github.com/MikeGawi/ePiframe/issues/5)
* (20.11.2021 since [ePiframe v0.9.6 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.6-beta)) WebUI (optional) - control the ePiframe with web user interface - [#9](https://github.com/MikeGawi/ePiframe/issues/9)
* (28.11.2021 since [ePiframe v0.9.7 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.7-beta)) Users and passwords for web interface - [#15](https://github.com/MikeGawi/ePiframe/issues/15)
* (05.12.2021 since [ePiframe v0.9.8 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.8-beta)) API - [#17](https://github.com/MikeGawi/ePiframe/issues/17)

| Color presets             | Different backgrounds     |
|:-------------------------:|:-------------------------:|
| ![](https://github.com/MikeGawi/ePiframe/blob/master/assets/movie.gif) | ![](https://github.com/MikeGawi/ePiframe/blob/master/assets/movie2.gif) |
|<ul align="left"><li>Floyd-Steinberg dither + enhanced contrast</li><li>Floyd-Steinberg dither + high remap</li><li>GIMP-like result</li><li>Floyd-Steinberg ordered dither</li><li>direct conversion to black-and-white</li><li>simple conversion to black-and-white + basic dither</li><li>inverted colors (all presets above will work with this function)</li></ul> |<ul align="left"><li>white</li><li>black</li><li>blurred and enlarged source photo to cover empty areas</li></ul> |


## Hardware required

<a href="http://www.raspberrypi.org"><img width="100" align="right" src="https://github.com/MikeGawi/ePiframe/blob/master/assets/RPi-Logo.png"></a>

* A Raspberry Pi (Zero W, 1, 2 were tested but I am sure all will work)
* [microSD card for Raspberry Pi OS](https://www.raspberrypi.org/documentation/installation/sd-cards.md), 4GB minimum
* [e-Paper Waveshare SPI display](https://www.waveshare.com/product/raspberry-pi/displays/e-paper.htm) (7.5 inch black and white with RasPi HAT was used but probably all B&W will work out-of-the-box, the rest as well but with small modifications)
* Raspberry Pi power supply (as display is usually powered from RasPi HAT then 5V/3A is preferred)
* Photo frame (for 7.5" screen I used 13x18cm /5"x7"/ with printed parts)


### Frame

You can use any photo frame for your ePiframe and cut the back to make place for the display connector and glue Raspberry Pi with HAT on to it. Also a good passe-partout piece should frame your display and cover all unwanted elements. 

Or you can 3D print a nice standing frame back with case for your Raspberry Pi and even passe-partout and assemble it with bought photo frame like I did here:

|<img src="https://github.com/MikeGawi/ePiframe/blob/master/assets/frame1.jpg" width="500"/>| 
|:--:| 
|*Printed back (black) of 13x18cm (5"x7") frame for 7.5" screen with passe-partout (white)*|

[Thing files](https://www.thingiverse.com/thing:4727060)


## Advantages

* Low power consuming and cheap ($90) photo frame on Raspberry Pi Zero W pulling photos from Google Photos albums shared between users who can modify the content
* Autonomic device, once configured can be left headless
* e-Paper display gives an unique look and you don't need to worry about ambient light control, light sensors or turning off screen light functions (as with LCDs)
* Photo is displayed even if power (or network) is down as e-Paper takes power only during refresh and doesn't have back light - so no blank frames
* Powerful [ImageMagick](https://imagemagick.org/) on board to convert photos on the fly and adjust them to the display. No matter what quality and what size they are
* Supports all image formats including RAW
* Currently displayed photo can be removed from the album but ePiframe will remember where to continue
* Simple script in Python to automate frame update, everything is configurable (within one [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file) and in one place
* System service supervising whole process that is auto recovering and auto starting by itself
* Fully customizable: from photos and how they are displayed (presets, different backgrounds or completely change [ImageMagick conversion](https://legacy.imagemagick.org/Usage/quantize/)), to display size and frame (buy one, print it or create/decorate it yourself)
* Simple yet powerful

ePiframe is a very nice handmade gift idea: create an album that whole family can edit, decorate frame (e.g. [decoupage](https://en.wikipedia.org/wiki/Decoupage)) or print it, print family signatures or baby drawings on the back, put some wishes picture on the display before handing it (using [command line](#command-line)) and many more. 


## Installation

* [Install Raspberry Pi OS](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) formerly known as Raspbian. Lite version is supported
* [Setup network connection](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
* [Enable SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) - chapter *3. Enable SSH on a headless Raspberry Pi (add file to SD card on another machine)*
* [Assemble Raspberry Pi and power it](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up)
* [Find Raspberry Pi IP address](https://www.raspberrypi.org/documentation/remote-access/ip-address.md)
* [Log in with SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) - chapter *4. Set up your client*
* [Configure Raspberry Pi](https://www.raspberrypi.org/documentation/configuration/raspi-config.md)
* [Update Raspberry Pi](https://www.raspberrypi.org/documentation/raspbian/updating.md)


### Automatic

Use *install.sh* script:

```
wget https://raw.githubusercontent.com/MikeGawi/ePiframe/master/install.sh -O install_now.sh
chmod +x install_now.sh
./install_now.sh
rm install_now.sh
```
Move to [next steps](#next-steps)


### Manual

* Install APTs:
```
sudo apt-get install imagemagick webp ufraw-batch libatlas-base-dev wiringpi python3 python3-pip
```
* Install PIPs:
```
sudo -H pip3 install requests python-dateutil configparser pandas RPi.GPIO spidev image pillow pyTelegramBotAPI flask flask-wtf
sudo -H pip3 install -I --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib
```
* Download ePiframe ZIP file (or use [git](https://github.com/MikeGawi/ePiframe)) and extract it to *path*:
```
cd <path>
wget -q https://github.com/MikeGawi/ePiframe/archive/master.zip -O ePiframe.zip
unzip -q ePiframe.zip
cp -r ePiframe-master/* .
rm -r ePiframe-master/ ePiframe.zip
chmod +x *.py
```
* Download Waveshare ZIP file (or use [git](https://github.com/waveshare/e-Paper)) and extract all RasPi Waveshare display libraries to *lib* inside *path*:
```
cd <path>
wget -q https://github.com/waveshare/e-Paper/archive/master.zip -O waveshare.zip
unzip -q waveshare.zip
cp -r e-Paper-master/RaspberryPi_JetsonNano/python/lib .
rm -r e-Paper-master/ waveshare.zip
sudo chown -R pi ..
```
* Enable SPI support:
```
sudo raspi-config
```
Go to *Advanced Options -> SPI* and choose *Yes* for both questions then select *Finish* to exit *raspi-config*

Reboot ePiframe device to start enabled SPI support.

* Install ePiframe service
  * replace paths
	```
	sed 's/EPIEPIEPI/'$(pwd | sed 's_/_\\/_g')'\//g' ePiframe.service.org > ePiframe.service
	```
  * enable service
	```
	sudo systemctl enable `pwd`/ePiframe.service
	```

Move to [next steps](#next-steps)


## Next steps

* Connect display to Raspberry Pi
* Add your Google account (the one used to pull photos from) support to Google Photos API on [Google Console](https://developers.google.com/photos/library/guides/get-started) - *Enable the Google Photos Library API*
  * Name it *ePiframe*
  * Use *TVs and Limited Input* as application type (sometimes works only with *Desktop Application* but You can change it later)
  * Or through the Google API Console:  
    * Go to the [Google API Console](https://console.developers.google.com/apis/library)
    * From the menu bar, select a project or create a new project
    * To open the Google API Library, from the Navigation menu, select *APIs & Services -> Library*
    * Search for *Google Photos Library API*. Select the correct result and click *Enable*
* Download credentials JSON file for the API from the previous step - *Download client configuration* button
  *  Or Download icon in *[Google Console](https://console.cloud.google.com/) -> Credentials -> OAuth 2.0 Client IDs*
* Generate token pickle file with *getToken.py* script to use with Google Photos:
  * ```wget https://raw.githubusercontent.com/MikeGawi/ePiframe/master/getToken.py && chmod +x getToken.py && ./getToken.py```
  * Run it on internet browser accessible machine as Google authentication is needed. It doesn't need to be ePiframe device
  * Script will produce *token.pickle* file
* Copy credentials JSON and token pickle file to ePiframe device inside installation path (using [*rsync*](https://ss64.com/bash/rsync.html) or [*scp*](https://ss64.com/bash/scp.html))
* Configure ePiframe with [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file inside installation path
* Check configuration with ```./ePiframe.py --check-config```
* Do a test with ```./ePiframe.py --test``` without sending photo to display
* Do a test with ```./ePiframe.py --test-display``` to test display
* Reboot ePiframe device to automatically run frame
* Enjoy your ePiframe!


### Weather Stamp

<img align="right" src="https://github.com/MikeGawi/ePiframe/blob/master/assets/weather.gif" width="400">

ePiframe can show  weather stamp (icon + temperature) in defined frame corner, color and size. The weather information is taken from [OpenWeather](https://openweathermap.org/api) according to [Maps.ie](https://www.maps.ie/coordinates.html) coordinates. You need to set up some values in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file.

To get the needed values:
* Create an account in [Open Weather Map API](https://home.openweathermap.org/users/sign_up)
* Sign in to OpenWeather account
* Go to _Profile->My API Keys_, copy the generated API key and put it in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file under ```[Weather]->apikey``` value
* Now go to [Maps.ie](https://www.maps.ie/coordinates.html)
* Find desired GPS coordinates for the weather information by location, ZIP code or simply click it on the map
* Copy Longtitude and Lattitude values and put them in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file under ```[Weather]->lon``` and ```[Weather]->lat``` values
* Enable ```[Weather]->show_weather=1``` flag in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file and set other weather stamp parameters like size, position and color
* Now the weather stamp will appear on the photo after next frame update

**_NOTE_** - To troubleshoot OpenWeather API key issues and connectivity check the [tools/testWeatherAPI.py](https://github.com/MikeGawi/ePiframe/blob/master/tools/testWeatherAPI.py) tool.

### Telegram Bot

<img align="right" src="https://github.com/MikeGawi/ePiframe/blob/master/assets/tg.gif" width="200">

ePiframe can optionally be controlled by a Telegram Bot and expose some basic commands to control the frame. Implementation uses [pyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI) and is a persistent thread running when ePiframe is online. You need to set up some values in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file.

To get the needed values:
* Create a [Telegram](https://telegram.org/) account on any device
* Talk to [Bot Father](https://telegram.me/BotFather) - father of all bots
* Create a new bot with ```/newbot``` command, set name ```ePiframeBot``` and username ```ePiframeBot``` (add some numbers at the end to make it unique or use other username)
* BotFather will present _HTTP API token_, copy it and put in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file under ```[Telegram bot]->token```
* You can set other bot options with _BotFather_ (i.e. description, image, if bot can be in group, etc.) but set up the possible commands by ```/mybots``` command, choose the _ePiframeBot_, then click _Edit Bot->Edit Commands_ and paste:
	```
	start - Show help
	help - Show help
	ping - Ping frame
	echo - Say # text
	status - Show frame status
	reboot - Reboot frame
	when - Show next update time
	next - Trigger frame update
	current - Show current photo
	original - Show current original photo
	longer - Display current photo # times longer	
	```
	Now the commands will be visible in the Telegram App as a list.
* Enable ```[Telegram bot]->use_telebot=1``` flag in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file
* [Restart](#service-control) ePiframe service and from now on sending commands to ePiframe bot (search in Telegram App for username set in _BotFather_) will control the frame

**_NOTE_** - To troubleshoot Telegram bot token key issues and connectivity check the [tools/testTelegramBot.py](https://github.com/MikeGawi/ePiframe/blob/master/tools/testTelegramBot.py) tool.

**_❗ IMPORTANT ❗_** - You can limit number of users/groups that can control the ePiframe bot (all bots are public and accessible by others!) by setting ```[Telegram bot]->chat_id``` list in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) - that will allow only the defined chat ids to control bot. To get chat id use the tool above.

### Web User Interface

<img align="right" src="https://github.com/MikeGawi/ePiframe/blob/master/assets/web.gif" width="400">

ePiframe can optionally be controlled by a web user interface under defined network port. Implementation uses [Flask](https://flask.palletsprojects.com/) and is a persistent thread running when ePiframe is online. You need to set up some values in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file.

To configure:
* Enable ```[Web interface]->use_web=1``` flag in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file
* Set IP address in ```[Web interface]->web_host``` option in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file. Set ```0.0.0.0``` for hosting on all possible public IP addresses.
* Set port in ```[Web interface]->web_port``` option in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file. Set port value between 1-65535 that You want to have WebUI hosted under. Sometimes it is needed to [have this port open in the Firewall](https://pimylifeup.com/raspberry-pi-ufw/).
* [Restart](#service-control) ePiframe service and from now on under given IP address and port (*http://[ip]:[port]/*), You'll be able to control the frame.

**_NOTE_** - To troubleshoot WebUI IP, port issues and connectivity check the [tools/testWebUI.py](https://github.com/MikeGawi/ePiframe/blob/master/tools/testWebUI.py) tool.

**_NOTE_** - Keep in mind that any port number below 5000 needs root privilleges to be possible to assign.

#### WebUI Users

It is possible to secure Web User Interface of ePiframe with usernames and passwords. You need to create an user (multiple possible) with ```./ePiframe.py --users``` [command](#command-line).

**_NOTE_** - Keep in mind that even one account added to the ePiframe users will block the Web Interface until successfull authentication. Deleting all users will unblock it for everyone.

#### API

It is possible to control ePiframe from a simple API and even secure it with authentication keys. It is not needed to have the key but in case You need to secure API calls create an user (multiple possible) with ```./ePiframe.py --users``` [command](#command-line). Every user has an API key generated automatically which You then get in the same command tool.

**_NOTE_** - Keep in mind that even one account added to the ePiframe users will block the Web Interface until successfull authentication or API key authentication. Deleting all users will unblock it for everyone.

**_NOTE_** - The users database created in previous ePiframe versions doesn't need to be updated, recreated or modified as it will be updated automatically to the newest version and with no data lost. Old users will have their keys generated automatically.

General API command:

```
<ePiframe IP with port>/api/<command>?api_key=<api key value>[&<optional parameter>=<optional value>&...]
```
e.g.: 

```
192.168.0.123:8080/api/get_image?api_key=1a2b3c4d5e6f7g8h9i0j1k2l3m4n5o6p&original&thumb
```

**_NOTE_** - When there are no users in the database API key can be ommited but then everyone can control the frame.

**_NOTE_** - Header authentication (basic) with API key (Base64 encoding allowed) is also possible.

---

| Command | Type | Parameters |
|--|--|--|
| ```/api/get_image``` | GET | <ul><li>```thumb``` - show thumbnail</li><li>```original``` - show original photo</li></ul> |

Returns image of displayed photo (by default). Can display thumbnail with ```thumb``` parameter and original photo with ```original```.

**Examples:**
* ```/api/get_image?original&thumb``` - original photo thumbnail
* ```/api/get_image?original``` - original photo
* ```/api/get_image?thumb``` - displayed photo thumbnail
* ```/api/get_image``` - displayed photo

**Returns:**
Image, MIME type according to the image type.

---

| Command | Type | Parameters |
|--|--|--|
| ```/api/get_status``` | GET | None |

Returns status of ePiframe in JSON format.

**Examples:**
* ```/api/get_status```

**Returns:**

JSON format:
* ```converted``` - converted/displayed photo modification timestamp (to keep track of photo change)
* ```original``` - original photo modification timestamp (to keep track of photo change)
* ```load``` - current OS load, 3 float values (1, 5, 15 minutes), space separated
* ```mem``` - allocated memory percentage status (with % sign at the end)
* ```service``` - ePiframe service status: _Running_ or _Not running!_
* ```state``` - ePiframe state: _Idle_ or _Busy_
* ```temp``` - current core temperature (with degree sign at the end)
* ```update``` - date and time of the next frame update in format: _DD.MM.YYYY_ (not visible when the same day) _at hh:mm:ss_ (next line) _in d days m mins s secs_ (days not visible when less than one day)
* ```uptime``` - device running time
* ```version``` - version of ePiframe

e.g.

```
{
   "converted":1638394810.5973678,
   "load":"0.8 0.11 0.09",
   "mem":"21%",
   "original":1638394806.737437,
   "service":"Running",
   "state":"Idle",
   "temp":"32.6\u00b0C",
   "update":"at 22:54:37\nin 0 mins 46 secs",
   "uptime":"up 1 week, 1 day, 14 hours, 52 minutes",
   "version":"v0.9.7 beta"
}
```

---

| Command | Type | Parameters |
|--|--|--|
| ```/api/get_log``` | GET | None |

Returns ePiframe log file for current day.

**Examples:**
* ```/api/get_log```

**Returns:**

Real time ePiframe log file in text format with line breaks

---

| Command | Type | Parameters |
|--|--|--|
| ```/api/action=<action>``` | GET | where ```<action>``` should be one of</br><ul><li>```next``` - trigger photo change</li><li>```restart``` - restart ePiframe service</li><li>```reboot``` - reboot ePiframe</li><li>```poweroff``` - power off ePiframe</li></ul> |

Performs action on ePiframe. **No confirmation is needed!**

**Examples:**
* ```/api/action=next``` - show next photo
* ```/api/action=reboot``` - reboot ePiframe

etc.

**Returns:**

Response or error in JSON format.

```
{ "status":"OK" }
```

**Errors:**

```
{ "error":"<error message>" }
```

* ```Action Unknown!``` - when action value is unknown
* ```No Action!``` - when no action value was provided

---

| Command | Type | Parameters |
|--|--|--|
| ```/api/upload_photo``` | POST | None |

Upload photo target that will automatically convert and display uploaded image. The next update time will be resetted.

**Examples:**
* ```/api/upload_photo```

**Returns:**

Response or error in JSON format.

```
{ "status":"OK" }
```

**Errors:**

```
{ "error":"<error message>" }
```

* ```File unknown!``` - when uploaded photo MIME type can't be recognized

**_HINT_** ```curl -F "file=@photo.jpg" "http://<IP>:<PORT>/api/upload_photo?api_key=<API key value>"```

## Update
### Update Automatically

Since [ePiframe v0.9.6 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.6-beta) [#10](https://github.com/MikeGawi/ePiframe/issues/10)

Use *install.sh* script:

```
cd [Your ePiframe path]
wget https://raw.githubusercontent.com/MikeGawi/ePiframe/master/install.sh -O install_update.sh
chmod +x install_update.sh
./install_update.sh --update
rm install_update.sh
```

**_NOTE_** - Since [ePiframe v0.9.6 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.6-beta) [#8](https://github.com/MikeGawi/ePiframe/issues/8) ePiframe has a [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file backward compatibility. That means that any existing configuration file can be used in the newer version of ePiframe and non-existing configuration properties will be set to default values.

### Update Manually

* Save Your [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file in other location.
* Save Your *credentials.json* file in other location. It may be under different name specified in the ```[Credentials]->cred_file``` entry in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file.
* Save Your *token.pickle* file in other location. It may be under different name specified in the ```[Credentials]->pickle_file``` entry in the [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file.

[Uninstall](#uninstalling), [install](#installation) ePiframe again and copy files from previous steps to it's path.

**_NOTE_** - Since [ePiframe v0.9.6 beta](https://github.com/MikeGawi/ePiframe/releases/tag/v0.9.6-beta) [#8](https://github.com/MikeGawi/ePiframe/issues/8) ePiframe has a [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) configuration file backward compatibility. That means that any existing configuration file can be used in the newer version of ePiframe and non-existing configuration properties will be set to default values.

## Uninstalling
### Automatic

Use *install.sh* script:
```
cd [Your ePiframe path]
./install.sh --uninstall
```
Move to [next steps](#next-steps-1)


### Manual

```
sudo systemctl stop ePiframe.service
sudo systemctl disable ePiframe.service
```
Move to [next steps](#next-steps-1)


### Next steps

* Whole ePiframe code is in the directory where it was installed so delete it if not needed
* All dependecies installed for ePiframe are [here](#manual)


## Configuration

* Configure ePiframe with [*config.cfg*](https://github.com/MikeGawi/ePiframe/blob/master/config.cfg) file inside installation path. Just one file and with lots of descriptions. No need to restart service after changing any of config file values as file is loaded per every display refresh/run
* **__ALWAYS__** check configuration with ```./ePiframe.py --check-config```

**_NOTE_** - Interval multiplication option which can enlonger the photo display time, uses *hot word* (i.e. *hotword #*, where # is interval multiplicator value) in the **photo description** field. You can change this attribute only for your own photos or for all *only* when you're an owner of the album. It's description in the photo information panel not photo comment. Comments are inacessible from Google Photos level (unfortunately) as [are stored in different database](https://support.google.com/photos/thread/3272278?hl=en) 😟


## Command line

Main ePiframe script *ePiframe.py* is written in Python and can work from CLI, the ePiframe service daemon *ePiframe_service.py* just runs it without any arguments. But here are additional available commands helpful for tests and debugging:

Syntax: ```ePiframe.py [option]```
* ```--check-config``` - checks configuration file syntax
* ```--test``` - tests whole chain: credentials, pickle file and downloads photo **but without** sending it to the display. Used to test configuration, photo filtering, etc
* ```--test-display [file]``` - displays the photo ```file``` on attached display with current ePiframe configuration. If no file is provided the ```photo_convert_filename``` from the configuration is used. __Only__ converted photos should be put on display! Use ```--test-convert``` for that
* ```--test-convert [file]``` - converts the photo ```file``` to configured ```photo_convert_filename``` with current ePiframe configuration. If no file is provided the ```photo_download_name``` from the configuration is used
* ```--no-skip``` - like ```--test``` but is not skipping to another photo, not marking photo as showed, etc.
* ```--users``` - manage users for the WebUI: add, change passwords, delete, etc.
* ```--help``` - show help

**_NOTE_** - To not interfere with working ePiframe thread it's better to [stop](#service-control) the service before using commands.


## Debugging

When ePiframe is not refreshing, it's a tragedy indeed. Check your wiring with display, check power supply, check internet connection and try to reboot the device. If that doesn't help:
* Check logs for service and ePiframe script that are stored in configured ```log_files``` location
* [Check configuration](#configuration)
* Do a test with ```./ePiframe.py --test``` without sending photo to display and get detailed log on what is happening
* Make sure that configured photo filtering is not narrowing too much, i.e. only one or no photos at all are filtered (test that in the step above)
* Check ePiframe service status: ```sudo systemctl status ePiframe.service``` and [restart](#service-control) if not running
* Sometimes changing a color preset can fix black screen problem as some photos react strange to image processing

If problem still occurs, please create an issue here.

**_NOTE_** - I've experienced some display issues like shadowing or distorted images when used bad or too weak power supplies so make sure you provide stable 5V/3A.


## Performance

Image processing is the most resources consuming process but ePiframe is meant to work on Raspberry Pi Zero. Script does one thing at a time and moves to another task, there are no parallel jobs (even image conversion has been stripped to one thread) and the peak of load is only during frame update. On Raspberry Pi Zero W v1.1 it took maximum up to 2 minutes (avg. 60 seconds) to pull the 4K photo, process it and put it on display. The conversion has been [optimized](https://stackoverflow.com/questions/28704984/how-to-speed-up-a-complex-image-processing): filters are not used, scale + resize instead of blur but with the same results, resampling instead of resizing, etc. Here's a graph of loads during ePiframe tests:

|<img src="https://github.com/MikeGawi/ePiframe/blob/master/assets/graph.png" width="720"/>| 
|:--:| 
|*Graph of loads for ePiframe run on Raspberry Pi Zero W v1.1 and Raspberry Pi OS 10 Buster (5.4.79+). Off hours from 23:30 to 5:30, frame refresh interval was 10 minutes, various photo types and quality (4K UHD photos too) with Floyd-Steinberg dither + enhanced contrast preset and photo background (so the heaviest conversion possible)*|

|||
|--|--|
|Highest load peak during runtime |*0.67* |
|Average of maximum load peaks during runtime |*0.43* |
|Average load during runtime (except off hours) |*0.105* |


## Service control

ePiframe comes with a system service that is fully autonomic, automatic and self-recovering. It can be left completely unsupervised but it is possible to control it if needed, the same way as every service in Linux:
```
#stop
sudo systemctl stop ePiframe.service
#start
sudo systemctl start ePiframe.service
#restart
sudo systemctl restart ePiframe.service
```

It is possible to start (for test purposes) only WebUI or TelegramBot thread from the service:
```
cd <Your ePiframe path>
#stop first if running
sudo systemctl stop ePiframe.service
#WebUI
./ePiframe_service.py start web
#or TelegramBot
./ePiframe_service.py start telegram
```

**_❗ IMPORTANT ❗_** - These services must be enabled in the configuration file!

**_NOTE_** - Service will not show any errors if the configuration is wrong or the thread cannot be started. Check [debugging section](#debugging).

**_NOTE_** - Keep in mind that any port number below 5000 needs root privilleges to be possible to assign (use ```sudo ./ePiframe_service.py ...```)

## Flow
 
|<img src="https://github.com/MikeGawi/ePiframe/blob/master/assets/flow.png" width="600"/>| 
|:--:| 
|*Flow diagram of ```ePiframe.py``` - main script. If any step fails or has no result then script will exit*|

	
## Future plans
	
ePiframe to-do list for 2021:
* [x] Add web interface based on [Flask](https://flask.palletsprojects.com/) for configuration, control and photos upload [#9](https://github.com/MikeGawi/ePiframe/issues/9)
* [x] Add Telegram bot service to control frame and upload photos [#5](https://github.com/MikeGawi/ePiframe/issues/5)
* [ ] Easier token generation from the web interface (is this even possible?)
* [x] Weather and temperature displayed on the photo - [#3](https://github.com/MikeGawi/ePiframe/issues/3)
* [ ] Frame lasers, robot arms and making lunch functionality...

Wait! There's more for 2021:
* [x] Configuration backward compatibility - [#8](https://github.com/MikeGawi/ePiframe/issues/8)
* [x] Update ePiframe version from script - [#10](https://github.com/MikeGawi/ePiframe/issues/10)
* [x] Users and passwords for web interface - [#15](https://github.com/MikeGawi/ePiframe/issues/15)
* [x] API - [#17](https://github.com/MikeGawi/ePiframe/issues/17)

Stay tuned!


## Resources
	
This project uses:
* [Google Photos API](https://developers.google.com/photos/library/guides/overview)
* [Official Waveshare e-Paper libraries](https://github.com/waveshare/e-Paper)
* [Pandas Dataframe](https://pandas.pydata.org/)
* [ImageMagick](https://imagemagick.org/)
* [OpenWeather API](https://openweathermap.org/api)
* [pyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI)
* [Flask](https://flask.palletsprojects.com/)
* [WTForms](https://wtforms.readthedocs.io/)
* [FlaskWTF](https://flask-wtf.readthedocs.io/)
* [Flask-Login](https://flask-login.readthedocs.io/)
* [Bootstrap](https://getbootstrap.com/)
* [jQuery](https://jquery.com/)
* [Dropzone.js](https://www.dropzone.dev/js/)
* [SQLite](https://www.sqlite.org)

Helpful links:
* [Najeem Muhammed: Analyzing my Google Photos library with Python and Pandas](https://medium.com/@najeem/analyzing-my-google-photos-library-with-python-and-pandas-bcb746c2d0f2)
* [Jie Jenn: Google Photos API Python tutorial](https://learndataanalysis.org/category/python-tutorial/google-photos-api/)
* [Leon Miller-Out: Auto-recovery of crashed services with systemd](https://singlebrook.com/2017/10/23/auto-restart-crashed-service-systemd/)
* [Sander Marechal: A simple unix/linux daemon in Python](https://www.jejik.com/articles/2007/02/a_simple_unix_linux_daemon_in_python/)
	

## This is not what I'm looking for

If you're looking for an LCD frame with Google Photos, [mrworf's Photo Frame](https://github.com/mrworf/photoframe/) is the best choice: color LCD support, ambient light sensor, off hours and many, many more. 


I also wanted to use [Magic Mirror](https://github.com/MichMich/MagicMirror) to create frame with [MMM-GooglePhotos](https://github.com/ChrisAcrobat/MMM-GooglePhotos) and doing a screen shot of the page for e-paper display like [rpi-magicmirror-eink](https://github.com/BenRoe/rpi-magicmirror-eink) does. Magic Mirror is a great software but I decided to do it by myself (not to get crazy during the lockdown).


Or you can just use Arduino or ESP controller (even with attached card controller) and display photos from the storage. There are some projects like that in the Web but you lose Google Photos synchronisation.
	
	
Also a very nice e-paper Waveshare display with Raspberry Pi idea is [inkycal](https://github.com/aceisace/Inky-Calendar)
