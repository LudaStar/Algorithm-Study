### 합친 LIS 문제

어떤 수열에서 0개 이상의 숫자를 지운 결과를 원 수열의 부분 수열이라고 부릅니다. 예를 들어 '4 7 6'은 '4 3 7 6 9'의 부분 수열입니다. 중복된 숫자가 없고 오름 차순으로 정렬되어 있는 부분 수열들을 가리켜 증가 부분 수열이라고 부르지요. 예를 들어 '3 6 9'는 앞의 수열의 증가 부분 수열입니다.

두 개의 정수 수열 A 와 B 에서 각각 증가 부분 수열을 얻은 뒤 이들을 크기 순서대로 합친 것을 합친 증가 부분 수열이라고 부르기로 합시다. 이 중 가장 긴 수열을 합친 LIS(JLIS, Joined Longest Increasing Subsequence)이라고 부릅시다. 예를 들어 '1 3 4 7 9' 은 '1 9 4' 와 '3 4 7' 의 JLIS입니다. '1 9' 와 '3 4 7' 을 합쳐 '1 3 4 7 9'를 얻을 수 있기 때문이지요.

A 와 B 가 주어질 때, JLIS의 길이를 계산하는 프로그램을 작성하세요.

### 입력

입력의 첫 줄에는 테스트 케이스의 수 c ( 1 <= c <= 50 ) 가 주어집니다. 각 테스트 케이스의 첫 줄에는 A 와 B 의 길이 n 과 m 이 주어집니다 (1 <= n,m <= 100). 다음 줄에는 n 개의 정수로 A 의 원소들이, 그 다음 줄에는 m 개의 정수로 B 의 원소들이 주어집니다. 모든 원소들은 32비트 부호 있는 정수에 저장할 수 있습니다.

### 출력

각 테스트 케이스마다 한 줄ㅇ에, JLIS의 길이를 출력합니다.

### 입력 예제

3
3 3
1 2 4
3 4 7
3 3
1 2 3
4 5 6
5 3
10 20 30 1 2
10 20 30

### 출력 예제

5
6
5

### 문제 해결 방법

합친 LIS문제는 앞서 풀었던 LIS문제의 응용 버전이다. 하지만 두개의 수열을 합친 후 활용해야 하므로 계산적으로는 조금 달라진다.

특히 입력값이 10,000이상이므로 32비트 정수형으로는 계산이 불가능 하므로 64비트 정수형으로 계산해야 한다.

똑같은 메모이제이션을 반복하나, 각각의 수열 A,B는 다르다는 것을 유의하면서 진행한다.

### 코드

```
const long long NEGINF = numeric_limits<long long>::min();
int n, m, A[100], B[100];
int cache[101][101];


int jlis(int indexA, int indexB) {
	int& ret = cache[indexA + 1][indexB + 1];
	if (ret != -1) return ret;

	ret = 2;
	long long a = (indexA == -1 ? NEGINF : A[indexA]);
	long long b = (indexB == -1 ? NEGINF : B[indexB]);
	long long maxElement = max(a, b);

	for (int nextA = indexA + 1; nextA < n; nextA++) {
		if (maxElement < A[nextA])
			ret = max(ret, jlis(nextA, indexB)+1);
	}
	for (int nextB = indexB + 1; nextB < n; nextB++) {
		if (maxElement < B[nextB])
			ret = max(ret, jlis(indexA+1, nextB)+1);
	}
	return ret;
}
```
위의 코드를 보면 알 수 있듯이 A와 B의 작은 수들을 고른 후 그 중 큰수를 MAXELEMENT로 사용한 후 두 수를 비교하는 방식으로 진행한다. 이 부분은 LIS에서 구현했던 부분이므로 다시한번 확인하기 바란다.
