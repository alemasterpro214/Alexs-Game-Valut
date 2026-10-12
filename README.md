# GameVault — Game launcher (modern UI)

A graphical launcher to organize and start your games, compatible with **Windows and Linux**.
Dark modern interface with sidebar, cards with hover, animated boxes and a **real blurred background**.
Links are saved across sessions. **The app NEVER uninstalls games** — it only removes the link from the library.

Contents:

- `gamelauncher.py` — single Python source file (Windows + Linux, requires Python 3.8+)
- `GameVault.exe` — standalone Windows executable (no installation needed)
- `GameVault` — standalone Linux executable (equivalent of the .exe)

## Interface

- **Sidebar** with icon-nav (Library / Settings) + brand title
- **Header** with built-in search bar
- **Modern cards** with large icon, highlighted hover, favorites asterisk, run counter
- **Background**: pick an image → it is shown **blurred** (cover + blur + dark veil) behind the whole UI, redrawn in real time on resize
- 11 languages: English, Italian, German, French, Spanish, Russian, Hindi, Korean, Chinese, Japanese, Portuguese

## Features

### Library
- All linked games in a grid with icons
- **Search bar** at the top to find a game instantly
- **"+ Game" button** in the library to add a new one
- **Favorites**: dedicated filter + star on each card
- **Folders**: organize games; create, rename, delete (top right)
- **Edit**: change name, link, icon, folder, favorite
- **Remove**: only the link, the game stays on disk
- Run counter for each game

### Add game wizard (3 steps)
1. **Executable or shortcut**: `.exe`, `.lnk`, `.url`, `.bat`, `.cmd` (Windows) — any Linux binary or script
2. **Icon**: extracted automatically from the executable, if present; otherwise pick an image
3. **Name**: how the game appears in the library (+ optional folder and favorite)

### Settings
- **Language**: 11 options applied instantly
- **Background**: pick an image → shown blurred behind the interface; you can remove it

## Running

### Windows
```
GameVault.exe    → double-click and go (no installation)
```

### Linux
```
chmod +x GameVault             (first time only)
./GameVault
```

### From source (both systems)
```
python gamelauncher.py          # Windows; Linux: python3
python gamelauncher.py --selftest
```

Source dependencies: `pip install pillow icoextract` + `python3-tk` on Linux.
The executables require nothing.

## Where is the data
Everything (games, folders, language, background) is saved in `~/.gamevault/library.json`.
Extracted icons are saved in `~/.gamevault/icons/`.

## Launching games
- **The working directory is always set to the game's folder**: essential for HaxeFlixel/Friday Night Funkin' games (Psych Engine, Kade Engine, Vs mods) which load assets with relative paths — without the correct CWD they crash or glitch on startup
- `.bat`/`.cmd` files are launched with the correct CWD (typical of itch.io games)
- `.lnk`/`.url` shortcuts are launched directly, so Windows also applies the arguments and working directory saved in the shortcut
- Any other file type falls back to the Windows default handler (jars, installers, `steam://` links, documents…) — like a double-click in Explorer, always with the correct CWD
- Windows: `os.startfile` fallback; Linux: runs the file directly; `.sh` scripts without +x are run with `sh`

## What it does NOT do (by design)
- ❌ Does not uninstall games: it only removes the link from the library
- ❌ Never deletes game files
- ✅ Everything is persistent across sessions

## License
MIT
