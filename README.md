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


### 2. 숫자 카드 게임 

1. n 행, m 열

2. 선택된 행에 포함된 카드들 중 가장 낮은 숫자 카드를 뽑아야 함 

3. 최종적으로 작은 숫자 카드 중 가장 높은 숫자의 카드 뽑기

**입력예시**

3 3

3 1 2

4 1 4

2 2 2 

**출력예시**

2

**point** - 각 행마다 가장 작은 수를 찾은 뒤에 그 수 중에서 가장 큰 수 찾기

* min()함수 이용
    n,m = map(int,input().split())
    result=0
    for i in range(n):
        data=list(map(int,input().split()))
        min_value = min(data)
        result=max(min_value,result)
    print(result)


* 2중 반복문 이용

    n,m = map(int,input().split())
    result=0

    for i in range(n):
        data=list(map(int,input().split()))
        min_value=100001

        for a in data:
            if a<min_value:
                min_value=a
        result = max(result,min_value)

    print(result)

### 3. 1 만들기

n과 k가 주어질 때 n이 1이 될 때까지 조건 1번 혹은 2번을 수행해야 하는 최소 횟수를 구하는 프로그램

<조건> 

1. n에서 1을 뺀다

2. n을 k로 나눈다 (n이 k로 나누어떨어질 때)

ex) n = 17, k = 4 일 때, 17 -> 16 -> 4 -> 1 답: 3

**입력예시**

25 5

**출력 예시**

2

**point** - 최대한 많이 나누기 
    
    n,k= map(int,input().split())
    result = 0
    
    while n>=k:
        while n%k != 0:
            n-=1
            result+=1
            
        n//=k
        result+=1
        
    while n>1:
        n-=1
        result+=1
    print(result)


* n이 100억 이상의 큰 수가 되는 경우 n이 k의 배수가 되도록 작성

        n,k = map(int,input().split())
        result = 0

        while True:
            # -1해주기
            target = (n//k)*k
            result +=(n-target)
            n=target

            if n<k:
                break
            #k로 나누기
            result +=1
            n//=k
        #남은 수에 대해 1씩 빼기
        result +=(n-1)
        print(result)

