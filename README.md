-- Script de Glissade Troll amélioré
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

if not humanoidRootPart then
    warn("Impossible de trouver HumanoidRootPart")
    return
end

-- Fonction pour faire glisser les joueurs proches avec un effet visuel
local function trollGlissade()
    for _, v in pairs(game.Players:GetPlayers()) do
        if v ~= player and v.Character and v.Character:FindFirstChild("HumanoidRootPart") then
            local victimHRP = v.Character.HumanoidRootPart
            local distance = (victimHRP.Position - humanoidRootPart.Position).magnitude
            
            if distance < 10 then -- Si le joueur est proche
                pcall(function()
                    -- Ajout de la force de poussée
                    local velocity = Instance.new("BodyVelocity")
                    velocity.Velocity = Vector3.new(math.random(-30,30), math.random(10,20), math.random(-30,30))
                    velocity.MaxForce = Vector3.new(4000, 4000, 4000)
                    velocity.Parent = victimHRP

                    game:GetService("Debris"):AddItem(velocity, 0.5) -- Supprime l'effet après 0.5 sec

                    -- Effet sonore troll
                    local sound = Instance.new("Sound", victimHRP)
                    sound.SoundId = "rbxassetid://138186576" -- Son cartoon de glissade
                    sound.Volume = 2
                    sound:Play()
                    game:GetService("Debris"):AddItem(sound, 2)

                    -- Effet visuel (onde de choc)
                    local shockwave = Instance.new("Part")
                    shockwave.Shape = Enum.PartType.Ball
                    shockwave.Material = Enum.Material.Neon
                    shockwave.Color = Color3.fromRGB(255, 255, 255)
                    shockwave.Size = Vector3.new(1, 1, 1)
                    shockwave.Anchored = true
                    shockwave.CanCollide = false
                    shockwave.Position = victimHRP.Position
                    shockwave.Parent = game.Workspace

                    -- Animation de l'onde de choc
                    game:GetService("TweenService"):Create(shockwave, TweenInfo.new(0.5), {Size = Vector3.new(6, 6, 6), Transparency = 1}):Play()
                    game:GetService("Debris"):AddItem(shockwave, 0.5)
                end)
            end
        end
    end
end

-- Exécute la fonction de troll toutes les 3 à 5 secondes pour éviter un pattern évident
while wait(math.random(3,5)) do
    pcall(trollGlissade)
end
sound.SoundId
Vector3.new(6, 6, 6), Transparency
