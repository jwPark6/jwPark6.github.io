---
title: "동계 모각코 5주차"
---

### 계획
  - 알고리즘 그래프 개념 복습 및 정리
  - 간단한 예제의 코드 이해, 백준 문제풀이를 목표

### 결과
  - 먼저 인프런 강의를 통해 그래프의 기초적인 내용인 DFS, BFS를 복습하였다.
  
  ![image](https://user-images.githubusercontent.com/67006945/106001729-a961a400-60f3-11eb-8ded-29647eed9d22.png)
  
  - 다음으로 백준 1012번 유기농 배추문제를 풀었다. DFS를 사용하여 인접그래프를 탐색하는 문제이다.

  ![image](https://user-images.githubusercontent.com/67006945/106002119-15dca300-60f4-11eb-9758-246872c46964.png)

  만약 위처럼 배추가 배치되었다고 할 때, 인접한 배추에는 한마리의 흰지렁이가 배치될 수 있고 최소한으로 배치되는 흰지렁이를 구하는 문제이다.

  아래는 작성한 코드이다.
```
import java.util.Scanner;

public class Main {
	static int totalCol = 0;
	static int totalRow = 0;
	
	public static boolean scanCabbage(int row, int col, int[][] cabbage, int[][] visit) {
		
		if(col < totalCol && row < totalRow && col >= 0 && row >=0 && cabbage[row][col] == 1 && visit[row][col] != 1) {
			visit[row][col] = 1;
			
			if(col+1 < totalCol && cabbage[row][col+1] == 1) {
				
				scanCabbage(row, col+1, cabbage, visit);
			}
			if(row+1 < totalRow && cabbage[row+1][col] == 1) {
				
				scanCabbage(row+1, col, cabbage, visit);
			}
			if(row-1 >= 0 && cabbage[row-1][col] == 1) {
				
				scanCabbage(row-1, col, cabbage, visit);
			}
			if(col-1 >= 0 && cabbage[row][col-1] == 1) {
				
				scanCabbage(row, col-1, cabbage, visit);
			}
			
			return true;
		}
		else {
			return false;
		}
	}
	
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		int testCase = scan.nextInt();
		int[][] cabbage = null;
		int[][] visit = null;
		
		int[] count = new int[testCase];
		
		for(int k = 0; k < testCase; k++) {
			totalCol = scan.nextInt();
			totalRow = scan.nextInt();
			int numberOfCabbage = scan.nextInt();
			
			cabbage = new int[totalRow][totalCol];
			visit = new int[totalRow][totalCol];
			
			for(int j = 0; j < numberOfCabbage; j++) {
				int col = scan.nextInt();
				int row = scan.nextInt();
				
				cabbage[row][col] = 1;
			}
			
			for(int i = 0; i < totalRow; i++) {
				for(int j = 0; j < totalCol; j++) {
					if(scanCabbage(i, j, cabbage, visit)) {
						count[k]++;
					}
				}
			}
			
		}
		for(int i = 0; i < testCase; i++) {
			System.out.println(count[i]);
		}			
	}
}
```

- 재귀와 융합되는 구조인지라 처음에는 코드가 복잡해질까봐 시도하지 않았는데 실제로 시도해보니 생각보다 간단한 코드라 다행히 해결할 수 있었다.