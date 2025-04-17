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
  :
```

3. build.gralde 

```
dependencies {
  implementation(libs.cart.sdk)
    :
}
```



## SDK 초기화

1. `Podfile` 수정


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
