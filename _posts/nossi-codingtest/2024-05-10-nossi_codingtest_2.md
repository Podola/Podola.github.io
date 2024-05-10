---
title: "[코딩 테스트] 2. List"

categories: 
    - 개발남노씨 코딩 테스트
tag: 
    - [python, 코딩 테스트, 알고리즘, 자료구조]
toc: true

date: 2024-05-10
last_modified_at: 2024-05-10

---

## 1️⃣ Array List

배열은 선언 시 size를 정하여 해당 size만큼 연속된 메모리를 할당 받아 data를 순차적으로 저장하는 자료구조이다.



### 🔸Static Array

1. 고정된 저장 공간
2. 순차적인 데이터 저장

#### ·  Random Access

메모리에 저장된 데이터에 접근하려면 주소값을 알아야 한다.

배열 변수는 자신이 할당받은 메모리의 첫 번째 주소값을 가리킨다.

배열은 연속적으로 저장되어 있기 때문에 첫 주소값만 알고 있다면 어떤 index에 **즉시 접근**이 가능하다. **O(1)**



#### ·  한계

선언시에 정한 size보다 더 많은 데이터를 저장해야 하는 경우 공간이 남아있지 않아서 문제가 발생한다.

그렇다고 매번 크기가 큰 배열을 선언한다면 메모리 비효율이 발생한다.



### 🔸Dynamic Array

선언 이후에 size를 변경할 수 없는 Static Array와 다르게 Dynamic Array는 size를 늘릴 수 있다. (리사이징)

일반적으로 2배 큰 크기로 resize 한다. (더블링)



#### 사용법

선언 시 배열의 크기를 정하지 않아도 되기 때문에 코딩 테스트에서 자주 사용한다.

python에서는 list 자료형을 통해 Dynamic Array를 이미 잘 구현해 두었다.



### 🔸비교

|                 | Static Array | Dynamic Array  |
| --------------- | ------------ | -------------- |
| access / update | O(1)         | O(1)           |
| insert_back     | O(1)         | amortized O(1) |
| delete_back     | O(1)         | O(1)           |
| insert_at       | O(n)         | O(n)           |
| delete_at       | O(n)         | O(n)           |



### 🔸[코테 적용] 반복문





### 🔸[코테 적용] two pointer







## 2️⃣Linked List

### 🔸메모리



메모리의 연속적인 공간을 사용하는 배열과 불연속적인 공간을 사용하는 리스트는 상황에 맞춰 사용해야 한다.



## 3️⃣ 시간 복잡도

### 🔸Big-O 표기법



Worst case는 Average case가 같은 경우가 많고, 비교적 구하기 이를 사용해 알고리즘의 시간 복잡도를 나타낸다.



#### ·  시간 복잡도 비교



### 🔸제약 조건





#### ·  Two Sum






***

<br>

    이 글은 코드조선님의 인프런 강의 Go Hard to Unreal를 정리하여 작성했습니다.
    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}





1️⃣2️⃣3️⃣4️⃣5️⃣6️⃣7️⃣8️⃣9️⃣🔟0️⃣



## 0️⃣ 대제목



### 🔸중제목



#### ·  소제목



{: .notice--warning}

🚀 결과

{: .notice--info}

💡 정보