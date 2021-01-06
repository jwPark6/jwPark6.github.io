---
title: "동계 모각코 2주차"
---

### 계획
  - 알고리즘 정렬 개념 숙지 및 복습(인프런 강의를 통해 복습예정) 
  - 간단한 예제의 코드 이해, 나아가서 백준 문제풀이를 목표로 함

### 결과
  - 인프런 강의를 먼저 학습하여 이론적 부분, 기존에 학습했던 개념을 복습위주로 빠르게 훝어봤다.

  ![image](https://user-images.githubusercontent.com/67006945/103775605-9ff39780-5071-11eb-9773-f505cb36a316.png)  
  
  이후 백준 문제를 실제로 풀어봤는데, [11399] 번 정렬문제를 퀵정렬을 사용하여 해결하였다.  
  
  ![image](https://user-images.githubusercontent.com/67006945/103776010-32943680-5072-11eb-9699-d97a697da061.png)  
  
  아래는 작성한 코드이다.  


  
```
  import java.util.Scanner;

  class Sort{
    public int partition(int[] aList, int left, int right) {
      
      this.swap(aList, left, right);//양 원소를 교환
      long pivotElement = aList[left];//left의 원소 저장
      int toRight = left;//교환된 값들을 저장
      int toLeft = right + 1;
      do {
        do {toRight++;} while(aList[toRight] < pivotElement);//pivot보다 큰 원소를 찾을 때까지 증가
        do {toLeft--;} while(aList[toLeft] > pivotElement);//pivot보다 작은 원소를 찾을 때까지 감소
        if(toRight < toLeft) {//서로 교차하지 않았을 때
          this.swap(aList, toRight, toLeft);//두 원소 교환
        }	
      }while(toRight < toLeft);//교차하지 않았을 때 반복
      this.swap(aList, left, toLeft);//분할이 끝난 후 left를 대략 중앙의 위치로 이동
      return toLeft;//pivot의 인덱스를 반환
    }
    
    public void sortRecur(int[] aList, int left, int right) {
      if(left < right) {//right가 클 때
        int mid = partition(aList, left, right);//분할된 pivot을 저장
        sortRecur(aList, left, mid - 1);//pivot을 기준으로 재귀함수 호출
        sortRecur(aList, mid+1, right);
      }
    }
    public boolean sort(int[] aList) {//정렬 함수
      if(aList.length < 1) {//길이가 1보다 작을 때
        return false;
      }
      if(aList.length > 1) {//길이가 1보다 클 때
        int maxLoc = 0;//최대값 초기화
        for(int i = 1; i < aList.length; i++) {//전체 크기만큼 반복
          if(aList[maxLoc] < aList[i]) {
            maxLoc = i;//i번째 값이 크면 변경
          }
        }
        this.swap(aList, maxLoc, aList.length-1);//마지막 인덱스로 이동
        this.sortRecur(aList, 0, aList.length-2);//해당값으로 재귀함수 호출
      }
      return false;
    }

    
    private void swap(int[] aList, int i, int j) {//원소 교환 함수
      int tempElement = aList[i];
      aList[i] = aList[j];
      aList[j] = tempElement;
    }
  }

  public class Main {
    public static void main(String[] args) {
      Scanner scan = new Scanner(System.in);
      
      int inputPersonNum = scan.nextInt();
      int[] personTime = new int[inputPersonNum];
      
      for(int i = 0; i<inputPersonNum; i++) {
        personTime[i] = scan.nextInt();
      }
      
      Sort s = new Sort();		
      s.sort(personTime);	
      long sum = 0;	
      for(int i=0; i<inputPersonNum; i++) {
        for(int j = 0; j <= i; j++) {				
          sum += personTime[j];		
        }
      }		
      System.out.println(sum);
    }
  }
```
  - 이외에도 2170번을 풀고자 하였으나, 아쉽게도 해결하지 못하였고 이는 추후 해결하기로 하였다.