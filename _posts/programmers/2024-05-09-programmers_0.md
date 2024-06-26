---
title: "[코딩 테스트] 0. 들어가기에 앞서"

categories: 
    - 프로그래머스
tag: 
    - [C++ 프로그래밍, 코딩 테스트, 알고리즘, 자료구조]
toc: true

date: 2024-05-09
last_modified_at: 2024-05-09
---

본격적으로 문제 풀이를 시작하기 전, 간단한 문제들로 몸을 풀어 보자.



## 1️⃣ 문자열

#### 1. 부분 문자열

```c++
//- 1. 부분 문자열
string s = "podola";
string sub = s.substr(0, 2);				//substr(index, length)


//- 2. 숫자를 문자열로
int num = 1234;
string s = to_string(num);


//- 3. 문자열을 숫자로
string s = "1234";
int num = stoi(s);


//- 4. 소문자로
string s = "ABCD";
for_each(s.begin(), s.end(), [](char& c) { c = tolower(c); });


// -5. 대문자로
string s = "abcd";
for_each(s.begin(), s.end(), [](char& c) {c = toupper(c); });


// -6. 각 자리의 숫자의 합
int answer = 0;						// answer = 1 + 2 + 3 + 4 + 5
string s = "12345";
for(char& c : s)
    answer += c - '0';


// -7. 배열을 홀짝으로 나누어 합하기
int answer = 0;						// answer = "153" + "4628"
vector<int> v = {1, 4, 5, 6, 3, 2, 8};
string odds = "";
string evens = "";
for(int n : v)
{
    if(n & 1)
        odds += n + '0';

    else
        evens += n + '0';
}
answer = stoi(odds) + stoi(evens);


// -8. 문자열 일부 치환
string s = "ABGGABD";
string findStr = "AB";
string changeStr = "XXX";

while(true)
{
    int pos = s.find(findStr);				// find(string, offset);
    if(pos == -1)
        break;
    replace(pos, findStr.size(), changeStr);		// replace(offset, size, newString)
    
}


// -9. 접두사
bool answer = true;					// answer == true면 접두사 존재
string s = "banana";
string prefix = "ba";
for(int i = 0; i < prefix.size(); i++)
{
    if(prefix[i] != s[i])
    {
        answer = false;
        break;
	}
}


// -10. A 강조하기
string s = "PodOLa";					// A가 아닌 대문자는 소문자로, a는 A로
for(char& c : s)
{
    if(c == 'a')
        c = 'A';
    if(c > 'A' && c <= 'Z')
        c += 'a' - 'A';					// c = tolower(c)
}


// -11. 부분 문자열 찾기
bool answer = true;					// answer == true면 부분 문자열 존재
string s = "banana";
string findStr = "ana";
int pos = s.find(findStr);
if(pos == -1)
    answer = false;


// -11. 부분 문자열 등장 횟수
int answer = 0;
int pos = 0;
string s = "banana";
string findStr = "ana";
while(true)
{
    pos = s.find(findStr, pos);
    if(pos == -1)
        break;
    answer++;
    pos++;
}

	
// -12. 공백으로 구분
vector<string> answer;
string s = "i love     you";
string tempStr = "";


// -13. 꼬리 문자열


// -14. 글자 지우기


// -15. s~e 뒤집기


// -16. a, b, c로 구분


// -17. 긴 두수의 합


```



## 2️⃣ 정렬








***

<br>

    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
