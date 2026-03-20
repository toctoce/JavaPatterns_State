Java Patterns | State
===

**State**는 객체가 자신의 내부 상태에 따라 동작을 바꿀 수 있게 해주는 *행위(behavioral) 디자인 패턴*입니다.

이 패턴은 *유한 상태 머신(Finite State Machine, FSM)* 개념과 매우 밀접한 관련이 있습니다.

- *참고 자료*: [State Pattern (refactoring guru)](https://refactoring.guru/design-patterns/state)

## 적용 예제

이 저장소는 다음과 같은 명령(공개 메서드)을 제공하는 `MusicPlayer`를 구현합니다.

- ⏯️ `play()`
- :rewind: `prev()`
- :fast_forward: `next()`
- ⏹️ `stop()`
- :question: `status()`

각 명령의 동작은 **State** 패턴을 통해 정의되어 있으며, 아래와 같은 FSM을 구현합니다.

![](images/fsm_1.png)

<hr/>

`Main` 클래스에 포함된 프로그램은 `MusicPlayer` 인스턴스를 조작할 수 있는 *명령줄 인터페이스(Command-Line Interface, CLI)* 를 제공합니다.

프로그램을 실행한 뒤, 실제로 위 다이어그램과 같은 방식으로 동작하는지 확인해 보세요.

## 실습 과제

1. `PausedState` 클래스로 새로운 *구체 상태(concrete state)* 를 만들고, 기존 상태 클래스들도 수정하여 아래 FSM을 구현해 보세요.

    ![](images/fsm_2.png)

    :bulb: `CLI` 클래스는 수정할 필요가 없습니다.

2. `MusicPlayer`에 `turnOn()`과 `turnOff()` 메서드를 추가하세요. 이 메서드들의 동작 역시 현재 *state* 에 위임되어야 합니다. 따라서 `MusicPlayerState` *interface* 도 함께 변경해야 합니다. 새로운 `OffState`를 만들고, 필요한 수정 사항을 반영하여 아래 FSM을 구현해 보세요.

    ![](images/fsm_3.png)

    - :warning: 주의 사항

        - 기존 상태들 사이의 *전이 규칙(transition rules)* 은 그대로 유지되며, 위 다이어그램에서는 생략되었습니다.

        - 초기 상태(initial state)는 `Off`입니다.

        - `Off` 상태에서는 `TURNON` 명령으로만 전이할 수 있으며, 그 외의 명령은 조용히 무시됩니다.

        - 다른 모든 상태에서는 `TURNON` 명령이 조용히 무시됩니다.

        - `Off` 상태에서 `Stopped` 상태로 전이할 때는 항상 *playlist* 의 첫 번째 곡을 로드해야 합니다.

        - `Stopped` 상태로 전이될 때마다 현재 *playback* 은 반드시 중지되어야 하며, 사용 중인 리소스도 해제되어야 합니다.

해답은 [SOLUTION.md](SOLUTION.md)에서 확인할 수 있습니다.
