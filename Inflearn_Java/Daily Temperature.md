## Daily Temperature

### 1. 문제

int형 배열 nums에 온도가 저장되어 있다. 각 온도보다 높아지는 순간까지의 index차이를 result 배열에 저장한다. <br>
ex ) 73도보다 높아지는 순간은 74도로 index차이가 1이므로 result[0]에 1저장되고,<br> 75도보다 높아지는 순간은 76도로 index 차이가 4이므로 result[2]에 4가 저장된다.

<img src ="https://user-images.githubusercontent.com/68332512/99179467-61241e00-2761-11eb-80eb-a078625f889b.PNG" width = "350" height = "250">

### 2. 접근 방법

Stak을 사용하여 자신보다 큰 숫자를 만날 때까지 stack을 쌓아가며 자신보다 큰 숫자를 만나면 stack에서 삭제한다.

### 3. 코드 설명
stack에 index값을 차례대로 넣으면서 자신보다 큰 값을 만나면 stack에서 삭제하고 index의 차이를 배열 ret에 넣는다.

```java
	    for(int i = 0; i < temperatures.length; i++) { 
	        while(!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i] ) {

	            int index = stack.pop();
	            ret[index] = i - index;
	        }
	        stack.push(i);
	    }
  ```
  
 ### 4. 전체 코드
 ```java
 package StringNArray;

import java.util.*;

public class DailyTemperature {

	public static void main(String[] args) {
		int[] nums = {73, 74, 75, 71, 69, 72, 76, 73};
		int[] res = dailyTemperatures(nums);

	}

	public static int[] dailyTemperatures(int[] temperatures) {
	    Stack<Integer> stack = new Stack<>();
	    int[] ret = new int[temperatures.length];
      
	    for(int i = 0; i < temperatures.length; i++) {
	        while(!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i] ) {
          
	            int index = stack.pop();
	            ret[index] = i - index;
	        }
	        stack.push(i);
	    }
	    return ret;
	}
}
	
```
