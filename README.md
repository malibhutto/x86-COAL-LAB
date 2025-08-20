### 8086 Assembly Projects (MASM + Irvine32)

This repository contains two x86 assembly console games built with MASM and Kip Irvine's support library.

- `2d-platformer/`: Collect coins, avoid the enemy, and let gravity/jumps move the player on a console grid.
- `pong-game/`: Bounce the ball using a right‑side paddle; each hit scores, a miss ends the game.

Each folder includes its own `README.md` with full details. This top‑level guide provides a quick setup and build reference for both.

### Prerequisites

- Windows with 32‑bit console support.
- MASM toolchain (`ml.exe`, `link.exe`) or Visual Studio with MASM enabled.
- Kip Irvine's library installed:
  - Includes: `C:\Irvine\Include`
  - Libs: `C:\Irvine\Lib`

Set environment variables so the tools can find includes and libs:

```bat
set include=%include%;C:\Irvine\Include
set lib=%lib%;C:\Irvine\Lib
```

### Quick Start: Build and Run

Open a Developer Command Prompt for VS (or a shell where `ml` and `link` are available), then:

2D Platformer

```bat
cd 2d-platformer
rem Build from the provided .txt source
ml /c /coff /Ta "2d platformer.txt"
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" "2d platformer.obj" Irvine32.lib kernel32.lib user32.lib
"2d platformer.exe"
```

Pong Game

```bat
cd pong-game
rem Build from the provided .txt source
ml /c /coff /Ta "pong game.txt"
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" "pong game.obj" Irvine32.lib kernel32.lib user32.lib
"pong game.exe"
```

Tip: You can optionally rename the sources to `.asm` (e.g., `pong.asm`, `platformer.asm`) and build without `/Ta`.

### Controls

- 2D Platformer: `W` jump, `A` left, `D` right, `X` exit
- Pong Game: `W` up, `S` down, `X` exit

### Troubleshooting

- cannot open file `Irvine32.inc`: Include path missing; add `C:\Irvine\Include` to the Include directories or environment.
- LNK1104: cannot open `Irvine32.lib`: Library path missing; add `C:\Irvine\Lib` to the Library directories.
- Colors or cursor artifacts: use a standard Windows console; default font/size generally works best.

### Structure

```
project/
  2d-platformer/
    README.md
    2d platformer.txt
  pong-game/
    README.md
    pong game.txt
```
