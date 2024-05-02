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

{: .notice--warning}

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

원하는 엔티티를 만들려면, 엔티티에 컴포넌트를 추가하고 프로퍼티를 수정해야 한다.

모델은 위 정보들을 저장해 재사용성을 높인다.

원하는 엔티티의 콘텍스트 메뉴에서 **Create Model From Entity**를 클릭하면 엔티티를 모델화 할 수 있다.



### 🔸리플렉션

모델은 자신의 컴포넌트와 프로퍼티 값을 물려받은 확장 모델을 생성할 수 있다.

워크스페이스에서 원하는 모델을 선택 후 컨텍스트 메뉴에서 **Extend**를 클릭해 확장 모델은 만든다.

자식 모델은 부모 모델의 컴포넌트와 프로퍼티 초깃값을 물려받는다.

부모 모델을 수정하면, 자식 모델에도 같은 변화가 적용된다.

모델 간의 관계는 프로퍼티 에디터의 **Model Extension Info**로 확인할 수 있다.



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