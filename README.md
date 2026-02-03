-- DZ HUB | Blox Fruits
-- DELTA & FLUXUS | MOBILE + PC

repeat task.wait() until game:IsLoaded()

local plr = game.Players.LocalPlayer
local chr = plr.Character or plr.CharacterAdded:Wait()
local hrp = chr:WaitForChild("HumanoidRootPart")

-- ===== ICON =====
local IconGui = Instance.new("ScreenGui", game.CoreGui)
local Icon = Instance.new("ImageButton", IconGui)

Icon.Size = UDim2.new(0,60,0,60)
Icon.Position = UDim2.new(0.02,0,0.5,0)
Icon.BackgroundTransparency = 1
Icon.Active = true
Icon.Draggable = true

-- 🔴 COLE SEU ID DA IMAGEM DZ AQUI
Icon.Image = "rbxassetid://12345678901"

-- ===== GUI =====
local Gui = Instance.new("ScreenGui", game.CoreGui)
Gui.Enabled = false

local Frame = Instance.new("Frame", Gui)
Frame.Size = UDim2.new(0,270,0,360)
Frame.Position = UDim2.new(0.3,0,0.2,0)
Frame.BackgroundColor3 = Color3.fromRGB(12,12,12)
Instance.new("UICorner", Frame).CornerRadius = UDim.new(0,16)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1,0,0,45)
Title.Text = "DZ HUB - DELTA"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 17
Title.BackgroundTransparency = 1

-- Button Creator
local function Btn(txt,y)
    local b = Instance.new("TextButton", Frame)
    b.Size = UDim2.new(0.9,0,0,42)
    b.Position = UDim2.new(0.05,0,y,0)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(35,35,35)
    b.TextColor3 = Color3.new(1,1,1)
    b.Font = Enum.Font.Gotham
    b.TextSize = 14
    Instance.new("UICorner", b)
    return b
end

local AutoFarm = Btn("Auto Farm [OFF]",0.15)
local AutoBoss = Btn("Auto Boss [OFF]",0.27)
local FarmFruit = Btn("Auto Farm Fruta [OFF]",0.39)
local ESPFruit = Btn("ESP Fruta",0.51)
local Speed = Btn("Speed Player",0.63)

local Flags = {
    farm=false,
    boss=false,
    fruit=false
}

-- Auto Farm Level
AutoFarm.MouseButton1Click:Connect(function()
    Flags.farm = not Flags.farm
    AutoFarm.Text = Flags.farm and "Auto Farm [ON]" or "Auto Farm [OFF]"

    task.spawn(function()
        while Flags.farm do
            for _,mob in pairs(workspace.Enemies:GetChildren()) do
                if mob:FindFirstChild("HumanoidRootPart")
                and mob:FindFirstChild("Humanoid")
                and mob.Humanoid.Health > 0 then
                    hrp.CFrame = mob.HumanoidRootPart.CFrame * CFrame.new(0,0,3)
                    task.wait(0.15)
                end
            end
            task.wait()
        end
    end)
end)

-- Auto Boss
AutoBoss.MouseButton1Click:Connect(function()
    Flags.boss = not Flags.boss

    task.spawn(function()
        while Flags.boss do
            for _,mob in pairs(workspace.Enemies:GetChildren()) do
                if mob.Name:find("Boss")
                and mob:FindFirstChild("HumanoidRootPart")
                and mob.Humanoid.Health > 0 then
                    hrp.CFrame = mob.HumanoidRootPart.CFrame * CFrame.new(0,0,4)
                end
            end
            task.wait(0.4)
        end
    end)
end)

-- Auto Farm Fruta
FarmFruit.MouseButton1Click:Connect(function()
    Flags.fruit = not Flags.fruit

    task.spawn(function()
        while Flags.fruit do
            for _,f in pairs(workspace:GetChildren()) do
                if f.Name:find("Fruit") and f:FindFirstChild("Handle") then
                    hrp.CFrame = f.Handle.CFrame
                    task.wait(0.2)
                end
            end
            task.wait(2)
        end
    end)
end)

-- ESP Fruta
ESPFruit.MouseButton1Click:Connect(function()
    for _,f in pairs(workspace:GetChildren()) do
        if f.Name:find("Fruit") and f:FindFirstChild("Handle") then
            local esp = Instance.new("BillboardGui", f.Handle)
            esp.Size = UDim2.new(0,120,0,40)
            esp.AlwaysOnTop = true

            local t = Instance.new("TextLabel", esp)
            t.Size = UDim2.new(1,0,1,0)
            t.Text = "🍎 FRUTA"
            t.TextColor3 = Color3.new(1,0,0)
            t.BackgroundTransparency = 1
            t.TextScaled = true
        end
    end
end)

-- Speed
Speed.MouseButton1Click:Connect(function()
    plr.Character.Humanoid.WalkSpeed = 35
end)

-- Toggle GUI
Icon.MouseButton1Click:Connect(function()
    Gui.Enabled = not Gui.Enabled
end)

print("DZ HUB | DELTA READY")
