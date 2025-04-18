# Sky Labs CART SDK for Android

Sky Labs CART SDK 연동 프로젝트입니다. 



## 요구사항

- Android 10 이상
- Android Kotlin



## 설치

### Gradle Implementation 추가

1. `libs.version.toml` SDK 패키지 추가
```
[versions]
cartSdk = "1.0.9"
  :

[libraries]
cart-sdk = { module = "com.github.SkyLabs-dev:cart", version.ref = "cartSdk" }
  :
```


2. `build.gralde`

```
dependencies {
  implementation(libs.cart.sdk)
    :
}
```



## SDK 초기화

1. `CARTManager` 생성 및 초기화
```
    CARTManager(
        context: Context,
        clientId: String,
        bleVersion: CARTProtocolVersion,
        cartListener: CARTListener
    )
```


- `clientId`
   SDK 사용 권한이 허용된 고유번호
   (계약이 체결되면 Sky Labs에서 발급합니다.)


- `CARTProtocolVersion`
    - V1 : 52 (Old)
    - V2 : 53 (New)


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

- `CARTManager.connect(address: String?)`
- 연결 및 연결해제 이벤트는 상기 CARTManager 초기화 시에 파라미터로 전달된 CARTListener에 전달된다.
```
interface CARTListener {
    fun bleConnectStatus(status: CARTDefs.ConnectStatus)
}
```


2. CART Scan

- `startScan(listener: CARTScanListener): Boolean`
- 스캔 리스트는 CARTScanListener에 실시간 전달된다.
```
interface CARTScanListener {
    fun bleScanList(scanStatus: CARTDefs.ScanStatus, device: CartDevice? = null)
}
```


3. 기타

- 자세한 사용법은 `SDK Sample 프로젝트` 참조
  - SDK Sample 프로젝트는 계약 체결 후 제공 됩니다.



## 라이선스

```
Sky Labs CART SDK for Android Kotlin
Copyright (c) 2025-present Sky Labs Inc.

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
