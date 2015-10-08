# data_sender_app
App send raw sensor data to a client
------------------------------------
The characterisitcs that can be sent are defined in the following configuration:

    {
        "data_send_delay": 1,
        "max_interval": 60*60*12,
        "temperature": true,
        "temp_min_change": 0.1,
        "temperature_polling_interval": 300,
        "irtemperature": false,
        "irtemp_min_change": 0.5,
        "humidity": true,
        "humidity_min_change": 0.2,
        "humidity_polling_interval": 300,
        "buttons": false,
        "accel": false,
        "accel_min_change": 0.02,
        "accel_polling_interval": 3.0,
        "gyro": false,
        "gyro_min_change": 0.5,
        "gyro_polling_interval": 3.0,
        "magnet": false,
        "magnet_min_change": 1.5,
        "magnet_polling_interval": 3.0,
        "binary": true,
        "luminance": true,
        "luminance_min_change": 10.0,
        "luminance_polling_interval": 300,
        "power": true,
        "power_min_change": 1.0,
        "power_polling_interval": 300,
        "battery": true,
        "battery_min_change": 1.0,
        "battery_polling_interval": 300,
        "connected": true
    }
    
  If a device that supplies a charadteristic (eg: temperature) is connected to the app, then that characterisitc will be sent to the ContinuumBridge data client. The characteristic will only be sent if the corresponding entry in the configuration has a values of true. Also, characterisitcs will only be sent is they and changed by the corresponding min_charge value. Eg: if temp_minn_change is set to 0.5, temperature will only be sent to the data client after it has changed by 0.5 degrees C or more from the previous value that was sent. Polling interval values will be sent to device adaptors to request the the characterisitc be updated at that interval. With temperature_polling_interval set to 300 seconds, temperature updates will be requested from connected devices every 300 seconds. 
  
The following should be noted about polling intervals:

* Don't set the polling interval to shorted than is needed. Battery powered devices consume more power, and hence run down their batteries, if you request characteristics more often.
* Some devices send characterisitcs when they change anyway, in which case the polling interval does not have any effect.
* If another app requests a characteristic more frequenty than this one, this app will also receive updates at the shorter interval.

