# wifi_configuration

A new Flutter plugin.

## Getting Started

This plugin allows Flutter apps to get available wifi ssid list,
user can connect to wifi with ssid and password.
This plugin works Android.
iOS will be released later.


Sample usage to check current status:



Note :-   This plugin requires the location permission to auto enable the wifi if android version is above 9.0.


For Android : -
Add below Permissions to your manifist.xml file -
```dart
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-feature android:name="android.hardware.wifi" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```



```dart
  import 'package:wifi_configuration/wifi_configuration.dart';
  
  
  
    WifiConnectionStatus connectionStatus = await WifiConfiguration.connectToWifi("ssidName", "passName", "your android packagename");
    //This will return state of a connection
    //Package name is required to redirect user to application permission settings page to let user allow location permission
    //in case connecting with wifi
  
  
        switch (connectionStatus) {
              case WifiConnectionStatus.connected:
                print("connected");
                break;
        
              case WifiConnectionStatus.alreadyConnected:
                print("alreadyConnected");
                break;
        
              case WifiConnectionStatus.notConnected:
                print("notConnected");
                break;
        
              case WifiConnectionStatus.platformNotSupported:
                print("platformNotSupported");
                break;
        
              case WifiConnectionStatus.profileAlreadyInstalled:
                print("profileAlreadyInstalled");
                break;
        
              case WifiConnectionStatus.locationNotAllowed:
                print("locationNotAllowed");
                break;
            }
  
  
        var listAvailableWifi = await WifiConfiguration.getWifiList();
          //If wifi is available then device will get connected
          //In case of ios you will not get list of connected wifi an empty list will be available
          //As Apple does not allow to scan the available hotspot list
          //If you try to access with private api's then apple will reject the app
  
  
        bool isConnected = await WifiConfiguration.isConnectedToWifi("ssidName");
        //to get status if device connected to some wifi
        
        String isConnected = await WifiConfiguration.connectedToWifi();
                //to get current connected wifi name
        
```
If user has not allowed the location permission for this app then it will ask everytime app try to connect to wifi for the location permission.


When you use connection on iOS (iOS 11 and above only)

1. 'Build Phases' -> 'Link Binay With Libraries' add 'NetworkExtension.framework'

2. in 'Capabilities' open 'Hotspot Configuration'

3. If you device is iOS12, in 'Capabilities' open 'Access WiFi Information'

If you want to use Wifi.list on iOS,



For help getting started with Flutter, view our 
[online documentation](https://flutter.dev/docs), which offers tutorials, 
samples, guidance on mobile development, and a full API reference.
### Sponsored by Jaaga Soft

