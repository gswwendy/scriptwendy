-- LocalScript para destacar todos os jogadores de vermelho neon ao pressionar F

local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local LOCAL_PLAYER = Players.LocalPlayer

-- Função para criar ou atualizar highlight
local function highlightPlayer(player)
    if player.Character then
        local already = player.Character:FindFirstChild("Highlight_Red")
        if not already then
            local highlight = Instance.new("Highlight")
            highlight.Name = "Highlight_Red"
            highlight.FillColor = Color3.fromRGB(255, 0, 0)
            highlight.OutlineColor = Color3.fromRGB(255, 0, 0)
            highlight.FillTransparency = 0.25
            highlight.OutlineTransparency = 0
            highlight.Parent = player.Character
        end
    end
end

-- Função para destacar todos os jogadores
local function highlightAll()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LOCAL_PLAYER then -- Se quiser destacar o próprio jogador, remova esta linha
            highlightPlayer(player)
        end
    end
end

-- Listener para pressionar F
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.F then
        highlightAll()
    end
end)

-- Atualiza highlights quando jogadores respawnam
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        -- Opcional: adicionar highlight automaticamente ao respawn se desejar
    end)
end)
