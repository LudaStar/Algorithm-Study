## Boggle Game

### 1. 문제

<img src="https://algospot.com/media/judge-attachments/09ee7a6e752f07b0d99b82a010938ab4/boggle.png" width="800" height="350">

보글(Boggle) 게임은 그림 (a)와 같은 5x5 크기의 알파벳 격자인
게임판의 한 글자에서 시작해서 펜을 움직이면서 만나는 글자를 그 순서대로 나열하여 만들어지는 영어 단어를 찾아내는 게임입니다. 펜은 상하좌우, 혹은 대각선으로 인접한 칸으로 이동할 수 있으며 글자를 건너뛸 수는 없습니다. 지나간 글자를 다시 지나가는 것은 가능하지만, 펜을 이동하지않고 같은 글자를 여러번 쓸 수는 없습니다.

예를 들어 그림의 (b), (c), (d)는 각각 (a)의 격자에서 PRETTY, GIRL, REPEAT을 찾아낸 결과를 보여줍니다.

보글 게임판과 알고 있는 단어들의 목록이 주어질 때, 보글 게임판에서 각 단어를 찾을 수 있는지 여부를 출력하는 프로그램을 작성하세요.

#### 입력
입력의 첫 줄에는 테스트 케이스의 수 C(C <= 50)가 주어집니다. 각 테스트 케이스의 첫 줄에는 각 5줄에 5글자로 보글 게임판이 주어집니다. 게임판의 모든 칸은 알파벳 대문자입니다.
그 다음 줄에는 우리가 알고 있는 단어의 수 N(1 <= N <= 10)이 주어집니다. 그 후 N줄에는 한 줄에 하나씩 우리가 알고 있는 단어들이 주어집니다. 각 단어는 알파벳 대문자 1글자 이상 10글자 이하로 구성됩니다.

### 출력
각 테스트 케이스마다 N줄을 출력합니다. 각 줄에는 알고 있는 단어를 입력에 주어진 순서대로 출력하고, 해당 단어를 찾을 수 있을 경우 YES, 아닐 경우 NO를 출력합니다.

### 예제 입력
	1
	URLPM
	XPRET
	GIAET
	XTNZY
	XOQRS
	6
	PRETTY
	GIRL
	REPEAT
	KARA
	PANDORA
	GIAZAPX

### 예제 출력
	PRETTY YES
	GIRL YES
	REPEAT YES
	KARA NO
	PANDORA NO
	GIAZAPX YES

### 문제 접근방식
이 문제는 각 스펠링이 게임판의 모든 위치에 있어야 하므로 완전 탐색 기법을 사용해야 한다.

완전 탐색기법중 메모리 관리가 뛰어난 재귀함수를 이용해 각각의 스펠링 별로 문제에 접근하는 방식을 사용한다.

1) 처음 X와 Y부분의 인덱스가 접근할 부분을 먼저 선언해준다.

'''
	int dx[8] = { -1,-1,-1,1,1,1,0,0 };
	int dy[8] = { -1,0,1,-1,0,1,-1,-1 };

'''
2)기저 사례를 분석한다.

'''
	if (x<0 || y<0) return false;//기저 사례 1: 시작 위치가 범위 밖이면 실패.
	if (borard[y][x] != word[0]) return false;//기저 사례 2: 첫 글자가 일치하지 않으면 실패
	if (word.size() == 1) return true;//기저 사례 3: 글자의 크기가 1이면 무조건 성공
'''
3)인접한 8칸의 위치를 파악한다.

'''
	for (int direction = 0; direction < 8; direction++) {
		int nextY = y + dy[direction], nextX = x + dx[direction];

		if (hasWord(word.substr(1), nextY, nextX))//이 부분에서 재귀가 들어감.
			return true;
	}
	return false;//전체가 없다면 false를 반환
'''

###전체 코드

'''
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>

int dx[8] = { -1,-1,-1,1,1,1,0,0 };
int dy[8] = { -1,0,1,-1,0,1,-1,1 };

char board[5][5];

using namespace std;

bool hasWord(const string& word, int y, int x) {
	if (x<0 || y<0) return false;
	if (board[y][x] != word[0]) return false;
	if (word.size() == 1) return true;
	for (int direction = 0; direction < 8; direction++) {
		int nextY = y + dy[direction], nextX = x + dx[direction];

		if (hasWord(word.substr(1), nextY, nextX))
			return true;
	}
	return false;
}

int main() {
	int c = 0;
	int N = 0;

	bool isFound = false;
	char (*out)[10];
	cin >> c;
	while (c > 0)
	{
		for (size_t i = 0; i < 5; i++)
		{
			for (size_t j = 0; j < 5; j++) {
				cin >> board[i][j];//보드판 입력
			}
		}
		cin >> N;
		out = new char[N][10];
		for (size_t i = 0; i < N; i++)
		{
			cin >> out[i];//검사할 글자 입력
		}
		for (size_t i = 0; i < N; i++) {
			for (size_t j = 0; j < 5; j++) {
				for (size_t k = 0; k < 5; k++)
				{
					if (hasWord(out[i], j, k))
					{
						isFound = true;//찾았다면 
						break;//멈춤
					}
					else {
						isFound = false;//못찾으면 False
					}
				}
				if (isFound) {
					string str = out[i];
					cout << str << "  YES" << endl;
					break;
				}
			}
			if (isFound) {
				continue;
			}
			string str = out[i];
			cout << str << "  NO" << endl;
		}
		c--;
	}
	return 0;
}
'''
