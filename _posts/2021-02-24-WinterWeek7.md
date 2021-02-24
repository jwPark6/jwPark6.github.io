---
title: "동계 모각코 못다한 문제들"
---

### 결과
  - 지난 동계 모각코 활동중 아쉽게도 해결하지 못한 문제들을 추후 해결하였다.

  - 첫 번째로 백준 2002번인 추월문제이다.

  ![image](https://user-images.githubusercontent.com/67006945/108970973-6c260d00-76c5-11eb-8ca9-2bac24e5ce26.png)

- 기존에는 내가 작성한 코드가 맞다고 생각하였는데 실제로는 정답을 얻지 못하였다. 해결방안을 찾기 위해 여러 글을 보던 중 위 문제가 올림피아드 	 제출문제라는 것을 알고 여러 테스트 케이스를 직접 넣어보며 잘못된 부분을 알 수 있었다.

  아래는 작성한 코드이다.

```
import java.util.Scanner;
import java.util.HashMap;

public class Main {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);

		HashMap hm = new HashMap();
		HashMap hm2 = new HashMap();

		int numberOfCar = scan.nextInt();
		String[] carNameIn = new String[numberOfCar];
		String[] carNameOut = new String[numberOfCar];
		
		int[] wrongCar = new int[numberOfCar];
		String s;
		for (int i = 0; i < numberOfCar; i++) {
			s = scan.next();
			carNameIn[i] = s;

			hm.put(s, i);
		}

		int count = 0;

		for (int i = 0; i < numberOfCar; i++) {
			s = scan.next();
			carNameOut[i] = s;
			
			hm2.put(s, i);
		}

		for (int i = 0; i < numberOfCar; i++) {
			int n = (int) hm.get(carNameOut[i]);
			
			for (int j = n + 1; j < numberOfCar; j++) {
				if (wrongCar[j] == 0 && i > (int) hm2.get(carNameIn[j])) {
					wrongCar[j] = 1;
					count++;
				}
			}
		}

		System.out.println(count);
	}
}
```

- 위 문제는 터널을 들어간 차량과 터널을 나온 차량의 번호판을 Key로 순서를 Value로 각각의 해쉬맵에 저장하여 기존의 인덱스보다 추월할 경우   Count를 세는 방식으로 해결하였다.

- 두 번째 문제는 백준 2170번인 선 긋기 문제이다.

![image](https://user-images.githubusercontent.com/67006945/108972121-58c77180-76c6-11eb-9733-bcca1214449f.png)

```
public class Main {

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

		int tryNum = Integer.parseInt(bf.readLine());
		int[][] point = new int[tryNum][2];

		for (int i = 0; i < tryNum; i++) {
			StringTokenizer st = new StringTokenizer(bf.readLine());
			point[i][0] = Integer.parseInt(st.nextToken());
			point[i][1] = Integer.parseInt(st.nextToken());
		}

		Arrays.sort(point, new Comparator<int[]>() {
			public int compare(int[] t1, int[] t2) {
				return t1[0] - t2[0];
			}
		});

		int minPointX = point[0][0], maxPointY = point[0][1];
		int sum = 0;

		for (int i = 1; i < tryNum; i++) {
			if (point[i][0] <= maxPointY) {
				if (maxPointY < point[i][1]) {
					maxPointY = point[i][1];
				}
			} else {
				sum += maxPointY - minPointX;
				minPointX = point[i][0];
				maxPointY = point[i][1];			
			}
		}
		sum += maxPointY - minPointX;
		bw.write(Integer.toString(sum));
		bw.flush();
		bw.close();
	}
}
```

- 위 문제는 먼저 두 점이 저장된 이차원배열을 0번째 열을 기준으로 오름차순으로 정리하였다. 이렇게 하면 X 를 기준으로 정리가 되고 하나의 선을 기준으로 다음 선들과 비교하며 겹칠경우 병합하고 겹치지 않을 경우 그 선을 따로 sum 에 더하는 방식으로 최종적인 선들의 길이를 구하였다.

- 마지막으로 백준 10825번이다.

![image](https://user-images.githubusercontent.com/67006945/108972661-e4d99900-76c6-11eb-91c7-bc65f9986b79.png)

```
class Person implements Comparable<Person>{
	String name;
	int kor;
	int eng;
	int mat;
	
	public Person(String n, int k, int e, int m) {
		this.name = n;
		this.kor = k;
		this.eng = e;
		this.mat = m;
	}

	@Override
	public int compareTo(Person p) {
		// TODO Auto-generated method stub\
		if(this.kor > p.kor) {
			return -1;
		}
		else if(this.kor == p.kor) {
			if(this.eng < p.eng) {
				return -1;
			}
			else if(this.eng == p.eng) {
				if(this.mat > p.mat) {
					return -1;
				}
				else if(this.mat == p.mat) {
					if(this.name.compareTo(p.name) < 0) {
						return -1;
					}
					else if(this.name.compareTo(p.name) == 0) {
						return 0;
					}
					else {
						return 1;
					}
				}
				else {
					return 1;
				}
			}
			else {
				return 1;
			}	
		}
		else {
			return 1;
		}
	}
}

public class Main {
	public static void main(String[] args) throws IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		
		int tryNum = Integer.parseInt(bf.readLine());
		String name;
		int kor;
		int eng;
		int mat;
		Person[] person = new Person[tryNum];
		
		for(int i = 0; i < tryNum; i++) {
			StringTokenizer st = new StringTokenizer(bf.readLine());
			name = st.nextToken();
			kor = Integer.parseInt(st.nextToken());
		    eng = Integer.parseInt(st.nextToken());
			mat = Integer.parseInt(st.nextToken());
			person[i] = new Person(name, kor, eng, mat);
		}
		
		Arrays.sort(person);
		
		for(int i = 0; i < tryNum; i++) {
			bw.write(person[i].name+"\n");
		}
		bw.flush();
		bw.close();
	}
}
```

- 위 문제는 다시 풀어보니 생각보다 간단한 원리였다.

  각 이름과 점수들을 객체를 생성하여 저장한 뒤 객체들을 비교하는 방식으로 해결하였다. 

  이 때 객체끼리 비교하게 되면 비교대상이 문제가 되는데, 이를 위해 compareTo 메소드를 Override 하여 국영수, 이름들을 비교하여 return 값을 설정해주었다. 이렇게 새로 작성된 메소드를 통해서 객체들의 값을 비교하여 원하는 결과를 얻을 수 있었다.