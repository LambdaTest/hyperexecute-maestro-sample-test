# LT Maestro Framework sample test

Support for directly running Maestro Tests on the device at Lambdatest using Hyperexecute and RealDevice

## Steps to launch test
1. Install hyperexecute cli from `Help` option on [hyperexecute](https://hyperexecute.lambdatest.com/hyperexecute/jobs) dashboard by going to Help -> Hyperexecute CLI

2. Move hyperexecute cli binary in the root directory of the repository.

3. To make cli executable run this: `chmod u+x ./hyperexecute`

4. From LT hyperexecute dashborad get your `USERNAME` and `ACCESS_KEY`

5. You can either upload the app through the dashboard mentioned below in Android and iOS or use this curl to upload app  and for getting the app_id for passing it in the script -
curl -u "<username>:<accessKey>" -X POST "https://manual-api.lambdatest.com/app/upload/realDevice" -F "appFile=@"<local_app_path>"" -F "name="sampleApp""

6. To start the test  `./hyperexecute --user <USERNAME> --key <ACCESS_KEY> --config yaml/maestro.yaml`

7. For iOS real devices, install the following JAR file and include it in your payload. https://prod-mobile-artefacts.lambdatest.com/assets/maestro-cli/1.41.0-beta-1/maestro.jar


## Android 

### Real Device

- You can use the `android-realdevice.yaml` to run test on android real device present in the yaml/android folder.

- `setup-script.sh` and `runTest.sh` present in the maestro-test folder are required to run test cases on android real device.

- You can also replace the `<app_id>` with your app id which you can get by upload the app to [real device dashboard](https://applive.lambdatest.com/app). You can use the `sample.apk` for testing present in the maestro-test folder.


### Emulator

- You can use the `android-emulator.yaml` to run test on android real device present in the yaml/android folder.

- `setup-script.sh` and `runTest_android_emulator.sh` present in the maestro-test folder are required to run test cases on android emulators.

- You can also replace the `<app_id>` with your app id which you can get by upload the app to [real time dashboard](https://app.lambdatest.com/console/realtime/app). You can use the `sample.apk` for testing present in the maestro-test folder.



## iOS

### Real Device

- You can use the `ios-realdevice.yaml` to run test on android real device present in the yaml/ios folder.

- `runTest_ios_realdevice.sh` present in the maestro-test folder is only required to run test cases in iOS real device

- You can also replace the `<app_id>` with your app id which you can get by upload the app to [real device dashboard](https://applive.lambdatest.com/app). You can use the `Proverbial_ios.ipa` for testing present in the maestro-test folder.


### Simulator

- You can use the `ios-simulator.yaml` to run test on android real device present in the yaml/ios folder.

- `setup-script-iOS.sh` and `runTest_ios.sh` present in the maestro-test folder are required to run test cases of 

- You can also replace the `<app_id>` with your app id which you can get by upload the app to [real time dashboard](https://app.lambdatest.com/console/realtime/app). You can use the `Proverbial_ios.zip` for testing present in the maestro-test folder.

#### Note

- Incase of iOS simulators we need .zip of the app and in case of real device we upload the .ipa. 