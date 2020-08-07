# Navisens Web SDK
Webassembly module for local intertial estimation in web browser

-----
## What it does
The sample website webcore.html demonstrates usage of the navisens motionDNA webassembly module to estimate your location in cartestian space. The DeviceMotion web api is used to capture accelerometer and gyroscope sensor data from the mobile device that is running the demo.

## Getting Started

### Prerequisites
The module itself must be run on a device with the DeviceMotion API properly implemented. It has been so far tested on newer Android and iOS phone hardware succussfully but may also work on other devices and browsers.

Tested OS:
- iOS 13, 12.1+
- Android 9 w/ Chrome 87

The website requesting the motion data must be served up on a secure site as the API will not be available on standard HTTP.

### Starting up
Navigate to where you are hosting the secure sample site and press start. On iOS there should be a request for sensor access. On Android it should simply startup. The website may not respond for a few second while the SDK starts up. This is expected behavior.

The Cartesian graph should begin to update with a x,y view of your trajectory relative to your initial location when the SDK started up

### API Calls

The API for this base demo is extremely simple and currently has no mechanism for customization of the estimation. This will likely be added in future iteration to align better with the feature set of our primary mobile SDK.

`start()`

This will load our inertial model and start process motion data. The call must be made after the user has granted the web site access to the motion sensors on the mobile device.

`stop()`

This call will end the estimation and stop processing sensor data.

### Callbacks

3 callback methods must be impemented in the javascript layer in order for the SDK to function properly

`receive(x,y,height,timestamp,motion)`

This is the primary callback and is where the estimation of the users position is passed back to the hmtl and javascript layers. The method also is handed the currently predictedmotion for the user, which is usual one of three possible motions... stationary, fidgeting, and forward.

`reportStatus(statusCode, description)`

This method will report some common errors or status updates on SDK.

## Known Issues
On iOS devices, sensor collection appears to pause during a touch event and during scrolling animataions. While it appears that most sensor events are still capture and delivered to our SDK, since the timestamps are not coupled with the sensor data, the timestamp will appear to be duplicate for all event cached for the duration of the pause. This may affect estimation negatively.

## Troubleshooting

#### DevieMotion api does not appear to exist.
Make sure you are serving the site up in a secure HTTPS context.

#### The Module does not load
This may be from trying to run the web site from running the html file directly in browser rather than being served up from NGINX or Apache or some other server. This will always fail and you need to configure a server like the ones mentioned above to make the module load proberly in the example.

#### Other problems
Reach out to the email(s) listed below if you are still experiencing issues

## Support
Contact Support@navisens.com for any additinal problems you may be having with this early release