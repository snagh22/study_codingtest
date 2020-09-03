# study_codingtest

## 1. GREEDY

"현재 상황에서 지금 당장 좋은 것만 고르는 방법"

* 대체로 정렬 알고리즘과 짝을 이룸 

### 대표예제 - 거스름돈 

**point** - 가장 큰 화폐 단위부터 거슬러 주는 것 

    n= 1260 
  
    count=0

    coin=[500, 100, 50, 10]
  
    for c in coin:
  
      count += n//c
    
      n%=c
    
    print(count)

화폐의 종류 K개라면 시간복잡도 O(K)

### 1. 큰 수의 법칙


주어진 수들을 m번 더하여 가장 큰 수를 만드는 법칙. 단, 특정 수가 연속해서 k번을 초과하여 더해질 수 없다.

ex1) [2, 4, 5, 4, 6] m=8, k=3일 때 -> 6 + 6 + 6 + 5 + 6 + 6 + 6 + 5 = 46

ex2) [3, 4, 3, 4, 3] m=7, k=2일 때 -> 4 + 4 + 4 + 4 + 4 + 4 + 4 = 28


**입력 예시**                        

5 8 3                                 

2 4 5 4 6

 **출력 예시**

46

**point** - 가장 큰 수를 k번 더하고 두 번째로 큰 수를 한 번 더하는 연산 

    n,m,k = map(int,input().split())
    array = list(map(int,input().split()))

    array.sort()
    first= array[-1]
    second = array[-2]

    result = 0

    while True:
        for i in range(k):
            if m==0:
                break
            result += first
            m -= 1
        
        if m==0:
            break
        result += second
        m -= 1
    
    print(result)
    
##### m의 크기가 100억 이상이라면 더 효율적인 방법이 필요

**point** - 반복되는 수열에 대해 파악

    n,m,k = map(int,input().split())
    array = list(map(int,input().split()))

    array.sort()
    first= array[-1]
    second = array[-2]

    result = 0

    count=int(m/(k+1))*k + m%(k+1)
    result+=first*count
    result+=second*(m-count)

    print(result)        


