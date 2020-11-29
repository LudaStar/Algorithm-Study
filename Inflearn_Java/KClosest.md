## KClosest 

### 1. 문제

좌표들이 주어지고 그 좌표의 거리들을 비교하여 k번째로 가까운 좌표를 구하면 된다.

<img src = "https://user-images.githubusercontent.com/68332512/100535065-d65f1b00-3258-11eb-8944-fb40c33ca4ef.PNG" width = "400" height = "300">

### 2. 접근
1) PriorityQueue 사용 
(일반적인 Queue는 FIFO이지만 PriorityQueue는 일정한 규칙으로 우선순위를 정해서 저장한다. <br>
보통은 낮은 숫자부터 큰 숫자까지 오름차순으로 정렬이지만 Comparator를 사용해서 순서를 재정의할 수 있다.)
2) Comparator 사용
(순서를 좌표의 거리순으로 정의한다.)
3) k만큼 queue에서 삭제한다.

### 3. 주요 코드
```java
	Comparator<int[]> Comp = new Comparator<int[]>() {

		@Override
		public int compare(int[] a, int[] b) {
			//오름차순 -> queue에 좌표의 거리가 작은 수 부터 정렬
			return (a[0] * a[0] + a[1] *a[1]) - (b[0] * b[0] + b[1] *b[1]);
		}
	};
```

### 4. 전체 코드
```java
package StringNArray;

import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;

public class KClosest {

	public static void main(String[] args) {
		KClosest a = new KClosest();
		int[][] points = {{1,3}, {-2,2}};
		int k = 1;
		int[][] result = a.solve(points,k);
		a.print(result);
	}
	
	public int[][] solve(int[][] points, int k) {
		Queue<int[]> queue = new PriorityQueue<>(points.length, Comp);
		int[][] result = new int[k][2];
		
		for(int[] p : points) { // points 배열에 들어있는 걸 하나씩 queue에 저장 {1,3}, {-2, 2}
			queue.offer(p);
		}
		
		int index = 0;
		while(index < k) {
			result[index] = queue.poll(); // k만큼 queue에서 삭제 후
			index++;
		}
		return result; //return
				
	}
	
	Comparator<int[]> Comp = new Comparator<int[]>() {

		@Override
		public int compare(int[] a, int[] b) {

			return (a[0] * a[0] + a[1] *a[1]) - (b[0] * b[0] + b[1] *b[1]);
		}
	};
	
  //배열 print
	public void print(int[][] result) {
		int m = result.length;
		int n = result[0].length;
		for(int i = 0; i < result.length; i++) {
			for(int j = 0; j < result[i].length; j++) {
				System.out.println(result[i][j]);
			}
		}
	}

}
```
