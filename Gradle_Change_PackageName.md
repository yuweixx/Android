# Android Studio Gradle Change PackageName
* 1.
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
