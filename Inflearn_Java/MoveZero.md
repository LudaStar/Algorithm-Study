## Move Zero

### 1. 문제 
배열중에 0이 아닌 값들 먼저 저장한 뒤 0은 나중에 저장합니다

<img src = "https://user-images.githubusercontent.com/68332512/98797285-b86b7b00-244f-11eb-8ea4-48b202099825.PNG" width = "400" height = "330">

### 2. 접근
0이 아닌 숫자들을 순서대로 저장한 후 남은만큼을 0으로 채워줍니다.

### 3. 코드 설명
1) 0이 아닌 숫자들을 저장하고 0이 나오는 위치를 변수 currentIndex에 담습니다.
```java
		for (int i = 0; i < nums.length; i++) {

			if (nums[i] != 0) {
				nums[currentIndex] = nums[i];
				currentIndex++;
			}
		}
```

2) currentIndex부터 배열의 길이만큼 0으로 채워줍니다.
```java
		while (currentIndex < nums.length) {
			nums[currentIndex] = 0;
			currentIndex++;
		}
```

### 4. 전체 코드
```java
public class MoveZero {

	public static void main(String[] args) {

		int[] nums = { 0, 3, 2, 0, 8, 5 };
		int currentIndex = 0;

		for (int i = 0; i < nums.length; i++) {

			if (nums[i] != 0) {
				nums[currentIndex] = nums[i];
				currentIndex++;
			}
		}

		while (currentIndex < nums.length) {
			nums[currentIndex] = 0;
			currentIndex++;
		}

	}
}
```

### 5. Complexity
데이터  int[] nums = {0,3, 2, 0, 8, 5}; 를 for문으로 모두 순회해야되니까 Time Complexity: O(n) <br>
주어진 문제에서 int currentIndex = 0; 상수는 하나만 사용했으니까 Space Complexity : O(1)
 
