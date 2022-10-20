<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcZp8KQ%2FbtrOZIDACZJ%2FOmcxZK64bn3Lvr7QhnPcS0%2Fimg.png" />

## Array

### 특징
+ Array은 입력된 데이터들이 메모리 공간에서 연속적으로 저장되어 있는 자료구조이다.
+ 메모리상에서 연속적으로 저장되어 있는 특징을 갖기때문에, index를 통한 접근이 용이하다.
+ index만 알고 있다면 시간 복잡도 O(1)만에 해당 원소로 접근할 수 있다.


### 조회
+ 각 데이터의 index를 가지고 있고 무작위 접근이 가능하기 때문에, index로 각 데이터에 직접 접근이 가능하다


### 데이터 삽입과 삭제
+ 데이터의 삽입과 삭제 시 그만큼 index를 맞춰주어야 한다
+ 예시 : 5개의 데이터가 있을 때 맨 앞을 삭제했다면 뒤쪽의 나머지 4개는 앞으로 한 칸씩 이동해야된다
+ 이로 인해 삽입과 삭제가 많다면 Array는 비효율적이다


## Linked List

### 특징
+ LinkedList는 여러 개의 노드들이 순차적으로 연결된 형태를 갖는 자료구조이며, 첫번째 노드를 헤드(Head), 마지막 노드를 테일(Tail) 이라고 한다.
+ 배열과는 다르게 메모리를 연속적으로 사용하지 않는다.
+ 각 데이터들 앞, 뒤 데이터의 주소값을 가지고 있다
+ index가 존재하지 않는다


### 조회

+ 순차적 접근이기 때문에 조회의 속도가 느리다

### 데이터 삽입과 삭제

+ 데이터의 삽입과 삭제 시 앞, 뒤의 데이터에 주소값만 변경해주면된다
+ 예시 : 5개의 데이터가 있을 때 두 번째 데이터를 삭제 했다면 1번 데이터에 3번의 주소값을 주고 3번 데이터에 1번 데이터의 주소값을 넣어주면된다
+ 이로 인해 삽입과 삭제가 많다면 Array에 비해 효율적이다
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyCODF%2FbtrO0o5GX5p%2FgJQY0mTJTGTYEBGjR2I5z1%2Fimg.png" />

+ 소량의 데이터를 바탕으로 측정하면 큰 차이는 없다
+ 위의 퍼포먼스 테스트처럼 조회 시에는 Array가 우위에 있고
+ 삽입/삭제 시에는 LinkedList가 우위에 있다 (특히 삭제)
1. 삽입/삭제 시에 처음 혹은 마지막부터 순차적으로 데이터를 삭제한다고 하면 Array도 충분히 빠르다
2. 하지만 중간부터(비순차적)으로 삽입/삭제하는 경우에는 LinkedList가 빠르다

## 📖 Array vs LinkedList

<img width="70%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdU2wrm%2FbtrOYwqnSB6%2F8FcyWtBWS1UrIQDekGlvBk%2Fimg.png" />

 

### 💡 답변
**Array vs LinkedList**
+ 정적인 데이터를 활용하면서 조회가 빈번하다면 index를 바탕으로 데이터에 접근이 가능한 array가 효율적이며 동적으로 추가/삭제 요청이 많다면 LinkedList가 효율적입니다.
+ 예시로 중간에 있는 한개의 데이터를 추가/삭제를 하게 된다면 array는 해당 index뒤의 데이터들을 한 칸씩 앞당겨야 되지만 LinkedList는 추가/삭제된 데이터의
앞, 뒤 데이터의 주소값을 해당 데이터로 바꿔주기만 하면됩니다.
