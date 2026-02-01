# 📋 Hướng Dẫn Thao Tác Code - 1.3 Animation Editor

> Tài liệu hướng dẫn từng bước: **Code ở đâu** và **Cách thực hiện** trong notebook này.

---

## 📍 Tổng Quan Vị Trí Code

Notebook **1.3 Animation Editor** chủ yếu hướng dẫn **thao tác giao diện** trong Roblox Studio (Animation Editor, Rig Builder). Code Lua chỉ xuất hiện ở các phần sau:

| Phần | Cell | Nội dung code |
|------|------|---------------|
| Save Locally | Cell 11 | Cấu trúc KeyframeSequence |
| Lấy Animation ID | Cell 13 | Sử dụng Animation ID trong script |
| Lấy Animation ID | Cell 13 | Module lưu trữ Animation IDs |

---

## 📂 SCRIPT ĐƯỢC LƯU Ở ĐÂU? (Chi tiết)

### Cấu trúc Roblox Studio Explorer

```
Roblox Studio - Explorer
│
├── StarterPlayer
│   └── StarterPlayerScripts      ← LocalScript phát animation sau khi Publish
│       └── PlayAnimationById (LocalScript)
│
├── ReplicatedStorage
│   └── AnimationIDs (ModuleScript)  ← Lưu trữ Animation IDs (BƯỚC 3)
│
└── Workspace
    └── Rig (Model)
        └── AnimSaves (Folder)        ← KeyframeSequence sau khi Save Locally
            ├── Walk (KeyframeSequence)
            ├── Run (KeyframeSequence)
            └── Wave (KeyframeSequence)
```

### Bảng vị trí Script và Dữ liệu

| Nội dung | Vị trí | Loại | Ghi chú |
|----------|--------|------|---------|
| Script phát animation | `StarterPlayer > StarterPlayerScripts` | **LocalScript** | Sau khi Publish và có Animation ID |
| Module lưu Animation IDs | `ReplicatedStorage` | **ModuleScript** | Tên: `AnimationIDs` |
| Animation đã Save (chưa Publish) | `Workspace > Rig > AnimSaves` | **KeyframeSequence** | Chỉ trong project, chưa có ID |
| Animation object (tạo trong Studio) | `ReplicatedStorage` | **Animation** | Tùy chọn, thay vì tạo bằng code |

### Cách tạo Script đúng vị trí

#### Script phát animation (BƯỚC 2)

| Bước | Thao tác |
|------|----------|
| 1 | Explorer → **StarterPlayer** → **StarterPlayerScripts** |
| 2 | Right-click **StarterPlayerScripts** → **Insert Object** → **LocalScript** |
| 3 | Đổi tên: `PlayAnimationById` (hoặc tên bạn chọn) |
| 4 | Paste code và thay `123456789` bằng Animation ID thật |

#### Module AnimationIDs (BƯỚC 3)

| Bước | Thao tác |
|------|----------|
| 1 | Explorer → **ReplicatedStorage** |
| 2 | Right-click **ReplicatedStorage** → **Insert Object** → **ModuleScript** |
| 3 | Đổi tên: `AnimationIDs` |
| 4 | Paste code và thay các ID |

### Đường dẫn đầy đủ trong code

```lua
-- Script trong StarterPlayerScripts gọi Module:
local AnimationIDs = require(game.ReplicatedStorage.AnimationIDs)

-- Script tham chiếu Animation object (nếu tạo trong ReplicatedStorage):
local walkAnim = game.ReplicatedStorage:WaitForChild("WalkAnim")
```

---

## BƯỚC 1: Hiểu Cấu Trúc KeyframeSequence (Save Locally)

**Vị trí:** Cell 11 - Phần "2.1 Save Animation Locally"

### Code ở đâu?
Phần **"KeyframeSequence là gì?"** - mô tả cấu trúc dữ liệu:

```lua
-- KeyframeSequence chứa tất cả keyframes của animation
-- Cấu trúc trong Explorer:

KeyframeSequence ("Walk")
├── Keyframe (Time = 0)
│   └── Pose ("LowerTorso")
│       ├── CFrame = ...
│       └── Pose ("UpperTorso")
│           └── Pose ("Head")
│           └── Pose ("LeftUpperArm")
│           └── ...
├── Keyframe (Time = 0.5)
│   └── ...
└── Keyframe (Time = 1.0)
    └── ...
```

### Thao tác từng bước

1. **Đây KHÔNG phải code chạy được** - đây là mô tả cấu trúc trong Explorer

2. **Sau khi Save animation:**
   - Vào Explorer → Rig (Model) → AnimSaves (Folder)
   - Bên trong có các KeyframeSequence (Walk, Run, v.v.)

3. **Dùng để:** Hiểu animation được lưu như thế nào; có thể đọc/duyệt qua code nếu cần

---

## BƯỚC 2: Sử Dụng Animation ID Trong Script

**Vị trí:** Cell 13 - Phần "2.3 Lấy Animation ID"

### Code ở đâu?
Phần **"Sử dụng Animation ID trong Script"**:

```lua
-- Cách sử dụng Animation ID

local animation = Instance.new("Animation")

-- Format đúng:
animation.AnimationId = "rbxassetid://123456789"

-- KHÔNG dùng URL đầy đủ:
-- animation.AnimationId = "https://www.roblox.com/library/123456789"  ❌

-- Load và phát
local animator = humanoid:WaitForChild("Animator")
local track = animator:LoadAnimation(animation)
track:Play()
```

### Script được lưu ở đâu?

| Vị trí | Đường dẫn | Loại Script |
|--------|-----------|-------------|
| Khuyến nghị | `StarterPlayer > StarterPlayerScripts` | LocalScript |
| Đường dẫn trong Explorer | `game.StarterPlayer.StarterPlayerScripts` | - |

### Thao tác từng bước

1. **Lấy Animation ID trước:**
   - Publish animation (Menu ⋮ → Publish to Roblox)
   - Copy ID từ popup sau khi publish
   - Hoặc: create.roblox.com → Development Items → Animations

2. **Tạo Script:** Explorer → **StarterPlayer** → **StarterPlayerScripts** → Right-click → **Insert Object** → **LocalScript**

3. **Copy code** và thay `123456789` bằng Animation ID thật

4. **Đảm bảo** đã có `humanoid` (ví dụ: `local humanoid = character:WaitForChild("Humanoid")`)

5. **Chạy game** để kiểm tra animation phát

---

## BƯỚC 3: Tạo Module Lưu Trữ Animation IDs

**Vị trí:** Cell 13 - Phần "Lưu trữ Animation IDs"

### Code ở đâu?
Phần **"Lưu trữ Animation IDs"** - ModuleScript:

```lua
-- Nên tạo module để lưu trữ tất cả Animation IDs

-- AnimationIDs.lua (ModuleScript)
local AnimationIDs = {
    -- Movement
    Walk = "rbxassetid://111111111",
    Run = "rbxassetid://222222222",
    Jump = "rbxassetid://333333333",
    
    -- Combat
    Attack1 = "rbxassetid://444444444",
    Attack2 = "rbxassetid://555555555",
    Block = "rbxassetid://666666666",
    
    -- Emotes
    Wave = "rbxassetid://777777777",
    Dance = "rbxassetid://888888888",
}

return AnimationIDs
```

### Module được lưu ở đâu?

| Vị trí | Đường dẫn | Loại |
|--------|-----------|------|
| Bắt buộc | `ReplicatedStorage` | ModuleScript |
| Đường dẫn trong code | `game.ReplicatedStorage.AnimationIDs` | - |

### Thao tác từng bước

1. **Tạo ModuleScript:** Explorer → **ReplicatedStorage** → Right-click → **Insert Object** → **ModuleScript** → Đổi tên thành `AnimationIDs`

2. **Xóa code mặc định** và paste code trên

3. **Thay thế** `111111111`, `222222222`, ... bằng Animation ID thật của bạn

4. **Script gọi module** phải ở `StarterPlayerScripts` (LocalScript). Ví dụ sử dụng:
   ```lua
   local AnimationIDs = require(game.ReplicatedStorage.AnimationIDs)
   
   local anim = Instance.new("Animation")
   anim.AnimationId = AnimationIDs.Walk
   local track = animator:LoadAnimation(anim)
   track:Play()
   ```

---

## BƯỚC 4: Quy Trình Tổng Hợp (Editor → Code)

### Từng bước từ tạo animation đến phát trong game

| Bước | Nơi thực hiện | Hành động |
|------|---------------|-----------|
| 1 | Roblox Studio - Avatar tab | Rig Builder → Create Rig R15 |
| 2 | Animation Editor | Chọn Rig → Create New Animation |
| 3 | Animation Editor | Thêm keyframes, rotate body parts |
| 4 | Animation Editor | Menu ⋮ → Save (lưu locally) |
| 5 | Animation Editor | Menu ⋮ → Publish to Roblox |
| 6 | Popup sau Publish | Copy Animation ID |
| 7 | Script | Dùng code BƯỚC 2 (hoặc BƯỚC 3) để phát |

---

## Các Thao Tác Không Phải Code (Ghi Chú)

Notebook 1.3 chủ yếu hướng dẫn **giao diện**, không cần gõ code:

- **Cell 2:** Mở Animation Editor (Avatar → Animation Editor)
- **Cell 3:** Tạo Rig R15 (Avatar → Rig Builder)
- **Cell 4:** Tạo animation mới (dropdown → Create New)
- **Cell 5:** Thêm/xóa keyframes (phím K, Delete)
- **Cell 6:** Rotate/Move body parts (phím R, T)
- **Cell 7:** Sử dụng Timeline (Space, mũi tên)
- **Cell 8:** Play/Preview (nút Play, Space)
- **Cell 9:** Easing Styles (Right-click keyframe → Easing Style)
- **Cell 11:** Save Locally (Menu ⋮ → Save)
- **Cell 12:** Publish (Menu ⋮ → Publish to Roblox)
- **Cell 13:** Lấy ID (popup sau publish, hoặc create.roblox.com)

---

## ✅ Checklist Thực Hành

- [ ] Tạo Rig R15 và animation mới trong Animation Editor
- [ ] Publish animation và copy Animation ID
- [ ] Viết script phát animation với `AnimationId` đúng format
- [ ] (Tùy chọn) Tạo ModuleScript `AnimationIDs` và require trong script

---

## 📂 Cấu Trúc File Trong Project

### Trên máy tính (folder dự án)

```
Level-1-Beginner/
└── 1.3-Animation-Editor/
    ├── Animation-Editor.ipynb        ← Notebook chính
    └── HUONG-DAN-THAO-TAC-CODE.md   ← File này (hướng dẫn tham chiếu)
```

### Trong Roblox Studio Explorer (sau khi thực hành)

```
Explorer
│
├── StarterPlayer
│   └── StarterPlayerScripts
│       └── PlayAnimationById (LocalScript)   ← Script phát animation (BƯỚC 2)
│
├── ReplicatedStorage
│   └── AnimationIDs (ModuleScript)           ← Module lưu IDs (BƯỚC 3)
│
└── Workspace
    └── Rig (Model)
        └── AnimSaves (Folder)                ← Sau khi Save Locally
            ├── Walk (KeyframeSequence)
            ├── Run (KeyframeSequence)
            └── Wave (KeyframeSequence)
```

### Tóm tắt đường dẫn Script

| Script/Module | Vị trí lưu | Đường dẫn trong code |
|---------------|------------|----------------------|
| Script phát animation | `StarterPlayer.StarterPlayerScripts` | `script` (tự tham chiếu) |
| Module AnimationIDs | `ReplicatedStorage` | `game.ReplicatedStorage.AnimationIDs` |
| KeyframeSequence | `Workspace.Rig.AnimSaves` | Dùng Animation Editor, không cần gọi từ script |
