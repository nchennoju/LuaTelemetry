# Lua Telemetry Flight Status Screen for INAV/Taranis

#### Taranis Q X7
![sample](http://www.leethost.com/link_pics/iNav1.png "Launch-based model orientation and location indicators")
![sample](http://www.leethost.com/link_pics/iNav2.png "Compass-based direction indicator")

#### Taranis X9D, X9D+ & X9E
![sample](http://www.leethost.com/link_pics/iNav3.png "View on Taranis X9D, X9D+ & X9E")

## Features

* Launch-based model orientation and location indicators (great for lost orientation or if you lose site of your model)
* Compass-based direction indicator
* Bar gauges for Fuel (% battery mAh capacity remaining), Battery voltage, RSSI strength, Tx battery (and Altitude for X9D, X9D+ & X9E transmitters)
* Display and voice alerts for flight modes and other flight status information (altitude hold, heading hold, etc.)
* Voice notifications for % battery remaining (based on current), voltage low/critical, high altitude, lost GPS, ready to arm, armed, disarmed, etc.
* GPS information: Satellites locked, GPS altitude, GPS coordinates
* Display of current/maximum: Altitude, Distance, Speed and Current
* Display of current/minimum: Battery voltage, RSSI strength
* Display of current Fuel (% battery mAh capacity remaining), Rx voltage and automatic flight timer
* Speed and distance values are displayed in metric or imperial based on transmitter telemetry settings

## Requirements

* [OpenTX v2.2.0+](http://www.open-tx.org/) running on Taranis Q X7, X9D, X9D+ & X9E
* FrSky receiver that supports SmartPort telemetry: X4R(SB), X8R, XSR, R-XSR, XSR-M, XSR-E, etc. (D-series receivers **NOT** supported)
* [INAV v1.7.3+](https://github.com/iNavFlight/inav/releases) running on your flight controller
* GPS, altimeter, and compass sensors

## Notes

> **Notice:** If you get the message `Script Panic not enough memory` you've run out of memory on your transmitter.
> This happens if you have too many Lua scripts running (this includes model, function, and telemetry scripts).
> It's also possible that you have less memory to work with when running firmware that uses more memory (for example, firmware that includes multimodule support).
> Using transmitter firmware with `luac` included should reduce memory usage and increase the telemetry screen speed.

* Designed for multirotor models, but should be valuable for fixed wing (fixed wing feedback would be appreciated)
* Optional amperage sensor needed for fuel and current displays
* Uses Taranis settings for RSSI warning/critical levels for bar gauge range and audio/haptic warnings
* Uses Taranis settings for transmitter voltage min/max for battery gauge in screen title

## Setup

#### In INAV Configurator

1. Setup telemetry to send to your transmitter - [INAV telemetry docs](https://github.com/iNavFlight/inav/blob/master/docs/Telemetry.md)
2. If you have an amperage sensor, configure `battery_capacity` and set `smartport_fuel_percent = ON` in CLI settings

#### From Transmitter

1. With battery connected and **after GPS fix** [discover telemetry sensors](https://www.youtube.com/watch?v=n09q26Gh858) so all telemetry sensors are discovered
2. Telemetry distance sensor name must be changed from `0420` to `Dist`

#### INAV Lua Telemetry Screen Setup

1. Copy `iNav.lua` file to Taranis SD card's `\SCRIPTS\TELEMETRY\` folder
2. Copy `iNav` folder to Taranis SD card's `\SCRIPTS\TELEMETRY\` folder
3. In model setup, page to `DISPLAY`, set desired screen to `Script`, and select `iNav`

## Usage

#### Screen Description
![sample](http://www.leethost.com/link_pics/iNav4.png "Screen description")

From the Taranis main screen, hold the `Page` button to show custom screens, then page to the screen you set to show iNav.
Flashing values are either because there's no telemetry or a warning.
To flip between max/min values and current values, use the dial or +/- buttons.
To flip between compass-based direction and launch-based orientation and location, use the dial or +/- buttons.
If model is further than 25 feet away, the launch direction view will show the direction of the model based upon launch position and orientation.
This can be used to locate a lost model, using the launch-based model location indicator and distance.
The launch-based orientation view is useful if model orientation is unknown.
The script gives voice feedback for flight modes, battery levels, and warnings (no need to manually set this up for each model).
Voice alerts will play in background even if iNav LuaTelemetry screen is not displayed.

## Tips

* Between flights, long-press the Enter/dial and select `Reset telemetry`

## Release History

#### v1.1.3 - 10/10/2017
* Shows metric or imperial values based on transmitter telemetry settings
#### v1.1.2 - 10/06/2017
* Lots of refactoring which greatly reduced memory usage
* Re-enabled altitude bar gauge for X9D, X9D+ & X9E transmitters
* Better information layout if no current sensor is present
* Refactored GPS lock calculation to prevent script syntax errors
#### v1.1.1 - 09/28/2017
* Refactored code to reduce memory
* Removed alititude bar gauge for X9D, X9D+ & X9E transmitters (used too much memory?)
#### v1.1.0 - 09/22/2017
* Repo moved to INAVFlight
* Screen formatting for Taranis X9D, X9D+ & X9E
#### v1.0.0 - 09/19/2017
* Initial release
