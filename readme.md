# LT Maestro Framework sample test — TestMu AI (Formerly LambdaTest)

Support for directly running Maestro Tests on the device at TestMu AI using Hyperexecute and RealDevice

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

## 🚀 [LambdaTest is Now TestMu AI](https://www.testmuai.com/lambdatest-is-now-testmuai/)

👋 Welcome to TestMu AI, the next evolution of LambdaTest. As of January 2026, LambdaTest has officially rebranded to TestMu AI. We have evolved from a cross-browser testing cloud into a unified, AI-native quality engineering platform designed for the modern DevOps era.

Whether you have been part of the LambdaTest community for years or are just discovering TestMu AI, our mission remains the same: to help you ship faster with high-scale test execution, autonomous testing, and deep quality analytics.

**🔄 Our Rebrand Journey**

We chose the name TestMu AI to reflect our shift towards intelligent, autonomous testing. While our identity has changed, our core technology and commitment to the testing community stay the same.

**✨ Specialties**

- 🤖 AI-Native Test Execution (Formerly LambdaTest)
- ⚡ Autonomous Test Automation
- 🌐 Cross-Browser & Mobile Testing
- 📊 Unified Quality Intelligence

👉 Find [LambdaTest's New Home](https://www.testmuai.com/).