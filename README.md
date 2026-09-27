# STM32 SPI Slave

## MCU / 설정

- MCU: STM32F446RET6
- 패키지: LQFP64
- SPI: SPI1, Slave, Full-Duplex, 8-bit
- SPI 모드: Mode 0 (CPOL=0, CPHA=0), MSB first
- CPOL=0: SCK 유휴 상태는 Low입니다.
- CPHA=0: 첫 번째 클럭 에지에서 데이터를 샘플링합니다. Mode 0에서는 상승 에지에서 샘플링하고 하강 에지에서 데이터를 변경합니다.
- 설정 도구: STM32CubeMX / STM32CubeIDE

## Pinout

| STM32 핀 | SPI 신호 | 연결 대상 (TI Master) |
| --- | --- | --- |
| PA5 | SPI1_SCK | SCLK |
| PA6 | SPI1_MISO | MISO 입력 |
| PA7 | SPI1_MOSI | MOSI 출력 |
| PC4 | CS (GPIO 입력, Pull-up) | GPIO 출력으로 제어하는 CS, Active Low |
| GND | Ground | GND |

PC4는 SPI 하드웨어 NSS가 아니라 GPIO 입력으로 사용합니다. 마스터가 전송하는 동안 CS를 Low로 유지하고, 전송이 끝나면 High로 올리세요.

## 연결 주의

- TI 보드와 STM32의 IO 전압 레벨이 호환되는지 확인하세요. STM32F446의 신호는 3.3 V 기준이며, 5 V 신호를 직접 연결하지 마세요.
- SPI 통신을 위해 양쪽 보드의 GND를 공통으로 연결하세요.
- Master와 Slave의 SPI 모드(Mode 0), 비트 순서(MSB first), 데이터 크기(8-bit)를 동일하게 설정하세요.
