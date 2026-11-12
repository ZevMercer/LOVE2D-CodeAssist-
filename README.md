# LÖVE2D Template for CodeAssist 🎮

A minimal Android template to run **LÖVE2D** games in [CodeAssist](https://github.com/tyron12233/CodeAssist) — the on-device IDE for Android. Build, run, and iterate on your LÖVE games directly on your phone or tablet.

---

## 📦 How It Works

1. **Write your game** in standard LÖVE2D Lua (`main.lua`, plus any assets, libraries, etc.).
2. **Package it as a `.love` file** — this is just a **ZIP archive** renamed to `.love` containing your game files:
   ```
   game.love/
   ├── main.lua
   ├── conf.lua          (optional)
   ├── assets/           (images, sounds, fonts, etc.)
   └── libs/             (any Lua libraries)
   ```
3. **Place `game.love` in `app/src/main/assets/`** (this folder already exists in the template).
4. **Open the project in CodeAssist** → Build → Run. The app loads your `.love` file from assets and runs it via the embedded LÖVE2D Android engine.

---

## 🚀 Quick Start

### 1. Clone this template
```bash
git clone https://github.com/ZevMercer/LOVE2D-CodeAssist-.git
```

### 2. Create your game
Edit or replace `main.lua` (and add assets) in a temporary folder, e.g. `mygame/`:
```
mygame/
├── main.lua
├── player.png
└── jump.wav
```

### 3. Package as `.love` (ZIP)
```bash
cd mygame
zip -r ../game.love .      # creates game.love one level up
cd ..
```

> **Tip:** On Android (Termux, etc.) or desktop, any ZIP tool works. Just ensure the ZIP contains `main.lua` at its root, not inside a subfolder.

### 4. Drop it in assets
```bash
mv game.love app/src/main/assets/game.love
```
(Overwrite the placeholder `game.love` already there.)

### 5. Open in CodeAssist
- Launch **CodeAssist** on your Android device.
- Choose **Open Project** → select this folder.
- Wait for Gradle sync (first time only).
- Press **▶ Run** (or *Build → Run*).

Your game launches fullscreen in landscape. 🎉

---

## 📁 Project Structure

```
love2d-template/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── assets/
│   │   │   │   └── game.love        ← YOUR GAME GOES HERE
│   │   │   ├── java/org/love2d/android/
│   │   │   │   └── GameActivity.java  (bootstraps LÖVE)
│   │   │   ├── jniLibs/               (native libs for arm64-v8a, armeabi-v7a)
│   │   │   ├── res/
│   │   │   └── AndroidManifest.xml
│   │   └── ...
│   ├── module.toml
│   └── build/
├── README.md
└── .platform/
```

---

## 🛠 Requirements

| Tool | Version |
|------|---------|
| **CodeAssist** | Latest (on Android) |
| **Android SDK** | API 21+ (handled by CodeAssist) |
| **LÖVE version** | 11.4 (bundled in this template) |

---

## ⚡ Tips & Best Practices

- **Keep the APK small** — this template + a typical 2D game stays **well under 20 MB**.
  - Compress assets (`.png`, `.ogg`, `.mp3`).
  - Avoid bundling huge libraries inside `.love`; use `require` for Lua libs only.
- **Iterate fast**: replace `game.love` in `assets/` and re-run — no Gradle rebuild needed for asset-only changes.
- **Debug with `print()`** — output appears in CodeAssist’s logcat pane.
- **Portrait mode?** Edit `AndroidManifest.xml` → change `android:screenOrientation="sensorLandscape"` to `sensorPortrait` or `user`.

---

## 🎨 Example `main.lua`

```lua
-- main.lua
function love.load()
    love.window.setTitle("Hello LÖVE on CodeAssist!")
    font = love.graphics.newFont(24)
    love.graphics.setFont(font)
    msg = "Tap or drag to draw circles!"
    circles = {}
end

function love.update(dt)
    -- game logic here
end

function love.draw()
    love.graphics.print(msg, 20, 20)
    for _, c in ipairs(circles) do
        love.graphics.setColor(c.r, c.g, c.b, 1)
        love.graphics.circle("fill", c.x, c.y, 30)
    end
end

function love.touchpressed(id, x, y, dx, dy, pressure)
    table.insert(circles, {
        x = x, y = y,
        r = math.random(), g = math.random(), b = math.random()
    })
end
```

---

## 📜 Credits & Licenses

| Component | License | Link |
|-----------|---------|------|
| **LÖVE2D (framework)** | zlib | <https://love2d.org/> • <https://github.com/love2d/love> |
| **love2d-android (port)** | zlib | <https://github.com/love2d/love/tree/master/platform/android> |
| **This template** | MIT | <https://github.com/ZevMercer/LOVE2D-CodeAssist-> |

> **LÖVE** is copyright © 2006–2024 Alex Szpakowski et al.  
> This template bundles the official Android port from the LÖVE repository.

---

## 🤝 Contributing

PRs welcome! Ideas:
- Add a sample game in `assets/sample.love`.
- Document how to use `conf.lua` for window settings.
- CI workflow to build APK automatically.

---

## 📄 License

This template is released under the **MIT License**.  
LÖVE2D itself is under the **zlib License** — see above.

---

**Happy coding!** 💙  
Made for the CodeAssist community — build games on the go.
