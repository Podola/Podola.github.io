---
title: "[언리얼5] 2. 언리얼 자료구조"

categories: 
    - UE5
tag: 
    - [언리얼 프로그래밍, 게임 프로그래밍]
toc: true

date: 2024-05-04
last_modified_at: 2024-05-04
---

## 1️⃣ 언리얼 문자열

### 🔸인코딩 방식

인코딩 방식의 다양성은 게임 개발의 유지보수에 큰 영향을 미친다.

언리얼은 UTF-16 방식을 기본으로 채택했다.



### 🔸FString

#### · 실습

```c++
// SGameInstance.cpp

...
    
void USGameInstance::Init()
{
    ...
    
   	TCHAR TextArray[] = TEXT("Hello Unreal");
    // UTF-16 인코딩의 문자열을 생성하기 위한 언리얼 표준 문자 타입이 TCHAR.
    // TCHAR 자료형 변수에 문자열을 저장하기 위해서 TEXT() 매크로 제공.
    
    FString String1 = TextArray;
    // TCHAR 배열을 Wrapping한 헬퍼 클래스가 FString.
    
    UE_LOG(LogTemp, Log, TEXT("String1: %s"), *String1);
    // FString에 *을 붙혀줘야 TCHAR 배열이 반환됨.
    
    if (true == String1.Contains(TEXT("Unreal"),  ESearchCase::IgnoreCase))
    {
        int32 Index = String1.Find(TEXT("Unreal"), ESearchCase::IgnoreCase))
        FString String2 = String1.Mid(Index);
        // "Unreal" 문자열이 시작되는 곳부터 마지막까지 자름.
	}
    
    int32 IntValue = 15;
    float FloatValue = 3.141592f;
    
    FString IntString = FromInt(IntValue);
    FString FloatString = SanitizeFloat(FloatValue);
}
```



### 🔸FName과 FText

FString은 FName과 FText로 변환 가능하다.



#### · FName

에셋 관리를 위한 문자열 클래스이다.

에셋 관리에 문자열을 그대로 사용하면 연산량이 늘어나므로, 내부적으로 해시값으로 변환하여 사용한다.

한번 선언하면 int32와 같은 정수로 변환되어 다시 원본 문자열로의 변경이 불가능하다. (대소문자 구분 없음)

언리얼은 FName과 관련된 전역 Pool 자료구조를 가지고 있다.



#### · FText

다국어 지원을 위한 문자열 클래스이다.

UI에서 자주 사용된다.



#### · 실습

```c++
#include SGameInstance.cpp

...
    
void USGameInstance::Init()
{
    FName KeyName1(TEXT("ZELDA"));
    FName KeyName2(TEXT("zelda"));
    // KeyName1 == KeyName2
    
    for (int i = 0; i < 10000; ++i)
    {
        FName SearchInNamePool = FName(TEXT("zelda"));
        const static FName StaticOnlyOnce(TEXT("zelda"));
        // FName은 전역 Pool을 조사하는 작업이 수반됨.
        // 그래서 static 키워드를 통해 재조사가 이뤄지지 않게 함.
	}
}

```



## 2️⃣ 컨테이너

언리얼 엔진이 자체 제작해서 제공하는 자료구조 라이브러리. (UCL)

STL은 많은 기능이 구현되어 있어 컴파일 시간이 오래 걸린다.

반대로 UCL은 게임 제작에 최적화 되어 있다.



### 🔸TArray

#### ·  개요

STL의 Vector와 유사하다.

언리얼 오브젝트를 순차적으로 담아 관리한다.

게임 제작에서는 TArray같은 가변 배열 자료구조를 효과적으로 활용해야 한다.

데이터가 순차적으로 나열되어 있어 메모리를 효율적으로 사용하고 캐시 효율이 높다.

캐시 지역성으로 인한 성능 향상은 굉장히 중요하다.

임의 데이터 접근이 빠르고, 고속으로 원소 순회하 것이 가능하다.

가변 배열의 단점은 중간값의 삽입/삭제의 비용이 크다.

데이터가 많을수록 검색, 삽입, 삭제가 느려진다.

많은 수의 데이터를 검색, 삽입, 삭제할 경우에는 TSet을 사용한다.



#### ·  실습

```c++
// SGameInstance.cpp

...
    
void USGameInstance()::Init()
{
    int32 ArraySize = 6;
    TArray<int32> IntArray;
    
    for (int32 i = 1; i <= ArraySize; i++)
    {
        IntArray.Add(i);
	}
    
    for (Element : IntArray)
    {
        int32 i = 0;
        UE_LOG(LogTemp, Log, TEXT("[%d]: %d"), i++, Element);
	}
    UE_LOG(LogTemp, Log, TEXT("====="));
    
    IntArray.RemoveAll([](int32 InElement)->bool { return 0 == InElement % 2; });
    
    for (Element : IntArray)
    {
        int32 i = 0;
        UE_LOG(LogTemp, Log, TEXT("[%d]: %d"), i++, Element);
	}
    UE_LOG(LogTemp, Log, TEXT("====="));
    
}
```

{: .notice--warning}

🚀 결과

![TArray]({{site.url}}\images\2024-05-01-2_unreal_data_structure\TArray.png)



### 🔸TSet

STL의 Unoredered Set과 유사하다.

중복되지 않는 키를 관리한다.



#### ·  실습

```c++
// SGameInstance.cpp

...
    
void USGameInstance()::Init()
{
    
}
```



### 🔸TMap

STL의 Unordered Map과 유사하다.

중복되지 않는 키-벨류 쌍의 자료를 관리한다.



#### ·  실습

```c++
// SGameInstance.cpp

...
    
void USGameInstance()::Init()
{
    
}
```






***
<br>

    이 글은 코드조선님의 인프런 강의 Go Hard to Unreal를 정리하여 작성했습니다.
    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}

