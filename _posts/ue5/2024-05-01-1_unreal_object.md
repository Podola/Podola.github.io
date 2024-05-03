---
title: "[언리얼5] 1. 언리얼 오브젝트"

categories: 
    - UE5
tag: 
    - [언리얼 프로그래밍, 게임 프로그래밍]
toc: true

date: 2024-05-01
last_modified_at: 2024-05-01
---

## 1️⃣ 언리얼 오브젝트란

### 🔸최적화와 유지보수

게임은 플레이어를 위해서 최대한 최적화하여 누구나 플레이 가능해야 한다.

또한 개발자를 위해서 규모가 커져도 실수 없이 관리돼야 한다.

c++은 메모리를 직접 관리하여 최적화가 가능하나 메모리 누수 등 유지보수가 까다롭다.

이러한 필요성에 의해 언리얼은 후발 언어의 기능들을 포함한 언리얼 c++을 만들었다.

이 기능들을 지원하는 클래스가 **언리얼 오브젝트 클래스**이다.

### 🔸게임 인스턴스 클래스

예시로 언리얼 오브젝트 클래스의 하나인 **게임 인스턴스** 클래스를 생성해보자.

GameInstance 부모 클래스 > Public > "SGameInstance"

```c++
// SUnrealObjectClass.h

#include "CoreMinimal.h"
#include "Engine/GameInstance.h"
#include "SGameInstance.generated.h"

UCLASS()
class STUDYPROJECT_API USGameInstance : public UGameInstance
{
    GENERATED_BODY()
}
```

```c++
// SGameInstance.cpp
#include "SUnrealObjectClass.h"
```

{: .notice}

접두사 S는 프로젝트명 StudyProject에서 가져옴.



게임 인스턴스는 실행 중에 단 하나만 존재한다.

Toolbar > Settings > Project Settings > Map & Modes

Game Instance Class에 SGameInstance 지정.



- CoreMinmal.h
  - Engine.h보다 경량화된 헤더이다.
  - 개발에 필요한 대부분의 헤더를 포함한다.
- Enegine/GameInstance.h
  - 부모 클래스의 헤더이다.

- SGameInstance.generated.h
  - 언리얼 헤더 툴에 의해 .h가 .generated.h 파일로 변환된다.

- UCLASS()
  - 언리얼 클래스를 생성하기 전 작성해야 하는 매크로

- STUDYPROJECT_API
  - 다른 모듈에서 해당 개체에 접근할 수 있게 한다. 
  - __declspec(dllexport)

- GENERATED_BODY
  - 이를 통해 .generated.body 파일을 만들어냄.



### 🔸언리얼 헤더 툴

언리얼 오브젝트의 헤더 파일에 작성된 매크로를 분석하는 툴. 

분석한 결과로 클래스명.generated.h 파일을 생성한다.

언리얼 오브젝트의 장점들을 제공하기 위한 전처리 작업을 진행해준다.



## 2️⃣ 언리얼 오브젝트의 장점

### 🔸Class Default Object

언리얼 엔진이 초기화되면 작성된 클래스들이 로드되면서 CDO가 클래스마다 생성된다.

클래스의 생성자에 작성된 로직에 따라 CDO가 생성되고, 엔진 종료까지 메모리에 올라가 있다.

개체 생성 시 아예 새로운 개체를 생성하지 않고 CDO를 복제하는 방식으로 메모리 효율을 높인다.

GetDefaut() 함수를 통해 CDO를 가져온다.



### 🔸리플렉션

리플렉션은 런타임 중 자기 자신을 조사하는 기능이다.

언리얼 오브젝트 클래스의 속성(*멤버 변수*)에 UPROPERTY(), 함수에 UFUNCTION()을 붙인다.

매크로를 통해 런타임 중인 언리얼 에디터에 메타 데이터를 전달한다.

모든 언리얼 오브젝트는 자기 클래스의 속성과 함수 정보를 컴파일 타임(StaticClass())과 런타임(GetClass())에서 조회 할 수 있다.

```c++
// SUnrealObjectClass.h

...
class STUDYPROJECT_API USUnrealObjectClass : public UObject
{
    GENERATED_BODY()

public:
    USUnrealObjectClass();

    UFUNCTION()
    void HelloUnreal();

    const FString& GetName() const { return Name; }

public:
    UPROPERTY()
    FString Name;
};
```

```c++
// SUnrealObjectClass.cpp

...
USUnrealObjectClass::USUnrealObjectClass()
{
    Name = TEXT("CDO");
}
void USUnrealObjectClass::HelloUnreal()
{
    UE_LOG(LogTemp, Log, TEXT("HelloUnreal() has been called."));
}
```

```c++
// SGameInstance.cpp
#include "SUnrealObjectClass.h"

...
void USGameInstance::Init()
{
    ...
    USUnrealObjectClass* USObject1 = NewObject<USUnrealObjectClass>();
    
    UE_LOG(LogTemp, Log, TEXT("USObject1's Name: %s"), *USObject1->GetName());
    // 직접 정의한 Getter()
    
    FProperty* NameProperty = USUnrealObjectClass::StaticClass()->FindPropertyByName(TEXT("Name"));
    // 프로퍼티 시스템을 활용한 Getter()
    
    FString CompiletimeName;
    // StaticClass()는 컴파일 타임에 조사
    if(nullptr != NameProperty)
    {
      NameProperty->GetValue_InContainer(USObject1, &CompiletimeName);
      UE_LOG(LogTemp, Log, TEXT("CompiletimeName: %s"), *CompiletimeName);
    }
    
    UFunction* HelloUnrealFunction = USObject1->GetClass()->FindFunctionByName(TEXT("HelloUnreal"));
    if(nullptr != HelloUnrealFunction)
    {
      USObject1->ProcessEvent(HelloUnrealFunction, nullptr);
    }    
}
...
```



### 🔸인터페이스

워크스페이스의 콘텍스트 메뉴에서 **Create Model**을 클릭해서 빈 모델을 생성합니다.

또는 이미 배치 되어있는 엔티티의 콘텍스트 메뉴의 **Create Model From Entity**를 클릭해 엔티티 모델을 만들 수 있습니다.



### 🔸가비지 컬렉션

원하는 모델을 씬으로 드래그 하면 됩니다.



### 🔸직렬화

프로퍼티 에디터 최상단에는 어떤 컴포넌트에도 속하지 않은 프로퍼티있는데, 이것이 모델 프로퍼티이다.

모델 프로퍼티는 모델에 포함된 컴포넌트의 일부 프로퍼티를 즐겨찾기처럼 모아놓은 것이다.



## 3️⃣ Entity, Component, Property



## 4️⃣ 월드 인스턴스



## 5️⃣ DataStorage


***
<br>

    이 글은 코드조선님의 인프런 강의 Go Hard to Unreal를 참고했습니다.
    잘못된 내용이 있을 경우 메일로 지적바랍니다!😄

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}