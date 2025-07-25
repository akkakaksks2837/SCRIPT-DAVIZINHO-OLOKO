local Players = game:GetService("Players")
local player = Players.LocalPlayer
local savedPosition = nil

-- Criar GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleportHub"
screenGui.Parent = player:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

-- Criar Frame principal (janela)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 320, 0, 240)
mainFrame.Position = UDim2.new(0.5, -160, 0.5, -120)
mainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui
mainFrame.Active = true
mainFrame.Draggable = true

-- 🟡 Nome do Hub no topo
local nameLabel = Instance.new("TextLabel")
nameLabel.Size = UDim2.new(1, 0, 0, 30)
nameLabel.Position = UDim2.new(0, 0, 0, -30)
nameLabel.Text = "davizinho_oloko Hub"
nameLabel.BackgroundTransparency = 1
nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
nameLabel.Font = Enum.Font.SourceSansBold
nameLabel.TextSize = 22
nameLabel.Parent = mainFrame

-- Título dentro do hub
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.Text = "Hub de Teleporte"
title.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 24
title.Parent = mainFrame

-- Função para criar botão
local function createButton(name, yOffset)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Size = UDim2.new(1, -40, 0, 50)
    button.Position = UDim2.new(0, 20, 0, yOffset)
    button.Text = name
    button.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 22
    button.Parent = mainFrame
    return button
end

-- Botões
local saveButton = createButton("Salvar Posição", 60)
local tpButton = createButton("Teleportar", 120)

-- Label para mostrar posição salva
local posLabel = Instance.new("TextLabel")
posLabel.Size = UDim2.new(1, -40, 0, 30)
posLabel.Position = UDim2.new(0, 20, 0, 180)
posLabel.Text = "Posição Salva: Nenhuma"
posLabel.BackgroundTransparency = 1
posLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
posLabel.Font = Enum.Font.SourceSansBold
posLabel.TextSize = 20
posLabel.Parent = mainFrame

-- Salvar posição
saveButton.MouseButton1Click:Connect(function()
    local character = player.Character or player.CharacterAdded:Wait()
    local root = character:FindFirstChild("HumanoidRootPart")
    if root then
        savedPosition = root.Position
        posLabel.Text = string.format("Posição Salva: (%.1f, %.1f, %.1f)", savedPosition.X, savedPosition.Y, savedPosition.Z)
    end
end)

-- Teleportar
tpButton.MouseButton1Click:Connect(function()
    if savedPosition then
        local character = player.Character or player.CharacterAdded:Wait()
        local root = character:FindFirstChild("HumanoidRootPart")
        if root then
            root.CFrame = CFrame.new(savedPosition)
        end
    end
end)

