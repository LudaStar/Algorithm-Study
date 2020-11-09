## MeetingRooms

### 1. 문제

<img src="https://user-images.githubusercontent.com/68332512/98521989-81626180-22b7-11eb-874d-8d338fafd688.PNG" width="400" height="350">

주어진 Input은 미팅 시간으로서 [[0,30],[5,10],[15,20]]의 의미는 0에 시작하여 30에 끝나는 미팅, 5에 시작하여 10에 끝나는 미팅, 15에 시작하여 20에 끝나는 미팅이 있다는 뜻이다.
세 개의 미팅은 서로 시간이 겹치기 때문에 false를 반환하고, [[7,10],[2,4]]는 겹치지 않기 때문에 true를 반환한다.

### 2. 접근
각 미팅을 객체로 만들어 각 미팅들을 소팅한 후 시작 시간과 끝나는 시간이 겹치는 지 확인한다.

### 3. 코드 설명
1) Interval이라는 클래스로 미팅이 시작 시간, 끝나는 시간을 담는다.
생성자를 선언하여 입력받을 값을 정하였다.
```java
class Interval{
	int start;
	int end;
	Interval(){
		this.start = 0;
		this.end =0;
	}
	Interval(int s, int e){
		this.start = s;
		this.end = e;
	}
}
```

2) Compartor 인터페이스 사용
  compare()메서드는 비교 대상 2개의 객체를 차례로 인자로 받고 두 인자의 차를 반환한다.
```java
	Comparator<Interval> Comp = new Comparator<Interval>() {

		@Override
		public int compare(Interval a, Interval b) {
			//오름차순
			return a.start - b.start;
		}
	};
  ```
  정렬 메서드인 Arrays.sort()의 인자로 넘겨 start를 기준으로 오름차순 정렬된다.
  ```java
  Arrays.sort(intervals, Comp);
  ```
  
3) 각 intervals의 start가 전의 intervals의 end보다 큰 경우(미팅시간이 겸치는 경우) false 반환
```java
		for(int i=1; i<intervals.length; i++) {
			if(intervals[i-1].end >intervals[i].start)
				return false;
		}
```

### 4. 전체 코드
```java
import java.util.Arrays;
import java.util.Comparator;

class Interval{
	int start;
	int end;
	Interval(){
		this.start = 0;
		this.end =0;
	}
	Interval(int s, int e){
		this.start = s;
		this.end = e;
	}
}

public class MeetingRooms {

	public static void main(String[] args) {
		
		MeetingRooms a = new MeetingRooms();
		
		
		Interval in1 = new Interval(15,20);
		Interval in2 = new Interval(5,10);
		Interval in3 = new Interval(0,30);
		
		Interval[] intervals = {in1, in2, in3};
		System.out.println(a.solve(intervals));
	}
	
	public boolean solve(Interval[] intervals) {
		if(intervals == null) return false;
		print(intervals);// 15,5,0
		Arrays.sort(intervals, Comp);
		System.out.println("===after sort====");
		print(intervals); //0,5,15
		
		for(int i=1; i<intervals.length; i++) {
			if(intervals[i-1].end >intervals[i].start)
				return false;
		}
			
		return true;
		
	}
	
	public void print(Interval[] intervals) {
		for(int i=0; i<intervals.length; i++) {
			Interval in = intervals[i];
			System.out.println(in.start+" "+in.end);
			
		}
	}
	
	Comparator<Interval> Comp = new Comparator<Interval>() {

		@Override
		public int compare(Interval a, Interval b) {
			//오름차순
			return a.start - b.start;
			
		}
		
	};
	
}
```
