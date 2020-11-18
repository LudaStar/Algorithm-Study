## Merge Interval

### 1. 문제
주어진 배열에서 겹치는 부분이 있으면 merge한다.

<img src = "https://user-images.githubusercontent.com/68332512/99532105-203d3b00-29e7-11eb-9a38-61227bbd0b29.PNG" width = 300 height = 250>

### 2. 접근
 - Interval 객체 생성
 - sort
 - Interval 객체의 start, end 비교 후 겹치면 merge
 
### 3. 코드 설명

주요 메서드 merge
```java
	public List<Interval> merge(List<Interval> intervals) {
		if (intervals.isEmpty())
			return intervals;

	  	Collections.sort(intervals, comp2);
//		람다식 사용. 아래의 식은 오름차순을 나타내는 것이고 (a,b) -> b.start - a.start이면 내림차순
//		Collections.sort(intervals,(a,b) -> a.start-b.start); 

    //새로운 Interval 담을 List를 생성
		List<Interval> ans = new LinkedList<Interval>();
		Interval hold = intervals.get(0);
    
    //List intervals를 차례로 스캔
		for (int i = 1; i < intervals.size(); i++) {
			Interval current = intervals.get(i);
      
      //hold의 end와 current의 start 비교 후 더 큰 end 값을 가진 것을 hold의 end로 넣음
			if (hold.end >= current.start) {
				hold.end = Math.max(current.end, hold.end);
        
        //겹치지 않으면 ans에 그대로 추가하고 hold를 한 칸 나아감
			} else {
				ans.add(hold);
				hold = current;
			}
		}
    //가장 마지막으로 들어가는 interval은 뒤에 더 비교할 것이 없기 때문에 그대로 집어넣는다
		if (!ans.contains(hold)) {
			ans.add(hold);
		}

		return ans;
	}
```

Comparator 중요!
```java
// 1
	Comparator comp = new Comparator<Interval>() {
		public int compare(Interval a, Interval b) {

			return a.start - b.start;
		}
	};
// 2
//	 리턴값이 int 양수: 현재 인스턴스가 비교대상인 인스턴스보다 크다 
//                음수:현재 인스턴스가비교대상인 인스턴스보다 작다
//                  0 :값이 동일

	Comparator<Interval> comp2 = new Comparator<Interval>() {
		@Override

		public int compare(Interval o1, Interval o2) {
			if (o1.start > o2.start) {
				return 1;
			} else if (o1.start < o2.start) {
				return -1;
			} else {
				return 0;
			}
		}
	};
```

### 4. 전체 코드
```java
package StringNArray;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.LinkedList;
import java.util.List;

//class Interval은 MeetingRooms.java에서 선언했음

public class MergeInterval {

	public static void main(String[] args) {
		
//	int[][] nums = {{1,3},{2,6},{8,10},{15,18}};
		Interval in1 = new Interval(1, 3);
		Interval in2 = new Interval(2, 6);
		Interval in3 = new Interval(8, 10);
		Interval in4 = new Interval(15, 18);

		List<Interval> intervals = new ArrayList<>();
		intervals.add(in1);
		intervals.add(in2);
		intervals.add(in3);
		intervals.add(in4);
		MergeInterval a = new MergeInterval();
		List<Interval> list = a.merge(intervals);
		a.print(list);

	}
	
	public List<Interval> merge(List<Interval> intervals) {
		if (intervals.isEmpty())
			return intervals;

		Collections.sort(intervals, comp2);

		List<Interval> ans = new LinkedList<Interval>();
		Interval hold = intervals.get(0);
		for (int i = 1; i < intervals.size(); i++) {
			Interval current = intervals.get(i);
			if (hold.end >= current.start) {
				System.out.println("hold.end: " + hold.end);
				hold.end = Math.max(current.end, hold.end);
			} else {
				System.out.println("22hold.end: " + hold.end);
				ans.add(hold);
				hold = current;
			}
		}

		if (!ans.contains(hold)) {
			System.out.println("333hold.end: " + hold.end);
			ans.add(hold);
		}

		return ans;
	}

// 1
	Comparator comp = new Comparator<Interval>() {
		public int compare(Interval a, Interval b) {

			return a.start - b.start;
		}
	};

	Comparator<Interval> comp2 = new Comparator<Interval>() {
		@Override

		public int compare(Interval o1, Interval o2) {
			if (o1.start > o2.start) {
				return 1;
			} else if (o1.start < o2.start) {
				return -1;
			} else {
				return 0;
			}
		}
	};

	void print(List<Interval> list) {
		for (int i = 0; i < list.size(); i++) {
			Interval in = list.get(i);
			System.out.println(in.start + " " + in.end);
		}
	}

}
```
