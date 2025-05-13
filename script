-- LocalScript (ex: StarterPlayerScripts)

local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

local localPlayer = Players.LocalPlayer
local ESPEnabled = false
local highlights = {}

-- Cria um Highlight vermelho
local function createHighlight(character)
    if not character then return end
    if highlights[character] then return end

    local highlight = Instance.new("Highlight")
    highlight.Name = "ESP_Highlight"
    highlight.FillColor = Color3.fromRGB(255, 0, 0)
    highlight.OutlineColor = Color3.fromRGB(255, 0, 0)
    highlight.FillTransparency = 0.5
    highlight.OutlineTransparency = 0
    highlight.Adornee = character
    highlight.Parent = character

    highlights[character] = highlight
end

-- Remove todos os highlights
local function clearHighlights()
    for character, highlight in pairs(highlights) do
        if highlight and highlight.Parent then
            highlight:Destroy()
        end
    end
    highlights = {}
end

-- Ativa o ESP
local function enableESP()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= localPlayer and player.Character then
            createHighlight(player.Character)
        end
    end
end

-- Atualiza automaticamente quando novos personagens aparecerem
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(char)
        if ESPEnabled then
            createHighlight(char)
        end
    end)
end)

-- Escuta a tecla K
UserInputService.InputBegan:Connect(function(input, processed)
    if processed then return end
    if input.KeyCode == Enum.KeyCode.K then
        ESPEnabled = not ESPEnabled
        if ESPEnabled then
            enableESP()
        else
            clearHighlights()
        end
    end
end)

-- Atualização contínua para manter o ESP ativo
RunService.RenderStepped:Connect(function()
    if ESPEnabled then
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= localPlayer and player.Character then
                createHighlight(player.Character)
            end
        end
    end
end)
