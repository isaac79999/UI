local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local Player = Players.LocalPlayer
local Gui = gethui()

if Gui:FindFirstChild("RayLikeUI") then
    Gui.RayLikeUI:Destroy()
end

local ScreenGui = Instance.new("ScreenGui", Gui)
ScreenGui.Name = "RayLikeUI"
ScreenGui.ResetOnSpawn = false

local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.fromScale(0.45, 0.55)
Main.Position = UDim2.fromScale(0.5, 0.5)
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.BackgroundColor3 = Color3.fromRGB(22, 22, 22)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true

local Corner = Instance.new("UICorner", Main)
Corner.CornerRadius = UDim.new(0, 14)

local Sidebar = Instance.new("Frame", Main)
Sidebar.Size = UDim2.fromScale(0.28, 1)
Sidebar.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
Sidebar.BorderSizePixel = 0

Instance.new("UICorner", Sidebar).CornerRadius = UDim.new(0, 14)

local Title = Instance.new("TextLabel", Sidebar)
Title.Size = UDim2.new(1, 0, 0, 60)
Title.BackgroundTransparency = 1
Title.Text = "Ray UI"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

local TabButton = Instance.new("TextButton", Sidebar)
TabButton.Size = UDim2.new(0.9, 0, 0, 42)
TabButton.Position = UDim2.new(0.05, 0, 0, 70)
TabButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TabButton.Text = "Exemplo"
TabButton.Font = Enum.Font.Gotham
TabButton.TextSize = 14
TabButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TabButton.BorderSizePixel = 0

Instance.new("UICorner", TabButton).CornerRadius = UDim.new(0, 8)

local Content = Instance.new("Frame", Main)
Content.Position = UDim2.fromScale(0.28, 0)
Content.Size = UDim2.fromScale(0.72, 1)
Content.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Content.BorderSizePixel = 0

local Layout = Instance.new("UIListLayout", Content)
Layout.Padding = UDim.new(0, 12)
Layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
Layout.VerticalAlignment = Enum.VerticalAlignment.Center

local Button = Instance.new("TextButton", Content)
Button.Size = UDim2.new(0.8, 0, 0, 44)
Button.BackgroundColor3 = Color3.fromRGB(55, 120, 255)
Button.Text = "Botão Exemplo"
Button.Font = Enum.Font.GothamBold
Button.TextSize = 14
Button.TextColor3 = Color3.new(1,1,1)
Button.BorderSizePixel = 0

Instance.new("UICorner", Button).CornerRadius = UDim.new(0, 10)

local SliderFrame = Instance.new("Frame", Content)
SliderFrame.Size = UDim2.new(0.8, 0, 0, 52)
SliderFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
SliderFrame.BorderSizePixel = 0

Instance.new("UICorner", SliderFrame).CornerRadius = UDim.new(0, 10)

local SliderBar = Instance.new("Frame", SliderFrame)
SliderBar.Position = UDim2.new(0.05, 0, 0.55, 0)
SliderBar.Size = UDim2.new(0.9, 0, 0, 6)
SliderBar.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
SliderBar.BorderSizePixel = 0

Instance.new("UICorner", SliderBar).CornerRadius = UDim.new(1, 0)

local Fill = Instance.new("Frame", SliderBar)
Fill.Size = UDim2.new(0.4, 0, 1, 0)
Fill.BackgroundColor3 = Color3.fromRGB(80, 160, 255)
Fill.BorderSizePixel = 0

Instance.new("UICorner", Fill).CornerRadius = UDim.new(1, 0)

local Dragging = false

SliderBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        Dragging = true
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        Dragging = false
    end
end)

UIS.InputChanged:Connect(function(input)
    if Dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
        local X = math.clamp((input.Position.X - SliderBar.AbsolutePosition.X) / SliderBar.AbsoluteSize.X, 0, 1)
        Fill.Size = UDim2.new(X, 0, 1, 0)
    end
end)
