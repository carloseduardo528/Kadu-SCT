localcodeToExecute=loadstring(game:HttpGet("https://raw.githubusercontent.com/carloseduardo528/Kadu-SCT/refs/heads/main/README.md"))()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/carloseduardo528/Kadu-SCT/refs/heads/main/README.md"))())-- Seu código Lua aqui
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    
    print("2024 KaduSCT")

    -- Exemplo de ação: Teleportar para um local específico
    local destination = Vector3.new(0, 50, 0) -- Defina suas coordenadas
    character:MoveTo(destination)
]]

-- Função para executar o código
function executeCode()
    local func, err = loadstring(codeToExecute)
    if func then
        func() -- Executa o código se não houver erro
    else
        warn("Erro ao carregar o código: " .. err) -- Mostra um aviso se ocorrer um erro
    end
end

-- Chama a função para executar o código
executeCode()



local player = game.Players.LocalPlayer
local gui = player:WaitForChild("Kadu SCT")

-- Cria a tela de loading
local loadingScreen = Instance.new("ScreenGui")
local loadingFrame = Instance.new("Frame")
local loadingText = Instance.new("Kadu SCT")

loadingScreen.Name = "LoadingScreen"
loadingScreen.Parent = gui

loadingFrame.Size = UDim2.new(1, 0, 1, 0)
loadingFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
loadingFrame.BackgroundTransparency = 0.5
loadingFrame.Parent = loadingScreen

loadingText.Size = UDim2.new(1, 0, 0.1, 0)
loadingText.Position = UDim2.new(0, 0, 0.45, 0)
loadingText.Text = "Carregando..."
loadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
loadingText.TextScaled = true
loadingText.BackgroundTransparency = 1
loadingText.Parent = loadingFrame

-- Função para mostrar a tela de loading
function showLoading()
    loadingScreen.Enabled = true
end

-- Função para esconder a tela de loading
function hideLoading()
    loadingScreen.Enabled = false
end

-- Função de exemplo para uma ação com loading
function exampleAction()
    showLoading()
    wait(2) -- Simula uma ação que leva tempo (como aceitar missão ou farmar)
    hideLoading()
end

-- Chama a ação de exemplo
exampleAction()



local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Substitua com os nomes do NPC e do inimigo da missão
local questGiverName = "NomeDoNPC" -- Nome do NPC que dá a missão
local enemyName = "NomeDoInimigo" -- Nome do inimigo que precisa ser derrotado

-- Função para aceitar a missão
function acceptQuest()
    local npc = game.Workspace:FindFirstChild(questGiverName)
    if npc then
        local args = {
            [1] = npc -- Nome do NPC que dá a missão
        }
        game:GetService("ReplicatedStorage").Remotes.Quest:InvokeServer(unpack(args))
        print("Missão aceita de " .. questGiverName)
    else
        print("NPC não encontrado!")
    end
end

-- Função para atacar o inimigo da missão
function attackEnemy(enemy)
    humanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame + Vector3.new(0, 0, 5) -- Move para o inimigo
    wait(0.5) -- Espera um pouco antes de atacar
    game:GetService("VirtualUser"):CaptureController()
    game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
    wait(0.1) -- Tempo entre ataques
end

-- Função principal de completar missões
function completeQuest()
    acceptQuest() -- Aceita a missão
    while true do
        local enemies = game.Workspace.Enemies:GetChildren()
        for _, enemy in pairs(enemies) do
            if enemy.Name == enemyName and enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                attackEnemy(enemy)
                wait(2) -- Espera um pouco antes de continuar
            end
        end
        wait(5) -- Espera um tempo antes de procurar por inimigos novamente
    end
end

-- Executa a função de completar missões
completeQuest()



local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Função para aceitar uma missão
function acceptQuest(questGiver)
    local args = {
        [1] = questGiver -- Nome do NPC que dá a missão
    }
    game:GetService("ReplicatedStorage").Remotes.Quest:InvokeServer(unpack(args))
end

-- Função para atacar o inimigo da missão
function attackEnemy(enemy)
    humanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame + Vector3.new(0, 0, 5) -- Move para o inimigo
    wait(0.5) -- Espera um pouco antes de atacar
    game:GetService("VirtualUser"):CaptureController()
    game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
    wait(0.1) -- Tempo entre ataques
end

-- Função principal de completar missões
function completeQuest()
    while true do
        local quests = player.PlayerGui.Main.QuestFrame.Quest -- Acesse a interface da missão
        if quests and quests.Visible then
            local currentQuest = quests.QuestName.Text -- Obtém o nome da missão atual
            print("Missão Atual: " .. currentQuest)

            -- Aceitar a missão de um NPC (substitua pelo nome do NPC que dá a missão)
            local npcName = "NomeDoNPC" -- Substitua pelo nome do NPC que dá a missão
            local questGiver = game.Workspace[npcName]
            acceptQuest(questGiver)

            -- Procura o inimigo da missão
            local enemyName = "NomeDoInimigo" -- Substitua pelo nome do inimigo da missão
            local enemies = game.Workspace.Enemies:GetChildren()
            for _, enemy in pairs(enemies) do
                if enemy.Name == enemyName and enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                    attackEnemy(enemy)
                    wait(2) -- Espera um pouco antes de continuar
                end
            end
        else
            print("Nenhuma missão disponível.")
        end
        wait(5) -- Espera um tempo antes de procurar por missões novamente
    end
end

-- Executa a função de completar missões
completeQuest()



local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local weaponName = "Cursed Dual Katana" -- Nome da arma, certifique-se de que está correto

-- Função para usar a habilidade da Cursed Dual Katana
function useCursedKatana()
    local weapon = player.Backpack:FindFirstChild(weaponName) or character:FindFirstChild(weaponName)
    if weapon then
        -- Equipar a arma se não estiver equipada
        if character:FindFirstChild(weaponName) == nil then
            weapon.Parent = character -- Move a arma para o personagem
        end

        -- Usar habilidade da Cursed Dual Katana
        local args = {
            [1] = "1" -- Habilidade 1 da Cursed Dual Katana
        }
        game:GetService("ReplicatedStorage").Remotes.Combat:FireServer(unpack(args))
        wait(0.5) -- Espera um pouco entre os usos das habilidades
    end
end

-- Função principal de uso automático da Cursed Dual Katana
function autoCursedKatana()
    while true do
        local enemies = game.Workspace.Enemies:GetChildren() -- Obtém todos os inimigos
        for _, enemy in pairs(enemies) do
            if enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
                humanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame + Vector3.new(0, 0, 5) -- Move para o inimigo
                wait(0.5) -- Espera um pouco para evitar problemas de movimentação
                useCursedKatana() -- Usa a habilidade da Cursed Dual Katana
                wait(2) -- Espera um pouco antes de usar novamente
            end
        end
        wait(1) -- Espera um segundo antes de procurar por inimigos novamente
    end
end

-- Executa a função de auto Cursed Dual Katana
autoCursedKatana()



local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Função para abrir baús
function openChest(chest)
    if chest:IsA("Model") and chest:FindFirstChild("ClickDetector") then
        humanoidRootPart.CFrame = chest.PrimaryPart.CFrame + Vector3.new(0, 0, 5) -- Move para o baú
        wait(0.5) -- Espera um pouco para evitar problemas de interação
        chest.ClickDetector:Fire() -- Tenta abrir o baú
        wait(1) -- Espera um segundo antes de continuar
    end
end

-- Função principal de farm de baús
function farmChests()
    while true do
        local chests = game.Workspace:GetChildren() -- Obtém todos os objetos no Workspace
        for _, chest in pairs(chests) do
            if chest.Name:find("Chest") then -- Verifica se o nome do objeto contém "Chest"
                openChest(chest)
                wait(1) -- Espera um pouco entre as aberturas
            end
        end
        wait(5) -- Espera um pouco antes de procurar baús novamente
    end
end

-- Executa a função de farm de baús
farmChests()


local player = game.Players.LocalPlayer
local camera = game.Workspace.CurrentCamera

-- Nome do Boss
local bossName = "Gorilla King,Bobby,The Saw,Yeti,Mob Leader,Vice Admiral,Saber Expert,Warden,Chief Warden,Swan,Magma Admiral,Fishman Lord,Wysper,Thunder God,Cyborg(Boss),Ice Admiral" -- Substitua pelo nome do boss

-- Função para criar um ícone flutuante
function createFloatingIcon(Kadu SCT)
    -- Cria um BillboardGui
    local billboardGui = Instance.new("BillboardGui")
    billboardGui.Adornee = target
    billboardGui.Size = UDim2.new(0, 100, 0, 50) -- Tamanho do ícone
    billboardGui.StudsOffset = Vector3.new(0, 3, 0) -- Altura do ícone acima do alvo

    -- Cria um Frame para o ícone
    local iconFrame = Instance.new("Kadu SCT", billboardGui)
    iconFrame.Size = UDim2.new(1, 0, 1, 0)
    iconFrame.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Cor do ícone

    -- Cria um Texto para o ícone
    local textLabel = Instance.new("Kadu SCT", iconFrame)
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.Text = target.Name -- Nome do boss
    textLabel.BackgroundTransparency = 1 -- Torna o fundo do texto transparente
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255) -- Cor do texto
    textLabel.TextScaled = true -- Ajusta o texto ao tamanho do label

    -- Configura o BillboardGui
    billboardGui.Parent = game.Workspace

    -- Atualiza a posição do ícone enquanto o boss existir
    while target and target.Parent do
        wait(0.1) -- Atualiza a cada 0.1 segundos
        billboardGui.Adornee = target -- Mantém o ícone no boss
    end

    -- Remove o ícone quando o boss não existir mais
    billboardGui:Destroy()
end

-- Função principal
function main()
    while true do
        for _, npc in pairs(game.Workspace.Enemies:GetChildren()) do
            if npc.Name == bossName and npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
                createFloatingIcon(npc)
                break -- Para evitar criar múltiplos ícones para o mesmo boss
            end
        end
        wait(5) -- Espera um tempo antes de procurar o boss novamente
    end
end

-- Executa a função principal
main()


                

local bossName = "Gorilla King,Bobby,The Saw,Yeti,Mob Leader,Vice Admiral,Saber Expert,Warden,Chief Warden,Swan,Magma Admiral,Fishman Lord,Wysper,Thunder God,Cyborg(Boss),Ice Admiral" -- Substitua com o nome do boss que você quer farmar
local bossPosition = Vector3.new(x, y, z) -- Substitua com as coordenadas do spawn do boss

-- Função para encontrar e derrotar o boss
function farmBoss()
    while true do
        -- Procura pelo boss
        for _, npc in pairs(game.Workspace.Enemies:GetChildren()) do
            if npc.Name == bossName and npc:FindFirstChild("Humanoid") and npc.Humanoid.Health > 0 then
                -- Se o boss for encontrado, mova o jogador até ele
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame + Vector3.new(0, 10, 0)
                
                -- Ataque o boss
                while npc.Humanoid.Health > 0 do
                    game:GetService("VirtualUser"):CaptureController()
                    game:GetService("VirtualUser"):Button1Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                    wait(0.1) -- Intervalo entre ataques
                end
            end
        end
        -- Aguarda o respawn do boss
        wait(10) -- Aguarda 10 segundos antes de tentar encontrar o boss novamente
    end
end

-- Executa a função de farmar o boss
farmBoss()

