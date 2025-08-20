### 2D Platformer — x86 Assembly (MASM + Irvine32)

**Overview**

- Simple console platformer in MASM using `Irvine32.inc`.
- Move a player character to collect coins while avoiding a randomly moving enemy. Score increases on coin pickup; touching the enemy ends the game with ASCII art.

**Controls**

- **W**: jump (short hop)
- **A**: move left
- **D**: move right
- **X**: exit

**How it works**

- The world is the console grid; ground is drawn at row 29.
- Player position (`xPos`, `yPos`) updates with gravity when above ground; jump briefly moves the player upward.
- Coins spawn near the bottom at random X; collecting increments `score` and respawns the coin away from player/enemy.
- Enemy at the bottom row teleports to a random X; collision with the player triggers Game Over.
- Uses Irvine32 functions: `Gotoxy`, `WriteString`, `WriteChar`, `Writedec`, `Delay`, `RandomRange`, etc.

**Requirements**

- Windows, 32‑bit toolchain support.
- MASM (ml.exe) and linker (link.exe) or Visual Studio with MASM.
- Kip Irvine's library installed (`Irvine32.inc`, `Irvine32.lib`).

**Build & Run (Command line)**
If the source is kept as `2d platformer.txt`, assemble with `/Ta`:

```bat
ml /c /coff /Ta "2d platformer.txt"
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" "2d platformer.obj" Irvine32.lib kernel32.lib user32.lib
"2d platformer.exe"
```

Alternatively, rename to `platformer.asm` and use:

```bat
ml /c /coff platformer.asm
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" platformer.obj Irvine32.lib kernel32.lib user32.lib
platformer.exe
```

Ensure includes and libs are discoverable:

```bat
set include=%include%;C:\Irvine\Include
set lib=%lib%;C:\Irvine\Lib
```

**Build & Run (Visual Studio)**

- Create an empty console project; enable MASM.
- Add the source file.
- VC++ Directories:
  - Include: `C:\Irvine\Include`
  - Library: `C:\Irvine\Lib`
- Linker → Input → Additional Dependencies: `Irvine32.lib; kernel32.lib; user32.lib`

**Troubleshooting**

- “cannot open file Irvine32.inc”: add the Irvine include path.
- LNK1104 for `Irvine32.lib`: add the Irvine lib path.
- Console cursor artifacts: the code already clears/redraws sprites; ensure you run in a standard console with default font/size.

**Credits**

- 23K-0730 Muhammad Ali, 23K-0608 Ayan Hussain, 23K-0798 Umer Khan
