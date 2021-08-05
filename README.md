# Activity

## LifeCycle

1. onCreate
2. onStart
3. onResume
4. onPause
5. onStop

  - CPU를 비교적 많이 소모하는 종료 작업

6. onRestart
7. onDestory
8. onSaveInstanceState 

  - '상태보존 하지 않는 경우'에 발생 
  - onDestory() 이전에 발생

9. onRestoreInstanceState 

  - 보통 onStart() 이후 호출 onCreate() 에서 savedInstanceState null check와 함께 활용하는데 onRestoreInstanceState 함수 블록에서 활용 가능
  - onStart() 이후 호출

#### A -> B 액티비티 이동 케이스

A: onCreate -> onStart -> onResume
A: onPause
B: onCreate -> onStart -> onResume
A: onStop -> onSaveInstanceState

### B -> A 백스택에 의한 종료

B: onPause
A: onRestart -> onStart -> onResume
B: onStop -> onDestroy



### 화면 회전시 Activity 라이프사이클

- onPause
- onStop
- onSaveInstanceState
- onDestroy
- onCreate
- onStart
- onRestoreInstanceState
- onResume

### Activity 상태보존 하는경우 or 하지 않는 경우

  #### 하지 않는 경우

    - finish() 메서드를 호출 혹은 뒤로 버튼 누르기
    - 활동에서 상위 항목으로 이동
    - 개요(최근 사용) 화면에서 활동 스와이프
    - 설정 화면에서 앱 종료

  #### 하는 경우

    - 화면 회전과 같은 구성 변경
    - 메모리 부족

### 상태보존

 - 원시 데이터 유형이거나 간단한 객체는 onSaveInstanceState()를 사용
 - 하지만 onSaveInstanceState() 직렬/역직렬화 비용이 발생하기 때문에 대부분의 경우 ViewModel과 onSaveInstanceState() 2

### 그 외 케이스 LifeCycle

 - Permissoin Dialog 팝업 시 onPause -> onResume


## Fragment

### Activity 생성시 Fragment과의 라이프사이클

1. onCreate

 - Fragment onAttach
 - Fragment onCreate
 - Fragment onCreateView
 - Fragment onViewCreated
 - Fragment onActivityCreated
 - Fragment onStart

2. onStart
3. onResume

 - Fragment onResume 



### Activity 파괴 시 Fragment와의 라이프사이클

1. onStop
   - onDestroyView
   - onDestroy
   - onDetach
2. onDestroy



### Fragment 화면 회전에 대한 케이스

1. 화면 회전

 - Fragment onPause

2. onPause

 - Fragment onStop

3. onStop

 - Fragment onDestroyView
 - Fragment onDestroy
 - Fragment onDetach

4. onDestroy

 - Fragment onAttach
 - Fragment onCreate

5. onCreate

 - Fragment onCreateView
 - Fragment onViewCreated
 - Fragment onActivityCrea
 - Fragment onStart

6. onStart
7. onResume

 - Fragment onResume

## Service

### Service 사용시 주의 점

 - Service를 시작할 때에는 명시적 인텐트만 사용, 인텐트 필터는 선언하지 않음(보안). 
 - Android 5.0(API 레벨 21)부터 시스템은 개발자가 암시적 인텐트로 bindService()를 호출하면 예외를 발생

### Service 생명주기

### 개발하면서 찾은 점

 - Service 클래스는 1개 인스턴스만 허용가능 여러개의 서비스를 돌리고 싶을 떄는 클래스를 더 만들어야 할듯
 - Service와 Activity는 BroadCast를 통해 통신 가능
 - 동작중인 서비스를 체크하는 방법은 ActivityManager의 RunningService를 재귀해서 하는 방법 말곤 없는듯

- onCreate()
- onDestory()
- onStartCommand()
  - START_NOT_STICKY: 다시 만들지 않음
  - START_STICKY: 서비스를 다시 만들지만 onStartCommand로 다시 전달하지 않음
  - START_REDELIVER_INTENT: 마지막 Intent를 onStartCommand의 인자로 다시 전달(파일 다운로드 서비스)
- onBind()



### Foreground Service

- Service 내의 startForeground() 
- Service 내의 stopForeground 를 호출해도 Service는 종료되지 않고 Background Service 로만 전환



### 버전 이슈

9.0 (API 28) 부터는 uses-permission에 권한을 명시해야한다

### Foreground 에서 명시해주어야 할 리스트

```
android:foregroundServiceType=
["connectedDevice" | 
"dataSync" |
"location" | 
"camera" | 
"microphone" | 
"mediaPlayback" | 
"mediaProjection" |
"phoneCall"]
```xxxxxxxxxx android:foregroundServiceType=["connectedDevice" | "dataSync" |"location" | "camera" | "microphone" | "mediaPlayback" | "mediaProjection" |"phoneCall"]
```xxxxxxxxxx android:foregroundServiceType=["connectedDevice" | "dataSync" |"location" | "camera" | "microphone" | "mediaPlayback" | "mediaProjection" |"phoneCall"]```xxxxxxxxxx android:foregroundServiceType=["connectedDevice" | "dataSync" |"location" | "camera" | "microphone" | "mediaPlayback" | "mediaProjection" |"phoneCall"]
```
