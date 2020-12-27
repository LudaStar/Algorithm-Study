# Tree

트리는 일상생활에 존재하는 많은 일들을 빠르게 검색하거나 간편하게 구조를 만들기 위해 자주 사용되는 자료구조 형태이다.

트리의 구성은 자료가 저장된 노드들이 간선으로 연결되어 있는 자료구조를 말합니다. 노드 간에는 상/하위 관계가 있으며, 노드가 연결되었을 때 한 노드는 좀더 상위, 다른 노드는 좀더 하위에 있어야 합니다.
노드들의 상대적인 관계로는 부모(Parent)노드, 부모노드의 하위에 존재하는 자식(Children)노드로 두가지가 존재한다. 부모가 같은 노드들을 형제(sibing) 노드라고 한다.
부모 노드와 부모 노드의 상위 노드들을 통틀어 선조(ancestor)라고 부르고, 자식노드와 그의 자식들을 통틀어 자손(descendant)라고 부릅니다.

쉽게 설명하면 어떤 한 노드를 선택했을 때 그보다 상위 노드들은 선조, 그보다 하위 노드들은 자손이라고 생각하면 됩니다.

여기서 노드의 특징을 부르는 부모 자식만 보더라도 트릐의 특징으로는 자식 노드는 단 하나의 부모노드를 가질 수 있습니다. 반대로 부모노드는 여러개의 자식 노드를 가질 수 있습니다.

## Tree & Node의 속성

루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수를 해당 노드의 깊이 라고 합니다. 따라서 깊이가 깊으면 깊을 수록 트리 아래 쪽에 있는 노드를 지칭하게 됩니다. 이 때 트리에서 가장 깊은 노드를 이 트리의 높이(height)라고 한다.

## Tree의 재귀적 속성

트리에서 한 노드와 그의 자손들을 모두 모으면 그들도 하나의 트리가 된다. 이때 어떤 노드 T와 그 자손들로 구성된 트리를 't를 루트로 하는 서브트리 라고합니다.
이와같은 재귀적인 특성을 가진 트리때문에 트리를 다루는 코드들은 대부분 재귀호출을 이용해 구현된다.

## 트리의 표현 

트리는 굉장히 다양한 방법으로 구현할 수 있습니다. 그중 가장 일반적인 형태는 각 노드를 하나의 구조체/객체로 표현하고, 이들을 서로 포인터로 연결하는 구조로 사용된다.

노드의 구현은 다음과 같이 간단하게 구현된다. 

```
struct TreeNode
{
	string label;
	TreeNode* parent;
	vector<TreeNode*> children;
};
```

이렇게 값을 나타내는 label, 부모 노드를 확인하는 parent 자식노드를 확인하는 children으로 구성되어 있는 것을 확인 할 수 있다.

## 트리의 순회

자료구조의 가장 기초 연산 중 하나는 포함되어 잇는 자료를 전부 순회하는 것입니다. 그러나 선형으로 구성된 배열과 달리 트리는 그 구조가 일정하지 않기 때문에 재귀적인 특성을 사용해서 방문 해야한다.

코드는 다음과 같다.
```
// 주어진 트리의 각 노드에 저장된 값을 모두 출력한다.

void printLabels(TreeNode* root) {
	// 루트에 저장된 값을 출력
	cout << root->label << endl;

	for (int i = 0; i < root->children.size(); i++) {
		printLabels(root->children[i]);
	}
}
```
이렇듯 재귀함수를 통해 자식 노드를 전부 방문하고 출력하는 방법을 찾는다. 여기선 간단히 부모노드부터 시작해서 첫 번째 자식노드에서 마지막 자식 노드까지 순차적으로 출력한다.

## 트리의 깊이

트리의 깊이를 찾기 위해서는 모든 자손들의 마지막 자식노드들의 최고 깊이를 탐색해서 해당 트리의 깊이를 찾아낼 수 있다.

코드는 다음과 같다.

```
// root를 루트로 하는 트리의 높이를 구한다.

int height(TreeNode* root) {
	int h = 0;
	for (int i = 0; i < root->children.size(); i++) {
		h = max(h, 1 + height(root->children[i]));
	}
	return h;
}

```

## 트리 예제

트리 순회 순서 변경 방법으로 전위 순회, 후위 순회, 중위 순회가 있다. 이 중 두개의 순회 방법만 주어진다면 나머지 한개의 순회 방법을 구현할 수 있다.

다음 예제는 전위 순회와 중위 순회가 주어졌을 때 후위 순회로 출력하는 코드를 나타낸다.

```
// 이진 트리의 왼쪽과 오른쪽으로 나누는 방법
vector<int> slice(const vector<int>& v, int a, int b) {
	return vector<int>(v.begin() + a, v.begin() + b);
}
// 트리의 전위 탐색 결과와 중위 탐색 결과를 input으로 받아 출력
void printPostOrder(const vector<int>& preorder, const vector<int>& inorder) {
	//전체 tree의 size
	const int N = preorder.size();
	//트리가 비어있으면 종료
	if (preorder.empty()) return;
	//전위 순회는 루트부터 탐색하므로 첫번째 노드가 부모 노드
	const int root = preorder[0];
	// Left방향의 크기를 확인 할 수 있는 크기
	const int L = find(inorder.begin(), inorder.end(), root)-inorder.begin();
	// Right방향의 크기를 확인 할 수 있는 크기
	const int R = N - 1 - L;
	// 왼쪽과 오른쪽 서브 트리의순회 결과를 출력.
	printPostOrder(slice(preorder, 1, L + 1), slice(inorder, 0, L));
	printPostOrder(slice(preorder, L+1, N), slice(inorder, L+1, N));

	cout << root << ' ';
}
```