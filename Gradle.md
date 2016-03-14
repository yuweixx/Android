# Android Studio Use Gradle

### 修改包名

```gradle
    flavorDimensions "flavor"
    
    productFlavors {
    a1 {
      flavorDimension "flavor"
      applicationID "com.app.a1"
    }
    
     a2 {
      flavorDimension "flavor"
      applicationID "com.app.a2"
    }
    }
```
### 修改应用名

Manifest.xml
```HTML
    <appliction
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="${APP_NAME}"
        android:theme="@style/Apptheme"
        <activity
            android:name=".MainActivity"
            android:label="${APP_NAME}"
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </appliction>
```

app/build.gradle
```gradle
    flavorDimensions "flavor"
    
    productFlavors {
    a1 {
      flavorDimension "flavor"
      manifestPlaceholders = [APP_NAME: "A1"]
    }
    
     a2 {
      flavorDimension "flavor"
      manifestPlaceholders = [APP_NAME: "A2"]
    }
    }
```

### 3.签名、混淆、对齐

```gradle
    signingConfigs {
        debug {
            storeFile file("/Users/pianpian/.android/debug.keystore")
        }
        
        release {
            storeFile file("/Users/pianpian/.android/acb123.keystore")
            storePassword "abc123"
            keyAlias "abc123"
            keyPassword "abc123"
        }
    }
    
    buildTypes {
        debug {
            buildConfigField "boolean","LOG_DEBUG","true"
            versionNameSuffix "-debug"
            minifyEnabled false
            zipAlignEnabled false
            shrinkResouces false
            signingConfig signingConfigs.debug
        }
        
        release {
            buildConfigField "boolean","LOG_DEBUG","true"
            minifyEnabled true
            zipAlignEnabled true
            shrinkResouces true
            signingConfig signingConfigs.release            
        }
    }
```
### 4.打包
* release
```sh
./gradlew assembleRelease
```

### 参考链接
http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Product-Flavor-Configuration
