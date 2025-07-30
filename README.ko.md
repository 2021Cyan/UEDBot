# UEDBot

## 🌐 View in other languages: [English 🇺🇸](./README.md)

**UEDBot**은 C++로 구축된 고성능 테란 스타크래프트 II 봇으로, 방어와 공격 모두에서 고급 전략을 활용합니다. 동적 램프 차단, 최적화된 자원 수집, 그리고 공격적인 러쉬를 통해 상대를 제압합니다. **UEDBot**은 University of Alberta의 CMPUT 350 수업에서 열린 11개 봇 참가 토너먼트에서 **1위**를 차지했으며, **57승**, **3무**, **0패**의 무패 기록을 세웠습니다.

## 기능

- **동적 램프 차단**
  UEDBot은 초반 수비를 위해 보급고와 병영을 사용해 주요 램프를 차단하여 적의 러쉬를 방지합니다.

- **최적화된 자원 수집**
  UEDBot은 SCV와 지게로봇을 효율적으로 사용해 빠르고 효과적으로 미네랄과 가스를 채취하여 안정적인 경제적 우위를 유지합니다.

- **유닛 카이팅**
  프로게이머들의 플레이에서 영감을 받아, UEDBot은 해병과 전투순양함을 활용한 고급 카이팅 전술로 교전 시 입는 피해를 최소화합니다.

- **전투순양함 순간이동을 이용한 초고속 러쉬 공격**
  UEDBot은 5분 30초 이전에 전투순양함을 적 기지로 순간이동시킨 뒤, 해병과 공성전차를 추가로 투입해 끊임없는 압박을 가합니다.

- **해병, 공성전차, 미사일 포탑을 조합한 혼합 방어**
  UEDBot은 해병과 공성전차로 지상 방어를 수행하는 동시에, 후반부에는 미사일 포탑을 확장 배치하여 공중 위협에도 대비합니다.

## 인게임 영상

<p align="center">
    <img src="./media/defense.gif"/>
    <br />
    입구 막기를 활용한 기지 방어
</p>

<p align="center">
    <img src="./media/kiting.gif"/>
    <br />
    해병을 활용한 카이팅
</p>

## 토너먼트 결과

UEDBot은 **11개의 스타크래프트 II 봇**이 참가한 토너먼트에서 **1위**를 차지했으며, **57승**, **3무**, **0패**라는 인상적인 기록을 세웠습니다.

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
