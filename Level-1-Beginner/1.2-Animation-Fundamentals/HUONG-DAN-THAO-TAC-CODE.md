# 📋 Hướng Dẫn Thao Tác Code - 1.2 Animation Fundamentals

> Tài liệu hướng dẫn từng bước: **Code ở đâu** và **Cách thực hiện** trong notebook này.

---

## 📍 Tổng Quan Vị Trí Code

| Phần | Cell | Nội dung code |
|------|------|---------------|
| 1.1 Animation | Cell 2 | Luồng phát animation cơ bản |
| 2.2 R15 Body Parts | Cell 8 | Danh sách 15 body parts |
| 2.3 HumanoidRootPart | Cell 9 | Sử dụng HumanoidRootPart trong script |
| 3.1 Priority | Cell 11 | Enum AnimationPriority |
| 3.2 Priority thực tế | Cell 12 | Setup combat system với Priority |

---

## 📂 SCRIPT ĐƯỢC LƯU Ở ĐÂU? (Chi tiết)

### Cấu trúc Roblox Studio Explorer

```
Roblox Studio - Explorer
│
├── StarterPlayer
│   └── StarterPlayerScripts      ← LocalScript phát animation cho player
│       ├── PlayBasicAnimation (LocalScript)
│       ├── PlayAnimationOnKeyPress (LocalScript)
│       └── AnimationSystem (LocalScript)
│
├── StarterCharacterScripts       ← Script clone vào mỗi character mới spawn
│   └── CharacterAnimationController (LocalScript)
│
├── ReplicatedStorage
│   └── AnimationIDs (ModuleScript)  ← Lưu trữ Animation IDs, dùng chung
│
└── ServerScriptService           ← Script server (ít dùng cho animation player)
    └── NPCEmoteController (Script)  ← Nếu cần control NPC animation
```

### Bảng chọn vị trí Script

| Mục đích | Vị trí | Loại Script | Ghi chú |
|----------|--------|-------------|---------|
| Phát animation cho **player** khi nhấn phím | `StarterPlayer > StarterPlayerScripts` | **LocalScript** | Khuyến nghị cho emotes, combat |
| Phát animation khi **character spawn** | `StarterPlayer > StarterPlayerScripts` | **LocalScript** | Dùng `CharacterAdded` |
| Script theo **character** (clone vào mỗi char) | `StarterCharacterScripts` | **LocalScript** | `script.Parent` = Character |
| Lưu Animation IDs | `ReplicatedStorage` | **ModuleScript** | `require()` từ script khác |
| Control **NPC** animation | `ServerScriptService` | **Script** | Server phát cho NPC |

### Cách tạo Script đúng vị trí

| Bước | Thao tác |
|------|----------|
| 1 | Mở **Explorer** (View → Explorer) |
| 2 | Mở rộng **StarterPlayer** |
| 3 | Right-click **StarterPlayerScripts** → **Insert Object** |
| 4 | Chọn **LocalScript** (phát animation cho player) |
| 5 | Đổi tên script (ví dụ: `PlayBasicAnimation`) |
| 6 | Double-click để mở và paste code |

### Vì sao dùng LocalScript trong StarterPlayerScripts?

- **LocalScript** chạy trên **client** (máy player) → Input (phím, chuột) hoạt động
- **StarterPlayerScripts** clone vào **PlayerGui** khi player join → luôn có character
- Animation player thường cần `UserInputService` (nhấn E, F...) → phải dùng LocalScript

---

## BƯỚC 1: Luồng Phát Animation Cơ Bản

**Vị trí:** Cell 2 - Phần "1.1 Animation là gì trong Roblox?"

### Code ở đâu?
Trong notebook, tìm phần có tiêu đề **"Ví dụ thực tế"** với đoạn code:

```lua
-- Luồng cơ bản để phát một animation

-- Bước 1: Tạo Animation instance
local animation = Instance.new("Animation")
animation.AnimationId = "rbxassetid://123456789"

-- Bước 2: Lấy Animator từ Humanoid
local humanoid = character:WaitForChild("Humanoid")
local animator = humanoid:WaitForChild("Animator")

-- Bước 3: Load animation thành AnimationTrack
local animationTrack = animator:LoadAnimation(animation)

-- Bước 4: Phát animation
animationTrack:Play()
```

### Script được lưu ở đâu?

| Kịch bản | Vị trí | Loại | Đường dẫn đầy đủ |
|----------|--------|------|------------------|
| Phát cho player khi game start | `StarterPlayer > StarterPlayerScripts` | LocalScript | `game.StarterPlayer.StarterPlayerScripts.PlayBasicAnimation` |
| Phát cho character cụ thể (NPC) | `ServerScriptService` | Script | `game.ServerScriptService.NPCAnimController` |
| Trong Character (script.Parent = Character) | `StarterCharacterScripts` | LocalScript | Clone vào `Character` khi spawn |

### Thao tác từng bước

1. **Mở Roblox Studio** → Explorer → **StarterPlayer** → **StarterPlayerScripts** → Right-click → **Insert Object** → **LocalScript**

2. **Copy 4 đoạn code** theo thứ tự:
   - Tạo Animation và gán `AnimationId` (thay `123456789` bằng ID thật)
   - Lấy Humanoid và Animator từ character
   - Load animation bằng `LoadAnimation()`
   - Gọi `Play()` để phát

3. **Lưu ý:** Biến `character` phải được định nghĩa (ví dụ: `local character = script.Parent` nếu script trong Character)

---

## BƯỚC 2: Danh Sách R15 Body Parts

**Vị trí:** Cell 8 - Phần "2.2 Các Body Parts của R15"

### Code ở đâu?
Phần **"Danh sách đầy đủ 15 Body Parts"** - table Lua chứa tên các bộ phận:

```lua
local R15_Parts = {
    "Head",
    "UpperTorso", "LowerTorso",
    "RightUpperArm", "RightLowerArm", "RightHand",
    "LeftUpperArm", "LeftLowerArm", "LeftHand",
    "RightUpperLeg", "RightLowerLeg", "RightFoot",
    "LeftUpperLeg", "LeftLowerLeg", "LeftFoot",
}
```

### Thao tác từng bước

1. **Dùng khi nào?** Khi cần iterate qua các body parts, kiểm tra animation, hoặc tham khảo tên chính xác

2. **Lưu script ở đâu?** Thường trong cùng script đang xử lý animation: `StarterPlayer > StarterPlayerScripts` (LocalScript)

3. **Ví dụ sử dụng:**
   ```lua
   for _, partName in ipairs(R15_Parts) do
       local part = character:FindFirstChild(partName)
       if part then
           print(partName, part.CFrame)
       end
   end
   ```

---

## BƯỚC 3: Sử Dụng HumanoidRootPart

**Vị trí:** Cell 9 - Phần "2.3 HumanoidRootPart và Vai trò của nó"

### Code ở đâu?
Phần **"Sử dụng trong Script"** với 4 ví dụ:

```lua
-- Lấy vị trí character
local position = character.HumanoidRootPart.Position

-- Teleport character
character.HumanoidRootPart.CFrame = CFrame.new(0, 100, 0)

-- Hướng character đang nhìn
local lookVector = character.HumanoidRootPart.CFrame.LookVector

-- Xoay character
character.HumanoidRootPart.CFrame = 
    CFrame.new(character.HumanoidRootPart.Position) * 
    CFrame.Angles(0, math.rad(90), 0)
```

### Thao tác từng bước

1. **Xác định mục đích:**
   - Lấy vị trí → dùng `Position`
   - Teleport → gán `CFrame` mới
   - Lấy hướng nhìn → `CFrame.LookVector`
   - Xoay → nhân `CFrame` với `CFrame.Angles()`

2. **Copy đoạn cần dùng** vào script trong `StarterPlayerScripts` hoặc `ServerScriptService` (tùy đối tượng: player hay NPC)

3. **Chạy trong game** - đảm bảo `character` đã có sẵn

---

## BƯỚC 4: Enum Animation Priority

**Vị trí:** Cell 11 - Phần "3.1 Hiểu các mức Priority"

### Code ở đâu?
Phần **"Enum trong Luau"**:

```lua
Enum.AnimationPriority.Core      -- 0 (thấp nhất)
Enum.AnimationPriority.Idle      -- 1
Enum.AnimationPriority.Movement  -- 2
Enum.AnimationPriority.Action    -- 3
Enum.AnimationPriority.Action2   -- 4
Enum.AnimationPriority.Action3   -- 5
Enum.AnimationPriority.Action4   -- 6 (cao nhất)
```

### Thao tác từng bước

1. **Chọn Priority** phù hợp với loại animation (xem bảng trong Cell 12)

2. **Áp dụng khi LoadAnimation:**
   ```lua
   local track = animator:LoadAnimation(animation)
   track.Priority = Enum.AnimationPriority.Action
   track:Play()
   ```

3. **Ghi nhớ:** Action cao hơn Movement → attack đè lên run

---

## BƯỚC 5: Setup Combat System với Priority

**Vị trí:** Cell 12 - Phần "3.2 Khi nào dùng Priority nào?"

### Code ở đâu?
Phần **"Ví dụ thực tế: Combat System"** - đoạn code dài setup Idle, Walk, Attack combo, Ultimate

### Thao tác từng bước

1. **Chuẩn bị:**
   - Có sẵn các Animation instance (idleAnim, walkAnim, attack1Anim, v.v.)
   - Đã có Animator từ Humanoid

2. **Copy từng block code:**
   - Idle: Priority Idle, Looped = true
   - Walk: Priority Movement
   - Attack 1/2/3: Priority Action, Action2, Action3
   - Ultimate: Priority Action4

3. **Tích hợp vào game logic:**
   - Gọi `walkTrack:Play()` khi player di chuyển
   - Gọi `attack1Track:Play()` khi nhấn attack
   - Điều kiện chuyển giữa các track

4. **Thiết lập Priority qua Script (nếu cần override):**
   ```lua
   track.Priority = Enum.AnimationPriority.Action2
   track:Play()
   ```

---

## ✅ Checklist Thực Hành

- [ ] Chạy được luồng phát animation cơ bản (Cell 2)
- [ ] Sử dụng R15 body parts table khi cần (Cell 8)
- [ ] Thao tác HumanoidRootPart (Cell 9)
- [ ] Áp dụng đúng Priority cho từng loại animation (Cell 11-12)
- [ ] Setup combat system với nhiều AnimationTrack (Cell 12)

---

## 📂 Cấu Trúc File Trong Project

### Trên máy tính (folder dự án)

```
Level-1-Beginner/
└── 1.2-Animation-Fundamentals/
    ├── Animation-Fundamentals.ipynb   ← Notebook chính (chứa tất cả code)
    └── HUONG-DAN-THAO-TAC-CODE.md    ← File này (hướng dẫn tham chiếu)
```

### Trong Roblox Studio (sau khi tạo scripts)

```
Explorer
├── StarterPlayer
│   └── StarterPlayerScripts
│       ├── PlayBasicAnimation (LocalScript)      ← BƯỚC 1
│       ├── R15PartsReference (LocalScript)      ← BƯỚC 2 (nếu tách riêng)
│       └── CombatAnimationSystem (LocalScript)  ← BƯỚC 5
│
└── ReplicatedStorage
    └── (tuỳ chọn) AnimationIDs (ModuleScript)   ← Nếu dùng module
```
