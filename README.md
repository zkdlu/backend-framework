# backend-framework

## Spring framework
- 스프링 어플리케이션은 요청당 Thread 한개가 할당 됨. Thread pool이 수용할 수 있는 요청까지만 동시적으로 작업이 처리 되고, 넘게 되면 큐에서 대기 함
- Thread 생성 비용은 크기 때문에 미리 생성하여 재사용한다. tomcat 기본 사이즈는 200

## ASP.NET Core
