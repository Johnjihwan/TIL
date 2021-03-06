## Thread Pool(스레드 풀) 이란??

간단하다. 스레드를 미리 만들어 놓은 하나의 풀장...이라고 생각하면된다.  
군대를 빗대어보면, 전쟁이 나서 사방팔방에서 국지전을 펼친다고 생각해보자.  
그때그때 추가병력을 요청할때마다 당신이 지휘관이라면, 1명씩 지원을 보낼텐가???  

> 미리 100명의 군인들을 섭외해서 다중적으로 발생되는 국지전에 예비 병력을 즉각 국지전에 대응해야한다.  

<br>

그렇다면 이제 SW적으로 접근해보자.  
"스레드"라는 녀석은 생성될 때 컴퓨터 내부적으로 운영체제가 OS가 요청을 받아드려 메모리공간을 확보해주고, 그 메모리를 스레드에게 할당해준다.  
스레드는 동일한 메모리영역에서 생성되고 관리되지만, 생성/수거에 드는 비용을 무시할 수 없다.  

<br>

> 그렇기 때문에 요청이 들어올 때 마다 스레드를 생성하고 일을 다하면 수거하고 하는 작업은 프로그램 퍼포먼스에 지대한 영향을 줄 수 있다.  


## Thread Pool(스레드 풀)의 동작 원리
우리가 만든 어플리케이션에서 사용자로부터 들어온 요청을 작업큐에 넣고  

스레드풀은 작업큐에 들어온 Task일감을 미리 생성해놓은 Tread들에게 일감을 할당한다.  

일을 다 처리한 Thread들은 다시 어플리케이션에게 결과값을 리턴한다.  

<img src="../../img/Thread.png">


> 자바에서는 스레드풀을 생성하고 사용할 수 있도록 ``java.util.concurrent Package``에서 ``ExecutorService`` 인터페이스와 ``Executors`` 클래스를 제공하고 있다. ``Executors``의 다양한 정적 메서드를 통해 ``ExecutorService`` 구현객체를 만들어서 사용할 수 있으며, 그것이 바로 스레드 풀이다. 

## 그래서 Thread Pool 왜 사용해야해?

<ins>1. 프로그램 성능저하를 방지하기 위해</ins>

매번 발생되는 작업을 병렬처리하기 위해 스레드를 생성/수거 하는데 따른 부담은 프로그램 전체적인 퍼포먼스 저하시킨다.  

<ins>2. 다수의 사용자의 요청을 처리하기 위해 </ins>

서비스적인 측면으로 바라볼때,  
특히 대규모 프로젝트에서 중요하다. 다수의 사용자의 요청을 수용하고, 빠르게 처리하고 대응하기 위해 스레드풀을 사용한다.  


## Thread Pool 의 단점?

<ins> 1. 과유불급.. 너무 많이 만들어 놓았다가 메모리 낭비만 발생. </ins>

많은 병렬처리를 예상해서 1억개의 스레드를 만들어 놓았다고 생각해보자, 실제로 100개정도의 요청과 병렬처리를 했다. 그러면 나머지 스레드들은 아무일도 하지 않고 메모리만 차지하는 최악의 경우를 발생할 수 있다.

<ins>2. 노는 스레드가 발생한다. </ins>

1번과 비슷하지만 조금 다르다.  

예를 들어 A,B,C 스레드 3개가 있는데, 병렬적으로 일을 처리하는 과정에서 A,B,C 작업완료 소요시간이 다른 경우 스레드 유휴시간 즉 A스레드는 아직 일이 많아서 허덕이고 있는데, B,C는 일을 다하고 A가 열심히 일하는 것을 보고 놀고만 있는 유휴시간이 발생된다.  

자바에서는 이를 방지하기 위해 forkJoinPool 을 지원한다. 아래 링크를 통해 알아보자  