# 🗺️ ROADMAP: Animation trong Roblox Studio (Luau)

## Tổng Quan

Roadmap này hướng dẫn bạn từ **người mới bắt đầu** đến **chuyên gia animation** trong Roblox Studio. Mỗi level có các kỹ năng cần học và project thực hành.

---

## 📊 Các Giai Đoạn

```
┌─────────────────────────────────────────────────────────────────────────┐
│  LEVEL 1: BEGINNER (2-4 tuần)                                          │
│  ↓                                                                      │
│  LEVEL 2: INTERMEDIATE (4-6 tuần)                                       │
│  ↓                                                                      │
│  LEVEL 3: ADVANCED (6-8 tuần)                                           │
│  ↓                                                                      │
│  LEVEL 4: EXPERT (Ongoing)                                              │
└─────────────────────────────────────────────────────────────────────────┘
```

---

# 🟢 LEVEL 1: BEGINNER (Người Mới)

## Mục Tiêu
> Hiểu cơ bản về animation trong Roblox và tạo được animation đơn giản

## 1.1 Kiến Thức Nền Tảng

### Roblox Studio Basics
- [ ] Cài đặt và làm quen Roblox Studio
- [ ] Hiểu cấu trúc Explorer và Properties
- [ ] Hiểu các loại Instance cơ bản (Part, Model, Script)
- [ ] Biết cách Test game (Play, Play Here)

### Luau Basics (Nếu chưa biết)
- [ ] Variables và Data Types
- [ ] Functions
- [ ] Events và Connections
- [ ] Tables
- [ ] Loops (for, while)

### Resources:
- 📚 [Roblox Creator Hub](https://create.roblox.com/docs)
- 📚 [Luau Documentation](https://luau-lang.org/)

---

## 1.2 Animation Fundamentals

### Hiểu về Animation
- [ ] Animation là gì trong Roblox?
- [ ] Keyframe là gì?
- [ ] Timeline hoạt động như thế nào?
- [ ] FPS (Frames Per Second) và timing

### Character Rigs
- [ ] Sự khác nhau giữa R6 và R15
- [ ] Các body parts của R15:
  ```
  Head, UpperTorso, LowerTorso
  LeftUpperArm, LeftLowerArm, LeftHand
  RightUpperArm, RightLowerArm, RightHand
  LeftUpperLeg, LeftLowerLeg, LeftFoot
  RightUpperLeg, RightLowerLeg, RightFoot
  ```
- [ ] HumanoidRootPart và vai trò của nó

### Animation Priority
- [ ] Hiểu các mức Priority:
  ```
  Core < Idle < Movement < Action < Action2 < Action3 < Action4
  ```
- [ ] Khi nào dùng priority nào?

---

## 1.3 Animation Editor

### Sử Dụng Animation Editor
- [ ] Mở Animation Editor (Avatar → Animation Editor)
- [ ] Tạo Rig R15 (Avatar → Rig Builder)
- [ ] Tạo animation mới
- [ ] Thêm/xóa keyframes
- [ ] Rotate và Move body parts
- [ ] Sử dụng Timeline
- [ ] Play/Preview animation
- [ ] Easing Styles (Linear, Cubic, Bounce...)

### Publish Animation
- [ ] Save animation locally
- [ ] Publish to Roblox
- [ ] Lấy Animation ID
- [ ] Hiểu về animation ownership

---

## 1.4 Scripting Animation Cơ Bản

### Các Class Quan Trọng
```lua
-- Animation: Chứa AnimationId
local animation = Instance.new("Animation")
animation.AnimationId = "rbxassetid://123456789"

-- Animator: Load và quản lý animations
local animator = humanoid:WaitForChild("Animator")

-- AnimationTrack: Animation đã được load, có thể Play/Stop
local track = animator:LoadAnimation(animation)
```

### Kỹ Năng Cần Có
- [ ] Tạo Animation object
- [ ] Load animation với Animator
- [ ] Play và Stop animation
- [ ] Thiết lập Looped và Priority
- [ ] Xử lý sự kiện Stopped

### Script Mẫu Đầu Tiên
```lua
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local animator = humanoid:WaitForChild("Animator")

local animation = Instance.new("Animation")
animation.AnimationId = "rbxassetid://YOUR_ID"

local track = animator:LoadAnimation(animation)
track:Play()
```

---

## 1.5 Project Thực Hành Level 1

### Project 1: Wave Emote
- [ ] Tạo animation vẫy tay đơn giản
- [ ] Phát khi nhấn phím E

### Project 2: Jump Animation
- [ ] Tạo custom jump animation
- [ ] Thay thế jump mặc định

### Project 3: Idle Variation
- [ ] Tạo 2-3 idle animations
- [ ] Random play sau vài giây đứng yên

---

## ✅ Checklist Level 1 Hoàn Thành
- [ ] Tạo được animation trong Animation Editor
- [ ] Publish animation lên Roblox
- [ ] Viết script phát animation cơ bản
- [ ] Hiểu Priority và Looping
- [ ] Hoàn thành 3 projects

---

# 🟡 LEVEL 2: INTERMEDIATE (Trung Cấp)

## Mục Tiêu
> Tạo được hệ thống animation hoàn chỉnh cho một loại game

## 2.1 Animation Nâng Cao

### Nhiều Animation Cùng Lúc
- [ ] Animation blending với Weight
- [ ] Phát nhiều tracks đồng thời
- [ ] Ưu tiên animation đúng cách

```lua
-- Blend 2 animations
walkTrack:Play()
walkTrack:AdjustWeight(0.5)

runTrack:Play()
runTrack:AdjustWeight(0.5)
```

### Animation Speed
- [ ] Điều chỉnh tốc độ animation
- [ ] Sync animation với game events

```lua
track:AdjustSpeed(1.5)  -- 150% speed
track:AdjustSpeed(0.5)  -- 50% speed
```

### Animation Events (Markers)
- [ ] Thêm markers trong Animation Editor
- [ ] Lắng nghe marker events trong script
- [ ] Sử dụng cho damage timing, sound effects, VFX

```lua
track:GetMarkerReachedSignal("HitPoint"):Connect(function()
    -- Deal damage here
end)
```

---

## 2.2 Combat Animation System

### Attack Animations
- [ ] Single attack animation
- [ ] Combo system (2-4 hits)
- [ ] Heavy/Light attacks
- [ ] Weapon-specific animations

### Defense Animations
- [ ] Block/Guard animation
- [ ] Parry animation
- [ ] Hit reaction (bị đánh)
- [ ] Death animation

### Movement Animations
- [ ] Dash/Dodge
- [ ] Roll
- [ ] Sprint

---

## 2.3 Animation State Machine

### Concept
Quản lý trạng thái animation một cách có tổ chức

```lua
local states = {
    IDLE = "idle",
    WALK = "walk",
    RUN = "run",
    ATTACK = "attack",
    BLOCK = "block",
}

local currentState = states.IDLE

local function changeState(newState)
    if currentState == newState then return end
    
    -- Stop current animation
    stopAnimation(currentState)
    
    -- Start new animation
    playAnimation(newState)
    
    currentState = newState
end
```

### Kỹ Năng
- [ ] Thiết kế state machine
- [ ] Transition giữa các states
- [ ] Handle input để change states
- [ ] Prevent invalid state changes

---

## 2.4 Tool & Weapon Animations

### Tool Animations
- [ ] Equip/Unequip animations
- [ ] Idle with tool
- [ ] Use tool animation

### Weapon System
- [ ] Sword animations
- [ ] Gun animations (aim, shoot, reload)
- [ ] Magic staff animations

### Attach Points
- [ ] Weld weapon to hand
- [ ] Motor6D cho weapon movement
- [ ] Grip positioning

---

## 2.5 Replacing Default Animations

### Animate Script
- [ ] Hiểu cấu trúc Animate script
- [ ] Thay thế individual animations
- [ ] Custom walk, run, jump, fall, climb, swim

```lua
-- Trong StarterCharacterScripts
local animate = character:WaitForChild("Animate")
local walk = animate:WaitForChild("walk")
walk.WalkAnim.AnimationId = "rbxassetid://YOUR_WALK_ID"
```

---

## 2.6 Project Thực Hành Level 2

### Project 1: Melee Combat System
- [ ] 3-hit combo
- [ ] Block and parry
- [ ] Hit reactions
- [ ] Death animation

### Project 2: Emote Wheel
- [ ] 8-12 emotes
- [ ] Wheel UI
- [ ] Looped và one-shot emotes

### Project 3: Custom Character Controller
- [ ] Custom walk/run
- [ ] Sprint system
- [ ] Dodge/roll

---

## ✅ Checklist Level 2 Hoàn Thành
- [ ] Tạo combo system
- [ ] Implement state machine
- [ ] Sử dụng animation markers
- [ ] Replace default animations
- [ ] Hoàn thành 3 projects

---

# 🟠 LEVEL 3: ADVANCED (Nâng Cao)

## Mục Tiêu
> Master animation systems và tối ưu hóa

## 3.1 Procedural Animation

### Inverse Kinematics (IK)
- [ ] Hiểu IK concept
- [ ] Foot IK (chân bám đất)
- [ ] Hand IK (tay hướng về target)
- [ ] Look At IK (đầu nhìn theo target)

```lua
-- Sử dụng IKControl
local ikControl = Instance.new("IKControl")
ikControl.Type = Enum.IKControlType.LookAt
ikControl.Target = targetPart
ikControl.ChainRoot = character.Head
ikControl.EndEffector = character.Head
ikControl.Parent = humanoid
```

### Procedural Movement
- [ ] Lean khi turning
- [ ] Head bob khi walking
- [ ] Breathing animation procedural
- [ ] Ragdoll physics

---

## 3.2 Network Animation (Multiplayer)

### Client-Server Animation
- [ ] Animation replication
- [ ] RemoteEvents cho animation sync
- [ ] Validate animation requests
- [ ] Anti-cheat considerations

```lua
-- Server Script
local AnimationEvent = game.ReplicatedStorage.AnimationEvent

AnimationEvent.OnServerEvent:Connect(function(player, animationName)
    -- Validate
    if not isValidAnimation(animationName) then return end
    
    -- Broadcast to other clients
    AnimationEvent:FireAllClients(player, animationName)
end)
```

### Optimization
- [ ] Animation pooling
- [ ] Level of Detail (LOD) for animations
- [ ] Cull animations out of view

---

## 3.3 Custom Rigs

### Tạo Custom Rig
- [ ] Non-humanoid characters
- [ ] Animals, monsters, vehicles
- [ ] Mechanical rigs
- [ ] Multi-limb creatures

### Skinned Meshes
- [ ] Import skinned mesh từ Blender
- [ ] Bone structure
- [ ] Weight painting
- [ ] Animation từ external software

---

## 3.4 Advanced VFX Integration

### Particles với Animation
- [ ] Emit particles at keyframes
- [ ] Trail effects
- [ ] Impact effects
- [ ] Aura/buff effects

### Camera Animation
- [ ] Camera shake
- [ ] Cinematic cameras
- [ ] FOV changes
- [ ] Focus effects

---

## 3.5 Animation Tools Development

### Custom Animation Tools
- [ ] Animation preview plugin
- [ ] Batch animation editor
- [ ] Animation converter

### Debug Tools
- [ ] Animation debugger
- [ ] State machine visualizer
- [ ] Performance profiler

---

## 3.6 Project Thực Hành Level 3

### Project 1: Boss Fight System
- [ ] Complex boss with many animations
- [ ] Phase transitions
- [ ] Attack patterns
- [ ] Environmental interactions

### Project 2: Vehicle Animation System
- [ ] Enter/exit animations
- [ ] Driving animations
- [ ] Damage states

### Project 3: Cutscene System
- [ ] Camera animations
- [ ] Character animations
- [ ] Dialog integration
- [ ] Trigger system

---

## ✅ Checklist Level 3 Hoàn Thành
- [ ] Implement IK system
- [ ] Handle multiplayer animations
- [ ] Create custom rigs
- [ ] Integrate VFX with animations
- [ ] Build animation tools
- [ ] Hoàn thành 3 projects

---

# 🔴 LEVEL 4: EXPERT (Chuyên Gia)

## Mục Tiêu
> Đóng góp cho cộng đồng và push boundaries

## 4.1 Chuyên Môn Sâu

### Animation Director
- [ ] Lead animation team
- [ ] Style guide creation
- [ ] Quality control
- [ ] Performance budgets

### Technical Animation
- [ ] Optimize cho mobile
- [ ] Memory management
- [ ] Frame budget management
- [ ] Profiling và optimization

---

## 4.2 Research & Innovation

### Mới Nhất Từ Roblox
- [ ] Follow Roblox release notes
- [ ] Beta features
- [ ] DevForum discussions

### Techniques Từ Industry
- [ ] GDC talks về animation
- [ ] AAA game animation techniques
- [ ] Motion capture concepts

---

## 4.3 Community Contribution

### Chia Sẻ Kiến Thức
- [ ] Viết tutorials
- [ ] Tạo plugins miễn phí
- [ ] Answer questions on DevForum
- [ ] YouTube/stream tutorials

### Open Source
- [ ] Publish animation frameworks
- [ ] Contribute to community resources
- [ ] Code reviews

---

## 4.4 Portfolio & Career

### Build Portfolio
- [ ] Showcase best work
- [ ] Diverse projects
- [ ] Before/after comparisons
- [ ] Technical breakdowns

### Career Paths
- [ ] Freelance animator
- [ ] Studio animator
- [ ] Technical animator
- [ ] Animation lead

---

# 📚 RESOURCES

## Official
- [Roblox Creator Hub - Animation](https://create.roblox.com/docs/animation)
- [Roblox DevForum](https://devforum.roblox.com/)
- [Luau Documentation](https://luau-lang.org/)

## Community
- YouTube: "Roblox animation tutorial"
- DevForum Animation category
- Discord servers (Hidden Developers, etc.)

## External Tools
- Blender (free 3D software)
- Moon Animator plugin
- Animation editors on Toolbox

---

# 🎯 TIMELINE GỢI Ý

| Level | Thời Gian | Focus |
|-------|-----------|-------|
| Level 1 | 2-4 tuần | Fundamentals, Editor, Basic scripting |
| Level 2 | 4-6 tuần | Combat, State machine, Tools |
| Level 3 | 6-8 tuần | IK, Multiplayer, Custom rigs |
| Level 4 | Ongoing | Mastery, Teaching, Innovation |

**Tổng thời gian đến proficient: ~3-4 tháng** (học mỗi ngày 1-2 tiếng)

---

# 💡 TIPS CHUNG

1. **Practice Daily**: Tạo ít nhất 1 animation mỗi ngày khi học
2. **Study Games**: Phân tích animation trong games bạn thích
3. **Reference Videos**: Quay video thực tế để reference
4. **Iterate**: Animation hiếm khi đúng lần đầu, iterate nhiều lần
5. **Get Feedback**: Chia sẻ và nhận feedback từ người khác
6. **Stay Updated**: Roblox cập nhật thường xuyên

---

## 🚀 BẮT ĐẦU NGAY

1. Đọc folder `Huong-Dan/` trong project này
2. Làm theo từng bước trong Level 1
3. Hoàn thành các project thực hành
4. Tiến lên Level tiếp theo

**Chúc bạn thành công trên hành trình trở thành Animation Expert trong Roblox!**
