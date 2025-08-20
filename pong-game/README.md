### Pong Game — x86 Assembly (MASM + Irvine32)

**Overview**

- Single‑player Pong written in MASM using `Irvine32.inc`.
- Bounce the ball with a paddle at the right edge; each successful hit increments the score. Missing the ball ends the game with ASCII art.

**Controls**

- **W**: move paddle up
- **S**: move paddle down
- **X**: exit

**How it works**

- Ball position updates with `ballDX`/`ballDY` and reflects on top/bottom walls.
- At the right wall (`x=79`), the ball must align with the paddle Y to bounce and score; otherwise, game over.
- Uses Irvine32 console I/O (`Gotoxy`, `WriteString`, `WriteChar`, `Delay`, `Randomize`).

**Requirements**

- Windows, 32‑bit toolchain support.
- MASM (ml.exe) and linker (link.exe) or Visual Studio with MASM.
- Kip Irvine's library installed (`Irvine32.inc`, `Irvine32.lib`).

**Build & Run (Command line)**
If you keep the file name as `pong game.txt`, assemble with `/Ta` so ML treats it as assembly:

```bat
ml /c /coff /Ta "pong game.txt"
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" "pong game.obj" Irvine32.lib kernel32.lib user32.lib
"pong game.exe"
```

Alternatively, rename the source to `pong.asm` and use:

```bat
ml /c /coff pong.asm
link /SUBSYSTEM:CONSOLE /LIBPATH:"C:\Irvine\Lib" pong.obj Irvine32.lib kernel32.lib user32.lib
pong.exe
```

Ensure the assembler can find includes:

```bat
set include=%include%;C:\Irvine\Include
set lib=%lib%;C:\Irvine\Lib
```

**Build & Run (Visual Studio)**

- Create an empty console project; enable MASM for the project.
- Add the source file to the project.
- Project Properties → VC++ Directories:
  - Include Directories: `C:\Irvine\Include`
  - Library Directories: `C:\Irvine\Lib`
- Linker → Input → Additional Dependencies: `Irvine32.lib; kernel32.lib; user32.lib`

**Troubleshooting**

- “cannot open file Irvine32.inc”: add `C:\Irvine\Include` to the Include path.
- LNK1104 for `Irvine32.lib`: add `C:\Irvine\Lib` to the Library path.
- If the console colors look odd, ensure `SetTextColor` calls aren’t overridden by your console theme.

**Credits**

- 23K-0730 Muhammad Ali, 23K-0608 Ayan Hussain, 23K-0798 Umer Khan
