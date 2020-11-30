# STL
## Standard Template Library

	c++에서 제공하는 표준 라이브러리로, 자료구조, 알고리즘 등을 편하게 사용할 수 있도록 해준다.

# Containers
## 객체(데이터)를 저장하는 자료 구조

1. 순차 컨테이너 (Sequence Container)
	자료를 순서대로 저장하여, 자료가 적은 경우 유리한 구조
	vector, list, deque, arrays, forward_list

	1. vector : 동적 배열
	2. array : 배열
	3. list : 양방향 리스트
	4. forward_list : 단방향 리스트
	5. deque : 양방향 큐

2. 연관 컨테이너 (Associative Container)
	빠르게 검색할 수 있는 노드 기반 이진 트리 구조
	set, multiset,map, multimap

	1. set : 정렬된 유일 key 집합(set)
	2. map : 정렬된 유일 key와 value의 집합(map) - 별명은 dictionary이다.
	3. multiset : 정렬된 중복 허용 key 집합
	4. multimap : 정렬된 중복허용 key와 value의 집합

3. 비정렬 연관 컨테이너
	1. unordered set : 유일 key 해시
	2. unordered map : 유일 key와 value의 해시
	3. unorderd multiset : 중복허용 key 해시
	4. unorderd multimap : 중복허용 key와 value의 해시

4. 그외. 
	1. stack : 선입후출, 먼저 넣은값은 뒤의 값들이 나가지 전에 빠져나가지 못한다.
	2. queue : 선입선출, 먼저 넣은 값이 제일 먼저 나오고순서대로 쌓임
	3. priority_queue :  우선순위큐 

각각의 사용법은 차차 추가하도록 하겠다.