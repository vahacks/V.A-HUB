--========================================================
-- V.A HUB - FULL MOBILE TEST HUB
-- For your own Roblox experience / testing
-- Password: Olol
--========================================================

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local player = Players.LocalPlayer
local camera = workspace.CurrentCamera

--========================================================
-- SETTINGS
--========================================================

local PASSWORD = "Olol"

local SPEED_VALUE = 9999
local JUMP_VALUE = 9999
local FLY_SPEED = 80
local AIM_SIZE = 9999

local speedOn = false
local jumpOn = false
local flyOn = false
local invisibleOn = false
local noclipOn = false
local espOn = false
local boxOn = false
local lineOn = false
local aimOn = false
local cameraLockOn = false
local godOn = false
local testModeOn = false

local currentTarget = nil
local flyVelocity = nil

--========================================================
-- GUI
--========================================================

local gui = Instance.new("ScreenGui")
gui.Name = "VA_HUB"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = player:WaitForChild("PlayerGui")

--========================================================
-- LOGIN
--========================================================

local login = Instance.new("Frame")
login.AnchorPoint = Vector2.new(0.5, 0.5)
login.Position = UDim2.new(0.5, 0, 0.5, 0)
login.Size = UDim2.new(0.42, 0, 0.32, 0)
login.BackgroundColor3 = Color3.fromRGB(6, 10, 8)
login.BorderSizePixel = 0
login.Parent = gui

local loginCorner = Instance.new("UICorner")
loginCorner.CornerRadius = UDim.new(0, 14)
loginCorner.Parent = login

local loginLimit = Instance.new("UISizeConstraint")
loginLimit.MinSize = Vector2.new(270, 180)
loginLimit.MaxSize = Vector2.new(450, 300)
loginLimit.Parent = login

local loginTitle = Instance.new("TextLabel")
loginTitle.Size = UDim2.new(1, -20, 0, 45)
loginTitle.Position = UDim2.new(0, 10, 0, 10)
loginTitle.BackgroundTransparency = 1
loginTitle.Text = "V.A HUB"
loginTitle.TextColor3 = Color3.fromRGB(0, 255, 120)
loginTitle.TextSize = 25
loginTitle.Font = Enum.Font.GothamBold
loginTitle.Parent = login

local passBox = Instance.new("TextBox")
passBox.Size = UDim2.new(1, -40, 0, 42)
passBox.Position = UDim2.new(0, 20, 0, 65)
passBox.BackgroundColor3 = Color3.fromRGB(15, 25, 20)
passBox.TextColor3 = Color3.fromRGB(230, 255, 240)
passBox.PlaceholderText = "Password"
passBox.PlaceholderColor3 = Color3.fromRGB(120, 150, 130)
passBox.Text = ""
passBox.TextSize = 16
passBox.Font = Enum.Font.Gotham
passBox.ClearTextOnFocus = false
passBox.Parent = login

local passCorner = Instance.new("UICorner")
passCorner.CornerRadius = UDim.new(0, 9)
passCorner.Parent = passBox

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(1, -40, 0, 42)
loginBtn.Position = UDim2.new(0, 20, 1, -57)
loginBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 70)
loginBtn.Text = "LOGIN"
loginBtn.TextColor3 = Color3.new(1, 1, 1)
loginBtn.TextSize = 16
loginBtn.Font = Enum.Font.GothamBold
loginBtn.Parent = login

local loginBtnCorner = Instance.new("UICorner")
loginBtnCorner.CornerRadius = UDim.new(0, 9)
loginBtnCorner.Parent = loginBtn

--========================================================
-- MAIN WINDOW
--========================================================

local main = Instance.new("Frame")
main.AnchorPoint = Vector2.new(0.5, 0.5)
main.Position = UDim2.new(0.5, 0, 0.5, 0)
main.Size = UDim2.new(0.48, 0, 0.82, 0)
main.BackgroundColor3 = Color3.fromRGB(6, 10, 8)
main.BorderSizePixel = 0
main.Visible = false
main.Parent = gui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 16)
mainCorner.Parent = main

local mainLimit = Instance.new("UISizeConstraint")
mainLimit.MinSize = Vector2.new(280, 420)
mainLimit.MaxSize = Vector2.new(700, 900)
mainLimit.Parent = main

local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(3, 8, 5)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(8, 25, 15)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(2, 7, 4))
})
gradient.Rotation = 135
gradient.Parent = main

task.spawn(function()
    while gui.Parent do
        gradient.Rotation = (gradient.Rotation + 1) % 360
        task.wait(0.03)
    end
end)

--========================================================
-- HEADER
--========================================================

local header = Instance.new("TextLabel")
header.Size = UDim2.new(1, -65, 0, 50)
header.Position = UDim2.new(0, 15, 0, 5)
header.BackgroundTransparency = 1
header.Text = "V.A  H U B"
header.TextColor3 = Color3.fromRGB(0, 255, 120)
header.TextSize = 23
header.Font = Enum.Font.GothamBold
header.TextXAlignment = Enum.TextXAlignment.Left
header.Active = true
header.Parent = main

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 42, 0, 42)
closeBtn.Position = UDim2.new(1, -50, 0, 8)
closeBtn.BackgroundColor3 = Color3.fromRGB(120, 20, 20)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.new(1, 1, 1)
closeBtn.TextSize = 18
closeBtn.Font = Enum.Font.GothamBold
closeBtn.Parent = main

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 10)
closeCorner.Parent = closeBtn

--========================================================
-- SCROLL
--========================================================

local scroll = Instance.new("ScrollingFrame")
scroll.Size = UDim2.new(1, -20, 1, -65)
scroll.Position = UDim2.new(0, 10, 0, 60)
scroll.BackgroundTransparency = 1
scroll.BorderSizePixel = 0
scroll.ScrollBarThickness = 4
scroll.Parent = main

local layout = Instance.new("UIGridLayout")
layout.CellSize = UDim2.new(0.47, 0, 0, 48)
layout.CellPadding = UDim2.new(0.03, 0, 0, 8)
layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = scroll

layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    scroll.CanvasSize = UDim2.new(
        0,
        0,
        0,
        layout.AbsoluteContentSize.Y + 15
    )
end)

--========================================================
-- HELPERS
--========================================================

local function getCharacter()
    return player.Character
end

local function getHumanoid()
    local char = getCharacter()
    return char and char:FindFirstChildOfClass("Humanoid")
end

local function getRoot()
    local char = getCharacter()
    return char and char:FindFirstChild("HumanoidRootPart")
end

local function createButton(text)
    local button = Instance.new("TextButton")
    button.BackgroundColor3 = Color3.fromRGB(12, 28, 19)
    button.TextColor3 = Color3.fromRGB(220, 255, 235)
    button.TextSize = 14
    button.Font = Enum.Font.GothamBold
    button.Text = text
    button.Parent = scroll

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 10)
    corner.Parent = button

    local stroke = Instance.new("UIStroke")
    stroke.Color = Color3.fromRGB(0, 180, 85)
    stroke.Transparency = 0.55
    stroke.Parent = button

    return button
end

local function createValueBox(value)
    local box = Instance.new("TextBox")
    box.BackgroundColor3 = Color3.fromRGB(15, 30, 21)
    box.TextColor3 = Color3.fromRGB(0, 255, 120)
    box.Text = tostring(value)
    box.TextSize = 15
    box.Font = Enum.Font.GothamBold
    box.ClearTextOnFocus = false
    box.Parent = scroll

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 10)
    corner.Parent = box

    return box
end

--========================================================
-- SPEED
--========================================================

local speedBtn = createButton("SPEED: OFF")
local speedBox = createValueBox(SPEED_VALUE)

speedBtn.MouseButton1Click:Connect(function()
    speedOn = not speedOn

    local hum = getHumanoid()

    if hum then
        hum.WalkSpeed = speedOn and SPEED_VALUE or 16
    end

    speedBtn.Text = speedOn
        and "SPEED: ON"
        or "SPEED: OFF"
end)

speedBox.FocusLost:Connect(function()
    local value = tonumber(speedBox.Text)

    if value then
        SPEED_VALUE = math.clamp(value, 0, 9999)

        if speedOn then
            local hum = getHumanoid()
            if hum then
                hum.WalkSpeed = SPEED_VALUE
            end
        end
    end

    speedBox.Text = tostring(SPEED_VALUE)
end)

--========================================================
-- JUMP
--========================================================

local jumpBtn = createButton("JUMP: OFF")
local jumpBox = createValueBox(JUMP_VALUE)

jumpBtn.MouseButton1Click:Connect(function()
    jumpOn = not jumpOn

    local hum = getHumanoid()

    if hum then
        hum.UseJumpPower = true
        hum.JumpPower = jumpOn and JUMP_VALUE or 50
    end

    jumpBtn.Text = jumpOn
        and "JUMP: ON"
        or "JUMP: OFF"
end)

jumpBox.FocusLost:Connect(function()
    local value = tonumber(jumpBox.Text)

    if value then
        JUMP_VALUE = math.clamp(value, 0, 9999)

        if jumpOn then
            local hum = getHumanoid()
            if hum then
                hum.UseJumpPower = true
                hum.JumpPower = JUMP_VALUE
            end
        end
    end

    jumpBox.Text = tostring(JUMP_VALUE)
end)

--========================================================
-- FLY
--========================================================

local flyBtn = createButton("FLY: OFF")

local function setFly(state)
    flyOn = state

    local root = getRoot()

    if flyOn and root then
        if flyVelocity then
            flyVelocity:Destroy()
        end

        flyVelocity = Instance.new("BodyVelocity")
        flyVelocity.MaxForce = Vector3.new(
            math.huge,
            math.huge,
            math.huge
        )
        flyVelocity.Velocity = Vector3.zero
        flyVelocity.Parent = root
    else
        if flyVelocity then
            flyVelocity:Destroy()
            flyVelocity = nil
        end
    end

    flyBtn.Text = flyOn
        and "FLY: ON"
        or "FLY: OFF"
end

flyBtn.MouseButton1Click:Connect(function()
    setFly(not flyOn)
end)

RunService.RenderStepped:Connect(function()
    if flyOn and flyVelocity then
        local hum = getHumanoid()

        if hum then
            flyVelocity.Velocity =
                hum.MoveDirection * FLY_SPEED
        end
    end
end)

--========================================================
-- INVISIBLE
--========================================================

local invisibleBtn = createButton("INVISIBLE: OFF")

local function setInvisible(state)
    invisibleOn = state

    local char = getCharacter()
    if not char then return end

    for _, obj in ipairs(char:GetDescendants()) do
        if obj:IsA("BasePart") then
            obj.LocalTransparencyModifier =
                invisibleOn and 1 or 0
        elseif obj:IsA("Decal") then
            obj.Transparency =
                invisibleOn and 1 or 0
        end
    end

    invisibleBtn.Text = invisibleOn
        and "INVISIBLE: ON"
        or "INVISIBLE: OFF"
end

invisibleBtn.MouseButton1Click:Connect(function()
    setInvisible(not invisibleOn)
end)

--========================================================
-- NOCLIP
--========================================================

local noclipBtn = createButton("NOCLIP: OFF")

local function updateNoclip()
    local char = getCharacter()
    if not char then return end

    for _, obj in ipairs(char:GetDescendants()) do
        if obj:IsA("BasePart") then
            obj.CanCollide = not noclipOn
        end
    end
end

noclipBtn.MouseButton1Click:Connect(function()
    noclipOn = not noclipOn

    noclipBtn.Text = noclipOn
        and "NOCLIP: ON"
        or "NOCLIP: OFF"

    updateNoclip()
end)

RunService.Stepped:Connect(function()
    if noclipOn then
        updateNoclip()
    end
end)

--========================================================
-- TEST MODE
--========================================================

local testBtn = createButton("TEST MODE: OFF")

testBtn.MouseButton1Click:Connect(function()
    testModeOn = not testModeOn

    player:SetAttribute(
        "VATestMode",
        testModeOn
    )

    testBtn.Text = testModeOn
        and "TEST MODE: ON"
        or "TEST MODE: OFF"
end)

--========================================================
-- ESP
--========================================================

local espFolder = Instance.new("Folder")
espFolder.Name = "VA_ESP"
espFolder.Parent = gui

local espObjects = {}

local function clearESP()
    for _, obj in ipairs(espObjects) do
        if obj then
            obj:Destroy()
        end
    end

    table.clear(espObjects)
end

local function updateESP()
    clearESP()

    if not espOn and not boxOn then
        return
    end

    local npcFolder = workspace:FindFirstChild("NPCs")
    if not npcFolder then return end

    for _, npc in ipairs(npcFolder:GetChildren()) do
        local hum = npc:FindFirstChildOfClass("Humanoid")
        local root = npc:FindFirstChild("HumanoidRootPart")

        if hum and root and hum.Health > 0 then

            if espOn then
                local highlight = Instance.new("Highlight")
                highlight.Adornee = npc
                highlight.FillColor =
                    Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor =
                    Color3.fromRGB(255, 255, 255)
                highlight.FillTransparency = 0.35
                highlight.OutlineTransparency = 0
                highlight.DepthMode =
                    Enum.HighlightDepthMode.AlwaysOnTop
                highlight.Parent = espFolder

                table.insert(espObjects, highlight)
            end

            if boxOn then
                local box = Instance.new("BoxHandleAdornment")
                box.Adornee = root
                box.Size = Vector3.new(4, 6, 2)
                box.Color3 = Color3.fromRGB(255, 0, 0)
                box.Transparency = 0.45
                box.AlwaysOnTop = true
                box.ZIndex = 5
                box.Parent = espFolder

                table.insert(espObjects, box)
            end
        end
    end
end

local espBtn = createButton("ESP: OFF")

espBtn.MouseButton1Click:Connect(function()
    espOn = not espOn

    espBtn.Text = espOn
        and "ESP: ON"
        or "ESP: OFF"

    updateESP()
end)

local boxBtn = createButton("BOX ESP: OFF")

boxBtn.MouseButton1Click:Connect(function()
    boxOn = not boxOn

    boxBtn.Text = boxOn
        and "BOX ESP: ON"
        or "BOX ESP: OFF"

    updateESP()
end)

--========================================================
-- ESP LINE
--========================================================

local lineGui = Instance.new("ScreenGui")
lineGui.Name = "VA_ESP_LINES"
lineGui.IgnoreGuiInset = true
lineGui.ResetOnSpawn = false
lineGui.Parent = player.PlayerGui

local lines = {}

local function clearLines()
    for _, line in ipairs(lines) do
        if line then
            line:Destroy()
        end
    end

    table.clear(lines)
end

local function updateLines()
    clearLines()

    if not lineOn then return end

    local folder = workspace:FindFirstChild("NPCs")
    if not folder then return end

    local viewport = camera.ViewportSize
    local startPos = Vector2.new(
        viewport.X / 2,
        viewport.Y
    )

    for _, npc in ipairs(folder:GetChildren()) do
        local hum = npc:FindFirstChildOfClass("Humanoid")
        local root = npc:FindFirstChild("HumanoidRootPart")

        if hum and root and hum.Health > 0 then
            local pos, visible =
                camera:WorldToViewportPoint(root.Position)

            if visible and pos.Z > 0 then
                local line = Instance.new("Frame")
                line.AnchorPoint = Vector2.new(0, 0.5)
                line.BorderSizePixel = 0
                line.BackgroundColor3 =
                    Color3.fromRGB(255, 0, 0)
                line.Size = UDim2.new(0, 0, 0, 2)
                line.Parent = lineGui

                local endPos = Vector2.new(
                    pos.X,
                    pos.Y
                )

                local delta = endPos - startPos
                local length = delta.Magnitude

                line.Position = UDim2.fromOffset(
                    startPos.X,
                    startPos.Y
                )

                line.Size = UDim2.fromOffset(
                    length,
                    2
                )

                line.Rotation = math.deg(
                    math.atan2(delta.Y, delta.X)
                )

                table.insert(lines, line)
            end
        end
    end
end

local lineBtn = createButton("ESP LINE: OFF")

lineBtn.MouseButton1Click:Connect(function()
    lineOn = not lineOn

    lineBtn.Text = lineOn
        and "ESP LINE: ON"
        or "ESP LINE: OFF"

    if not lineOn then
        clearLines()
    end
end)

--========================================================
-- LOCK CAMERA
--========================================================

local cameraBtn = createButton("LOCK CAMERA: OFF")

cameraBtn.MouseButton1Click:Connect(function()
    cameraLockOn = not cameraLockOn

    cameraBtn.Text = cameraLockOn
        and "LOCK CAMERA: ON"
        or "LOCK CAMERA: OFF"

    if not cameraLockOn then
        camera.CameraType = Enum.CameraType.Custom
    end
end)

--========================================================
-- SUPER AIM - NPC ONLY
--========================================================

local aimBtn = createButton("SUPER AIM: OFF")
local aimBox = createValueBox(AIM_SIZE)

local function getNearestNPC()
    local folder = workspace:FindFirstChild("NPCs")
    local root = getRoot()

    if not folder or not root then
        return nil
    end

    local nearest = nil
    local nearestDistance = AIM_SIZE

    for _, npc in ipairs(folder:GetChildren()) do
        local hum = npc:FindFirstChildOfClass("Humanoid")
        local npcRoot =
            npc:FindFirstChild("HumanoidRootPart")

        if hum and npcRoot and hum.Health > 0 then
            local distance =
                (npcRoot.Position - root.Position).Magnitude

            if distance < nearestDistance then
                nearestDistance = distance
                nearest = npc
            end
        end
    end

    return nearest
end

aimBtn.MouseButton1Click:Connect(function()
    aimOn = not aimOn

    if not aimOn then
        currentTarget = nil
    end

    aimBtn.Text = aimOn
        and "SUPER AIM: ON"
        or "SUPER AIM: OFF"
end)

aimBox.FocusLost:Connect(function()
    local value = tonumber(aimBox.Text)

    if value then
        AIM_SIZE = math.clamp(value, 1, 9999)
    end

    aimBox.Text = tostring(AIM_SIZE)
end)

RunService.RenderStepped:Connect(function()
    if not aimOn then return end

    if currentTarget then
        local hum =
            currentTarget:FindFirstChildOfClass("Humanoid")

        local root =
            currentTarget:FindFirstChild("HumanoidRootPart")

        if not hum or not root or hum.Health <= 0 then
            currentTarget = nil
        end
    end

    if not currentTarget then
        currentTarget = getNearestNPC()
    end

    if currentTarget then
        local target =
            currentTarget:FindFirstChild("Head")
            or currentTarget:FindFirstChild("HumanoidRootPart")

        if target then
            camera.CFrame = CFrame.lookAt(
                camera.CFrame.Position,
                target.Position
            )
        end
    end
end)

--========================================================
-- GOD MODE
--========================================================

local godBtn = createButton("GOD MODE: OFF")

godBtn.MouseButton1Click:Connect(function()
    godOn = not godOn

    local hum = getHumanoid()

    if hum and godOn then
        hum.MaxHealth = math.huge
        hum.Health = math.huge
    elseif hum and not godOn then
        hum.MaxHealth = 100
        hum.Health = math.min(hum.Health, 100)
    end

    godBtn.Text = godOn
        and "GOD MODE: ON"
        or "GOD MODE: OFF"
end)

--========================================================
-- FLOATING V.A ICON
--========================================================

local floating = Instance.new("TextButton")
floating.Name = "VA_FLOATING"
floating.AnchorPoint = Vector2.new(0.5, 0.5)
floating.Position = UDim2.new(0.08, 0, 0.5, 0)
floating.Size = UDim2.new(0, 58, 0, 58)
floating.BackgroundColor3 = Color3.fromRGB(0, 120, 60)
floating.Text = "V.A"
floating.TextColor3 = Color3.new(1, 1, 1)
floating.TextSize = 17
floating.Font = Enum.Font.GothamBold
floating.Visible = false
floating.Active = true
floating.Selectable = true
floating.AutoButtonColor = false
floating.ZIndex = 100
floating.Parent = gui

local floatingCorner = Instance.new("UICorner")
floatingCorner.CornerRadius = UDim.new(1, 0)
floatingCorner.Parent = floating

local floatingStroke = Instance.new("UIStroke")
floatingStroke.Color = Color3.fromRGB(0, 255, 120)
floatingStroke.Thickness = 2
floatingStroke.Parent = floating

--========================================================
-- MOBILE FLOATING DRAG
--========================================================

local draggingFloating = false
local floatingMoved = false
local floatingStart
local floatingStartPos

local DRAG_THRESHOLD = 10

floating.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch then
        draggingFloating = true
        floatingMoved = false
        floatingStart = input.Position
        floatingStartPos = floating.Position
    end
end)

UIS.TouchMoved:Connect(function(input)
    if not draggingFloating then return end

    local delta = input.Position - floatingStart

    if math.abs(delta.X) > DRAG_THRESHOLD
        or math.abs(delta.Y) > DRAG_THRESHOLD then
        floatingMoved = true
    end

    floating.Position = UDim2.new(
        floatingStartPos.X.Scale,
        floatingStartPos.X.Offset + delta.X,
        floatingStartPos.Y.Scale,
        floatingStartPos.Y.Offset + delta.Y
    )
end)

UIS.TouchEnded:Connect(function()
    if not draggingFloating then return end

    local moved = floatingMoved

    draggingFloating = false
    floatingMoved = false

    if not moved then
        main.Visible = true
        floating.Visible = false
    end
end)

--========================================================
-- MAIN MENU MOBILE DRAG
--========================================================

local draggingMain = false
local mainStart
local mainStartPos

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.Touch then
        draggingMain = true
        mainStart = input.Position
        mainStartPos = main.Position
    end
end)

UIS.TouchMoved:Connect(function(input)
    if not draggingMain then return end

    local delta = input.Position - mainStart

    main.Position = UDim2.new(
        mainStartPos.X.Scale,
        mainStartPos.X.Offset + delta.X,
        mainStartPos.Y.Scale,
        mainStartPos.Y.Offset + delta.Y
    )
end)

UIS.TouchEnded:Connect(function()
    draggingMain = false
end)

--========================================================
-- CLOSE
--========================================================

closeBtn.MouseButton1Click:Connect(function()
    main.Visible = false
    floating.Visible = true
end)

--========================================================
-- LOGIN
--========================================================

loginBtn.MouseButton1Click:Connect(function()
    if passBox.Text == PASSWORD then
        login.Visible = false
        main.Visible = true
    else
        loginBtn.Text = "WRONG PASSWORD"

        task.delay(1, function()
            if loginBtn then
                loginBtn.Text = "LOGIN"
            end
        end)
    end
end)

--========================================================
-- RESPAWN
--========================================================

player.CharacterAdded:Connect(function()
    task.wait(1)

    local hum = getHumanoid()

    if hum then
        if speedOn then
            hum.WalkSpeed = SPEED_VALUE
        end

        if jumpOn then
            hum.UseJumpPower = true
            hum.JumpPower = JUMP_VALUE
        end

        if godOn then
            hum.MaxHealth = math.huge
            hum.Health = math.huge
        end
    end

    if invisibleOn then
        setInvisible(true)
    end

    if noclipOn then
        updateNoclip()
    end

    if flyOn then
        setFly(true)
    end

    currentTarget = nil
end)

--========================================================
-- REFRESH
--========================================================

task.spawn(function()
    while gui.Parent do

        if espOn or boxOn then
            updateESP()
        end

        task.wait(0.25)
    end
end)

RunService.RenderStepped:Connect(function()

    if lineOn then
        updateLines()
    end

    if cameraLockOn then
        local root = getRoot()

        if root then
            camera.CameraType =
                Enum.CameraType.Scriptable

            camera.CFrame = CFrame.lookAt(
                camera.CFrame.Position,
                root.Position
            )
        end
    end
end)
