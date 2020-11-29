## LicenseKeyFormatting

### 1. 문제
<img src = "https://user-images.githubusercontent.com/68332512/100534866-10c7b880-3257-11eb-8e3e-c8ae64df4666.PNG" width = "400" height = "350"><img src = "https://user-images.githubusercontent.com/68332512/100534891-508ea000-3257-11eb-9cbc-717aeff63223.PNG" width = "400" height = "350">


주어지는 문자열에서 하이픈을 모두 제거하고, 뒤에서 k만큼 떨어진 곳 모두에 하이픈을 넣습니다. <br>
이때 알파벳은 모두 대문자여야 합니다.

### 2. 접근
1) 주어진 문자열에서 하이픈 제거
2) 모두 대문자로 변경
3) StringBuilder 사용
4) 원하는 위치에 하이픈 삽입

#### String VS StringBuilder VS StringBuffer
String class는 private final char형임을 유의해야 한다. <br>
String은 char의 배열 형태로 저장되고, 이 값들은 외부에서 접근할 수 없도록 private으로 보호된다.<br>
또한, final형이기 때문에 초기값으로 주어진 String 값은 불변으로 바뀔 수가 없다.따라서 String은 새로운 값을 할당할 때마다 새로운 메모리를 사용하기 때문에 메모리를 많이 차지한다.<br>

반면에 StringBuilder와 StringBuffer는 메모리에 append하는 방식으로 클래스를 직접 생성하지 않는다.<br>
둘의 차이점은 StringBuilder는 변경가능한 문자열이지만 synchronization이 적용되지 않았다. <br>
하지만 StringBuffer는 변경가능하지만 multiple thread환경에서 안전한 클래스라고 한다. <br>
이와 달리 StringBuffer는 multi thread환경에서 다른 값을 변경하지 못하도록 하므로 web이나 소켓환경과 같이 비동기로 동작하는 경우가 많을 때는 StringBuffer를 사용하는 것이 안전할 것이다.

### 3. 전체 코드
```java
package StringNArray;

public class LicenseKeyFormatting {

	public static void main(String[] args) {
		String S = "5F3Z-2e-9-w";  //  String S = "2-5g-3-J";
		int k = 4;
		System.out.println(solve(S, k));
	}
	
	public static String solve(String str, int k) {
		String newStr = str.replace("-", ""); // 주어진 문자열에서 - 삭제
		newStr = newStr.toUpperCase(); // 모두 대문자로 변겅
		
		StringBuilder sb = new StringBuilder(); 
		for(int i = 0; i < newStr.length(); i++) {
			sb.append(newStr.charAt(i)); // StringBuilder에 옮겨 담아줌
		}
		
		int len = sb.toString().length();
		
		for(int i = k; i < len; i=i+k) {
			sb.insert(len-i,'-'); // 문자열 뒤부터 k만큼 떨어진 곳에 - 삽입
		}
		
		return sb.toString();
	}
}

```

