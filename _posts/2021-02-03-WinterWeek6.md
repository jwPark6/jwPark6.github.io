---
title: "동계 모각코 6주차"
---

### 계획
  - 동적계획법 학습 및 정리, 미숙한 부분, 최종적인 부분들 확인
  - 간단한 예제의 코드 이해, 백준 문제풀이를 목표

### 결과
  - 먼저 인프런 강의를 통해 개념을 학습하였다. 제일 부족한 부분이여서 그런지 개념자체가 살짝 생소한 감이 있었다.

  ![image](https://user-images.githubusercontent.com/67006945/107143156-c3fb0f00-6976-11eb-8b1d-e4a2aa0fcd01.png)
  
  - 다음으로 백준 1003번 피보나치 수열을 풀었다. 보통 이러한 문제는 재귀를 통해 풀지만 문제가 원하는 0, 1 의 사용여부를 알기 위해서는 소문제부터 탐색할 필요가 있었다.

 ![image](https://user-images.githubusercontent.com/67006945/107143172-e5f49180-6976-11eb-956f-725a32dcaf41.png)

 - 이를 해결하기 위해 배열을 사용하여 n 차 피보나치 함수의 결과를 각각 저장하고 이미 연산으로 알아낸 결과라면 또 다시 재귀처럼 연산을 하지 않게 작성하였다.


  아래는 작성한 코드이다.
```
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class Main {
	public static void fibo(int n, int[] zero, int[] one) {			
		for(int i = 2; i <= n; i++) {
			if(zero[i] == 0) {	
				zero[i] = zero[i-1] + zero[i-2];
				one[i] = one[i-1] + one[i-2];
			}
		}	
	}
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		int testCase = Integer.parseInt(bf.readLine());
		int[] inputN = new int[testCase];
		
		int[] countZero = new int[41];
		int[] countOne = new int[41];
		countZero[0] = 1;
		countZero[1] = 0;
		countOne[0] = 0;
		countOne[1] = 1;
		
		for(int i = 0; i < testCase; i++) {
			int n = Integer.parseInt(bf.readLine());
			fibo(n, countZero, countOne);	
			inputN[i] = n;
		}
		
		for(int i = 0; i < testCase; i++) {
			bw.write(Integer.toString(countZero[inputN[i]]) + " " + Integer.toString(countOne[inputN[i]]) + "\n");
		}
		bw.flush();
		bw.close();
	}
}

```

- 처음에는 Scanner를 사용하여 입출력을 처리하였으나, 확실히 여러 배열을 사용하여 그런지 시간이 더 소요되었고 이로 인하여 백준에서 시간초과가 발생하였다. 시간을 줄이기 위해 고민하다 Buffer 를 사용하면 입출력의 시간을 감소할 수 있을거라 생각하고 코드를 수정하니 해결할 수 있었다. 평소에는 생각하지 않던 단순한 입출력도 프로그램의 성능에 영향을 끼친다는 사실을 다시금 깨닫게 해주었다.

- 이 외에도 지금까지 짧은 주차동안 여러 과정을 할려고 했더니 확실히 아쉬운 부분들이 존재하였다. 개념을 복습하는데 급급하여 문제를 해결하지 못한 부분도 많았고 문제를 해결하고 싶어서 개념을 미숙하게 처리된 부분도 있었다. 비록 계획한 주차는 끝났지만 시간이 된다면 추가적으로 학습을 하고 싶은 마음이 있다.