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
* Opwn project setting and add new module and select the cloned folder location of the SDK.
* Add link to folder in the app/build.gradle file:

```
dependencies {
    compile project(':datasnapsdk-folder')
```
