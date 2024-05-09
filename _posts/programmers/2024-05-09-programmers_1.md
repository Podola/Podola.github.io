---
title: "[코딩 테스트] 1. 저주의 숫자 3"

categories: 
    - 프로그래머스
tag: 
    - [C++ 프로그래밍, 코딩 테스트, 알고리즘, 자료구조]
toc: true

date: 2024-05-09
last_modified_at: 2024-05-09



---

## 1️⃣ 문제

![problem]({{site.url}}\images\2024-05-09-programmers_1\problem.png)



{: .notice--info}

💡 정보

정수 n이 주어지면 3의 배수이거나 3을 포함하면 스킵하고 카운팅하는 문제이다.

## 2️⃣ 풀이

```c++
#include <string>
#include <vector>
using namespace std;

int solution(int n)
{
    int answer = 0;
    
    for(int 1 = 1; i <= n; i++)
    {
        answer++;
        
        // answer가 3의 배수거나 3을 포함하지 않을 때까지
        while(answer % 3 == 0 || to_string(answer).find('3') != -1)
            answer++;
	}
    
    return answer;
}
```



## 3️⃣ 해설

| i    | answer |
| ---- | ------ |
| 1    | 0 -> 1 |
| 2    | 1 -> 2 |

i가 n까지 1씩 증가 할 때, answer도 1씩 증가한다.

<br>

| i    | answer      |
| ---- | ----------- |
| 3    | 2 -> 3 -> 4 |
| 4    | 4-> 5       |

증가된 answer가 3의 배수거나 3을 포함하고 있으면, 그렇지 않을 때까지 answer를 1씩 증가 시킨다.

answer가 3의 배수거나 3을 포함하고 있지 않으면, while문을 탈출하여 i와 함께 1씩 증가한다.








***

<br>

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