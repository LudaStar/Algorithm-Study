## Meeting Room2

### 1. 문제
주어지는 회의시간들을 보고 몇 개의 회의실이 필요한지 알아내는 문제입니다. <br>
회의시간이 겹치지 않을 때에는 회의실이 1개만 필요하고 회의 시간이 겹치면 그 이상의 회의실이 필요합니다.
<img src = "https://user-images.githubusercontent.com/68332512/99897507-57f4fd00-2cdd-11eb-99fb-7f5be5657032.PNG" width = "400" height = "300">

### 2. 접근
1) 첫 번째 방법 : 
- 회의 시작 시간을 기준으로 정렬한다.
- 앞 회의의 끝나는 시간과 그 다음 회의의 시작하는 시간이 겹치면 회의실이 1개 더 필요하므로 그대로 heap에 넣는다.
- 하지만 앞 회의 끝나는 시간이 그 다음 회의 시작시간보다 이르다면 회의실이 필요하지 않기 때문에 두 회의를 merge 해준 뒤에 heap에 넣는다.
<img src = "https://user-images.githubusercontent.com/68332512/99897511-5fb4a180-2cdd-11eb-8417-32b7aff302b5.PNG" width = "450" height = "350">

2) 두 번째 방법 : 
- 회의 시작 시간을 기준으로 정렬한다.
- 회의실이 필요한 상황에만 heap에 넣는다. (minHeap사용 - minHeap은 작은 것이 루트노드가 됨)
<img src ="https://user-images.githubusercontent.com/68332512/99897513-6511ec00-2cdd-11eb-938f-3041f62b86ac.PNG" width ="450" height = "350">


### 3. 코드 설명
1) 첫 번째 방법의 코드
```java
		for(int i=1; i<intervals.length; i++) {
			Interval interval = heap.poll(); //힙에 넣었던 것을 꺼내서
			if( interval.end <= intervals[i].start) { //비교
				interval.end = intervals[i].end; //겹치지 않으면 merge 해줌
			} 
			else {
				heap.offer(intervals[i]); // 겹치면 heap에 넣음
			}
			 heap.offer(interval); //merge 해준 것을 heap에 넣음
		}
```
2) 두 번째 방법의 코드
```java
		for(int i = 0; i < intervals.length; i++) {
			
			//회의실이 필요없는 애들은 heap에서 빼주는 과정
			while(!minHeap.isEmpty() && minHeap.peek().end <= intervals[i].start) {
				minHeap.poll(); //5 10
			}
			
			minHeap.offer(intervals[i]); // 0 30, 15 20
			max = Math.max(max, minHeap.size());
		}
```

4. 전체 코드
```java
package StringNArray;

import java.util.Arrays;
import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;

public class MeetingRoom2 {

	public static void main(String[] args) {
		MeetingRoom2 a = new MeetingRoom2();
		Interval in1 = new Interval(5,10);
		Interval in2 = new Interval(15,20);
		Interval in3 = new Interval(0,30);
		Interval[] intervals = {in1,in2,in3};
		System.out.println(a.solve1(intervals));
	}
	
	public int solve2(Interval[] intervals) {
		if(intervals == null || intervals.length == 0)
			return 0;
		
		Arrays.sort(intervals, (a,b) -> (a.start - b.start));
		
		Queue<Interval> minHeap = new PriorityQueue<>(intervals.length,(a,b) -> (a.end - b.end));
		int max = 0;
		
		for(int i = 0; i < intervals.length; i++) {
			
			while(!minHeap.isEmpty() && minHeap.peek().end <= intervals[i].start) {
				minHeap.poll();
			}
			
			minHeap.offer(intervals[i]); 
			max = Math.max(max, minHeap.size());
		}
		return max;
	}
	
	public int solve1(Interval[] intervals) {
		if(intervals == null || intervals.length == 0)
			return 0;
		
		Arrays.sort(intervals, Comp);
		Queue<Interval> heap = new PriorityQueue<Interval>(intervals.length, Comp2);
		
		heap.offer(intervals[0]);
		
		for(int i=1; i<intervals.length; i++) {
			Interval interval = heap.poll();
			if( interval.end <= intervals[i].start) {
				interval.end = intervals[i].end;
			} 
			else {
				heap.offer(intervals[i]);
			}
			 heap.offer(interval);
		}
		return heap.size();
	}

	Comparator<Interval> Comp2 = new Comparator<Interval>() {
		@Override
		public int compare(Interval o1, Interval o2) {
			return o1.end - o2.end;
		}
	};
	
	Comparator<Interval> Comp = new Comparator<Interval>() {
		@Override
		public int compare(Interval o1, Interval o2) {
			return o1.start - o2.start;
		}
	};
}
```
