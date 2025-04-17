# Sky Labs CART SDK for Android

Sky Labs CART SDK 연동 프로젝트입니다. 



## 요구사항

- Android 10 이상
- Android Kotlin



## 설치

### Gradle Implementation 추가

1. libs.version.toml SDK 패키지 추가
```
[versions]
cartSdk = "1.0.0"
  :

[libraries]
cart-sdk = { module = "com.github.SkyLabs-dev:cart", version.ref = "cartSdk" }
retrofit = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
retrofit-converter-gson = { group = "com.squareup.retrofit2", name = "converter-gson", version.ref = "retrofit" }
retrofit-converter-scalars = { group = "com.squareup.retrofit2", name = "converter-scalars", version.ref = "retrofit" }
okhttp = { group = "com.squareup.okhttp3", name = "okhttp", version.ref = "okhttp" }
okhttp-urlconnection = { group = "com.squareup.okhttp3", name = "okhttp-urlconnection", version.ref = "okhttpUrlConnection" }
logging-interceptor = { group = "com.squareup.okhttp3", name = "logging-interceptor", version.ref = "loggingInterceptor" }

kotpref = { group = "com.chibatching.kotpref", name = "kotpref", version.ref = "kotpref" }
kotpref-gson-support = { group = "com.chibatching.kotpref", name = "gson-support", version.ref = "kotpref" }
kotpref-enum-support = { group = "com.chibatching.kotpref", name = "enum-support", version.ref = "kotpref" }

timber = { group = "com.jakewharton.timber", name = "timber", version.ref = "timber" }

datadoghq = { group = "com.datadoghq", name = "dd-sdk-android-rum", version.ref = "datadog" }
datadoglogs = { group = "com.datadoghq", name = "dd-sdk-android-logs", version.ref = "datadog" }
  :
```

3. build.gralde 

```
dependencies {
  implementation(libs.cart.sdk)
  
  implementation libs.retrofit
    implementation libs.retrofit.converter.gson
    implementation libs.retrofit.converter.scalars
    implementation libs.okhttp
    implementation libs.okhttp.urlconnection
    implementation libs.logging.interceptor

    implementation(libs.timber)

    implementation libs.kotpref
    implementation libs.kotpref.gson.support
    implementation libs.kotpref.enum.support

    implementation libs.datadoghq
    implementation libs.datadoglogs
    :
}
```



## SDK 초기화

1. `CARTManager` 생성 및 초기화
```
    CARTManager(
        val context: Context,
        bleVersion: CARTProtocolVersion,
        cartListener: CARTListener
    )
```

2. `CARTProtocolVersion`
    - V1 : nrf52 (Old)
    - V2 : nrf53 (New)


3. `CARTListener`
```
interface CARTListener {
    fun bleConnectStatus(status: CARTDefs.ConnectStatus)

    fun bleScanList(scanStatus: CARTDefs.ScanStatus, device: CartDevice? = null)

    fun systemStatus(logCount: Int, bpCount: Int, batteryLevel: Int, charge: Boolean)

    fun batteryStatus(level: Int, charge: Boolean)

    fun notification(type: CARTDefs.NotiType)
}
```

4. 기타 자세한 사용법은 SDK Sample 프로젝트 참조


## 라이선스

```
Naver ID Login SDK for iOS Swift
Copyright (c) 2025-present NAVER Corp.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
