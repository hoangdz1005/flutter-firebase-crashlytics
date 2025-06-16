# flutter_firebase_crashlytics

- Thêm dependencies trong pubspec.yaml
```yaml
  firebase_core: ^3.14.0
  firebase_crashlytics: ^4.3.7
```

- Trong hàm main
```dart
WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp();
FlutterError.onError = FirebaseCrashlytics.instance.recordFlutterFatalError;
```

## Setup android
- Thêm app android trong project firebase
![](assets/1.png)

- Thêm plugin và dependencies trong app/build.gradle.kts
```kotlin
id("com.google.gms.google-services")
```
```kotlin
dependencies {
  implementation(platform("com.google.firebase:firebase-bom:33.15.0"))
  implementation("com.google.firebase:firebase-analytics")
}
```
- Thêm plugin trong settings.gradle.kts
```kotlin
id("org.jetbrains.kotlin.android") version "2.1.0" apply false
id("com.google.gms.google-services") version "4.4.2" apply false
```
- Crash app log trên firebase
![](assets/5.png)

## Setup IOS
- Thêm app ios trong project firebase
  ![](assets/2.png)

- Trong Build Settings, đặt giá trị Debug Information Format thành DWARF with dSYM File
  ![](assets/7.png)

- Trong Build Phases, chọn New Run Script Phase
  ![](assets/8.png)

- Thêm cấu hình như sau
  ![](assets/9.png)

``` 
"${PODS_ROOT}/FirebaseCrashlytics/run"
```
```
${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}
${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}/Contents/Resources/DWARF/${PRODUCT_NAME}
${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}/Contents/Info.plist
$(TARGET_BUILD_DIR)/$(UNLOCALIZED_RESOURCES_FOLDER_PATH)/GoogleService-Info.plist
$(TARGET_BUILD_DIR)/$(EXECUTABLE_PATH)
```