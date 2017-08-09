# connects to xDrip and G5



xdrip/xbridge/G5 reader for iOS devices - 

* Alerts
* Chart
* Always on notification (not really always but almost always) that allows to see the current value by just lifting up the phone (iOS 10).
* Upload to Nightscout (works always for G5, for xDrip not recently tested since I don't use G4 anymore, there may be some delay in upload).
* store values in HealthKit


# Alerts

Alerts are configured in the Settings. 
Possible alerts are
 * High
 * Very High
 * Low
 * Very Low
 * Missed Reading
 * Phone Muted (warns you if your phone is muted)
 * Calibration Request
 * Battery Low

Each Alert requires an Alert Type.

__Per Alert Type define__
 * enabled or disabled : Example between 8 in the morning and midnight I don't need a low alert. For me the Low alert has a disabled alert type between 8 and midnight. There's
 always an alert named "No Alert" created by the application which is disabled. You can use that one for all cases where you want a disabled alert type.
 * Name : name of the alert type
 * Vibration enabled yes or no : if yes the device will vibrate when the alert goes off
 * Snooze from notification yes or no : if yes, you can do a quick snooze of an alert from the home screen (why would I say 'no' ? because many times during the night when an alarm goes off, I just snooze it and continue sleeping without doing something about my values - if I have to unlock my device for snoozing then I'm sure I'll be awake)
 * Snooze period (in minutes) : value used when you snooze from the home screen
 * Repeat yes or no : it's an iOS thing, if yes the notification will repeat every minute until you open the notification or snooze it. In any case the alert will go off again 5 minutes later if you haven't snoozed it and if it's still applicable
 * Sound : the sound to use. 
   The phone will not generate any sound if it's in silent mode.
   At the time of writing there are three options
   * "No Sound" : you will not hear anything
   * "Default iOS Sound" : the sound generated by iOS
   * "xDrip Sound" : it's a copy of the sound generated by the Android version

__Next step : the Alerts__

For each alert (except 'Always on Notification' and 'Additional Calibration Request'), you can define for each moment of the type which Alert Type needs to be used. 
For example you could say 
* between 00:00 and 08:00, the Low Value alert needs to use an Alert Type with vibration, with the xDrip sound, without a snooze possibility on the home screen.
* between 08:00 and 23:59, the Low Value alert only needs to vibrate, no sound, with a possibility to snooze on the Home Screen.
In such case you would need two Alert Types, and assign each of them to the correct interval.
You can create as many Alert Types and intervals as you want.
Alert Types can be re-used for different types of alerts.

# To Install the app.

The application is not available on iTunes and must be signed for your device.
If you have an Apple Developer Account then you can easily do this yourself as described here : https://github.com/dabear/iphoneipa-resign
The ipa file to download is here, take the latest release : https://github.com/JohanDegraeve/iosxdripreader/releases
Regulary check for updates.

If you don't have an Apple Developer Account, and you don't know anybody who can help you with this, you can ask me.
Send my the UDID of your device in a mail please. (johan.degraeve@gmail.com).
To retrieve your UDID you must use iTunes (apps don't give you the right UDID). Here you can find an explanation how to find the UDID http://whatsmyudid.com/ . Follow the instructions "iTunes".
I'll update the latest release version with a release signed for your device.

Then

Easist is if you have xCode on a Mac : Connect your iphone to your mac,
Select "Window", "Devices", go to "Installed apps", click the + sign, then select the ipa file.

Or if you don't have xCode you can use iTunes 

* Open iTunes, select File > Add to Library and add the application IPA file to iTunes (or drag and drop it onto the iTunes dock icon).
* Locate your new application in Apps. (see http://wwwimages.adobe.com/content/dam/Adobe/en/devnet/air/articles/packaging-air-apps-ios/fig_18.jpg)
* Connect your iOS device to your computer's USB port.
* In iTunes, select the attached device and make sure your application is selected to be synced on the device and then sync the device (see http://wwwimages.adobe.com/content/dam/Adobe/en/devnet/air/articles/packaging-air-apps-ios/fig_19.jpg)
* Locate the application on the device and run it. (See http://wwwimages.adobe.com/content/dam/Adobe/en/devnet/air/articles/packaging-air-apps-ios/fig_20.jpg and http://wwwimages.adobe.com/content/dam/Adobe/en/devnet/air/articles/packaging-air-apps-ios/fig_20.jpg)

# To compile (only if you want to develop):
- install Flash Builder 4.7 with FLex SDK 4.15.0, AIR 22.0 en_US
- an ios developer membership is required, full explanation : http://help.adobe.com/en_US/flex/mobileapps/WS064a3073e805330f6c6abf312e7545f65e-8000.html
- clone the repository, lets say folder iosxdripreader
- purchase license for distriqt Notifications, Dialog, Application, Message, NetworkInfo ane at http://airnativeextensions.com/
- create a folder named ane under iosxdripreader
- download the zip package, extract, and copy the file com.distriqt.BluetoothLE.ane to the folder ane
- on the site of airnativeextensions.com, create an application key, application id = net.johandegraeve.iosxdripreader (you can use another application id if you want, but then change the name also in iosxdripreader-app.xml)
- create a folder named src/distriqtkey under iosxdripreader
- create a new class in that package, DistriqtKey.as
- add a public static const distriqtKey:String = your key from distriqt
- as explained here http://airnativeextensions.com/knowledgebase/tutorial/1#ios
- donwload the ios sdk (there should be a zip corresponding to the latest ios version) and put it in a new folder under iosxdripreader
- and add it in the flash builder project properties (also explained on  http://airnativeextensions.com/knowledgebase/tutorial/1#ios)
- (explained : right click in project, properties, flex build path, native extensions, browse to the ane folder and add the new ane, then go to flex build packaging, ios, native extensions, add the file com.distriqt.BluetoothLE.ane as native extensions, check the "package" check box, also add the Apple iOS SDK that was downloaded
- in the same way as above, do this also for the Notifications, Dialog, Application, Message, NetworkInfo, AndroidSupport and core ane.
- it also uses my own ANE : https://github.com/JohanDegraeve/ANE-BackgroundFetch/tree/master/build
