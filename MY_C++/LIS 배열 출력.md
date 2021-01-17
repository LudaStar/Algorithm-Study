## 최대 증가 부분 수열 출력

다음과 같은 수열 LIS가 있다고 보자 S = {4,7,6,9,8,10}이 있을 때, 여기서 부분 수열 최대 길이는 4이다.

이 때 부분 수열을 출력해보라.

### 입력

테스트 케이스 T<10를 입력 하고 수열은 1000이하의 자연수 이다.

### 출력

최대 수열의 길이 및 수열을 출력

### 예제 입력

	6
	4 7 6 9 8 10
	10
	3 2 4 5 1 22 192 168 202 111 300

### 예제 출력 

	4 6 9 10
	3 4 5 22 192 202

### 문제 접근 

이 문제는 LIS문제에서 접근이 가능하다. 먼저 LIS문제를 풀어낙는 함수안에서 최고 길이 수열에 넣어줄 수들의 인덱스를 따로 저장해두는 배열을 만들면 된다.

### 코드
```
int n;
int cache[101], S[100], choices[101];

int lis4(int start) {
	int& ret = cache[start + 1];
	if (ret != -1) return ret;

	ret = 1;
	int bestNext = -1;
	for (int next = start + 1; next < n; ++next) {
		if (start == -1 || S[start] < S[next]) {
			int cand = lis4(next) + 1;
			if (cand > ret) {
				ret = cand;
				bestNext = next;

			}
		}
	}
	choices[start + 1] = bestNext;
	return ret;
}
```
위의 함수에서 보면 bestNext라는 변수를 통해 index를 기억하고 있다는것을 확인 할 수있다. 여기서 기억한 인덱스를 기반으로 다시 수열을 만드는 함수를 만들어 주면 간단하게 해결이 가능하다.
```
void reconstruct(int start, vector<int>& seq) {
	if (start != -1) seq.push_back(S[start]);
	int next = choices[start + 1];
	if (next != -1) reconstruct(next, seq);
}
```
여기서 보면 굳이 재귀함수로 구현하지 않아도 된다는 것을 알 수 있다. 하지만 메모리적으로 사용법을 늘리기 위해 재귀함수로 구현해 보았다.

### 전체 코드
	
```
#include <iostream>
#include <vector>

using namespace std;

int n;
int cache[101], S[100], choices[101];

int lis4(int start) {
	int& ret = cache[start + 1];
	if (ret != -1) return ret;

	ret = 1;
	int bestNext = -1;
	for (int next = start + 1; next < n; ++next) {
		if (start == -1 || S[start] < S[next]) {
			int cand = lis4(next) + 1;
			if (cand > ret) {
				ret = cand;
				bestNext = next;

			}
		}
	}
	choices[start + 1] = bestNext;
	return ret;
}

void reconstruct(int start, vector<int>& seq) {
	if (start != -1) seq.push_back(S[start]);
	int next = choices[start + 1];
	if (next != -1) reconstruct(next, seq);
}

int main() {
	
	cin >> n;

	for (int i = 0; i < n; i++) {
		cin >> S[i];
	}
	memset(cache, -1, sizeof(cache)); 
	lis4(0);
	vector<int> seq;
	reconstruct(0, seq);
	for (int i = 0; i < seq.size(); i++) {
		cout << seq[i]<< endl;
	}
	return 0;
}
```
