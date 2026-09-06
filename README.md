# UEDBot

## 🌐 다른 언어로 보기: [한국어 🇰🇷](./README.ko.md)

<p align="center">
    <img src="./media/defense.gif" width="600" alt="Base defense with a ramp wall" />
    <br />
    Base defense with ramp blocking
</p>

<p align="center">
    <img src="./media/kiting.gif" width="600" alt="Marines kiting enemy units" />
    <br />
    Kiting with Marines
</p>

UEDBot is a Terran StarCraft II bot written in C++. It combines an opening wall, automated economy management, micro-oriented combat control, and a Battlecruiser timing attack into a complete ladder-ready strategy.

> **Tournament result:** 1st place in an 11-bot tournament for the University of Alberta's CMPUT 350 course — **57 wins, 3 draws, 0 losses**.

## My contributions

- **Battlecruiser control** — implemented and refined teleport timing, target selection, retreat behavior, and combat movement in `ControlBattlecruisers.cpp`.
- **Ground-unit micro** — added Marine control and completed Siege Tank control, then iterated on target prioritization, kiting, siege-mode behavior, and duplicate-order handling in `ControlMarines.cpp` and `ControlSiegeTanks.cpp`.
- **Opening and production flow** — built and evolved the build-order and production logic for Terran structures, Marines, and Battlecruisers in `Build_Order.cpp` and `Build_Units.cpp`.


## Highlights

- **Opening wall and base defense**  
  Uses Supply Depots and a Barracks to close key ramps early, then layers Marines, Siege Tanks, and Missile Turrets as the game develops.

- **Economy automation**  
  Coordinates SCVs, MULEs, mineral saturation, and gas collection to support continuous production.

- **Combat micro**  
  Controls Marines and Battlecruisers with kiting behavior to preserve units while trading efficiently.

- **Battlecruiser timing pressure**  
  Teleports a Battlecruiser into the enemy base before 5:30, with Marine and Siege Tank reinforcements following behind.

- **Modular behavior code**  
  Separates economy, scouting, defense, offense, build orders, and unit-control logic into focused C++ modules.

## What is in this repository

- Core bot orchestration: `BasicSc2Bot.*`
- Economy, defense, offense, and build-order behaviors
- Specialized control modules for SCVs, Marines, Siege Tanks, and Battlecruisers
- Map and helper utilities, plus the `cpp-sc2` submodule dependency


# Developer Install / Compile Instructions
## Requirements
* [CMake](https://cmake.org/download/)
* Starcraft 2 ([Windows](https://starcraft2.com/en-us/)) ([Linux](https://github.com/Blizzard/s2client-proto#linux-packages)) 
* [Starcraft 2 Map Packs](https://github.com/Blizzard/s2client-proto#map-packs), The maps we will be using are in the `Ladder 2017 Season 1` pack. Read the instructions for how to extract and where to place the maps.

## Windows

Download and install [Visual Studio 2022](https://www.visualstudio.com/downloads/) if you need it.

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

Note: Try opening the SC2 game client before installing. If the game crashes before opening, you may need to change your Share name:
* Open `System Preferences`
* Click on `Sharing`
* In the `Computer Name` textfield, change the default 'Macbook Pro' to a single word name (the exact name shouldn't matter, as long as its not the default name)

To build, you must use the version of clang that comes with MacOS. 
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
The Linux version is headless, meaning that you will not be able to see your bot 
First, download the [Linux package](https://github.com/Blizzard/s2client-proto#linux-packages).
Unzip it to your home directory. 
The directory should read as `/home/<USER>/StarCraftII/`.

Rename the `Maps` directory to lowercase, and place any downloaded maps inside this directory:
```bash
$ mv /home/<USER>/StarCraftII/Maps /home/<USER>/StarCraftII/maps
```

Finally, create a directory (note the added space) which contains a file `ExecuteInfo.txt`, which lists the executable directory:
```bash
$ mkdir "/home/<USER>/StarCraft II"
$ echo "executable = /home/<USER>/StarCraftII/Versions/Base75689/SC2_x64" > "/home/<USER>/StarCraft II/ExecuteInfo.txt"
```
The `Base75689` will need to match the correct version which matches the version you downloaded. To check, navigate to `/home/<USER>/StarCraftII/Versions/`.

Remember to replace `<USER>` with the name of your user profile.

# Playing against the built-in AI

In addition to competing against other bots using the [Sc2LadderServer](https://github.com/solinas/Sc2LadderServer), this bot can play against the built-in
AI by specifying command line argurments.

You can find the build target under the `bin` directory. For example,

```
# Windows
./UEDBot.exe -c -a zerg -d Hard -m CactusValleyLE.SC2Map

# Mac
./UEDBot -c -a zerg -d Hard -m CactusValleyLE.SC2Map
```

will result in the bot playing against the zerg built-in AI on hard difficulty on the map CactusValleyLE.
