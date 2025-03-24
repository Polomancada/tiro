local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local flying = false
local aimbotActive = false

-- Função para ativar/desativar o voo
function toggleFly()
    flying = not flying
    if flying then
        while flying do
            player.Character.HumanoidRootPart.Position = player.Character.HumanoidRootPart.Position + Vector3.new(0, 1, 0)
            wait(0.1)
        end
    end
end

-- Função para aimbot
function aimbot()
    if aimbotActive then
        local target = mouse.Target
        if target then
            -- Ajusta a mira para o alvo
            player.Character.HumanoidRootPart.CFrame = CFrame.new(target.Position)
        end
    end
end

-- Menu de ativação
local menu = Instance.new("ScreenGui")
local flyButton = Instance.new("TextButton", menu)
flyButton.Text = "Ativar Voo"
flyButton.MouseButton1Click:Connect(toggleFly)

local aimbotButton = Instance.new("TextButton", menu)
aimbotButton.Text = "Ativar Aimbot"
aimbotButton.MouseButton1Click:Connect(function()
    aimbotActive = not aimbotActive
end)

menu.Parent = player.PlayerGui

-- Loop para aimbot
game:GetService("RunService").RenderStepped:Connect(aimbot)
