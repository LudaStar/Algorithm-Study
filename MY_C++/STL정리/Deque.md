# Deque container

deque 는 vector의 단점을 보완하기 위해 만들어진 container입니다.
deque도 vector와 마찬가지로 배열기반의 구조
vector의 단점으로는 새로운 원소가 추가 될 때 메모리 재할당 후 이전 원소를 복사하는 방식으로, 삽입시에 성능이 저하합니다.

deque는 이러한 vector의 단점을 보완하기위해 여러개의 메모리블록을 할당하고 하나의 블록처럼 여기는 기능을 제공한다.

deque는 메모리가 부족할 땜다 일정한 크기의 새로운 메모리 블록을 할당한다.

deque에서는 데이터 삽입과 삭제가 front와 back 에서 이루어 질 수 있음을 확인할 수 있습니다.

##Deque 사용법

```
#include<deque>		//deque의 모든 멤버함수를 포함하는 헤더
using namespace std;	//deque를 편안하게 사용하기 위한 namespace

deque<Data type>[변수이름]//deque의 선언방식

```

## Dequ의 생성자와 연산자
* deque<int> dq;
	* 비어있는 deque를 선언

* deque<int> dq(10);
	*defualt(0)으로 초기화된 10개의 원소를 가진 변수를 선언

* deque<int> dq(10,4);
	* 4의 값으로 초기화된 10개의 원소를 가진 변수 선언

* deque<int> dq(dq1)
	* dq에 dq1의 값을 복사해서 가져옵니다.

* 연산자 :
	* "==", "!=","<",">","<=",">=" 사용 가능

## Deque의 멤버 함수

* dq.assign(4,3)
	* 3의 값으로 4개의 원소를 할당

* dq.at(idx)
	* idx번째 원소를 참조
	* 유효범위를 확인하느로 dq[idx]로 확인하는 것보다 느림
	* dq[idx]로도 참조 가능

* dq.front()
	* 첫 번째 원소값을 반환

* dq.back()
	* 맨 마지막 원소값을 반환

* dq.clear()
	* deque의 원소를 전부 제거

* dq.push_front(3)
	* 3의 원소값을 맨 앞에 추가

* dq.pop_front()
	* 맨 앞의 원소를 반환 후 제거

* dq.push_back(6)
	* 6의 원소값을 맨 뒤에 추가

* dq.pop_back()
	* 맨 뒤의 원소를 반환 후 제거

* dq.begin();
	* 첫번째 원소를 가리킵니다. (iterator와 사용)
	* ex) deque<int>::iterator iter = dq.begin();

* dq.end();
	* 마지막의 "다음"을 가리킵니다. (iterator와 사용)
	* ex) deque<int>::iterator iter = dq.end();

* dq.rbegin();
	* reverse begin을 가리킵니다.
	* 맨 마지막원소를 마치 첫 번째 원소처럼 가리킵니다. (역으로)
	* iterator와 사용.
	* ex) deque<int>::iterator iter = dq.rbegin();

*  dq.rend();
	* reverse end 을 가리킵니다.
	* 맨 첫번째 원소의 "앞"을 마지막 원소의 "다음" 처럼 가리칩니다.
	* iterator와 사용.
	* ex) deque<int>::iterator iter = dq.rend();


* dq.resize(n);
	* 크기를 n 으로 변경합니다.
	* 만약 크기가 더 커졌을 경우 비어있는 원소를 default값인 0으로 초기화 합니다.

* dq.resize(n,2);
	* 크기를 n 으로 변경합니다.
	* 만약 크기가 더 커졌을 경우 빈 원소를 2로 초기화합니다.

* dq.size();
	* 원소의 개수를 리턴합니다.

* dq2.swap(dq1);
	* dq1과 dq2를 바꾸어 줍니다. (swap)


* dq.insert(1, 2, 3);
	* 1번째 위치에 2개의 3값을 삽입합니다.
	* 삽입 시에 앞뒤 원소의 개수를 판단하여 적은 쪽으로 미루어서 삽입합니다.
	* 만약 앞의 원소의 개수가 적을 경우, 앞쪽으로 블록을 만들어서 원소를 옮기고 삽입합니다.
	* 만약 뒤의 원소의 개수가 적을 경우, 뒤쪽으로 블록을 만들어서 원소를 옮기고 삽입합니다.
 
* dq.insert(3, 4);
	* 3번째 위치에 4의 값을 삽입합니다.
	* 삽입한 곳의 iterator를 반환합니다.

* dq.erase(iter);
	* iter가 가리키는 원소를 제거합니다.
	* 제거 한 후 앞 뒤의 원소의 개수를 판단하여 적은쪽의 원소를 당겨서 채웁니다.
	* 제거한 곳의 iterator 를 반환합니다.
* dq.empty()
	* dq가 비었으면 true를 반환합니다.


### 마치며

Vector와 매우 비슷한 구조이지만 시간이 더 빠르다는거에 다른 코드를 작성할 때 deque로 한번 해보도록 하겠다.
list와도 비슷하지만 다른구조에 무엇을 사용할지 시기에 맞춰 잘 써야겠다.