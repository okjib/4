# 
if game:GetService('Players').LocalPlayer then
    game:GetService('Players').LocalPlayer.Idled:Connect(function()
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
    end)
end


--[[ Services ]]--

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService") -- Potrzebny do animacji UI
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")


--[[ Destroy Existing UI ]]--

-- Usuwamy stare wersje GUI, aby uniknąć konfliktów
local oldGui = PlayerGui:FindFirstChild("VenomHubScreenGui")
if oldGui then
    oldGui:Destroy()
end

local oldCategorizedGui = PlayerGui:FindFirstChild("VenomHubScreenGui_Categorized")
if oldCategorizedGui then
    oldCategorizedGui:Destroy()
end

local oldKeyGui = PlayerGui:FindFirstChild("KeyVerificationUI")
if oldKeyGui then
    oldKeyGui:Destroy()
end


-------------------------------------------------------------------------------
--  1. Tworzenie Głównego UI (Czytelne, Wieloliniowe)
-------------------------------------------------------------------------------

-- Główny kontener GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "VenomHubScreenGui_Categorized"
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent = PlayerGui

-- Ramka główna
local mainFrame = Instance.new("Frame")
mainFrame.Name = "VenomHubMainFrame"
mainFrame.Size = UDim2.new(0, 450, 0, 350) -- Dostosowany rozmiar
mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
mainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
mainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 20) -- Ciemne tło jak w drugim skrypcie
mainFrame.BorderSizePixel = 0
mainFrame.ClipsDescendants = true
mainFrame.Visible = true
mainFrame.Active = true
mainFrame.Draggable = false -- Wyłączymy standardowe przeciąganie, bo mamy własne
mainFrame.Parent = screenGui

-- Zaokrąglenie rogów ramki głównej
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = mainFrame

-- Obramowanie ramki głównej
local stroke = Instance.new("UIStroke")
stroke.Color = Color3.fromRGB(60, 60, 75) -- Obramowanie jak w drugim skrypcie
stroke.Thickness = 1
stroke.Transparency = 0.5
stroke.Parent = mainFrame

-- Tytuł
local titleLabel = Instance.new("TextLabel")
titleLabel.Name = "Title"
titleLabel.Size = UDim2.new(1, -40, 0, 40) -- Dostosowany rozmiar tytułu
titleLabel.Position = UDim2.new(0, 20, 0, 5) -- Trochę niżej
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "EQR Hub v.1.19B"
titleLabel.Font = Enum.Font.GothamSemibold -- Font jak w drugim skrypcie
titleLabel.TextColor3 = Color3.fromRGB(220, 220, 220)
titleLabel.TextSize = 20 -- Rozmiar fontu
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.Parent = mainFrame

-- Linia pod tytułem
local line = Instance.new("Frame")
line.Name = "Divider"
line.Size = UDim2.new(1, -40, 0, 1)
line.Position = UDim2.new(0, 20, 0, 40) -- Pod tytułem
line.BackgroundColor3 = Color3.fromRGB(60, 60, 75)
line.BorderSizePixel = 0
line.Parent = mainFrame

-- Podpis (Footer)
local footerLabel = Instance.new("TextLabel")
footerLabel.Name = "Footer"
footerLabel.Size = UDim2.new(1, -20, 0, 20) -- Rozmiar i pozycja stopki
footerLabel.Position = UDim2.new(0, 10, 1, -25)
footerLabel.BackgroundTransparency = 1
footerLabel.Text = "By helloitsme#4243 | Press K to Toggle" -- Dodano info o K
footerLabel.Font = Enum.Font.Gotham -- Font jak w drugim skrypcie
footerLabel.TextSize = 10
footerLabel.TextColor3 = Color3.fromRGB(100, 100, 120)
footerLabel.TextXAlignment = Enum.TextXAlignment.Right
footerLabel.Parent = mainFrame

-- Sidebar na kategorie
local sidebarFrame = Instance.new("Frame")
sidebarFrame.Name = "SidebarFrame"
sidebarFrame.Size = UDim2.new(0, 120, 1, -70) -- Szerokość paska bocznego, wysokość dopasowana
sidebarFrame.Position = UDim2.new(0, 10, 0, 50) -- Pozycja pod linią, z lewej
sidebarFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 25) -- Nieco inny odcień tła
sidebarFrame.BorderSizePixel = 0
sidebarFrame.Parent = mainFrame

local sidebarCorner = Instance.new("UICorner")
sidebarCorner.CornerRadius = UDim.new(0, 8)
sidebarCorner.Parent = sidebarFrame

local sidebarLayout = Instance.new("UIListLayout")
sidebarLayout.Padding = UDim.new(0, 5)
sidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
sidebarLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
sidebarLayout.Parent = sidebarFrame

-- Główny kontener na przyciski (z prawej strony)
local contentFrame = Instance.new("ScrollingFrame")
contentFrame.Name = "ContentFrame"
contentFrame.Size = UDim2.new(1, -150, 1, -70) -- Szerokość (całość - sidebar - marginesy), wysokość
contentFrame.Position = UDim2.new(0, 140, 0, 50) -- Pozycja obok sidebara
contentFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 25) -- Taki sam jak sidebar dla spójności
contentFrame.BorderS
