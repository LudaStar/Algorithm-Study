# STACK

스텍은 마지막에 들어온 것이 먼저나가는 LIFO(Last In First Out) 구조를 가진 자료구조이다.  
일상 생활과 비교를 한다면 책을 쌓은다음 책을 꺼낼 때 위에서 부터 내려가는 것을 볼 수 있다.

stack은 특이한게 잇는데 container 가 아닌 container adapter 인데 기존의 컨테이너에서 인터페이스를 제한하여 만든것이다.

## stack의 생성자 및 초기화

stack의 생성자는
#include 에 포함된다.

```
#include <stack>

stack<in> st;//비어있는 stack을 생성한다.

stack<int> st({1,2,3,4,5}); 	// 1 2 3 4 5로 초기화 된 stack을 생성

deque<int> d1(5,10)
stack<int> st(d1) 		// deque를 복사하여 stack을 생성
			//위의 식이 성립하는 이유는 밑에서 다시 설명하겠다.

stack<int,vector<int>> st;	// first parameter : type of elemet the stack holds
			//second parameter : the container type used to implement the stack
```

## stack의 함수

* iterator 부분이 존재하지 않는다. 

* st.empty()
	* 비어있으면 true 값이 있으면 false을 반환

* st.size()
	* 원소 수를 반환

* st.top()
	* 맨 마지막 원소를 리턴

* s.push(n)
	* 맨 마지막에 원소를 추가

* s.pop() 
	* 맨 마지막의 원소를 삭제

# Deque

deque 컨테이너는 vector 컨테이너와 기능과 동작이 비슷한데 vector의 단점을 몇ㄱ지 보완하는 특징이있다.

## Deque의 생성자

deque는 #include에 포함되어있는 헤더이다.

```
#include <deque>  

deque<int> dq		//deque의 빈 컨테이너
deque<int> dq(n) 		//defualt로 초기화된 n개의 원소를 생성
deque<int> dq(n,x)	//x로 초기화된 n개의 원소를 생성
deque<int> dq(dq1)	//dq1의 원소를 dq로 복사
deque<int> dq(iterater a,iterater b)//반복자 구간 으로 초기화된 원소를 갖는다.

```
## Deque의 함수

* dq.assing(n,x)
	* dq에 x값으로 n개의 원소를 할당

* dq.assign(b,e)
	* dq에 반복자구간 (b,e)로 할당한다.

* dq.at(i)
	* dq의 i번째 원소를 반환

* dq.back()
	* dq의 마지막 원소를 반환

* dq.begin()
	* dq의 첫 원소를 가리키는 반복자

* dq.clear()
	* dq의 모든 원소를 삭제

* dq.empty()
	* dq값이 비어잇으면 true, 값이 있으면 false이다.

* dq.end()
	* dq의 마지막을 가리키는 반복자

* dq.erase(i)
	* dq의 i번째 원소를 제거하고 그 다음 원소를 반환

* dq.erase(b,e)
	* dq의 (b,e)구간의 원소를 삭제

* dq.front()
	* dq의 첫번째 원소를 반환

* dq.insert(p,x)
	* p위치에 x의 값을 삽입

* dq.insert(p,n,x)
	* p의 위치에 n개의 x값을 삽입

* dq.insert(p,b,e)
	* p의 위치에 (b,e) 반복자 구간의 원소를 삽입

* dq.max_size()
	* dq가 담을 수 있는 최대 원소의 갯수

* dq.pop_back()
	* dq의 맨뒤의 원소를 삭제

* dq.pop_front()
	* dq의 맨 앞 원소를 삭제

* dq.push_back(i)
	* dq의 맨 마지막에 원소 i를 삽입

* dq.push_front(i)
	* dq의 맨 앞에 원소 i를 삽입

* dq.rbegin()
	* dq의 역 순차열 원소의 첫 번째를 가리키는 반복자

* dq.rend()
	* dq의 역 순차열 원소의 마지막을 가리킨는 반복자

* dq.resize(n)
	* dq의 크기를 n으로 변경하고 확장되는 공간의 값을 기본값으로 초기화

* dq.resize(n,x)
	* dq의 크기를 n으로 변경하고 확장되는 공간의 값을 x로 초기화

* dq.size()
	* dq의 크기를 반환

* dq.swap(dq1)
	* dq1과 dq의 원소를 바꾼다.

## deque의 연산자

==,!=,<,>,[]로 계산식에 사용이 가능하다.

멤버 형식으로는

* allocator_type
	* 메모리 관리자 형식

* const_iterator
	* const 반복자 형식

* const_pointer
	* const value_type *형식

* const_reference
	* const value_type& 형식

* const_reverse_iterator
	* const 역 반복자 형식

* iterator
	* 반복자 형식

* pointer
	* value_type *형식

* reference
	* value_type & 형식
