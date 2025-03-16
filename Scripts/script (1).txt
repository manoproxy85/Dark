local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/zalador498/Void/refs/heads/main/source.txt')))()
local Window = OrionLib:MakeWindow({Name = "DarkVoid Hub", HidePremium = false, SaveConfig = true, ConfigFolder = "DarkVoidHubConfig", IntroEnabled = false})

local ScriptsTab = Window:MakeTab({
    Name = "Scripts",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

ScriptsTab:AddButton({
    Name = "Fly gui v3",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-FLY-GUI-V3-19840"))()
    end
})

local PlayerTab = Window:MakeTab({
Name = "Jogador",
Icon = "rbxassetid://4483345998",
PremiumOnly = false
})

local Section1 = PlayerTab:AddSection({
Name = "Mudanças no jogador"
})

PlayerTab:AddTextbox({
Name = "Velocidade",
Default = "",
TextDisappear = true,
Callback = function(Value)
local Speed = tonumber(Value)
if Speed then
game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Speed
end
end
})

PlayerTab:AddTextbox({
Name = "Pulo",
Default = "",
TextDisappear = true,
Callback = function(Value)
local Jump = tonumber(Value)
if Jump then
game.Players.LocalPlayer.Character.Humanoid.JumpPower = Jump
end
end
})

PlayerTab:AddSlider({
Name = "Gravidade",
Min = 0,
Max = 300,
Default = 196,
Color = Color3.fromRGB(255, 0, 0),
Increment = 1,
ValueName = "Gravidade",
Callback = function(Value)
game.Workspace.Gravity = Value
end
})

game.Workspace.Gravity = 196

local Section2 = PlayerTab:AddSection({
Name = "Outros"
})

local TargetPlayer = ""

PlayerTab:AddTextbox({
Name = "Nome do Jogador",
Default = "",
TextDisappear = false,
Callback = function(Value)
for _, player in ipairs(game.Players:GetPlayers()) do
if string.find(string.lower(player.Name), string.lower(Value), 1, true) then
TargetPlayer = player.Name
break
end
end
end
})

PlayerTab:AddButton({
Name = "Teleportar para o jogador",
Callback = function()
local player = game.Players.LocalPlayer
local char = player.Character

if char and char:FindFirstChild("HumanoidRootPart") then  
        local target = game.Players:FindFirstChild(TargetPlayer)  
        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then  
            char:SetPrimaryPartCFrame(target.Character.HumanoidRootPart.CFrame)  
        end  
    end  
end

})

local Section3 = PlayerTab:AddSection({
Name = "Nome e bio"
})

local function trocarCorRP(cor)
    local args = {
        [1] = "PickingRPNameColor",
        [2] = cor
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eColo1r"):FireServer(unpack(args))
end

local function trocarCorBioRP(cor)
    local args = {
        [1] = "PickingRPBioColor",
        [2] = cor
    }
    game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eColo1r"):FireServer(unpack(args))
end

local function gerarCorAleatoria()
    return Color3.fromRGB(math.random(0, 255), math.random(0, 255), math.random(0, 255))
end

PlayerTab:AddTextbox({
    Name = "Mude o nome",
    Default = "",
    TextDisappear = false,
    Callback = function(value)
        if value ~= "" then
            local args = {
                [1] = "RolePlayName",
                [2] = value
            }
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
        end
    end
})

PlayerTab:AddTextbox({
    Name = "Mude a bio",
    Default = "",
    TextDisappear = false,
    Callback = function(value)
        if value ~= "" then
            local args = {
                [1] = "RolePlayBio",
                [2] = value
            }
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1RPNam1eTex1t"):FireServer(unpack(args))
        end
    end
})

local corRPNameToggle = false
PlayerTab:AddToggle({
    Name = "Nome rgb",
    Default = false,
    Callback = function(state)
        corRPNameToggle = state

        while corRPNameToggle do
            trocarCorRP(gerarCorAleatoria())
            wait(0.5)
        end
    end
})

local corRPBioToggle = false
PlayerTab:AddToggle({
    Name = "Bio rgb",
    Default = false,
    Callback = function(state)
        corRPBioToggle = state

        while corRPBioToggle do
            trocarCorBioRP(gerarCorAleatoria())
            wait(0.5)
        end
    end
})

local TrollTab = Window:MakeTab({
    Name = "Troll",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Section4 = TrollTab:AddSection({
    Name = "Mudança no jogador"
})

TrollTab:AddButton({
    Name = "Deixar boneco pequeno",
    Callback = function()
        local args = {
            [1] = "CharacterSizeUp",
            [2] = 2
        }
        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
    end
})

TrollTab:AddButton({
    Name = "Voltar ao normal",
    Callback = function()
        local args = {
            [1] = "CharacterSizeUp",
            [2] = 1
        }
        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
    end
})

local Section5 = TrollTab:AddSection({
    Name = "Kill"
})

TrollTab:AddTextbox({
Name = "Nome do Jogador",
Default = "",
TextDisappear = false,
Callback = function(Value)
for _, player in ipairs(game.Players:GetPlayers()) do
if string.find(string.lower(player.Name), string.lower(Value), 1, true) then
TargetPlayer = player.Name
break
end
end
end
})

TrollTab:AddToggle({
    Name = "Kill sofa",
    Default = false,
    Callback = function(state)
        teleportLoop = state
        local previousPosition

        if teleportLoop then
            local player = game.Players.LocalPlayer
            local char = player.Character

            if char and char:FindFirstChild("HumanoidRootPart") then
                previousPosition = char.HumanoidRootPart.Position
                local humanoid = char:FindFirstChildOfClass("Humanoid")
                task.wait(1)

                if humanoid then
                    humanoid.PlatformStand = false
                end

                local args = {
                    [1] = "PickingTools",
                    [2] = "Couch"
                }
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

                local backpack = player:FindFirstChild("Backpack")
                if backpack then
                    local couch = backpack:FindFirstChild("Couch")
                    if couch and couch:IsA("Tool") then
                        couch.Parent = char
                    end
                end

                task.wait(1)

                task.spawn(function()
                    local startTime = tick()

                    while teleportLoop do
                        task.wait(0.1)
                        local target = game.Players:FindFirstChild(TargetPlayer)
                        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                            local targetPosition = target.Character.HumanoidRootPart.Position
                            local newPosition = Vector3.new(targetPosition.X, targetPosition.Y - 5, targetPosition.Z)

                            char:SetPrimaryPartCFrame(CFrame.new(newPosition))
                        end

                        if tick() - startTime >= 1 then
                            teleportLoop = false
                        end
                    end

                    char:SetPrimaryPartCFrame(CFrame.new(-12678, -74, -4185))

                    task.wait(1)

                    local args = {
                        [1] = "ClearAllTools"
                    }

                    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer(unpack(args))

                    char:SetPrimaryPartCFrame(CFrame.new(previousPosition))
                end)
            end
        end
    end
})

TrollTab:AddToggle({
    Name = "Bring",
    Default = false,
    Callback = function(state)
        teleportLoop = state

        if teleportLoop then
            local player = game.Players.LocalPlayer
            local char = player.Character

            if char and char:FindFirstChild("HumanoidRootPart") then
                local args = {
                    [1] = "PickingTools",
                    [2] = "Couch"
                }
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))

                task.wait(0.5)

                local backpack = player:FindFirstChild("Backpack")
                if backpack then
                    local couch = backpack:FindFirstChild("Couch")
                    if couch and couch:IsA("Tool") then
                        couch.Parent = char
                    end
                end

                local lastPosition = char.HumanoidRootPart.CFrame

                task.spawn(function()
                    local startTime = tick()

                    while tick() - startTime < 1 do
                        task.wait(0.1)
                        local target = game.Players:FindFirstChild(TargetPlayer)
                        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                            local targetPosition = target.Character.HumanoidRootPart.CFrame * CFrame.new(0, -3, 0)
                            char:SetPrimaryPartCFrame(targetPosition)
                        end
                    end

                    char:SetPrimaryPartCFrame(lastPosition)

                    local args = {
                        [1] = "ClearAllTools"
                    }

                    game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clea1rTool1s"):FireServer(unpack(args))
                    
                    teleportLoop = false
                end)
            end
        end
    end
})

local CasaTab = Window:MakeTab({
    Name = "Casa",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Section6 = CasaTab:AddSection({
    Name = "Tirar banimento"
})

local ativado = false
local objetosParaApagar = {
    "BannedBlock1", "BannedBlock2", "BannedBlock3", "BannedBlock4", "BannedBlock5",
    "BannedBlock6", "BannedBlock7", "BannedBlock8", "BannedBlock9", "BannedBlock10",
    "BannedBlock11", "BannedBlock12", "BannedBlock13", "BannedBlock14", "BannedBlock15",
    "BannedBlock16", "BannedBlock17", "BannedBlock18", "BannedBlock19", "BannedBlock20",
    "BannedBlock21", "BannedBlock22", "BannedBlock23", "BannedBlock24", "BannedBlock28",
    "BannedBlock29", "BannedBlock30", "BannedBlock31", "BannedBlock32", "BannedBlock33",
    "BannedBlock34", "BannedBlock35", "BannedBlock36", "BannedBlock37"
})

CasaTab:AddToggle({
    Name = "Auto unban",
    Default = false,
    Callback = function(value)
        ativado = value
        while ativado do
            for _, objName in ipairs(objetosParaApagar) do
                local obj = game.Workspace:FindFirstChild(objName)
                if obj then
                    obj:Destroy()
                end
            end
            wait(0.1)
        end
    end
})

CasaTab:AddButton({
    Name = "Unban",
    Callback = function()
        for _, objName in ipairs(objetosParaApagar) do
            local obj = game.Workspace:FindFirstChild(objName)
            if obj then
                obj:Destroy()
            end
        end
    end
})

OrionLib:Init()
