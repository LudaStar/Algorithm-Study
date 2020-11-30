# LIst

LIst는 C++의 자료구조중 하나인 linked list의 기능을 C++에서 개발해놓은 것입니다.

즉 linked list와 같은 기능을 한다고 알고있으면 됩니다.

## List Container

시퀀스 컨테이너의 일종으로 순서를 유지하는 구조입니다.

여기서 시퀀스 컨테이너란 : 데이터를 선형으로 저장하며, 특별한 제약이나 규칙이 없는 가장 일반적인 컨테이너입니다.

시퀀스 컨테이너에서는 삽입된 요소의 순서가 그대로 유지됩니다.

노드기반 컨테이너라고 하는데 하나의 클레스안에 front key값, back key값 그리고 다음 노드의 주소값을 가지고 있습니다.(이중 연결 리스트)

vector, deque와는 다르게 멤버 함수에서 정렬, 이어붙이기 가 있씁니다.
원소를 탐색할때, 임의접근 반복자(at,[])가 불가능하고 양방향 반족자(++,--)를 이용해 탐색을 합니다.

insert,erase를 이용해 삽입, 또는 삭제가 가능합니다(vector와 같은 기능)

## List의 사용법

list의 사용법은 간단합니다.

```
#include <list>
using namesapce std;

```
를 이용하면 간편하게 코드에 작성할 수 있습니다.

선언의 기본은 list<data Type>[변수이름];으로 vector와 구조가 같다고 보시면됩니다.

## List의 생성자와 연산자

```
list<int> it;		//비어있는 list 컨테이너를 생성합니다.
list<int> it(10);		//defualt(0)으로 초기화된 10개의 원소를 갖는 list를 생성합니다.
list<int> it(3,2);		//2값으로 초기화된 원소 3개를 생성합니다.
list<int> it2(it);		//list it을 it2에 복사합니다.
```

연산자는 ==,!=,<,>,<=,>= 등을 사용할 수 있습니다.

## list의 멤버함수

* it.assign(3,4)
	*4로 초기화된 3개의 원소를 할당한다.

* it.front()
	*맨 앞의 원소 값을 반환

* it.back()
	*맨 뒤의 원소를 반환

* it.begin()
	*맨 앞의 원소를 가리키는 iterator를 반환

*it.end()
	*맨 뒤의 원소를 가리키는 iterator를 반환

*it.rbegin()
	*뒤에서부터 원소를 순차적으로 접근할때 사용

*it.push_back(k)
	*뒤쪽으로 원소  k를 삽입

*it.pop_back()
	*맨뒤의 원소를 제거

*it.push_front(k)
	*앞쪽으로 원소 k를 삽입

*it.pop_front(k)
	*앞쪽의 원소를 제거

*it.insert(iter,k)
	*iter가 가르키는 위치에서 원소 k를 삽입
	*삽입한 원소를 가리키는 iterator를 반환한다.

*it.erase(iter)
	*iter가 가르키는 위치의 값을 제거
	*삭제한 원소의 다음 원소를 가리키는 iterator를 반환

*it.size()
	*원소의 갯수

*it.remove(k)
	*k와 같은 원소를 모두 제거

*it.remove_if(Predicate)
	*단항 조건자 predicate에 해당하는 원소를 모두 제거

*it.reverse()
	*원소들의 순차열을 뒤집는다.

*it.sort()
	*모든 원소를 default(오름차순)
	*sort의 파라미터로 이항조건자가 올 수 있습니다. 그때는 이항조건자의 기준으로 정렬

* it2.swap(it)
	*it2와 it을 swap합니다.

* it2.splice(iter2,it1)
	*it2에서 iter2이 가리키는 곳에 it1의 모든 원소를 잘라 붙입니다.
	*it2.splice(iter2,it1,iter1) : it2의 iter2가 가리키는 곳에 it1의 iter1이 가리키는 원소를 잘라 붙입니다.
	*it2.splice(iter2,it1,iter1_1,iter1_2) : it2의 iter2가 가리키는 곳에서 it1의(iter1_1,iter1_2)까지의 원소를 잘라 붙입니다.
	*[start,end] 까지는 start보다는 크거나 같고, end보다는 작은 원소를 뜻합니다.

* it.unique()
	*인접한(양옆의) 원소가 같으면 유일하게 만듭니다(하나빼고 삭제)

* it2.merge(it1)
	*it1을 it2내부로 합병 정렬합니다. 기준은 오름차순입니다.
	*두번째 파라미터로 이항 조건자가 올 수 있습니다. 그때는 그 기준으로 정렬합니다.
