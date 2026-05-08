-- [[ 𝐃ᴍ𝐍x Music V1 - Full Script ]] --
-- Created by: Mahir07048

local UserInputService = game:GetService("UserInputService")
local player = game.Players.LocalPlayer

-- ==========================================
-- 1. AUTOMATIC SETUP (NAME & CHAT)
-- ==========================================
local sayMessage = "⚜️𝐃ᴍ𝐍x MUSIC LOADED⚜️"
local chatRemote = game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest
chatRemote:FireServer(sayMessage, "All")

local char = player.Character or player.CharacterAdded:Wait()
local remote = game:GetService("ReplicatedStorage").RemoteEvents.PlayerNameDone
remote:FireServer("🎶𝐃ᴍ𝐍x MUSIC HUB🎶", "WELCOME DEAR DmNx_Ji")

-- ==========================================
-- 2. MAIN UI SETUP
-- ==========================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "DmNxMusicAdvanced"
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

local MainFrame = Instance.new("Frame")
local UICorner_Main = Instance.new("UICorner")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.Position = UDim2.new(0.5, -250, 0.5, -175)
MainFrame.Size = UDim2.new(0, 500, 0, 350)
MainFrame.ClipsDescendants = true
UICorner_Main.CornerRadius = UDim.new(0, 10)
UICorner_Main.Parent = MainFrame

-- Sidebar
local Sidebar = Instance.new("Frame")
Sidebar.Name = "Sidebar"
Sidebar.Parent = MainFrame
Sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Sidebar.Size = UDim2.new(0, 120, 1, 0)

local SidebarLayout = Instance.new("UIListLayout")
SidebarLayout.Parent = Sidebar
SidebarLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
SidebarLayout.Padding = UDim.new(0, 5)

local Logo = Instance.new("TextLabel")
Logo.Text = "DmNx MUSIC"
Logo.Size = UDim2.new(1, 0, 0, 40)
Logo.TextColor3 = Color3.fromRGB(255, 255, 255)
Logo.BackgroundTransparency = 1
Logo.Font = Enum.Font.GothamBold
Logo.Parent = Sidebar

-- Action Buttons UI (The Right Side)
local Content = Instance.new("Frame")
Content.Position = UDim2.new(0, 130, 0, 50)
Content.Size = UDim2.new(0, 350, 0, 280)
Content.BackgroundTransparency = 1
Content.Parent = MainFrame

local AudioInput = Instance.new("TextBox")
AudioInput.Size = UDim2.new(1, 0, 0, 40)
AudioInput.PlaceholderText = "Enter Audio ID..."
AudioInput.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
AudioInput.TextColor3 = Color3.fromRGB(255, 255, 255)
AudioInput.Parent = Content
Instance.new("UICorner").Parent = AudioInput

local function CreateActionBtn(text, color, pos)
    local btn = Instance.new("TextButton")
    btn.Text = text
    btn.Size = UDim2.new(1, 0, 0, 40)
    btn.Position = pos
    btn.BackgroundColor3 = color
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.GothamBold
    btn.Parent = Content
    Instance.new("UICorner").Parent = btn
    return btn
end

local PlayBtn = CreateActionBtn("Play Music", Color3.fromRGB(0, 120, 255), UDim2.new(0, 0, 0, 60))
local RGBBtn = CreateActionBtn("Play with RGB", Color3.fromRGB(150, 50, 255), UDim2.new(0, 0, 0, 110))
local StopBtn = CreateActionBtn("Stop Music", Color3.fromRGB(255, 50, 50), UDim2.new(0, 0, 0, 160))

-- ==========================================
-- 3. FUNCTIONALITY (DRAG & CLOSE)
-- ==========================================
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Position = UDim2.new(1, -40, 0, 10)
CloseBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Parent = MainFrame
Instance.new("UICorner").Parent = CloseBtn

local dragging, dragInput, dragStart, startPos
MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true; dragStart = input.Position; startPos = MainFrame.Position
        input.Changed:Connect(function() if input.UserInputState == Enum.UserInputState.End then dragging = false end end)
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

CloseBtn.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)

print("𝐃ᴍ𝐍x Music V1 Fully Loaded!")
