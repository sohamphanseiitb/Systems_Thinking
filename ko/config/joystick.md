# 조이스틱 설정

*QGroundControl*에 연결된 [조이스틱](https://en.wikipedia.org/wiki/Joystick) 또는 게임 패드를 사용하여 [RC 송신기](../config/radio.md)를 *대체*하여 기체를 수동으로 제어할 수 있습니다.

이 방법은 지상제어 프로그램이 있는 수동 제어 장치에서 사용할 수 있습니다 (아래 표시된 *UAVComponents* [MicroNav](https://www.uavcomp.com/command-control/micronav/)). 조이스틱은 일반적으로 비행 시뮬레이션용으로 많이 사용합니다.

![조이스틱 MicroNav.](../../assets/peripherals/joystick/micronav.jpg)

:::tip
조이스틱은 RC 컨트롤러가 아니므로, 조이스틱을 사용하는 경우에는 [무선 조종기 설정](../config/radio.md)이 필요하지 않습니다!
:::

:::note
*QGroundControl*은 크로스 플랫폼 [SDL2](http://www.libsdl.org/index.php) 라이브러리를 사용하여 조이스틱 움직임을 MAVLink [MANUAL_CONTROL](https://mavlink.io/en/messages/common.html#MANUAL_CONTROL) 메시지로 변환하여 텔레메트리를 통하여 PX4로 전송합니다. 결과적으로 조이스틱 기반 제어 시스템은 차량이 조이스틱 움직임에 반응하기 위해 안정적인 고대역폭 원격 채널이 필요합니다.
:::

## PX4 조이스틱 지원 활성화

조이스틱 설정 방법에 대한 정보는 [QGroundControl > 조이스틱 설정](https://docs.qgroundcontrol.com/en/SetupView/Joystick.html)을 참고하십시오.

요약:
* *QGroundControl*을 시작합니다.
* 매개 변수 [COM_RC_IN_MODE = 1](../advanced_config/parameter_reference.md#COM_RC_IN_MODE) - `조이스틱/RC 검사 없음`을 설정합니다 (매개 변수 설정에 대한 정보는 [매개 변수](https://docs.qgroundcontrol.com/en/SetupView/Parameters.html) 참조).
* 조이스틱을 연결합니다.
* 연결된 조이스틱(**기체 설정 > 조이스틱**)을 설정하세요.
