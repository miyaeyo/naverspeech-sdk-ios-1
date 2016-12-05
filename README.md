# **Naverspeech SDK for iOS**

> 본 [저장소](https://github.com/naver/naverspeech-sdk-ios) 는 iOS용 네이버 음성인식 라이브러리 및 예제 프로젝트를 포함하고 있습니다.

자세한 내용은 [네이버개발자 음성인식 API 명세](https://developers.naver.com/docs/labs/vrecog) 및 [iOS API Document](http://naver.github.io/naverspeech-sdk-ios/) 를 참고하세요.

사용법
==
**1.** 제공된 sample app의 repository를 clone하거나 zip으로 내려받아 framework폴더 안의 `NaverSpeech.framework`를 target app의 `Embedded Binaries`에 추가 시켜줍니다. 음성인식 framework는 fat binary 형태로 제공되고 있습니다. 따라서 `Build Settings`의 `Enable Bitcode` 옵션을 사용할 수 없으니 `No`로 변경해 주어야 합니다. 

**2.** iOS Bundle Identifier 확인 및 설정
* Bundle Identifier: Target app의 `Bundle Identifier`를  ['내 애플리케이션'](https://developers.naver.com/appinfo)의 '설정' 탭에 있는 'iOS Bundle ID'와 일치시켜주세요.
* 권한 설정: 음성인식을 위해선 마이크를 통해 녹음해야 하고 녹음된 데이터를 서버로 전송해야 합니다. 따라서, 아래처럼 Info.plist에 마이크 사용과 관련한 property key값을 추가 해야 합니다.

```xml
<key>NSMicrophoneUsageDescription</key>
<string></string>
```
**3.** 네이버 OpenAPI는  iOS 버전 8.0 이상을 지원합니다. `Deployment Target` 값을 확인해주세요.

**4.** NSKRecognizerDelegate protocol을 구현해 음성인식 이벤트 발생에 해당하는 처리를 할 수 있습니다. 

```objective-c
@protocol NSKRecognizerDelegate <NSObject>

@optional
- (void)recognizerDidEnterReady:(NSKRecognizer *)aRecognizer;
- (void)recognizerDidDetectEndPoint:(NSKRecognizer *)aRecognizer;
- (void)recognizerDidEnterInactive:(NSKRecognizer *)aRecognizer;
- (void)recognizer:(NSKRecognizer *)aRecognizer didRecordSpeechData:(NSData *)aSpeechData;
- (void)recognizer:(NSKRecognizer *)aRecognizer didSelectEndPointDetectType:(NSNumber *)aEPDType;
- (void)recognizer:(NSKRecognizer *)aRecognizer didReceivePartialResult:(NSString *)aResult;
- (void)recognizer:(NSKRecognizer *)aRecognizer didReceiveError:(NSError *)aError;

@required
- (void)recognizer:(NSKRecognizer *)aRecognizer didReceiveResult:(NSKRecognizedResult *)aResult;

@end

```

License
==

See [LICENSE](https://github.com/naver/naverspeech-sdk-ios/blob/master/LICENSE) for full license text.

Copyright 2016 Naver Corp.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

