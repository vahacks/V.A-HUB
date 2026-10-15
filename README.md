--========================================--
--             V.A HUB                    --
--          VIOLET NEON EDITION            --
--========================================--

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")

local player = Players.LocalPlayer
local PASSWORD = "Olol"

-- VIOLET THEME
local BG = Color3.fromRGB(14, 8, 24)
local PANEL = Color3.fromRGB(25, 13, 40)
local VIOLET = Color3.fromRGB(160, 50, 255)
local NEON = Color3.fromRGB(205, 120, 255)
local WHITE = Color3.fromRGB(245, 235, 255)

local gui = Instance.new("ScreenGui")
gui.Name = "VA_HUB"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = player:WaitForChild("PlayerGui")

-- UI HELPER
local function corner(object, radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, radius or 10)
    c.Parent = object
end

local function stroke(object)
    local s = Instance.new("UIStroke")
    s.Color = VIOLET
    s.Thickness = 1.5
    s.Parent = object
end

local function makeButton(parent, text, position, size)
    local b = Instance.new("TextButton")
    b.Size = size
    b.Position = position
    b.BackgroundColor3 = PANEL
    b.TextColor3 = NEON
    b.Text = text
    b.TextSize = 14
    b.Font = Enum.Font.GothamBold
    b.BorderSizePixel = 0
    b.AutoButtonColor = true
    b.Parent = parent
    corner(b, 9)
    stroke(b)
    return b
end

local function makeBox(parent, placeholder, position)
    local box = Instance.new("TextBox")
    box.Size = UDim2.new(1, -30, 0, 38)
    box.Position = position
    box.BackgroundColor3 = BG
    box.TextColor3 = WHITE
    box.PlaceholderColor3 = NEON
    box.PlaceholderText = placeholder
    box.Text = ""
    box.TextSize = 14
    box.Font = Enum.Font.Gotham
    box.ClearTextOnFocus = false
    box.BorderSizePixel = 0
    box.Parent = parent
    corner(box, 8)
    stroke(box)
    return box
end

-- LOGIN WINDOW
local login = Instance.new("Frame")
login.Name = "Login"
login.Size = UDim2.new(0, 300, 0, 240)
login.Position = UDim2.new(0.5, -150, 0.5, -120)
login.BackgroundColor3 = BG
login.BorderSizePixel = 0
login.Parent = gui
corner(login, 14)
stroke(login)

local loginTitle = Instance.new("TextLabel")
loginTitle.Size = UDim2.new(1, 0, 0, 40)
loginTitle.BackgroundTransparency = 1
loginTitle.Text = "V.A HUB"
loginTitle.TextColor3 = NEON
loginTitle.Font = Enum.Font.GothamBlack
loginTitle.TextSize = 23
loginTitle.Parent = login

local nameBox = makeBox(
    login,
    "Enter your name for script",
    UDim2.new(0, 15, 0, 55)
)

local passBox = makeBox(
    login,
    "Enter password",
    UDim2.new(0, 15, 0, 102)
)
passBox.ClearTextOnFocus = false

local loginBtn = makeButton(
    login,
    "LOGIN",
    UDim2.new(0, 15, 0, 155),
    UDim2.new(1, -30, 0, 38)
)

local loginStatus = Instance.new("TextLabel")
loginStatus.Size = UDim2.new(1, -20, 0, 22)
loginStatus.Position = UDim2.new(0, 10, 1, -25)
loginStatus.BackgroundTransparency = 1
loginStatus.Text = "Violet Neon Edition"
loginStatus.TextColor3 = NEON
loginStatus.TextSize = 11
loginStatus.Font = Enum.Font.Gotham
loginStatus.Parent = login

-- MAIN WINDOW
local main = Instance.new("Frame")
main.Name = "MainWindow"
main.Size = UDim2.new(0, 330, 0, 390)
main.Position = UDim2.new(0.5, -165, 0.5, -195)
main.BackgroundColor3 = BG
main.BorderSizePixel = 0
main.Visible = false
main.Parent = gui
corner(main, 14)
stroke(main)

local header = Instance.new("TextLabel")
header.Name = "CustomTitle"
header.Size = UDim2.new(1, -55, 0, 45)
header.Position = UDim2.new(0, 10, 0, 0)
header.BackgroundTransparency = 1
header.Text = "V.A HUB"
header.TextColor3 = NEON
header.TextSize = 19
header.Font = Enum.Font.GothamBlack
header.TextXAlignment = Enum.TextXAlignment.Left
header.TextTruncate = Enum.TextTruncate.AtEnd
header.Parent = main

local closeBtn = makeButton(
    main,
    "X",
    UDim2.new(1, -43, 0, 7),
    UDim2.new(0, 34, 0, 30)
)

-- SCROLLING CONTENT
local content = Instance.new("ScrollingFrame")
content.Name = "Controls"
content.Size = UDim2.new(1, -20, 1, -60)
content.Position = UDim2.new(0, 10, 0, 50)
content.BackgroundColor3 = PANEL
content.BorderSizePixel = 0
content.ScrollBarThickness = 5
content.ScrollBarImageColor3 = VIOLET
content.CanvasSize = UDim2.new(0, 0, 0, 440)
content.Parent = main
corner(content, 10)

local layout = Instance.new("UIListLayout")
layout.Padding = UDim.new(0, 8)
layout.SortOrder = Enum.SortOrder.LayoutOrder
layout.Parent = content

local padding = Instance.new("UIPadding")
padding.PaddingTop = UDim.new(0, 10)
padding.PaddingLeft = UDim.new(0, 10)
padding.PaddingRight = UDim.new(0, 10)
padding.PaddingBottom = UDim.new(0, 10)
padding.Parent = content

local function addControl(text, callback)
    local button = makeButton(
        content,
        text,
        UDim2.new(),
        UDim2.new(1, 0, 0, 38)
    )
    button.LayoutOrder = #content:GetChildren()
    button.Activated:Connect(function()
        callback(button)
    end)
    return button
end

local function addNumberInput(placeholder, defaultValue)
    local box = makeBox(
        content,
        placeholder,
        UDim2.new()
    )
    box.LayoutOrder = #content:GetChildren()
    box.Text = tostring(defaultValue)
    box.Size = UDim2.new(1, 0, 0, 38)
    return box
end

-- FLOATING ICON
local floating = makeButton(
    gui,
    "V.A",
    UDim2.new(0, 20, 0.5, -30),
    UDim2.new(0, 58, 0, 58)
)
floating.Name = "FloatingIcon"
floating.TextSize = 16
floating.Visible = false
corner(floating, 18)

-- DRAG MAIN WINDOW BY HEADER
do
    local dragging = false
    local dragStart
    local startPosition

    header.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPosition = main.Position
        end
    end)

    UIS.InputChanged:Connect(function(input)
        if dragging and (
            input.UserInputType == Enum.UserInputType.MouseMovement
            or input.UserInputType == Enum.UserInputType.Touch
        ) then
            local delta = input.Position - dragStart
            main.Position = UDim2.new(
                startPosition.X.Scale,
                startPosition.X.Offset + delta.X,
                startPosition.Y.Scale,
                startPosition.Y.Offset + delta.Y
            )
        end
    end)

    UIS.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)
end

-- DRAG FLOATING ICON
do
    local dragging = false
    local moved = false
    local startPos
    local startInput

    floating.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            moved = false
            startInput = input.Position
            startPos = floating.Position
        end
    end)

    UIS.InputChanged:Connect(function(input)
        if dragging and (
            input.UserInputType == Enum.UserInputType.MouseMovement
            or input.UserInputType == Enum.UserInputType.Touch
        ) then
            local delta = input.Position - startInput
            if math.abs(delta.X) > 8 or math.abs(delta.Y) > 8 then
                moved = true
            end
            floating.Position = UDim2.new(
                startPos.X.Scale,
                startPos.X.Offset + delta.X,
                startPos.Y.Scale,
                startPos.Y.Offset + delta.Y
            )
        end
    end)

    UIS.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then
            if dragging and not moved then
                main.Visible = true
                floating.Visible = false
            end
            dragging = false
        end
    end)
end

-- GAME CONTROL INPUTS
local speedInput = addNumberInput("Speed value", 16)
local jumpInput = addNumberInput("Jump power", 50)

local speedEnabled = false
local jumpEnabled = false

local function getHumanoid()
    local character = player.Character
    return character and character:FindFirstChildOfClass("Humanoid")
end

addControl("SPEED: OFF", function(button)
    speedEnabled = not speedEnabled
    button.Text = speedEnabled and "SPEED: ON" or "SPEED: OFF"
    button.TextColor3 = speedEnabled and Color3.fromRGB(255, 255, 255) or NEON

    local humanoid = getHumanoid()
    local value = tonumber(speedInput.Text)

    if humanoid and value then
        humanoid.WalkSpeed = speedEnabled and math.clamp(value, 0, 100) or 16
    end
end)

addControl("JUMP: OFF", function(button)
    jumpEnabled = not jumpEnabled
    button.Text = jumpEnabled and "JUMP: ON" or "JUMP: OFF"

    local humanoid = getHumanoid()
    local value = tonumber(jumpInput.Text)

    if humanoid and value then
        humanoid.UseJumpPower = true
        humanoid.JumpPower = jumpEnabled and math.clamp(value, 0, 150) or 50
    end
end)

addControl("RESET MOVEMENT", function()
    speedEnabled = false
    jumpEnabled = false

    local humanoid = getHumanoid()
    if humanoid then
        humanoid.WalkSpeed = 16
        humanoid.UseJumpPower = true
        humanoid.JumpPower = 50
    end
end)

addControl("VIOLET THEME: ACTIVE", function(button)
    button.Text = "💜 VIOLET NEON ACTIVE"
end)

addControl("TEST MODE: LOCAL UI", function(button)
    button.Text = "TEST MODE: READY"
end)

addControl("HIDE MENU", function()
    main.Visible = false
    floating.Visible = true
end)

-- LOGIN
loginBtn.Activated:Connect(function()
    local enteredPassword = passBox.Text
    local enteredName = nameBox.Text:match("^%s*(.-)%s*$")

    if enteredPassword ~= PASSWORD then
        loginStatus.Text = "Incorrect password"
        return
    end

    if enteredName == "" then
        loginStatus.Text = "Please enter your name"
        return
    end

    enteredName = string.sub(enteredName, 1, 24)
    header.Text = enteredName

    login.Visible = false
    main.Visible = true
    floating.Visible = false
end)

closeBtn.Activated:Connect(function()
    main.Visible = false
    floating.Visible = true
end)

-- CHARACTER RESPAWN
player.CharacterAdded:Connect(function()
    task.wait(1)

    local humanoid = getHumanoid()
    if humanoid then
        if speedEnabled then
            humanoid.WalkSpeed = math.clamp(tonumber(speedInput.Text) or 16, 0, 100)
        end

        if jumpEnabled then
            humanoid.UseJumpPower = true
            humanoid.JumpPower = math.clamp(tonumber(jumpInput.Text) or 50, 0, 150)
        end
    end
end)

print("V.A HUB Violet Neon UI loaded")
