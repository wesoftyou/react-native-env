# react-native-env
Guide on how to set up env for react native

## Used for set up:
- Android productFlavors
- IOS scheme
- react-native-config

**Warning**
*  use only "dev" scheme/productFlavor for development,  "staging"/"prod" are going to be used while QA/Production
*  For iOS  only "dev" scheme is debuggable, "stage"/"production" are signed via release configs

## How to use
### Android
**Run on device/emulator (debug mode)**
1. `npm run  react-native run-android --variant=devDebug` (uses config from .env.dev)
2. `npm run  react-native run-android --variant=stagingDebug` (uses config from .env.staging)
3. `npm run  react-native run-android --variant=prodDebug` (uses config from .env.prod)

**After success build you can see  error:**
 `Intent { cmp=com.app/.MainActivity } Error type 3 Error: Activity class {com.app/com.app.MainActivity} does not exist`
 - but it's ok, just launch application on  device/emulator**
 
**Assembling build (release mode)**
 1. `npm run  react-native run-android --variant=assembleDevRelease` (uses config from .env.dev)
 2. `npm run  react-native run-android --variant=assembleStagingRelease` (uses config from .env.staging)
 3. `npm run  react-native run-android --variant=assembleProdRelease` (uses config from .env.prod)

### IOS
**NOT use `react-native run-ios`**
**Running on simulator/real device:**
1. Choose schema
2. Run on device/simulator

**Assembling build (release mode):**
1. Choose schema
2. Run "Product/Archive";

## Make changes

### Android
* `react-native-config` - basic link changes (MainApplication.java, settings.gradle, android/app/build.gradle);
* `android/app/build.gradle`
![alt text](readme-img/build-gradle-defaultConfig.png)
![alt text](readme-img/build-gradle-flavors.png)
* `proguard-rules.pro`
![alt text](readme-img/proguard-rules.png)

- added `app/src/dev/res/values/strings.xml` for "dev" productFlavor - for bundle name `DEV-app`;
- added `app/src/stage/res/values/strings.xml` for "stage" productFlavor - for bundle name `STAGING-app`;
- added `app/src/production/res/values/strings.xml` for "production" productFlavor - for bundle name `app`;

### IOS

- `react-native-config` - basic link changes (Libraries, Build Setting, Linked Frameworks and Libraries, Build Phases);

- Added new configuration (Staging)
![alt text](readme-img/ios-project-configuration.png)

- Added new User-Defined Settings (APP_BUNDLE_ID_SUFFIX, APP_ENVIRONMENT, APP_PRODUCT_NAME)

![alt text](readme-img/ios-project-additions.png)

- Updated Product Bundle Identifier for each configuration (Debug, Staging, Release)

![alt text](readme-img/ios-product-bundle-identifier.png)

- Added Library Search Paths fix for new configuration (Staging)

![alt text](readme-img/ios-library-search-paths.png)

- Added Per-configuration build products path fix for new configuration (for "App Target" on tab "Build Settings") (Staging) 

![alt text](readme-img/ios-per-configuration-build-products-path.png)

- Updated Product Name (Added Prefix)

![alt text](readme-img/ios-product-name-with-prefix.png)

- Duplicated "production" scheme - called "stage" scheme

![alt text](readme-img/ios-scheme-duplicate.png)

- Edited ALL schemes ("dev", "stage", "production"); For each scheme - setting up `Pre-actions`

![alt text](readme-img/ios-scheme-edit.png)

- Set up Pre-action script for ALL schemes (Build, Run, Archive):

1. "dev" - ".env.dev"
1. "stage" - ".env.stage"
1. "production" - ".env.production"

![alt text](readme-img/ios-preaction-script.png)

- Set up Build Configuration script for ALL schemes (Run, Archive):

1. "dev" - "Debug"
1. "stage" - "Staging"
1. "production" - "Release"

![alt text](readme-img/ios-scheme-run-staging.png)
![alt text](readme-img/ios-scheme-archive-staging.png)
