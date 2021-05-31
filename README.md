# Kiki App


## Setting Up Outgoing Kiki Gmail address for use in Firebase

Kiki Gmail is deployed in cloud functions.  See /functions/index.js 

To enable Gmail address for use from Firebase, set it to "Less Secure" here: 
https://myaccount.google.com/lesssecureapps

Remember the Firebase plan needs to be subscribed to at least Blaze status.

## App Store Connect

Identifier should have HotSpot Config and Wifi enabled 

## Current Tasks

Last updated: 10/21/2020

App UI/UX
1. Button or an icon to let Seller see there is an active Buyer, with option to cancel that user
  > Consider, we will need to have logic to stop the subscription; 
  > I will see if we can just "pause" it , rather than cancel outright because subscription is to Kiki, not to Seller

Cloud functions
1. When new Seller joins and they match w/Waiting Buyer, send email
2. Reminder email to Buyer that Trial will expire
3. Seller cancels Buyer

## Branch: varnt/macbook11

The **varnt/macbook11** branch is a parallel branch where the code under /lib, etc can be updated on the MacBook 2011.  
However the actual builds are run on **develop** branch.
So after changes are made on the *varnt/macbook11* branch, they are just copied over to *develop* 
That is why at the time of commit for this portion, *develop* branch is missing the /functions folder and this ReadMe

## References

- [Example goes to Google](https://google.com)

## WiFi functional differences per platform
WiFi related logic is tested on iOS(14.0), Android 10+ and Android < 10
#### WiFi connect
WiFi connection with known SSID and password works on all platforms
##### iOS and Android < 10
During the connection a new network profile is created which stays on device until explicitly deleted. If app is killed connection also stays active until manually disconnected.
##### Android 10+
WiFi connection initiated from the app is bound to app lifecycle i.e. connection is terminated one app is killed. After that no network profile stays on device.

### WiFi disconnect
WiFi disconnect is currently triggered by "Disconnect" button

##### iOS and Android < 10
WiFi disconnect and network profile deletion works as expected

##### Android 10+
Separate code for WiFi disconnect and network profile deletion is not needed

### Network status retrieval(Detecting if wifi is connected or not)
##### iOS and Android < 10
Network status retrieval works as expected
<b>Note1:</b> Normally app is only allowed to disconnect network which it has connected before
<b>Note2:</b> Currently "Connect" button is hidden if wifi is currently connected

##### Android 10+
For some reason even after establishing wifi connection from the app device reports mobile network as active connection method. This might be device-specific behaviour. Additional testing is needed.