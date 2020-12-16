# POLY

정사각형들의 변들을 서로 완전하게 붙여 만든 도형들을 폴리오미노 (Polyomino)라고 부른다. N개의 정사각형을 붙여 하나의 폴리오미노를 만들 때 수직방향-단조(vertically monotone)인 폴리오미노를 만들 수 있는 가짓수가 몇 개나 되는지 세고 싶다. 다각형이 수직방향-단조라는 것은, 어떤 수평선도 이 다각형을 두 번 이상 교차하지 않을 때를 말한다.

<img src = "http://jungol.co.kr/data/editor/1512/e3050b66a1b29a01767400d7560a4131_1449735654_8688.jpg">
 

예를 들어 아래 그림의 (a)는 맨 오른쪽 아래 정사각형이 다른 정사각형과 변을 완전히 맞대고 있지 않기 때문에 폴리오미노가 아니며 (b)는 두 개의 다각형이 꼭지점만을 맞대고 있으므로 폴리오미노가 아니다. (c)는 폴리오미노이지만 점선과 같은 수평선에 대해 두 번 교차하므로 수직 방향-단조가 아니다. (d) (e) (f)는 모두 7개의 정사각형으로 만들어진 수직방향-단조 폴리오미노이다.

## 입력

입력의 첫 번째 줄에는 테스트 케이스의 수 T(1≤T≤50) 가 주어진다. 각 테스트 케이스는 각 줄에 하나의 정수 N(1≤N≤100)이 주어진다.

## 출력

각 테스트 케이스마다 N개의 정사각형으로 만들 수 있는 수직방향-단조 폴리오미노의 수를 한 줄에 하나씩 출력한다. 단 폴리오미노의 수가 10,000,000 (1천만) 보다 클 경우 1천만으로 나눈 나머지를 출력한다.

## 입력 예제

	5
	1
	4
	2
	3
	5

## 출력 예제

	1
	19
	2
	6
	61

### 문제 접근

이 문제는 정 사각형의 네 변에 접한다 라는 생각을 가지고 가야한다. 즉 1x1의 정사각형이 2개가 있다면 총 폴리오미노의 갯수는 2개 뿐이다. 왜냐하면 왼쪽에 두나 오른쪽에 두나 같은 모양의 폴리오미노 이기 때문이다.

그럼 문제를 어떻게 풀어야 할까? 그 답은 폴리오미노를 한개부터 네개까지 만들어보면 알 수 있다. 한 개로 만들 수 있는 폴리오미노의 갯수는 1개이다. 2개로 만들 수 있는 폴리오미노의 갯수는 2개이다. 3개로 만들 수 있는 폴리오미노의 갯수는 6개 이다. 4개로 만들 수 있는 폴리오 미노의 갯수는 19개 이다.

여기서 직접 몰리오미노를 그려본다면 정해야 될것이 세 가지가 있다는 것을 알 수 있다.

1. 첫번째 줄에 몇개의 사각형을 그릴 것인가?(왼쪽과 오른쪽에 어디에 두든 똑같은 모양의 폴리오미노)

2. n개의 사각형을 포함하면서 첫 줄에 몇개의 사각형을 포함하는 폴리오노미오의 개 수

3. 폴리오미노는 우 하 에만 붙을 수 있다.

첫 번째는 쉽게 생각하면 재귀함수를 사용하기 좋다 첫번째 줄의 사각형 갯수를 구하고 두번째 줄의 사각형의 갯수를정하면

폴리오미노의 갯수를 정할 수 있다.

수식으로 나타내게 된다면, First = 첫번째 줄의 정사각형 갯수 Second = 두번째 줄의 정사각형 갯수 가 되는데

첫 번째 줄과 두 번째줄의 갯수 증가 즉, First+second -1 의 값을 몰리오미노 개수 구하는 함수에 곱해주게 되면 값은 매우 간단하게 구해진다

### 코드

```
const int MOD = 10 * 1000 * 1000;
int cache[101][101];

int poly(int n, int first) {
	if (n == first) return 1;

	int& ret = cache[n][first];
	if (ret != -1) return ret;
	ret = 0;
	for (int secont = 1; secont <= n - first; ++secont) {
		int add = secont + first - 1;
		add *= poly(n - first, secont);
		add %= MOD;
		ret += add;
		ret %= MOD;
	}
	return ret;
}

int main() {
	int T, N;
	int ret = 0;


	cin >> T;
	for (int i = 0; i < T; ++i) {
		cin >> N;
		memset(cache, -1, sizeof(cache));
		for (int j = 1; j <= N; j++) {
			ret += poly(N, j);
		}
		cout << ret << endl;
		ret = 0;
	}
	return 0;
}

```

위에서 보시다시피 POLY함수는 폴리오니모를 구하는 함수를 구현한 것이다.

첫번째줄과 두번째 줄의 갯수를 비교하고 전체에서 첫번째 줄에 사용한 정사각형의 길이를 구하면 총 갯수를 구할 수 있다.