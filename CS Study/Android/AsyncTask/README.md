# AsyncTask

## 안드로이드 Main thread(UI thread)

안드로이드 어플리케이션이 실행되면 안드로이드 시스템은 하나의 실행 스레드로 어플리케이션의 프로세스를 실행합니다.

어플리케이션의 구성요소가 생성될 때 `별도의 스레드가 생성되는 것은 아니며` `앞서 말한 하나의 실행 스레드에서 실행`됩니다. 이 스레드를 Main thread라고 합니다.

안드로이드 시스템에 의해 생성된 이 Main thread는 `화면 구성에 관한 역할을 담당`합니다.

예를 들어 Button, CheckBox, TextView 등의 UI도구 키트 구성요소를 생성 및 조작하였을 때 상호작용하는 스레드가 Main thread입니다.

그래서 반응성 좋은 어플리케이션을 만드려면 시간이 오래 걸리는 작업은 main thread에 구현하지 않고 별도의 thread에서 동작하도록 구현하면 됩니다.

만약 개발자가 데이터를 다운로드하는 작업을 Main Thread(UI thread)에 구현하였다면 다운로드가 완료될때까지 화면은 멈추어 있는것 처럼 보일것입니다.

이러한 점들이 어플리케이션의 반응성을 떨어지게 만들고 사용자는 답답함을 느끼게 됩니다.



**UI thread가 아닌 스레드에서는 UI 구성요소를 조작하는 것은 허용되지 않습니다.**

UI 입장에서 봤을때 UI 동작은 단일 스레드로 동작하는 구조. 따라서 UI thread에서 시간이 오래 걸리는 작업을 수행하는 것은 그 작업이 수행되는 동안 UI업데이트가 지연 되고 있다는 것을 의미.



## AsyncTask 개념

앱이 실행되며 안드로이드 시스템은 메인 스레드를 생성합니다. 이 스레드는 안드로이드 UI 툴킷에 접근합니다. 사용자의 입력을 기다리거나 디바이스 화면에 그리는 작업등을 다룹니다. 그래서 UI 스레드 라고 부릅니다.

앱의 모든 컴포넌트(Activity, Service, Content Provider. Broadcastreceiver 등)들은 같은 스레드 내에서 실행됩니다. 필요에 따라 추가 스레드를 생성할 수 있습니다. UI 스레드가 thread-safe하지 않기 때문에 스레드 사용시 다음 2가지를 지켜야 합니다. 

* UI 스레드가 블록되지 않도록 해야합니다.
* UI 스레드 외에 다른 스레드에서 UI 컴포넌트 접근을 하면 안됩니다.

위에서 UI 스레드는 블록되면 안된다 했는데 안드로이드는 single thread model모델을 따르기 때문에 문제가 생깁니다. 오랜 시간이 걸리는 작업을 UI 스레드에서 수행한다면 작업이 완료 될때 까지 UI스레드가 대기해야 하므로 UI는 먹통이 됩니다. 

UI 반응성 향상과 처리시간이 오래 걸리는 작업 처리를 같이 해결하기 위해선 별도의 스레드가 필요합니다.  예를들어 네트워크 관련 처리는 메인 스레드에서 수행하는게 금지되어 있습니다.

이문제를 해결하기 위해 안드로이드에서는 Handler, Runnable, AsyncTask등을 제공합니다. AsyncTask는 메인 스레드에서 생성후 실행되며, 메인 스레드에서 처리시간이 오래 걸리는 작업을 백그라운드 스레드로 넘기고 계속 메인 스레드 작업을 진행 하기위해 사용됩니다. AsyncTask를 실행시켜놓고 메인스레드는 다음 작업을 바로 할 수 있습니다.  



## Reference

* 안드로이드 Main thread : https://codetravel.tistory.com/9
* AsyncTask : https://webnautes.tistory.com/1082