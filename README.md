# app_automate_browserstack_integration



## Getting Started

[BrowserStack](https://www.browserstack.com/) is a cloud web and mobile testing platform that provides developers with the ability to test their websites and mobile applications across on-demand browsers, operating systems and real mobile devices. 


Now it is possible test your applications via **Codemagic** using the real devices offered by **BrowserStack**. 




The process is quite straightforward and it is easily configured in **comdemagic.yaml** 




Add the following curl command in the yaml file after building **.ipa** or **.apk**:




```
curl -u "$BROWSERSTACK_USERNAME:$BROWSERSTACK_ACCESS_TOKEN" -X POST "https://api-cloud.browserstack.com/app-live/upload" -F "file=@build/ios/ipa/your_app_release.ipa"
```




**$BROWSERSTACK_USERNAME** and **$BROWSERSTACK_ACCESS_TOKEN** are generated to you automatically after signing up with **BrowserStack** and setting up the enviorment variables in the Codemagic UI will allow them to be used during a build.


In order to successfully upload your app to BrowserStack environment, you will also need to provide the generated .ipa and .apk inside the curl command above and their paths are sent to where you configure your artifacts.


You can test your native and hybrid apps on BrowserStack through Codemagic. For that purpose, you need to go through three steps using REST API endpoints:


1. Upload your app
2. Upload Test Suite
3. Start testing


In order to upload test Suites for android apps, you need to run ./gradlew assembleAndroidTest. Make sure that **app/build.gradle** file includes Instrumentation runner:

```
  defaultConfig {
     testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
}
```

If you are building your app in release mode, then you also need to build your test Suite .apk in release mode by adding the following in **app/build.gradle**:

```
    testBuildType "release"
```
