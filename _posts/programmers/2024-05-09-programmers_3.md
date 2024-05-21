---
title: "[코딩 테스트] 3. 모의고사"

categories: 
    - 프로그래머스
tag: 
    - [python, 코딩 테스트, 알고리즘, 자료구조]
toc: true

date: 2024-05-09
last_modified_at: 2024-05-09




---

## 1️⃣ 문제



![모의고사](D:\Blog\podola.github.io\images\2024-05-09-programmers_3\모의고사.png)

## 2️⃣ 생각

각각 수포자들의 기본 패턴을 리스트로 만들어  answers와 비교하면 되겠다.



## 3️⃣ 풀이

```python
def solution(answers):
    answer = []
    
    student1 = [1,2,3,4,5]
    student2 = [2,1,2,3,2,4,2,5]
    student3 = [3,3,1,1,2,2,4,4,5,5]
    
    temp = [0,0,0]
    # answers:  1 2 3 4 5
    # loop:     0 ~ 4
    for i in range(len(answers)):
        if answers[i] == student1[i%len(student1)]:
            temp[0] += 1
        if answers[i] == student2[i%len(student2)]:
            temp[1] += 1
        if answers[i] == student3[i%len(student3)]:
            temp[2] += 1
            
    for i in range(len(temp)):
        if temp[i] == max(temp):
            answer.append(i+1)    
    
    return answer
```

파이썬으로 인덱스 써서 푸는게 아직 어색하다.

처음에 i 대신에 i1,i2,i3, cnt1,cnt2,cnt3 변수를 왕창 추가했다.

핵심은 반복되는 패턴을 배열로 만들어서 비교하는것.

그리고 temp 리스트로  정답 개수를 기록하는 것이다.


***

<br>

    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
