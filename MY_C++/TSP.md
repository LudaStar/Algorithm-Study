## TSP 문제

### 1. 문제

외판원이 마을들을 다니며 어떤 경로로 가는게 가장 빠른지 찾아라.

<img src="https://seongjaemoon.github.io/assets/uploads/algorithm/tsp.png">

### 2. 접근 방법

외판원 문제는 현재 시간 복잡도 NP 가 되는 것이 없으므로, 완전 탐색 기법을 사용해서 풀이를 작성 해야한다.
완전 탐색 기법중 재귀 함수를 사용해 문제 해결을 해 보았다.

### 3. 풀이 방법

path : 지금 까지 만든 경로
visited : 각 도시의 방문 여부
currentLength : 지금까지 만든 경로의 길이
나머지 도시들을 모두 방문하는 경로들 중 가장 짧은 것의 길이를 반환한다.
n : 도시의 갯수

1) 먼저 마을을 전체를 돌았을때 재귀함수를 빠져나올 수 있도록 설정한다.

```
if (path.size() == n)
	return currentLength + dist[path[0]][path.back()];
```

2) 다음에 방문할 도시를 전부 시도한다.

``` 
for (int next = 0; next < n; next++) {
		if (visited[next]) continue;//이미 방문했다면 루프를 건너 뜀.
		int here = path.back();
		path.push_back(next);
		visited[next] = true;
		//나머지 경로를 재귀 호출을 통해 완성하고 가장 짧은 경로의 길이를 얻는다.
		double cand = shortestPath(path, visited, currentLength + dist[here][next]);
		ret = min(ret, cand);
		visited[next] = false;
		path.pop_back();
	}
```


### 4. 전체 코드

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <cfloat>

#define MAX 10000

using namespace std;
//path : 지금 까지 만든 경로
//visited : 각 도시의 방문 여부
//currentLength : 지금까지 만든 경로의 길이
//나머지 도시들을 모두 방문하는 경로들 중 가장 짧은 것의 길이를 반환한다..
int n; // 도시의 갯수
double dist[MAX][MAX];

double shortestPath(vector<int>& path, vector<bool>& visited,double currentLength) {
	if (path.size() == n)
		return currentLength + dist[path[0]][path.back()];

	double ret = INFINITY;
	//다음 방문할 도시를 전부 시도해 본다.
	for (int next = 0; next < n; next++) {
		if (visited[next]) continue;
		int here = path.back();
		path.push_back(next);
		visited[next] = true;
		//나머지 경로를 재귀 호출을 통해 완성하고 가장 짧은 경로의 길이를 얻는다.
		double cand = shortestPath(path, visited, currentLength + dist[here][next]);
		ret = min(ret, cand);
		visited[next] = false;
		path.pop_back();
	}
	return ret;
}

int main() {
	vector<int> Country_distans;//마을 사이의 거리
	vector<bool> visited;
	for (size_t i = 0; i <n; i++) {
		visited.push_back(false);
	}

	dist[0][0] = 0;
	dist[0][1] = 2;
	dist[0][2] = 4;
	dist[0][3] = 1;
	dist[0][4] = 3;

	dist[1][0] = 2;
	dist[1][1] = 0;
	dist[1][2] = 2;
	dist[1][3] = 3;
	dist[1][4] = 5;

	dist[2][0] = 4;
	dist[2][1] = 2;
	dist[2][2] = 0;
	dist[2][3] = 2;
	dist[2][4] = 6;

	dist[3][0] = 1;
	dist[3][1] = 3;
	dist[3][2] = 2;
	dist[3][3] = 0;
	dist[3][4] = 2;

	dist[4][0] = 3;
	dist[4][1] = 5;
	dist[4][2] = 6;
	dist[4][3] = 2;
	dist[4][4] = 0;

	int result = INFINITY;
	int next = 0;
	for (size_t i = 0; i < n; i++) {
		Country_distans.push_back(Country_distans.at(i));
		next=shortestPath(Country_distans, visited, 0);
		result = min(result, next);
		Country_distans.pop_back();
	}
		

	cout << result;
	return 0;

}
```

###끝내며

완전탐색 기법보다 빠른 동적 계획법을 다시 공부해 볼 필요성을 느꼈다.