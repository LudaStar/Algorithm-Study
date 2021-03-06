### 삼각형 위의 최대 경로

	6
	1  2
	3  7  4
	9  4  1  7
	2  7  5  9  4
위 형태와 같이 삼각형 모양으로 배치된 자연수들이 있습니다. 맨 위의 숫자에서 시작해, 한 번에 한 칸씩 아래로 내려가 맨 아래 줄로 내려가는 경로를 만들려고 합니다. 경로는 아래 줄로 내려갈 때마다 바로 아래 숫자, 혹은 오른쪽 아래 숫자로 내려갈 수 있습니다. 이 때 모든 경로 중 포함된 숫자의 최대 합을 찾는 프로그램을 작성하세요.

### 입력

입력의 첫 줄에는 테스트 케이스의 수 C(C <= 50)가 주어집니다. 각 테스트 케이스의 첫 줄에는 삼각형의 크기 n(2 <= n <= 100)이 주어지고, 그 후 n줄에는 각 1개~n개의 숫자로 삼각형 각 가로줄에 있는 숫자가 왼쪽부터 주어집니다. 각 숫자는 1 이상 100000 이하의 자연수입니다.

### 출력

각 테스트 케이스 마다 한 줄에 최대 경로의 숫자 합을 출력합니다.

### 예제 입력

	2
	5
	6
	1  2
	3  7  4
	9  4  1  7
	2  7  5  9  4
	5
	1 
	2 4
	8 16 8
	32 64 32 64
	128 256 128 256 128

### 예제 출력
	28
	341

### 문제 접근 

분할 정복에서 배운 메모리제이션을 통해 계획할 수 있었다. 또한 이부분은 매우 간단하게 구현할 수 있ㅇㅆ다.

먼저 무조건 시작은 0,0부터 시작해서 아래로 1칸 아래 오른쪽으로 한칸만 움직일 수 있다. 이때 (y,x)가 움직일 수 있는 좌표는(y+1,x),(y+1,x+1)의 좌표 두개뿐이므로 둘 중에 가장 큰 값을 찾아서 이전 층에서나온 값중 가장 큰값에 더해주면 된다.

수식으로 나타내면 max((y+1,x),(y+1,x+1))+(이전에 계산된 (y,x)좌표값)이 된다 이 수식을 그대로 코드에 구현하면

```
int n;//삼각형의 높이
int cache2[100][100];//이미 계산된 수치를 저장할 값

int path2(int y, int x) {
	if (y == n - 1) return triangle[y][x];//기저사례 : 삼각형의 맨 아래층에 도달하면 triangle값을 반환
	int& ret = cache2[y][x];
	if (ret != -1) return ret;
	return ret = max(path2(y + 1, x), path2(y + 1, x + 1)) + triangle[y][x];// 수식 적용
}

### LIS

수열 A가 주어졌을 때, 가장 긴 증가하는 부분 수열을 구하는 프로그램을 작성하시오.

예를 들어, 수열 A = {10, 20, 10, 30, 20, 50} 인 경우에 가장 긴 증가하는 부분 수열은 A = {10, 20, 10, 30, 20, 50} 이고, 길이는 4이다.


### 입력

첫째 줄에 수열 A의 크기 N (1 ≤ N ≤ 1,000)이 주어진다.

둘째 줄에는 수열 A를 이루고 있는 Ai가 주어진다. (1 ≤ Ai ≤ 1,000)

### 출력

첫째 줄에 수열 A의 가장 긴 증가하는 부분 수열의 길이를 출력한다.

### 문제 해결

이 부분은 매우 단순하다. 그저 앞 부분부터 수의 값을 비교해 큰 수를 출력하게 되면 간단하다.

코드는 다음과 같다

```
int lis(const vector<int>& A) {
	if (A.empty) return 0;
	int ret = 0;
	for (int i = 0; i < A.size(); i++) {
		vector<int> B;
		for (int j = i + 1; j < A.size(); j++) {
			if (A[i] < A[j])
				B.push_back(A[j]);
			ret = max(ret, 1 + lis(B));
		}
	}
	return ret;
}
```

위의 코드에서는 단순히 뒤의 수가 앞의 수 보다 큰지 작은지만 확인해 보면된다. 하지만 이 답은 최적화가 전혀 되어있지않다. for문도 2개를 사용해 시간 복잡도도 O(n<sup>3</sup>)을 나타내고 있기 때문이다. 이 문제를 좀 더 빠르게 계산 할 방법을 찾다가. 마찬가지로 메모이제이션이 매우 적합하다는 생각을 하였다..

그 이유는 여러개를 한번에 검사하는데 미리 검사해둔 값이 있다면 더 빠르게 해결 할 수 있을 것 같았기 때문이다.

코드는 다음과 같다

```
int n;
int S[100];
int cache[101];

int lis2(int start) {
	int& ret = cache[start];
	if (ret != -1) return ret;

	ret = 1;
	for (int i = start + 1; i < n; i++) {
		if (S[start] < S[i]) {
			ret = max(ret, lis2(i) + 1);
		}
	}
	return ret;
}
```
이 때 S는 전체 수열의 순서, cache는 메모이제이션 할때 저장된 값을 나타낸다.

식에서 보다시피 이미 결정된 값은 반환하고 무조건 수열의 길이는 1 이상이므로 1로 설정한다.

이렇게 되면 for문을 하나만 수행 함으로써 시간복잡도가 O(n<sup>2</suo>)이 되는 것을 알 수있었다.

근데 여기서 조금 더 빠르게 확인하는 방법이 있었다.

위의 식은 보다시피 무조건 그 다음 수를 확인하고 검사를 한 후에 넘어가므로 시간이 꾀 걸린다는 것을 알 수 있었다.

그렇다면 시작 위치를 다음에 넣은 값으로 고정하게 된다면 조금더 빨라진다는 것을 알 수 있을것이다.

코드는 다음과 같다.

```
int lis3(int start) {
	int& ret = cache[start];
	if (ret != -1) return ret;
	ret = 1;
	for (int i = start + 1; i < n; i++) {
		if (start == -1 || S[start] < S[i]) {
			ret = max(ret, lis3(i) + 1);
		}
	}
	return ret;
}
```

위 코드를 확인해보면 start위치가 -1의 값을 가지고 있지 않다면 건너 뛰는 형식을 볼 수 있는데 이렇게 만들면 검사 단계를 한번 건너 뛸 수 있으므로 시간복잡도가 줄어드는 것을 확인 할 수 있다.