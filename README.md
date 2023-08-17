# FNCY Wallet SDK for Android

[![Maven Central](https://img.shields.io/maven-central/v/io.github.FNCYchain/fncy-wallet-android-sdk.svg)](https://search.maven.org/artifact/io.github.FNCYchain/fncy-wallet-android-sdk)
[![API](https://img.shields.io/badge/API-23%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=23)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)


## Minimum Requirement
- Java 11+
- Android API 23+


## Installation

### 1. Add the mavenCentral() on project level(root level) build.gradle file:
``` gradle
allprojects {
    repositories {
        mavenCentral()
    }
}
```

### 2. Add dependency on module level build.gradle file:

#### build.gradle
``` groovy
dependencies {
    implementation "io.github.FNCYchain:fncy-wallet-android-sdk:$latestVersion"
}
```

#### build.gradle.kts
``` kotlin dsl
dependencies {
    implementation("io.github.FNCYchain:fncy-wallet-android-sdk:$latestVersion")
}
```

### 3. Add permission, meta-data to AndroidManifest.xml
``` xml
<uses-permission android:name="android.permission.INTERNET"/>

<application
    ...
<!-- meta-data의 Key값은 반드시 다음과 같이 작성 -->
        <meta-data
            android:name="com.metaverse.world.fncy.ApiKey"
            android:value="@string/api_key"/>
        <meta-data
            android:name="com.metaverse.world.fncy.BaseUrl"
            android:value="@string/base_url"/>
</application>
```

### 4. Add proguard-rules:
[proguard-rules.pro](https://github.com/FNCYchain/fncy-wallet-android-sdk/blob/main/app/proguard-rules.pro)
```
-keep,allowobfuscation,allowshrinking class kotlin.coroutines.Continuation
-keep class com.metaverse.world.wallet.sdk.model.** { *; }
-keep class com.metaverse.world.wallet.sdk.repository.network.** { *; }
```

## Getting Started

``` kotlin
class FncyApplication : Application() {

    override fun onCreate() {
        super.onCreate()
        FncyWalletSDK.initSDK(
            application = this@FncyApplication,
        )
    }
}
```

``` kotlin
// In ViewModel
class FncyViewModel() : ViewModel() {

    fun getWallet() {
        viewModelScope.launch {
            val fncyWallet = FncyWalletSDK("token")
            val result = fncyWallet.getWallet()
            result
                .onSuccess { wallet ->
                    // 성공 처리
                }.onFailure { throwable ->
                    // 실패 처리
                }
        }
    }

} 
```

## Dependencies Library
fncy-wallet-android-sdk for Android uses libraries below:

- androidx.core:core-ktx:1.10.1
- org.jetbrains.kotlinx:kotlinx-serialization-json:1.2.1
- com.squareup.okhttp3:okhttp:4.11.0
- com.squareup.okhttp3:logging-interceptor:4.11.0
- com.squareup.retrofit2:retrofit:2.9.0
- com.jakewharton.retrofit:retrofit2-kotlinx-serialization-converter:0.8.0
- org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.1
- io.insert-koin:koin-android:3.4.3
- com.google.android.gms:play-services-auth:20.6.0
- com.jakewharton.timber:timber:5.0.1



## How to use FNCY Wallet SDK for Android?
[FNCY-GitBook](https://app.gitbook.com/o/sxbvsaQu6S0zvfR1DBLL/s/rtEQIDnbkvSB2krcokD0/~/changes/173/for-developers/fncy-mobile-app/fncy-wallet-sdk/android)

<!--## License

fncy-wallet-android-sdk is released under the Apache 2.0 license. <a href="https://github.com/FNCYchain/fncy-wallet-android-sdk/blob/main/LICENSE">See LICENSE</a> for details.-->
