# My Pixel3a GrapheneIOS Setup
The idea of this project is to make an old google pixel 3a usable again in line with some of the philosophies of [permacomputing](https://permacomputing.net/). The phone required a new phone and battery, which I learnt how to install using youtube tutorials, and some trial and error. This repo details the software side of this project. 

## Operating System
There are [many](https://github.com/devadigax/awesome-android-custom-rom) android-based operating systems to choose from. My main requirements for an operating system were:
1. Degoogle my phone as much as possible
2. Remove as much bloatware as possible for performance reasons
3. A focus on privacy and security.
I ultimately chose [GrapheneOS](https://grapheneos.org/) as it largely met these criteria as well as its active and helpful forums. The downside is that pixel 3a phones are no longer supported are no longer supported by GrapheneOS. Other shortlisted operating systems were [LineageOS](https://lineageos.org/) and [/e/](https://e.foundation/). [This site](https://eylenburg.github.io/android_comparison.htm) compares these three OSs. 
## Image
The pixel 3a is no longer supported by AOSP, and so isn't supported by GrapheneOS. I found this [reddit thread](https://www.reddit.com/r/GrapheneOS/comments/15g81rx/pixel_3a_how_to_get_old_builds/) with two options:

1. Try the wayback machine
2. Some random [mega upload link](https://mega.nz/folder/TjgUzKgD#o8kbyLchUE7M9jTn3BQ-Pg)

The first option would start downloading but I could never get it to complete. Maybe it wasn't properly captured in that snapshot. So I used the second option. Which requires a massive WARNING attached to it: as it is no longer supported, it is not possible to verify the image. That is to say, it is impossible to say if the operating system image has had additional code injected without this verification. Please proceed at your own risk. 

## Installation
GrapheneOS has two install methods; a web-based installer and [command line installation method](https://grapheneos.org/install/cli). As pixel 3a is no longer supported, I had to use the CLI method. I followed the install instructions line by line on my ubuntu 24.04 laptop, except for a few important things:
- I used the image I had found instead of downloading from GrapheneOS's website. 

### Troubleshooting
- I needed to do a factory reset before I could into developer mode
- I got the following error on `fastboot flashing unlock
```
FAILED (remote: 'flashing unlock is not allowed')
fastboot: error: Command failed
``` 
In a random forum post: [You need to activate oem-unlock in developer settings first.](https://xdaforums.com/t/failed-remote-flashing-unlock-is-not-allowed-error.4368515/)

- The `flash_all.sh` script was hanging at one point. Ultimately, I found a forum post that suggested using a usb-a to usb-c instead of a usb-c to usb-c to connect my laptop and phone. This worked. There's something funky up with linux usb drivers.
- After flashing the rom on one pixel3a, I got the `no valid slot to boot` reason for entering the bootloader. When restarting, I kept ending up in the bootloader with this message. I did the following things and it worked:
	- unwound my usb-a to usb-c cable (it was coiled up)
	- used a different usb-a slot on my laptop (went from the right one to the left one)
	- removed `platform-tools` and it's zip from my present working directory and put it elsewhere
	- I may have missed the ssh-keygen step, so I attempted that, though it failed (maybe this did something though?)

## App Installation
### App Stores
Installing apps is a little more involved in GrapheneOS. It requires using multiple app stores. The installation order for these app stores is:
1. Update GrapheneOS App Store
2. Install Accrescent using the GrapheneOS App Store
3. Install Google Play Store + Google Play Services using the GrapheneOS App Store
4. Install F-droid using the F-droid apk
5. Install Aurora using F-droid
6. Install Obtanium using F-droid

#### GrapheneOS App Store
As the stock GrapheneOS App Store didn't work for me (can't find servers error), I downloaded and installed the apk from [here](https://github.com/GrapheneOS/AppStore/releases). Use vanadium (GrapheneOS stock browser) to download and install the most recent version of the apk on the Assets menu. For me, this was `AppStore-30.apk`.
#### Accrescent
An app store with only GrapheneOS dev approved apps. Installed from GrapheneOS App Store.
#### Google Play Store + Google Play Services
I couldn't get my banking app to work using Aurora, so I installed play store and play services using the GrapheneOS App Store. GrapheneOS runs these in a sandbox so that these apps don't have any special privileges beyond other apps (they are super privileged in google android). I've since deleted Google Play Store and everything still works fine. 
#### F-droid
Open-source app store. Downloaded the F-droid apk from [here](https://f-droid.org/) using Vanadium. From f-droid I could install a bunch of other things. 
#### Aurora
An app store that is an anonymous frontend to the google play store. It doesn't come with Play Services or a replacement, so a lot of apps dont work. Installed aurora via f-droid.
#### Obtanium
Used to install builds directly from github/gitlab repos. Installed using fdroid. 

#### Summary of Apps Installed with App Stores
##### Accrescent
- Aves Gallery Libre
- Ironfox
- Organic Maps
##### Aurora
- Bank Australia
- Proton Authenticator
- Spotify
##### F-droid
- AntennaPod
- Aurora
- Bitwarden (after adding bitwarden repo)
- Fossify Clock
- FUTO Keyboard
- Joplin
- Obtainium
- Open Camera
- Tubular
- VLC
##### GrapheneOS App Store
- Accrescent
- Google Play Store (later deleleted) + Google Play Services
##### Obtainium
- Iceraven
- Proton Calendar
- Proton Drive
- Proton Mail
- Signal

### System
#### Fossify Clock
The default android clock app is not pretty and isn't customisable. Fossify clock is very similar to the android clock, but it customisable.  
#### FUTO Keyboard
The stock keyboard isn't great. FUTO was the first one I tried after trawling GrapheneOS forum posts. It's pretty neat. Need to add the [repo](https://app.futo.org/fdroid/repo/) to f-droid.

### Browser
#### Iceraven
Web browser. GrapheneOS comes with Vanadium, which is a chrome/chromium fork. It doesn't have any/much ad-blocking and has no ability to add extensions. Ice Raven is a Firefox fork, with a focus on removing tracking, allows extensions from both firefox and chrome stores, and is a bit faster than stock firefox. It also seems to be updated quite regularly and has an active community. Downloaded the apk file from [here](https://github.com/fork-maintainers/iceraven-browser?tab=readme-ov-file#-installation). $\mu$block origin is a must-have with this. 
#### Ironfox
Ironfox is arguably a tiny bit better with the privacy stuff than Ice Raven. Weirdly it's a chrome fork. I've only played with this a little bit, but if you like your chromium based browsers, try this one. On first usage it will ask if you want to install an ad blocker ($\mu$block origin) - say yes. Installed with accrescent.   

### Comms
#### Signal
Installed using Obtanium using github repo [here](https://github.com/signalapp/Signal-Android). 

### Maps
#### Organic Maps
Open source google maps usage replacement. Trying this out instead of OsmAnd+. Installed with Accrescent.

### Media
#### AntennaPod
For podcasts. Installed with f-droid.
#### Aves Gallery Libre
Media gallery. The stock GrapheneOS one isn't great. Installed using Accrescent.
#### OpenCamera
The stock GrapheneOS isn't great. OpenCamera is pretty good and packed with a huge amount of features. Installed with f-droid.
#### Spotify
Currently looking for and trialling alternatives to spotify. Installed with aurora.

#### Tubular
It's a fork of NewPipe. NewPipe is a front end to youtube that doesn't track you or send information back to youtube, and it doesn't insert ads. Tubular is essentially NewPipe with SponsorBlock (a firefox extension) installed. Installed with f-droid
#### VLC
We all love it. Installed with f-droid.

### Notes
#### Joplin
Note-taking app that can sync with encryption across multiple devices using my otherwise unused dropbox account. Installed with f-droid. 

### Password Manager
#### Bitwarden
Isn't available out of the box in f-droid, but you can add the [bitwardern repository](https://mobileapp.bitwarden.com/) to f-droid and then you can download it.

### Proton Suite
I'm looking to move away from the google suite for personal cloud services. 
#### Proton Authenticator
Installed using aurora.
#### Proton Calendar
Installed using obtainium from apk from [here](https://proton.me/calendar/download)
#### Proton Drive
Installed using obtainium from apk from [here](https://proton.me/drive/download)
#### Proton Mail
Installed using obtainium (github repo [here](https://github.com/ProtonMail/android-mail/releases)). 

### Services
#### Bank Australia
Ensure Play Store and Play Services are installed as the Bank Australia app uses some of the security features from Play Services. Then install the Bank Australia app with Aurora.

## App Summary
I haven't listened any of the stock apps besides the GrapheneOS AppStore and Vanadium.

| App                                                        | Description                                                                        |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Accrescent                                                 | An app store for apps approved by the GrapheneOS developers                        |
| AntennaPod                                                 | Podcast App. Very similar to Pocketcast.                                           |
| Aurora                                                     | Access Google Play Store without logging in.                                       |
| Aves Gallery Libre                                         | Media gallery.                                                                     |
| Bank Australia                                             | The official Bank Australia app.                                                   |
| Bitwarden                                                  | Password manager.                                                                  |
| F-droid                                                    | An app store for open source apps.                                                 |
| Fossify Clock                                              | A slightly nicer clock. Will be very familiar if you've used google android clock. |
| FUTO Keyboard                                              | A keyboard with swipey words                                                       |
| GrapheneOS AppStore                                        | The store app store that comes with GrapheneOS.                                    |
| Google Play Store (later deleleted) + Google Play Services | Needed to install some apps in Aurora                                              |
| Iceraven                                                   | Web broswer - Firefox with trackers removed                                        |
| Ironfox                                                    | Web broswer - Chrome with trackers removed.                                        |
| Joplin                                                     | Note taking and organising app.                                                    |
| Obtainium                                                  | Managers app obtained from github.                                                 |
| Open Camera                                                | A full featured camera app.                                                        |
| Organic Maps                                               | Google maps replacement.                                                           |
| Proton Authenticator                                       | For two-factor authentication.                                                     |
| Proton Calendar                                            | Google calendar replacement.                                                       |
| Proton Drive                                               | Google drive replacement.                                                          |
| Proton Mail                                                | Gmail replacment.                                                                  |
| Signal                                                     | Secure messaging app.                                                              |
| Spotify                                                    | Music streaming.                                                                   |
| Tubular                                                    | Watch/listen/download/play in background youtube videos and soundcloud music.      |
| Vanadium                                                   | Stock GrapheneOS web browser.                                                      |
| VLC                                                        | A media player that will play almost any media format.                             |
## Todo
- [ ] Find a replacement for spotify
- [ ] Investigate microG as a Google Play Service replacement