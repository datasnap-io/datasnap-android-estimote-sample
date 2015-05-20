Datasnap Android Sample App
* Integrates with Estimote beacon hardware
* Optional use of google location services
* DataSnapEstimoteActivity contains main logic
* Initialize Analytics and send an instance of IEvent to send event to datasnap
* Example includes a Beacon Sighting Event
* See other event types here: http://datasnap-io.github.io/sendingdata/


## Building the Sample App

First, clone the repo:

`git clone git@github.com:datasnap-io/datasnap-android-estimote-sample.git`

Next, you will need to have a Datasnap.io Org and project to send events to. CA member of the Datasnap.io Team should have already provided you with the org and project keys needed. If not ask them at support@datasnap.io

Open the file `app/src/main/res/values/datasnap.xml` and enter the project informationy for your project.

* Add a datasnap.xml resources file to your project containing the following information (See more details in the sample app project - required fields : datasnap server, apiKey, organizationIds, projectIds):    
```xml  
    <!-- Datasnap Server-->    
        <string name="datasnap_server">https://api-events-staging.datasnap.io/v1.0/events</string>
        <!-- Api Key-->
        <string name="datasnap_apiKey">K8xBSjg0S1RYWDRDV1hBQUM4VUJQSlRWWjp3ZHBjWWdOR2VheWxGUTBRZ1JKZ3RIaUhSdUZSK2lNR1JrWGVCUNSRTNV</string>
        <!-- Organization Ids -->
        <string-array name="datasnap_organizationIds">
            <item>56xj08dMrRFeaOOler4eYa</item>
        </string-array>
        <!-- Project Ids -->
        <string-array name="datasnap_projectIds">
            <item>56xj08dMrRFeaOOler4eYa</item>
        </string-array>   
```

Building the sample then depends on your build tools.

### Android Studio (Recommended)

(These instructions were tested with Android Studio version 0.9.3.)

* Open Android Studio and select `Import Project`
* Select the file `build.gradle` in the root of the cloned repo


There is a /datasnapsdk folder that already had a precompiled aar archive that is linked in the app/build.gradle file:

```
dependencies {
    compile project(':datasnapsdk')
```

#### Include latest SDK in this sample App:

* Git clone the latest SDK Repo: git@github.com:datasnap-io/datasnap-android-sdk.git
* In the SDK folder run
* place the aar archive into the datasnapsdk folder and make sure the build.gradle file is in this folder still or add it in if its not:
* 
```
configurations.create("default")
artifacts.add("default", file('datasnapsdk.aar'))
```

Then make sure this entry is still in the app/build.gradle file:
```
dependencies {
    compile project(':datasnapsdk')
```


#### Libs location

You can also use a libs folder to organizae your dependencies:

* Create a /libs directory inside your project and copy all the AAR files there.

*Edit your build.gradle file, and add a "flatDir" entry to your repositories like so:

    repositories {
        mavenCentral()
        flatDir {
            dirs 'libs'
        }
    }

* Edit your build.gradle file to add this AAR as a dependency like below:

#### Sampel app in SDK Repo

Also we included a sample app in the SDK project itself to make it even easier to test the latest SDK code:

https://github.com/datasnap-io/datasnap-android-sdk/tree/development/sampleapp

##  Android Permissions

Add below permissions to AndroidManifest.xml  Note we Also descibe what they are used for:
```

<!-- Required for sending events via HTTPS to our REST API. -->
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

<!-- Required for dumping events to SD to handle queuing of events as needed. -->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

<!-- Allow you to get LOGCAT information when a crash occurs. -->
<uses-permission android:name="android.permission.READ_LOGS"/>

<!-- Allow you to see which activity was active when a crash occurs. -->
<uses-permission android:name="android.permission.GET_TASKS"/>


```


## Sample API Calls

Here is a sample method using some hardcoded values and some live data beinf retrieve via the Estimote SDK.

This method will also send the event to us:

```
    public void createBeaconSightingEvent(){
        String eventType = "beacon_sighting";
        User user = new User();
        PropId propId = new PropId();
        propId.setMobileDeviceIosIdfa("1a847de9f24b18eee3fac634b833b7887b32dea3");
        propId.setGlobalDistinctId("userid1234");
        user.setId(propId);
        Place majorPlace = new Place();
        majorPlace.setName("major");

        Place minorPlace = new Place();
        minorPlace.setName("major");
       // minorPlace.setAddress();

        Beacon1 beacon1 = new Beacon1();
        DeviceInfo deviceInfo = new DeviceInfo();
        deviceInfo.setCreated(Utils.getTime());
        deviceInfo.setDevice(device);
        Beacon1 beacon2 = new Beacon1();
        String beaconid2 = "SHDG-test";
        beacon2.setIdentifier(beaconid2);
        Map<String, Object> additionalProperties = new HashMap<String, Object>();
        additionalProperties.put("beacontest", beacon2);
        additionalProperties.put("beacontest2", beacon2);
        IEvent event = new BeaconEvent(eventType, organizationIds, projectIds, majorPlace, minorPlace, user, beacon1,
                deviceInfo, additionalProperties);
        addToEventStore(event);
    }

```


