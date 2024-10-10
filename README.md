-- Script de voo para Roblox com aba móvel

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local flying = false
local speed = 50

-- Função para iniciar o voo
local function startFlying()
    local character = player.Character
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    local bodyGyro = Instance.new("BodyGyro", character.HumanoidRootPart)
    local bodyVelocity = Instance.new("BodyVelocity", character.HumanoidRootPart)
    
    bodyGyro.P = 9e4
    bodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
    bodyGyro.cframe = character.HumanoidRootPart.CFrame
    
    bodyVelocity.velocity = Vector3.new(0, 0.1, 0)
    bodyVelocity.maxForce = Vector3.new(9e9, 9e9, 9e9)
    
    flying = true
    
    while flying do
        wait()
        humanoid.PlatformStand = true
        bodyVelocity.velocity = (character.HumanoidRootPart.CFrame.lookVector * speed)
    end
    
    bodyGyro:Destroy()
    bodyVelocity:Destroy()
    humanoid.PlatformStand = false
end

-- Função para parar o voo
local function stopFlying()
    flying = false
end

-- Criar a aba móvel
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0, 200, 0, 50)
frame.Position = UDim2.new(0.5, -100, 0, 0)
frame.BackgroundColor3 = Color3.new(0, 0, 0)
frame.Active = true
frame.Draggable = true

local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(1, 0, 1, 0)
button.Text = "Ativar Voo"
button.BackgroundColor3 = Color3.new(1, 1, 1)

button.MouseButton1Click:Connect(function()
    if flying then
        stopFlying()
        button.Text = "Ativar Voo
