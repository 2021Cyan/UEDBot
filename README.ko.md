# UEDBot

## 🌐 다른 언어로 보기: [English 🇺🇸](./README.md)

<p align="center">
    <img src="./media/defense.gif" width="600" alt="입구 차단을 활용한 기지 방어" />
    <br />
    입구 막기를 활용한 기지 방어
</p>

<p align="center">
    <img src="./media/kiting.gif" width="600" alt="해병 카이팅" />
    <br />
    해병을 활용한 카이팅
</p>

UEDBot은 C++로 작성한 테란 스타크래프트 II 봇입니다. 초반 입구 차단, 자동 경제 관리, 교전 마이크로, 전투순양함 타이밍 공격을 하나의 완성된 전략으로 결합했습니다.

> **토너먼트 성과:** University of Alberta의 CMPUT 350 수업에서 열린 11개 봇 토너먼트에서 **1위** — **57승, 3무, 0패**.

## 내가 기여한 코드

- **전투순양함 제어** — `ControlBattlecruisers.cpp`에서 순간이동 타이밍, 목표 선정, 후퇴 동작, 교전 이동 로직을 구현하고 개선했습니다.
- **지상 유닛 마이크로** — `ControlMarines.cpp`, `ControlSiegeTanks.cpp`에 해병 제어와 공성전차 제어를 추가·완성한 뒤, 목표 우선순위·카이팅·공성 모드·중복 명령 처리 로직을 고도화했습니다.
- **빌드 오더와 생산 흐름** — `Build_Order.cpp`, `Build_Units.cpp`에서 테란 건물, 해병, 전투순양함 생산을 위한 빌드 오더와 생산 로직을 구현·개선했습니다.

## 주요 특징

- **초반 입구 차단과 기지 방어**
  보급고와 병영으로 주요 입구를 초반에 막고, 게임이 진행될수록 해병·공성전차·미사일 포탑을 조합해 방어선을 구축합니다.

- **경제 자동화**
  SCV와 지게로봇, 광물 포화도, 가스 채취를 관리해 지속적인 생산을 뒷받침합니다.

- **교전 마이크로**
  해병과 전투순양함에 카이팅 동작을 적용해 유닛을 보존하면서 효율적으로 교전합니다.

- **전투순양함 타이밍 압박**
  5분 30초 이전에 전투순양함을 적 기지로 순간이동시키고, 해병과 공성전차 증원으로 압박을 이어 갑니다.

- **모듈형 동작 코드**
  경제, 정찰, 방어, 공격, 빌드 오더, 유닛 제어 로직을 목적별 C++ 모듈로 분리했습니다.

## 저장소 구성

- 봇 전체 동작 제어: `BasicSc2Bot.*`
- 경제, 방어, 공격, 빌드 오더 동작
- SCV, 해병, 공성전차, 전투순양함 전용 제어 모듈
- 맵·헬퍼 유틸리티와 `cpp-sc2` 서브모듈 의존성

# 개발자 설치 및 컴파일 가이드

## 요구 사항

* [CMake](https://cmake.org/download/)
* 스타크래프트 II ([Windows](https://starcraft2.com/en-us/) / [Linux](https://github.com/Blizzard/s2client-proto#linux-packages))
* [스타크래프트 II 맵 팩](https://github.com/Blizzard/s2client-proto#map-packs)

  * 사용될 맵은 `Ladder 2017 Season 1` 팩에 포함되어 있습니다. 맵을 추출하고 설정하는 방법은 해당 페이지의 가이드를 참고하세요.

## Windows

* 필요하다면 [Visual Studio 2022](https://www.visualstudio.com/downloads/)를 다운로드하고 설치하세요.

```bat
:: Clone the project
$ git clone --recursive https://github.com/Team-UED/UEDBot.git
$ cd UEDBot

:: Create build directory.
$ mkdir build
$ cd build

:: Generate VS solution.
$ cmake ../ -G "Visual Studio 17 2022"

:: Build the project using Visual Studio.
$ start UEDBot.sln
```

## Mac

**참고:** 설치하기 전에 SC2 게임 클라이언트를 한 번 실행해 보세요. 게임이 열리기 전에 충돌이 발생하면 공유 이름을 변경해야 할 수 있습니다:

* `시스템 환경설정`을 열고
* `공유`를 클릭합니다
* `컴퓨터 이름` 텍스트 필드에서 기본값인 ‘Macbook Pro’를 하나의 단어 이름으로 변경하세요(정확한 이름은 중요하지 않으며, 기본 이름이 아니면 됩니다)

빌드하려면 macOS에 기본으로 제공되는 clang 버전을 사용해야 합니다.

```bat
:: Clone the project
$ git clone --recursive https://github.com/Team-UED/UEDBot.git
$ cd UEDBot

:: Create build directory.
$ mkdir build
$ cd build

:: Set Apple Clang as the default compiler
export CC=/usr/bin/clang
export CXX=/usr/bin/clang++

:: Generate a Makefile
:: Use 'cmake -DCMAKE_BUILD_TYPE=Debug ../' if debug info is needed
$ cmake -DCMAKE_BUILD_TYPE=Release ../

:: Build
$ make
```

## Linux

Linux 버전은 헤드리스(headless)로, 봇을 화면에서 확인할 수 없습니다.
먼저 [Linux 패키지](https://github.com/Blizzard/s2client-proto#linux-packages)를 다운로드하세요.
다운로드한 압축 파일을 홈 디렉터리에 풀면 경로가 `/home/<USER>/StarCraftII/`가 되어야 합니다.

`Maps` 디렉터리 이름을 소문자로 변경하고, 다운로드한 맵 파일을 이 디렉터리 안에 넣으세요:

```bash
$ mv /home/<USER>/StarCraftII/Maps /home/<USER>/StarCraftII/maps
```

마지막으로, `ExecuteInfo.txt` 파일을 포함하는 디렉터리를 하나 만드세요(디렉터리 이름에 공백 주의):

```bash
$ mkdir "/home/<USER>/StarCraft II"
$ echo "executable = /home/<USER>/StarCraftII/Versions/Base75689/SC2_x64" > "/home/<USER>/StarCraft II/ExecuteInfo.txt"
```

여기서 `Base75689`는 다운로드한 버전에 맞게 변경해야 합니다. 올바른 버전을 확인하려면 `/home/<USER>/StarCraftII/Versions/` 디렉터리 내용을 확인하세요.

`<USER>` 부분은 실제 사용자 계정 이름으로 바꿔 사용하세요.

# 내장 AI와 대결하기

다른 봇들과 Sc2LadderServer를 통해 경쟁하는 것 외에도, 이 봇은 커맨드라인 인자를 지정하여 내장 AI와 대결할 수 있습니다.

빌드된 실행 파일은 `bin` 디렉터리에서 찾을 수 있습니다. 예를 들어,

```
# Windows
./UEDBot.exe -c -a zerg -d Hard -m CactusValleyLE.SC2Map

# Mac
./UEDBot -c -a zerg -d Hard -m CactusValleyLE.SC2Map
```

위 명령은 봇이 Hard 난이도의 저그 내장 AI와 CactusValleyLE 맵에서 대결하도록 설정합니다.
