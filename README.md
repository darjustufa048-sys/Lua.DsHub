# Lua.DsHub
Lua source hider made by darjus
local DsHub = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TitleBar = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseBtn = Instance.new("TextButton")
local ToggleBtn = Instance.new("TextButton")
local StatusLabel = Instance.new("TextLabel")
local UICorner = Instance.new("UICorner")
local Corner1 = Instance.new("UICorner")
local Corner2 = Instance.new("UICorner")
local Corner3 =Instance.new("UICorner")

DsHub.Name = "DsHub"
DsHub.Parent = game.CoreGui
DsHub.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

MainFrame.Name = "MainFrame"
MainFrame.Parent = DsHub
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
MainFrame.Size = UDim2.new(0, 300, 0, 200)
MainFrame.Active = true
MainFrame.Draggable = true
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

TitleBar.Name = "TitleBar"
TitleBar.Parent = MainFrame
TitleBar.BackgroundColor3 = Color3.fromRGB(45, 45, 55)
TitleBar.Size = UDim2.new(1, 0, 0, 35)
Corner1.CornerRadius = UDim.new(0, 10)
Corner1.Parent = TitleBar

Title.Name = "Title"
Title.Parent = TitleBar
Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 15, 0, 0)
Title.Size = UDim2.new(0, 100, 1, 0)
Title.Font = Enum.Font.GothamBold
Title.Text = "DsHub"
Title.TextColor3 = Color3.fromRGB(0, 200, 255)
Title.TextSize = 20
Title.TextXAlignment = Enum.TextXAlignment.Left

CloseBtn.Name = "CloseBtn"
CloseBtn.Parent = TitleBar
CloseBtn.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
CloseBtn.Position = UDim2.new(1, -30, 0, 7.5)
CloseBtn.Size = UDim2.new(0, 20, 0, 20)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.TextSize = 15
Corner2.CornerRadius = UDim.new(0, 5)
Corner2.Parent = CloseBtn

ToggleBtn.Name = "ToggleBtn"
ToggleBtn.Parent = MainFrame
ToggleBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 255)
ToggleBtn.Position = UDim2.new(0.5, -50, 0.5, -20)
ToggleBtn.Size = UDim2.new(0, 100, 0, 40)
ToggleBtn.Font = Enum.Font.GothamBold
ToggleBtn.Text = "ENABLE"
ToggleBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleBtn.TextSize = 16
Corner3.CornerRadius = UDim.new(0, 8)
Corner3.Parent = ToggleBtn

StatusLabel.Name = "StatusLabel"
StatusLabel.Parent = MainFrame
StatusLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Position = UDim2.new(0, 0, 0.75, 0)
StatusLabel.Size = UDim2.new(1, 0, 0, 30)
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.Text = "Status: DISABLED"
StatusLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
StatusLabel.TextSize = 14

local infiniteJumpEnabled = false

local function updateUI()
    if infiniteJumpEnabled then
        ToggleBtn.Text = "DISABLE"
        ToggleBtn.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
        StatusLabel.Text = "Status: ENABLED"
        StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
    else
        ToggleBtn.Text = "ENABLE"
        ToggleBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 255)
        StatusLabel.Text = "Status: DISABLED"
        StatusLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
    end
end

local Player = game:GetService("Players").LocalPlayer
local UserInputService = game:GetService("UserInputService")

UserInputService.JumpRequest:Connect(function()
    if infiniteJumpEnabled and Player.Character and Player.Character:FindFirstChild("Humanoid") then
        Player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

ToggleBtn.MouseButton1Click:Connect(function()
    infiniteJumpEnabled = not infiniteJumpEnabled
    updateUI()
end)

CloseBtn.MouseButton1Click:Connect(function()
    DsHub:Destroy()
end)

updateUI()
