-- Carregar a OrionLib
local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/SoulXploit/main/source"))()

-- Criar a janela principal
local Window = OrionLib:MakeWindow({
    Name = "SoulXploit | Blox Fruits",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "SoulXploitCFG"
})

-- Aba de Auto Farm
local FarmTab = Window:MakeTab({
    Name = "Auto Farm",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

FarmTab:AddToggle({
    Name = "Auto Farm",
    Default = false,
    Callback = function(Value)
        getgenv().AutoFarm = Value
        while getgenv().AutoFarm and wait() do
            pcall(function()
                -- Coloque aqui sua função de farm
                print("Farmando...")
            end)
        end
    end
})

-- Aba de Teleporte
local TeleportTab = Window:MakeTab({
    Name = "Teleportes",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

TeleportTab:AddButton({
    Name = "Ir para a Ilha Inicial",
    Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2068, 39, 902)
    end
})

-- Exibir imagem do SoulXploit no canto superior
local ScreenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
local Logo = Instance.new("ImageLabel", ScreenGui)
Logo.Size = UDim2.new(0, 250, 0, 80)
Logo.Position = UDim2.new(0.01, 0, 0.01, 0)
Logo.BackgroundTransparency = 1
Logo.Image = "rbxassetid://113422439338527"
