---
sidebar_position: 3
tags: ['독후감']
last_update:
  date: 11/16/2022
  author: sewonkimm
---

# Refactoring; 코드 품질을 개선하는 객체지향 사고법

## 서문
> 2022.11.16

- 리팩토링이란; 겉으로 드러나는 코드의 기능은 바꾸지 않으면서 내부 구조를 개선하는 것.
- 사소한 수정이 누적되면 설계가 놀랍도록 향상된다.

## 1장 - 맛보기 예제

- 설계가 조잡한 시스템은 어디를 수정해야 하는지 찾기 힘들어 수정도 어렵다. 수정할 위치를 찾기 힘들면 프로그래머가 실수할 가능성이 높아져서 버그가 생긴다.
- 프로그램이 당장은 문제가 없을지 몰라도 나중엔 사용자가 요구한 기능을 수정하기 힘들어서 애먹을 것이다. 이 상황이 바로 리팩토링해야 할 시점이다.

### 리팩토링 첫 단계

- 리팩토링할 코드 부분에 대한 신뢰도 높은 각종 테스트를 작성하는 것.
- 적절한 테스트 코드를 사용하는 것은 리팩토링의 기본이다.

### 긴 메서드 분해와 기능 재분배

- 코드를 잘게 쪼개면 관리도 편하고 다른 코드와 연동하거나 이리저리 옮기기도 쉽다.
- 우선 논리적 코드 뭉치를 찾아 **메서드 추출기법**을 적용. 어떤 코드를 그룹으로 묶어도 되겠다고 판단될 때, 그 코드를 빼내어 목적을 잘 나타내는 직관적 이름의 메서드로 만든다.
- 좋은 코드는 그것이 무슨 기능을 하는지 분명히 드러나야 하는데, 코드의 기능을 분명히 드러내는 열쇠가 바로 직관적인 변수명이다.
- 철저한 타입 선언과 테스트 작성만 하면 어떤 실수든 눈에 확 들어온다.
- 메서드는 대체로 자신이 사용하는 데이터와 같은 객체에 들어 있어야한다. 이 작업은 **메서드 이동기법**을 실시한다. 메서드가 자신이 속한 클래스보다 다른 클래스의 기능을 더 많이 이용할 땐 그 메서드가 제일 많이 이용하는 클래스 안에서 비슷한 내용의 새 메서드를 작성한다. 기존의 메서드는 삭제한다.
- 메서드 결과를 저장하는데만 사용되는 **임시변수는 메서드 호출로 전환**한다. 임시변수가 많으면 불필요하게 많은 매개변수를 전달하게 되는 문제가 흔히 생기므로 최대한 없애는 것이 좋다.
  

