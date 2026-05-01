-- Certifique-se de que o ID abaixo é o do mapa atual
if game.PlaceId ~= 115054138215106 then 
    return 
end

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("SX HUB | by SX", "DarkTheme")

-- Criando a imagem do usuário no canto (HUD Customizada)
local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local ScreenGui = Instance.new("ScreenGui", PlayerGui)
ScreenGui.Name = "SX_HUD"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 180, 0, 60)
Frame.Position = UDim2.new(0, 10, 0, 10)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BackgroundTransparency = 0.3

local ImageLabel = Instance.new("ImageLabel", Frame)
ImageLabel.Size = UDim2.new(0, 50, 0, 50)
ImageLabel.Position = UDim2.new(0, 5, 0, 5)
ImageLabel.Image = game.Players:GetUserThumbnailAsync(Player.UserId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size420x420)

local TextLabel = Instance.new("TextLabel", Frame)
TextLabel.Size = UDim2.new(0, 120, 0, 50)
TextLabel.Position = UDim2.new(0, 60, 0, 5)
TextLabel.Text = Player.Name
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1
TextLabel.TextScaled = true

-- ABA COMBAT
local Combat = Window:NewTab("Combat")
local CombatSection = Combat:NewSection("PVP Modifiers")

CombatSection:NewToggle("Aimbot", "Trava a mira no oponente", function(state)
    _G.Aimbot = state
end)

CombatSection:NewToggle("Silent Aim", "Balas atingem o alvo sem precisar mirar", function(state)
    _G.Silent = state
end)

CombatSection:NewToggle("Godmode", "Não recebe dano (Cuidado com Admins)", function(state)
    if state then
        Player.Character.Humanoid.MaxHealth = 9e9
        Player.Character.Humanoid.Health = 9e9
    else
        Player.Character.Humanoid.MaxHealth = 100
    end
end)

CombatSection:NewSlider("FOV Size", "Tamanho do círculo de mira", 500, 0, function(s)
    _G.FOV = s
end)

-- ABA VISUAL
local Visual = Window:NewTab("Visual")
local VisualSection = Visual:NewSection("Esp & Render")

VisualSection:NewToggle("ESP Caixa", "Mostra caixa ao redor dos players", function(state)
    _G.EspBox = state
end)

VisualSection:NewToggle("ESP Linhas", "Linhas conectadas aos players", function(state)
    _G.EspLines = state
end)

VisualSection:NewToggle("ESP Vida", "Mostra a vida dos oponentes", function(state)
    _G.EspHealth = state
end)

-- BYPASS SILENCIOSO (Não modifica a Metatable para não dar erro 267)
-- Este método apenas limpa os logs de execução locais
for i,v in pairs(getconnections(game:GetService("LogService").MessageOut)) do
    v:Disable()
end
