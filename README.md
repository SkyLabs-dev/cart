# Sky Labs CART SDK for Android

Sky Labs CART SDK 연동 프로젝트입니다. 



## 요구사항

- Android 10 이상
- Android Kotlin



## 설치

### Gradle Implementation 추가

1. `settings.gradle.kts` 
```
dependencyResolutionManagement {
  repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
  repositories {
    mavenCentral()
    maven { url 'https://jitpack.io' }
  }
}
```


2. `libs.version.toml`
- 기본 설정
```
[versions]
cartSdk = "Tag"

[libraries]
cart-sdk = { module = "com.github.SkyLabs-dev:cart", version.ref = "cartSdk" }
```
- 추가 설정
```
[versions]
retrofit = "2.9.0"
okhttp = "4.12.0"
okhttpUrlConnection = "4.9.0"
okhttpLoggingInterceptor = "4.9.3"
timber = "5.0.1"
kotpref = "2.13.1"
activity = "1.9.3"
roomKtx = "2.6.1"
datadog = "2.19.2"

[libraries]
retrofit = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
retrofit-converter-gson = { group = "com.squareup.retrofit2", name = "converter-gson", version.ref = "retrofit" }
retrofit-converter-scalars = { group = "com.squareup.retrofit2", name = "converter-scalars", version.ref = "retrofit" }
okhttp = { group = "com.squareup.okhttp3", name = "okhttp", version.ref = "okhttp" }
okhttp-urlconnection = { group = "com.squareup.okhttp3", name = "okhttp-urlconnection", version.ref = "okhttpUrlConnection" }
okhttp-logging-interceptor = { group = "com.squareup.okhttp3", name = "logging-interceptor", version.ref = "okhttpLoggingInterceptor" }

kotpref = { group = "com.chibatching.kotpref", name = "kotpref", version.ref = "kotpref" }
kotpref-gson-support = { group = "com.chibatching.kotpref", name = "gson-support", version.ref = "kotpref" }
kotpref-enum-support = { group = "com.chibatching.kotpref", name = "enum-support", version.ref = "kotpref" }

timber = { group = "com.jakewharton.timber", name = "timber", version.ref = "timber" }

datadoghq = { group = "com.datadoghq", name = "dd-sdk-android-rum", version.ref = "datadog" }
datadoglogs = { group = "com.datadoghq", name = "dd-sdk-android-logs", version.ref = "datadog" }
```

3. `build.gralde`
- 기본 설정  
```
dependencies {
  implementation(libs.cart.sdk)
}
```
- 추가 설정  
```
dependencies {
  implementation libs.retrofit
  implementation libs.retrofit.converter.gson
  implementation libs.retrofit.converter.scalars
  implementation libs.okhttp
  implementation libs.okhttp.urlconnection
  implementation libs.okhttp.logging.interceptor

  implementation libs.androidx.room.ktx

  implementation libs.timber

  implementation libs.kotpref
  implementation libs.kotpref.gson.support
  implementation libs.kotpref.enum.support

  implementation libs.datadoghq
  implementation libs.datadoglogs
}
```


## SDK 초기화

1. `CARTManager` 생성 및 초기화
```
  CARTManager(
    context: Context,
    clientId: String,
    clientSec: String,
    bleVersion: CARTProtocolVersion,
    cartListener: CARTListener
  )
```


- `clientId`, `clientSec`
   SDK 사용 권한이 허용된 고유번호  
   (계약이 체결되면 Sky Labs 에서 발급합니다.)


- `CARTProtocolVersion`
    - V1 : 52
    - V2 : 53


- `CARTListener`
```
interface CARTListener {
    fun bleConnectStatus(status: CARTDefs.ConnectStatus)

    fun systemStatus(logCount: Int, bpCount: Int, batteryLevel: Int, charge: Boolean)

    fun batteryStatus(level: Int, charge: Boolean)

    fun notification(type: CARTDefs.NotiType)
}
```

## SDK 사용법

1. CART Connect  
  `CARTManager.connect(address: String?)`  
  연결 및 연결해제 이벤트는 상기 CARTManager 초기화 시에 파라미터로 전달된 CARTListener에 전달된다.  
```
interface CARTListener {
    fun bleConnectStatus(status: CARTDefs.ConnectStatus)
}
```


2. CART Scan  
  `startScan(listener: CARTScanListener): Boolean`  
  스캔 리스트는 CARTScanListener에 실시간 전달된다.  
```
interface CARTScanListener {
    fun bleScanList(scanStatus: CARTDefs.ScanStatus, device: CartDevice? = null)
}
```


3. 기타  
  자세한 사용법은 `SDK Sample 프로젝트` 참조  
  **SDK Sample 프로젝트는 계약 체결 후 제공 됩니다.**



## 라이선스

```
Sky Labs CART SDK for Android Kotlin
Copyright (c) 2025-present Sky Labs Inc.
```
