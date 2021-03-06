﻿# process

Electron의 `process` 객체는 기존의 node와는 달리 약간의 차이점이 있습니다:

* `process.type` String - 프로세스의 타입, `browser` (메인 프로세스) 또는 `renderer`가 됩니다.
* `process.versions['electron']` String - Electron의 버전.
* `process.versions['chrome']` String - Chromium의 버전.
* `process.resourcesPath` String - JavaScript 소스코드의 경로.

## Events

### Event: 'loaded'

Electron 내부 초기화 스크립트의 로드가 완료되고, 웹 페이지나 메인 스크립트를 로드하기 시작할 때 발생하는 이벤트입니다.

이 이벤트는 preload 스크립트를 통해 node 통합이 꺼져있는 전역 스코프에 node의 전역 심볼들을 다시 추가할 때 사용할 수 있습니다: 

```javascript
// preload.js
var _setImmediate = setImmediate;
var _clearImmediate = clearImmediate;
process.once('loaded', function() {
  global.setImmediate = _setImmediate;
  global.clearImmediate = _clearImmediate;
});
```

## Methods

`process` 객체는 다음과 같은 메서드를 가지고 있습니다:

### `process.hang()`

현재 프로세스의 주 스레드를 중단시킵니다.

### `process.setFdLimit(maxDescriptors)` _OS X_ _Linux_

* `maxDescriptors` Integer

`maxDescriptors`에 file descriptor 소프트 리미트를 설정하거나 OS 하드 리미트를 설정합니다. 값은 현재 프로세스에 대해 낮은 값이어야 합니다.
