# backend-framework

## Spring framework
- 스프링 어플리케이션은 요청당 Thread 한개가 할당 됨. Thread pool이 수용할 수 있는 요청까지만 동시적으로 작업이 처리 되고, 넘게 되면 큐에서 대기 함
- Thread 생성 비용은 크기 때문에 미리 생성하여 재사용한다. tomcat 기본 사이즈는 200

## ~ASP.NET~ 
- ~스프링처럼 Thread pool을 이용해 처리 됨.~
- ~각 I/O호출은 스레드 내에서 동기로 처리 됨.~
- ~.NET Framework 4.5부터는 async/await패턴을 사용~
- > 사실상 뒤졌죠

## ASP.NET Core
- async/await패턴으로 request를 비동기로 처리.
- 각 request handler는 비동기로 지정될 수 있고 I/O 호출이 대기 할 수 있음
- 모든 request가 각각 스레드에서 실행되고 각 request별로 I/O작업은 비동기로 처리 됨.
> - 명확한 문서가 너무 안보이넴..
> - Node.js의 패러다임을 가져온거로 알고있는데 확실치 않음.

## Node.js
- 클라이언트의 Request가 들어오면 Event Queue에 입력이 되고 Event Loop가 동작하면서 event queue에 request가 있는지 확인함
- Event Loop는 Single-thread이고 Non-Blocking I/O로 동작함.
- 내부적으로 C++ 내부의 thread pool로 request를 보내서 처리 됨 (thread-pool에서는 blocking I/O로 동작). 
- 다시 Event Loop는 event queue를 돌면서 반복함.
- 내부 thread pool에서 작업이 끝나면 Event Loop에 response를 반환.



### 키워드
- Spring, ASP.NET Core 프로그램 실행 후 첫 request의 경우 객체 생성이 굉장히 느림 
- > Warm up 알아보셈
