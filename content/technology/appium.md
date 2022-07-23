---
title: "How To Setup Appium Test Environment For Mac"
date: 2020-05-14T14:04:42+08:00
author:
  name: "阿金"
comments: true
description: "appium iOS Android"
keywords: ["appium","ios","android"]
images:
tags:
  - test
---

-----------------Preparation-------------------

1、Install Java JDK latest version

https://www.oracle.com/technetwork/java/javase/downloads/index.html


setting Java Path,Android Path

java env
```
 export JAVA_HOME=$(/usr/libexec/java_home)
 export PATH=${PATH}:$JAVA_HOME/bin

```
android env
```
export ANDROID_HOME=/Users/yourfolder/Library/Android/sdk
export PATH=${PATH}:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/bundle-tool/
```

2、Install the latest Xcode Desktop version

Install xcode 



3、Install Xcode command line (use Command: Xcode-select --install)


4、Install Homebrew with below command 
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

5、carthage
```
brew install libimobiledevice --HEAD

brew install carthage
```

6、node
```
brew install node
```

7、npm
```
brew install npm
```

8、xcpretty

```
gem install xcpretty
```

if show this: "You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory."
```
brew install ruby
```
and set path export PATH="/usr/local/opt/ruby/bin:$PATH"


9、Download Appium Desktop and install it

https://github.com/appium/appium-desktop/releases



10、appium-doctor
```
npm install -g appium-doctor

```
and then you can put 'appium-doctor' in terminal 


11、opencv4nodejs
```
brew install opencv4nodejs
```
12、ffmpeg
```
brew install ffmpeg
```

13、mjpeg-consumer
```
npm install mjpeg-consumer
```
14、set-simulator-location
```
brew install lyft/formulae/set-simulator-location
```
15、idb
```
brew tap facebook/fb

brew install idb-companion

pip3.6 install fb-idb
```
Note: The idb client requires python 3.6 or greater to be installed.

16、applesimutils
```
brew tap wix/brew

brew install applesimutils
```
17、ios-deploy
```
npm install -g ios-deploy

```
18、bundletool.jar

在 [bundletool](https://github.com/google/bundletool/releases) 下载最新的bundletool.jar

jar package rename bundletool.jar

in android sdk floder add bundle-tool document

put bundletool.jar in bundle-tool

in terminal chmod +x bundletool.jar


update bash_profile ，android PATH env add   :$ANDROID_HOME/bundle-tool/


19、Setting up WebdriverAgent in XCode


download GitHub - [facebook/WebDriverAgent: A WebDriver server for iOS that runs inside the Simulator.](https://github.com/facebookarchive/WebDriverAgent)

under WebDriverAgent floder in terminal :

./Scripts/bootstrap.sh -d

if download successfully  WebDriverAgent's dependence

should go to :/Applications/Appium.app/Contents/Resources/app/node_modules/appium/node_modules/

new a floder :appium-xcuitest-driver

and copy all WebDriverAgent floder in it 

like this :

/Applications/Appium.app/Contents/Resources/app/node_modules/appium/node_modules/appium-xcuitest-driver/WebDriverAgent



**some error**

- WebDriverAgent failed to build: Assign property / Could not build RoutingHTTPServer

https://github.com/appium/appium/issues/13307


- 'assign' property of object type may become a dangling reference; consider using 'unsafe_unretained'



get iphone's UUID and APP's bundleID

{{< image src="/images/appium.png" alt="IAP" position="center" style="border-radius: 8px;" >}}

use tidevice launch the WebDriverAgent

tidevice:https://github.com/alibaba/taobao-iphone-device

```shell
# running WebDriverAgent and listen on port 8200 
$ tidevice wdaproxy -B com.facebook.wda.WebDriverAgent.Runner --port 8200
```
open terminal:

```shell
iproxy 8100:8200
```
lastly, launch appium :)

**some error**

- can not get session ID

if you can not get session ID

open a terminal,put this :

```shell
curl -X POST -d '{"capabilities": {}, "desiredCapabilities": {}}' 'http://localhost:8100/session'
```


