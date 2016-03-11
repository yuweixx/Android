# Android Studio Use Gradle

### 1.Change PackageName

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
### 2.Change AppName

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
