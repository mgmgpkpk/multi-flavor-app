# Multi Flavor App
This app is the sample of using product flavors.  

## Strange error of Gradle tasks
When the app needs multi `signingConfigs` that are defined with the environments,  `Gradle tasks` would show an strange error.

### 1 flavor - flavor-darjeeling
```groovy
    signingConfigs {
        release {
            storeFile file("./src/darjeeling_prd/keystore/darjeeling-prd.keystore")
            storePassword System.getenv("darStorePass")
            keyAlias System.getenv("darKeyAlias")
            keyPassword System.getenv("darKeyPass")
        }
    }
```
In this case, there is no an error with the commands like below.
```
$ export darStorePass=XXXXXX
$ export darKeyAlias=XXXXXX
$ export darKeyPass=XXXXXX
$ ./gradlew assenmbleDarjeeling_prd
```