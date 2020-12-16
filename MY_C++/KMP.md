## KMP 알고리즘

여기서 KMP알고리즘은 커누스 모리스 플랫 알고리즘으로 흔히 KMP로 불리는 알고리즘이다. 

이 알고리즘은 문자열을 찾는데 이용되는데 주어진 H의 긴 문자열안에 N의 문자열을 찾아내는 알고리즘이다.

이 때 단순 알고리즘은 처음부터 끝까지 수가 일치하는지 안하는지를 확인하면서 찾아내게 되는데 문제는 문자열안에 시작부분이 일치하는 문자열이 있을 때 시간을 좀더 줄일 수 있을까 라는 부분에서 시작된 알고리즘이다.

예를 들어 aabaaab라는 문자열을 찾는 문제가 있다고 생각하자. 단순 알고리즘에서는 aabaaa까지 맞추고 마지막 b에서 틀렸다고 하면 이 알고리즘은 두번째 a부터 다시 검사를 시작하게 될것이다. 이를 방지하고자 만든 방법이 바로 KMP알고리즘 이다.

방지하는 방법은 조금 헷갈린다. 나도 책으로 읽으면서 이해하려고 꽤 많은 시간을 들인 것 같다. 

중복되는 부분을 방지하는 방법은 문자열 내에서 일치하는 문자열을 찾는 것이다. 이말이 무엇이냐하면, aabaaab에서(앞서 일치했던 문자열) 에서 마지막 b가 틀렸다면 aaba는 문자열에서 찾으려 해봤자 정답이 아닌것이다. 따라서 다시 대응되는 위치로 옮기기 위해서라면 aabaaab의 네번째 a에서 시작하게 만들어 검색을 하는 것이다.
그 전에있는 문자들 a,a,b,a는 정답이 될 수 없으니 검사를 진행하지 않아도 되는것을 의미한다.

즉 KMP는 앞에서도 보이듯 불일치가 일어났을 때 지금까지 일치한 글자의 수를 이용해 다음으로 시도해야 할 위치를 찾는 것이다.

실제 문자열 검색의 구현이다.

적절한 전처리를 통해 pi라는 부분 일치 테이블을 만들어야 한다. 일치하는 숫자 N을 넘겨줄 때 N의 값에 따라 빠르게 어디서부터 시작해야 되는지 알려주는 일종의 미리 계산해 두는 문자열 검색 프로그램 이다.

코드는 다음과 같다.


```
using namespace std;

vector<int> getPartialMatch(const string& N) {
	int m = N.size();//일치한 문자열의 길이
	vector<int> pi(m, 0);

	int begin = 1, matched = 0;//begin을 0부터 시작하게 되면 무조건 일치하므로 1부터 시작해야 된다.
	while (begin + matched < m) {
		if (N[begin + matched] == N[matched])//부분이 일치한다면
		{
			++matched;//matche를 하나 늘림 즉, 다음 문자열을 검사하기 위함
			pi[begin + matched - 1] = matched;//위치를 기록
		}
		else {// 부분일치하지 않는다면
			if (matched == 0)
				++begin;
			else {
				begin += matched - pi[matched];
				matched = pi[matched - 1];
			}
		}
	}	
}
```

위의 코드는 pi를 최적화하는 과정이다. 이 때 최적화에도 마찬가지로 KMP를 적용 시킬 수 있다. 왜냐하면 전처리 또한 문자열내에서 일치하는 문자열을 검색하는 알고리즘 이므로 KMP로 쉽게 구현이 가능하다. (물론 내용이 쉽진 않지만..)

다음으론 KMP 문자열 탐색 알고리즘 부분이다.

```
vector<int> kmpSearch(const string& H, const string& N) {
	int n = H.size(), m = N.size();
	vector<int> ret;
	vector<int> pi = getPartialMatch(N);// 미리 PI를 검사해두어 시간을 단축
	int begin = 0, matched = 0;//문자열 처음부터 검색
	while (begin <= n-m)
	{
		if (matched < m && H[begin + matched] == N[matched]) {// match부분 즉 tail부분이 m보다 크면 배열범위를 벗어남
			++matched;
			if (matched == m) ret.push_back(begin);
		}
		else {
			if (matched == 0)
				++begin;
			else
			{
				begin += matched - pi[matched - 1];
				matched = pi[matched - 1];
			}
		}
	}
	return ret;
}

```
이렇듯 kmp알고리즘을 책을 통해 구현해 보았다. 이 알고리즘자체는 이론은 매우 단순했다. 문자열 안에 반복되는 문자열이 있거나 일치하는 문자열이 있으면 검색이 빠르다는 것이다. 하지만 단순한 이론안에 복잡한 계산식이 들어가면서 이해가 매우 힘들었던 상황이었다.


### 마치며

이 코드는 자주 사용될거 같은 생각에 따로 정리해두고 추후에 계속해서 사용하고 이해하려 노력해 내꺼로 만들어야 될 코드중 하나이다.
