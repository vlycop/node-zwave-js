# Changelog
[Older changelog entries (v1...v8)](CHANGELOG_v8.md)

<!--
	Add placeholder for next release with `wip` snippet
-->
## __WORK IN PROGRESS__
<!-- ### Breaking changes

### Features -->

### Bugfixes
* Route health checks now approach the minimum power level linearly from the normal power to avoid nodes with a suboptimal implementation getting stuck in test mode and causing a wrong test result (#4494)
* For `Door Lock CC` V3 and below, the lock/bolt/latch sensors are now created again, since support cannot be tested in these versions (#4490)
* The initial connection to a TCP socket is now retried if the connection cannot be established immediately (#4492)

<!-- ### Config file changes -->

### Changes under the hood
* Expose "safe" entrypoint in each package which can be used from non-Node.js contexts (#4469)


## 9.0.3 (2022-04-20)
### Bugfixes
* Fixed an issue where version based feature testing of 500 series controllers with support for the `GetProtocolVersion` API would fail
* Fixed an issue causing certain unsolicited messages like `Notification CC Reports` not to be processed while an API command was ongoing

### Config file changes
* Treat Basic Set as event for Philio PSR03-B (#4487)
* Treat Basic Set as event for Philio PSR03-A (#4488)
* Add metadata to Shenzhen Heiman HS1SA-Z (#4244)
* Add Nexia One Touch NX1000 (#4231)
* Add Minoston Outdoor Plug Dimmer MP22ZD (#4342)
* Add Cherubini Ora ZRX (#4463)
* Add param 92 (Battery Calibration Check) to aërQ v2.01 (#4472)

### Changes under the hood
* The CC index in the documentation now uses relative paths, so it also works in the non-rendered version on GitHub  (#4476)

## 9.0.2 (2022-04-14)
### Bugfixes
* The door/latch/bolt status sensors are no longer created if unsupported by the door lock (#4448)
* Fixed an issue where `securityClasses` in provisioning entries were returned as strings instead of their enum values (#4462)

### Config file changes
* Add metadata to ZooZ ZEN26 (#4348)
* Add metadata to ZooZ ZEN21 (#4349)
* Add metadata to ZooZ ZEN27 (#4347)
* Remove option 4 of LED Indicator Mode for Zooz ZSE40, FW 32.32+ (#4451)
* Extend Heatit TF016 config to include TF021 (#4452)
* Correct valueSize for param 15 on GE/Jasco 26931 / ZW4006 (#4441)
* Add manual to GE/Jasco 26932 / 26933 / ZW3008 (#4446)
* Correct reporting groups for Aeotec ZW132 Dual Nano Switch (#4447)
* Removed the optional `min/maxValue` from many config files where the values were unnecessary or incorrect (#4455)

### Changes under the hood
* Added documentation for the `Multilevel Switch CC` notifications (#4444)

## 9.0.1 (2022-04-03)
### Bugfixes
* The auto-generated argument validation now considers `{ prop1: undefined }` and `{}` to be equivalent.

## 9.0.0 (2022-04-03) · _„You had my curiosity. But now you have my attention.”_
Roughly nine months after the [last major release](https://github.com/zwave-js/node-zwave-js/releases/tag/v8.0.1), we've reached a new milestone.
Z-Wave JS is now 4 years old, its usage has more than doubled over the course of the `v8.x` release line and it is still growing steadily. There are many exciting things yet to come, so stay tuned!

### Breaking changes · [Migration guide](https://zwave-js.github.io/node-zwave-js/#/getting-started/migrating-to-v9)
* The `route` parameter in `SendDataBridgeRequest` has been removed, since it isn't supported in any known SDK version (#3741)
* Faster timeout while waiting for a response to a GET request (#3756)
* Renamed  properties and methods of the `Controller` class and related message classes (#3761)
* Converted the `isControllerNode` method on the `ZWaveNode` class to a readonly property (#3972)
* (possibly breaking) Upgraded `serialport` library to version 10.x (#4225)
* The legacy network cache file `<homeid>.json` was converted to an appendonly `.jsonl` file in order to prevent data loss (#4263)
* Almost all CC API methods now validate their arguments and will throw if they don't match the expected type (#4405)

### Features
* The node statistics now include RSSI and the actual routes taken (LWR, NLWR) for communication (#4022)
* A utility method `rssiToString` was added to convert RSSI values to a human readable string
* Export some commonly used string formatting utilities (#4318)
* Add support for `Irrigation CC` (#4270)
* The controller's `sdkVersion` property now includes the build number (or minor version) if supported (#4355, #4398)
* Also expose `sdkVersion` on the controller node (#4388)
* Added a compat flag to expose received `MultilevelSwitchCCSet` commands via the `event` property (#4282)
* Received `MultilevelSwitchCC` `Start/StopLevelChange` commands are now emitted as notifications (#4282)
* Added an `sdkVersion` property for nodes (#4371)
* `LogContext` and related types are now exported (#4378)
* Map `Basic CC Set` to appropriate CCs for devices with `Remote Switch` device class (#4382)
* User codes and network keys are no longer logged (#4383)

### Bugfixes
* Error reporting is now opt-in (#4279) and should no longer force-exit the application when an unhandled rejection occurs (#4291)
* Increase the default controller response timeout to 10s to work around an issue where some 500 series controllers take too long to confirm execution of a SendData command when the target node is unresponsive (#4259)
* Fix parsing of BridgeApplicationCommandRequest that do not contain an RSSI reading (#4337)
* Fixed an issue with automatic clock correction where rounding the time up could lead to the clock being 1 hour late (#4346)
* Notification event parameters containing a `UserCodeCC` report now correctly indicate the user ID again (#4356)
* Fixed an issue in the NVM migration routine that could lead to nonsensical radio settings which can only be changed by editing the NVM file manually (#4368)
* Prevent infinite loop in health check when the node responds but there is no progress (#4372)
* Route health checks can no longer have sleeping nodes as the target (#4373)
* Lifeline health checks now wait for sleeping nodes to wake up instead of considering the wait time latency (#4376)
* Route health check rounds now indicate when there were zero failed pings (#4377)
* Multi Channel encapsulation now correctly uses V1 commands if this is the highest supported version of a node (#4387)
* The versions of CCs that are not supported by the root device but only endpoints are now correctly queried (#4419)

### Config file changes
* Correct device description for Leviton DZMX1 (#4317)
* Add metadata to Zooz ZSE18 (#4338)
* Add metadata to AEON Labs DSB29 (#4334)
* Add metadata to Vision Security GZ8101 (#4350)
* Add metadata to AEON Labs DSC26 (#4343)
* Add metadata to Ecolink DWZWAVE25 (#4339)
* Merge redundant config files for Fibaro Walli Double Switch (#4370)
* Add value 2 to Aeotec ZW100 param 81, FW 1.10-1.12 (#4361)
* Add parameters and correct default values for Fibaro Smart Module FGS214 and Double Smart Module FGS224 (#4345)
* Correct value size for Zooz ZEN20 v2 (#4358)
* Preserve all endpoints for Qubino ZMNKAD1 Luxy Smart Switch (#4366)
* Enable Multilevel Switch `event` value for Aeotec ZW111 (#4380)
* Add metadata to AEON Labs DSB09 (#4391)
* Correct value for Brightness After Power Failure for LZW31-SN (#4409)
* Add value 3 to param 4 for Zooz Zen16 (#4404)
* Add values for Alarm and Doorbell Sound Selection to Shenzhen Neo Siren Alarm (#4400)

### Changes under the hood
* Lots of dependency updates
* We no longer use `lerna` for monorepo management. It is largely unmaintained and doesn't support `yarn`'s `workspace:` protocol (#4071)
* The bot now considers `zip` a valid extension for Z-Wave JS logfiles
* Added missing `toLogEntry` implementations (#4389)
* Implemented a transformer-based codegen to auto-implement method argument checks based on types (#4394, #4396)
* In VSCode, the project now gets precompiled before running the test script (#4397)
