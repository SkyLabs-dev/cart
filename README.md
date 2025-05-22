![Sky Labs logo](https://github.com/SkyLabs-dev/cart/blob/main/SkyLabs.png)

# Sky Labs CART SDK for Android

[![kotlin](https://img.shields.io/badge/kotlin-2.1.0-blue.svg)]() [![codecov](https://codecov.io/gh/chibatching/Kotpref/branch/master/graph/badge.svg)](https://codecov.io/gh/chibatching/Kotpref) [![license](https://img.shields.io/github/license/chibatching/Kotpref.svg?maxAge=2592000)]()

Sky Labs CART SDK 연동 프로젝트입니다. 



## 요구사항

- Android 10 이상
- Android Kotlin



## 설치

### AndroidManifest.xml Permission 추가
```groovy
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

### Gradle Implementation 추가

1. `settings.gradle.kts` 
```groovy
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
```groovy
    [versions]
    cartSdk = "Tag"
    
    [libraries]
    cart-sdk = { module = "com.github.SkyLabs-dev:cart", version.ref = "cartSdk" }
```

3. `build.gralde`
- 기본 설정  
```groovy
    dependencies { 
        implementation(libs.cart.sdk)
    }
```


## SDK 초기화

1. `CARTManager` 생성 및 초기화
```kotlin
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
```kotlin
interface CARTListener {
    fun bleConnectStatus(status: CARTDefs.ConnectStatus)

    fun batteryStatus(level: Int, charge: Boolean)

    fun notification(type: CARTDefs.NotiType)

    fun error(type: CARTDefs.ErrorType)
}
```

## SDK 사용법

1. CART Connect  
  `CARTManager.connect(address: String?)`  
  연결 및 연결해제 이벤트는 상기 CARTManager 초기화 시에 파라미터로 전달된 CARTListener에 전달된다.  
```kotlin
interface CARTListener {
    fun connectStatus(status: CARTDefs.ConnectStatus)
}
```


2. CART Scan  
  `startScan(listener: CARTScanListener): Boolean`  
  스캔 리스트는 CARTScanListener에 실시간 전달된다.  
```kotlin
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
