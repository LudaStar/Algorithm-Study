## Jewels and Stones

### 1. 문제
<img src = "https://user-images.githubusercontent.com/68332512/100534942-c5fa7080-3257-11eb-86f4-1dd3b2347801.PNG" width = "350" height = "300">

String 형식으로 Jewel과 Stone이 주어질 경우 stone에 jewel을 얼마나 포함하고 있는지 구하면 됩니다.
Jewel이 "aA"이고 Stone이 "aAAbbbb"라면 jewel은 a와 A로 총 2개이고, stone에 jewel은 3개가 있는 것 입니다. 
이때 주의할 점은 대소문자를 다르게 생각해야 되는 것입니다.


### 2. 접근
set에 저장을 jewel을 저장하면 중복이 제거되고 저장되는데 set에 저장된 것과 stone을 비교하여 jewel이 몇 개 들어 있는지 확인할 수 있습니다.


### 3. 전체 코드
```java
package StringNArray;

import java.util.HashSet;
import java.util.Set;

public class JewelsAndStones {

	public static void main(String[] args) {
		String J = "aA";
		String S = "aAAbbbb";
		System.out.println(solve(J,S));
	}
	
	public static int solve(String jew, String stone) {
		//set은 중복을 허용하지 않음
		Set<Character> set = new HashSet<>();
		for(char jewel : jew.toCharArray()) {
			set.add(jewel); //a, A
		}
		
		int count = 0;
		for(char st : stone.toCharArray()) {
			System.out.println("st : " + st); // a, A, A, b, b, b, b
			if(set.contains(st)) {
				count++; //a, A, A
			}
		}
		return count;
	}
}
```
