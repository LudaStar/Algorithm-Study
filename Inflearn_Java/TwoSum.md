## TwoSum

### 1. 문제
int 타입의 배열 nums와 int 타입의 변수 target이 주어졌을 때, 배열 nums에 있는 값 2개를 더하여 target을 구할 수 있을 때, <br>
2개의 index를 구하여 배열 result에 담는다.

<img src="https://user-images.githubusercontent.com/68332512/99178940-dbea3a80-275b-11eb-8016-3e3872ef06f5.PNG" width = "300" height="150">

### 2. 접근
Map을 사용하여 키에는 target - nums[i]를 저장하고 value에는 nums[i]의 index값을 저장한다.

* 이중 for문 사용하면 쉽지만 time Complexity(n^2)이기 때문에 nums의 크기가 커지면 비효율적이다.
* Array+Map(고유키를 저장 했다가 Array를 for문 돌려서 나오면 후려쳐서 값 얻기) 대표문제이므로 잘 기억하자

### 3. 코드 설명

for문으로 배열 nums을 돌면서 Map의 키 값으로 target-nums[i]를 넣고 target-nums[i]가 nums에 있는 값이면 배열 result에 담는다.
```java
		for(int i=0; i<nums.length; i++) {
			if(map.containsKey(nums[i])){
				int mapValue = map.get(nums[i]); //i=1일때 8 , map(8,0)
				result[0]  = mapValue +1; 
			  result[1]  = i+1 ;        
				
			}else {
				map.put(target-nums[i], i); //key 10-2=8, value i=0 
			}
		}
 ```
 
 ### 4. 전체 코드
 ```java
 package StringNArray;

import java.util.*;

public class TwoSum {

	public static void main(String[] args) {
		int[] nums = {2,8,11,21};
        int target =10;
        TwoSum a = new TwoSum();
        int[]  result = a.solve(nums, target);
	}
	
	public int[] solve(int[] nums, int target) {

		Map<Integer, Integer> map = new HashMap<>();
		int[] result = new int[2];

		for(int i=0; i<nums.length; i++) {
			if(map.containsKey(nums[i])){
				int mapValue = map.get(nums[i]); //i=1일때 8 , map(8,0)
				result[0]  = mapValue +1;
			  result[1]  = i+1 ;     
				
			}else {
				map.put(target-nums[i], i); //key 10-2=8, value i=0 
			}
		}
		return result;
	}
  
}
```
