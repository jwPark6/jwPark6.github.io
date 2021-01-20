---
title: "동계 모각코 4주차"
---

### 계획
  - 알고리즘 해싱 개념 숙지 및 복습(인프런 강의를 통해 복습예정) 해싱 파트같은 경우 다른 파트보다 이론이 부족하므로 이론에 집중할 예정
  - 여유가 된다면 간단한 예제의 코드 이해, 백준 문제풀이를 목표

### 결과
  - 먼저 인프런 강의를 통해 해싱파트의 개념을 다시 공부하였다. 예상한대로 다른 파트에 비해 이해가 낮아 저번모임보다는 이론학습에 시간이 더 소모되었다.


  ![image](https://user-images.githubusercontent.com/67006945/105186511-254c7100-5b75-11eb-9011-45f3517d17ad.png)


  - 이후 백준 문제를 풀어보았다.


```
  import java.util.Scanner;

public class Main {
	public static void hash(String c) {
		int sum = 0;
		for(int i = 0; i < c.length(); i++) {
			int n = c.charAt(i)-96;
			sum += n*Math.pow(31, i);
		}
		System.out.println(sum);
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);

	    int L = scan.nextInt();
	    String c = scan.next();
	    hash(c);
	}
}
```

- 간단한 예제를 통해 개념을 정립하였고 아래와 같은 결과를 얻었다.


![image](https://user-images.githubusercontent.com/67006945/105186875-7eb4a000-5b75-11eb-8533-333fe62fb682.png)

- 다음으로는 더 난이도 있는 백준 2002번 문제를 해결할려고 했다. 그러나 이클립스에서 내가 생각한 테스트케이스는 성공했지만 실제 문제 제출에서는 정답을 얻지 못하였고 이는 추가적으로 다음 모임까지 확인하기로 하였다.
- 터널을 들어갈 때 추월한 차량을 세는 문제인데, 아래는 실제 작성한 코드이다.

```
import java.util.Scanner;
import java.util.HashMap;

public class Main {	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		HashMap hm = new HashMap();
		
		int numberOfCar = scan.nextInt();
				
		for(int i = 0; i < numberOfCar; i++) {
			String s = scan.next();
			
			hm.put(s, i);
		}
		
		int count = 0;
		
		String s = scan.next();
		int prevCar = (int) hm.get(s);
		
		for(int i = 0; i < numberOfCar-1; i++) {
			s = scan.next();
			
			if((prevCar - (int) hm.get(s)) >0) {
				count++;
			}
			
			prevCar = (int) hm.get(s);	
		}
		
		System.out.println(count);
	}
}
```