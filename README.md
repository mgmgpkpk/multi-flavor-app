# Multi Flavor App
This app is the sample of using product flavors.  

## Strange error of Gradle tasks
When the app needs multi `signingConfigs` that are defined with the environments,  `Gradle tasks` would show an strange error.

### 1 flavor - darjeeling
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
$ ./gradlew assembleDarjeeling_prd
```

### 2 flavor - darjeeling and assam
When we execute the same commands after added `flavor-assam.gradle`, the error will be occurred.
```
FAILURE: Build failed with an exception.

* What went wrong:
Some problems were found with the configuration of task ':app:packageDarjeeling_prdRelease'.
> No value has been specified for property 'signingConfig.keyAlias'.
> No value has been specified for property 'signingConfig.storePassword'.
```
We think there is the problem about **darjeeling flavor signingConfigs** because of the error message.  
(It says something wrong with the task named `:app:packageDarjeeling_prdRelease`)  
But this is the mislead.  
The solution is set the environments for **assam flavor signingConfigs**.
```
$ export asmStorePass=XXXXXX
$ export asmKeyAlias=XXXXXX
$ export asmKeyPass=XXXXXX
$ ./gradlew assembleDarjeeling_prd
```

