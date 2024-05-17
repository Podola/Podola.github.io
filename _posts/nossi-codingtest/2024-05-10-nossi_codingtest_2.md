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

1. 고정된 저장 공간이다.
2. 순차적으로 데이터를 저장한다.



#### ·  Random Access

메모리에 저장된 데이터에 접근하려면 주소값을 알아야 한다.

배열 변수는 자신이 할당받은 메모리의 첫 번째 주소값을 가리킨다.

배열은 연속적으로 저장되어 있기 때문에 첫 주소값만 알고 있다면 즉시 접근이 가능하다. **O(1)**



#### · 한계

선언시에 정한 size보다 더 많은 데이터를 저장해야 하는 경우 공간이 남아있지 않아서 문제가 발생한다.

그렇다고 매번 크기가 큰 배열을 선언한다면 메모리 비효율이 발생한다.

<br>

### 🔸Dynamic Array

1. size를 늘릴 수 있다. (리사이징)

2. 일반적으로 2배 큰 크기로 resize 한다. (더블링)



#### · 사용법

선언 시 배열의 크기를 정하지 않아도 되기 때문에 코딩 테스트에서 자주 사용한다.

python에서는 list 자료형을 통해 Dynamic Array를 이미 잘 구현해 두었다.

<br>

#### · 비교

|                 | Static Array | Dynamic Array  |
| --------------- | ------------ | -------------- |
| access / update | O(1)         | O(1)           |
| insert_back     | O(1)         | amortized O(1) |
| delete_back     | O(1)         | O(1)           |
| insert_at       | O(n)         | O(n)           |
| delete_at       | O(n)         | O(n)           |

<br>

### 🔸[예제] Two Sum

**문제**

정수가 저장된 배열 nums가 주어집니다.

nums의 원소 중 두 숫자를 더해서 target이 될 수 있으면 True, 불가능하면 False를 반환하세요. 

같은 원소를 두 번 사용할 수 없습니다. 

<br>

**제약 조건**

case1.   &nbsp; &nbsp;   $$ 2 <= nums.length <= 10^4 $$

case2. $$ -10^9 <= nums[i] <= 10^9 $$

case3. $$ -10^9 <= target <= 10^9 $$ 

<br>

**예시**

input : nums = {4, 1, 9, 7, 5, 3, 16}, target  :14

output : True

<br>

------

**STEP1. 문제 이해**

$$ O(n \log n) $$, 혹은 이보다 빠른 시간 복잡도가 요구된다.

<br>

**STEP2. 접근 방법**

- 직관적으로 해석하기
  - 완전 탐색으로 시작
  - 문제 상황을 단순화
  - 문제 상황을 극한화
- 자료구조와 알고리즘 활용
  - **문제 이해**에서 파악한 내용을 토대로 어떤 자료구조를 사용 할지 결정.
- 메모리 사용
  - 시간 복잡도를 줄이기 위해 메모리를 사용
  - 대표적으로 해시테이블

<br>

#### 1. 반복문

**STEP3. 코드 설계**

완전 탐색으로 진행한다.

#### · pseudocode

```pseudocode
for i  0~ n
    for j = i+1 ~ n
        if nums[i] + nums[j] == 14:
            return true
return false
```

<br>

#### · code

```python
def twoSum(nums, target):
    n = len(nums)
    for i in range(n):
        for j in range(i+1, n):
            if nums[i] + nums[j] == target:
                return True
    return False

print(twoSum(nums[4,1,9,7,5,3,16], target=14))

```

<br>

#### 2. Sort & Two Pointer

**STEP3. 코드 설계**

Two Pointer로 진행한다. 

Two Pointer는 정렬이 된 상황에서 쓰이므로 우선 **정렬**이 필요하다.  $$ O(n \log n) $$

<br>

**pseudocode**

```pseudocode
nums.sort()
l = 0;
r = n-1;

while(l != r):
	if nums[l] + nums[r] == target:
	return True
	if nums[l] + nums[r] > target:
	r = r-1
	else
	l = l+1

return False
```

<br>

**code**

```python
def twoSum(nums, target):
    	nums.sort()
        l, r = 0, len(nums)-1
        
        while l < r:
            if nums[l] + nums[r] > target: r -= r
            elif nums[l] + nums[r] < target: l += l
        	else: return True
        
        return False
```

<br>

## 2️⃣Linked List

1. Node 구조체가 연괼되는 형식으로 데이터를 저장한다.
2. Node는 데이터와 next node의 주소를 저장한다.
3. 메모리상에서는 비연속적이지만 next node를 통해 논리적인 연속성을 갖는다.



### 🔸Node

Linked List는 Node로 이루어져 있다. 

Node를 어떻게 구현하냐에 따라서 Linked List, Tree, Graph가 될 수 있다.

Array List는 python에 이미 있는걸 썼다.

Linked List는 문제에 따라서 내가 어떻게 구현하냐가 중요하다.

<br>

#### · Singly Linked List

```python
class Node:
	def __init__(self, value = 0, next = None):
        self.value = value
        self.next = next
        
class LinkedList(object):
    def __init__(self):
        self.size = 0
        self.head = None        
    
    def insert_back(self, value):
        current = self.head
        while (current.next):
            current = current.next
        new_node = Node(value)
        current.next = new_node
        
    def get(self, idx):
        if idx < 0 || idx >= self.size
        	raise Exception("out of range")
        current = self.head
        for _ in range(idx):
            current = current.next
        return current.value
    
    def insert(self, idx, value):
        new_node = Node(value)
        if idx == 0:
           	new_node.next = self.head
            self.head = new_node
        else:
            current = self.head
            for _ in range(idx-1):
                current = current.next
            new_node.next = current.next
            current.next = new_node                
        
    def remove(self, idx):
        if idx == 0:
            self.head = self.head.next
        current = self.head
        for _ in range(idx-1):
            current = current.next
        current.next = current.next.next        
        
    def print(self):
        current = self.head
        while(current):
            print(current.value, end="")
            current = current.next
            if current:
              print("->", end="")
        print()      
        
```



#### Double Linked List

```python

```

<br>

### 🔸[예제] Design Browser History

<div class="notice">
    💡 Linked List의 코테 적용 방법<br>
    	1. Linked List 자유자재로 구현 (선형 자료구조 + 중간에 데이터 추가/삭제 용이)<br>
    	2. Tree or Graph에 활용
</div>



#### · Two Sum

**문제**

인터넷 브라우저에서 방문기록과 동일한 작동을 하는 BrowerHistory Class를 구현한다.

구현할 브라우저는 homepage에서 시작하고, 이후에는 다른 url에 방문할 수 있다.

"뒤로가기"와 "앞으로 가기"가 작동되도록 구현하라.

- BrowserHistory(string homepage)를 호출하면 브라우저는 homepage에서 시작된다.
- visit(string url)을 호출하면 현재 page의 앞에 있는 페이지 기록은 모두 삭제되고 url로 방문한다.
- back(int step)을 호출하면 step 만큼 "뒤로가기" 한다. 완료되면 현재 url을 리턴한다.
- forward(int step)을 호출하면 step만큼 "앞으로 가기"한다. 완료되면 현재 url을 리턴한다.

<br>

**제약 조건**

case1.   &nbsp; &nbsp;   $$ 1 <= homepage.length <= 20 $$

case2.   &nbsp; &nbsp;   $$ 1 <= url.length <= 20 $$

case3.   &nbsp; &nbsp;   $$ 1 <= step <= 100 $$

homepage와 url은 '.'을 포함한 lower case 영어 문자로 구성되어 있다.

visit, back 그리고 forward는 최대 5000번의 호출이 있을 수 있다.

<br>

**예제**

![example]({{site.url}}\images\2024-05-10-nossi_codingtest_2\example.png)

<br>

------

**STEP1. 문제 이해**

- input 값의 특징 (정수인가? 범위는? 마이너스도 되는가? 소수인가? 자료형은 문자열인가? 등)
- output 값의 특징 (어떤 값을 반환해줘야 하는지, 정해진 형식대로 반환하려면 어떻게 구현할지)
- input size N 확인 (시간 복잡도를 계산하기 위한 N 또는 M이 무엇인지)
- 제약 조건 확인 (시간복잡도 제한, 내가 선택할 수 있는 알고리즘이 무엇인지)
- 예상할 수 있는 오류 파악 (입력값의 범위, stack overflow 등)

<br>

**STEP2. 접근 방법**

- 직관적으로 해석하기
  - Input, Output을 보자.
- 자료구조와 알고리즘 활용
  - **문제 이해**에서 파악한 내용을 토대로 어떤 자료구조를 사용 할지 결정
  - 대놓고 특정 자료구조와 알고리즘을 묻는 문제도 많음
- 메모리 사용
  - 시간 복잡도를 줄이기 위해 메모리를 사용
  - 대표적으로 해시테이블

<br>

**STEP3. 코드 설계**

완전 탐색으로 진행한다.

<br>


***

<br>

    이 글은 개발남노씨님의 인프런 강의 코딩테스트 [ALL IN ONE]을 정리하여 작성했습니다.
    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}