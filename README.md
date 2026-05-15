# KCSeahug--// 🌊 KC SEA HUB 🌊 //--
--// Tổng hợp: Đánh nhanh + Sea Event //--

repeat task.wait() until game:IsLoaded()

---------------------------------------------------
-- LOADING KC HUB
---------------------------------------------------

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local LoadingBar = Instance.new("Frame")
local Loading = Instance.new("Frame")
local Percent = Instance.new("TextLabel")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(20,20,20)
Frame.Position = UDim2.new(0.35,0,0.4,0)
Frame.Size = UDim2.new(0,320,0,160)

UICorner.Parent = Frame

Title.Parent = Frame
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1,0,0,50)
Title.Font = Enum.Font.GothamBold
Title.Text = "🌊 KC SEA HUB"
Title.TextColor3 = Color3.fromRGB(255,255,255)
Title.TextSize = 24

LoadingBar.Parent = Frame
LoadingBar.BackgroundColor3 = Color3.fromRGB(45,45,45)
LoadingBar.Position = UDim2.new(0.1,0,0.6,0)
LoadingBar.Size = UDim2.new(0,250,0,20)

Instance.new("UICorner",LoadingBar)

Loading.Parent = LoadingBar
Loading.BackgroundColor3 = Color3.fromRGB(0,170,255)
Loading.Size = UDim2.new(0,0,1,0)

Instance.new("UICorner",Loading)

Percent.Parent = Frame
Percent.BackgroundTransparency = 1
Percent.Position = UDim2.new(0,0,0.78,0)
Percent.Size = UDim2.new(1,0,0,30)
Percent.Font = Enum.Font.Gotham
Percent.Text = "Đang tải KC Hub... 0%"
Percent.TextColor3 = Color3.fromRGB(255,255,255)
Percent.TextSize = 18

for i = 1,100 do
   task.wait(0.03)

   Loading.Size = UDim2.new(i/100,0,1,0)
   Percent.Text = "Đang tải KC Hub... "..i.."%"
end

task.wait(1)
ScreenGui:Destroy()

---------------------------------------------------
-- GUI LIBRARY
---------------------------------------------------

local Library = loadstring(game:HttpGet(
"https://raw.githubusercontent.com/shlexware/Rayfield/main/source"))()

local Window = Library:CreateWindow({
   Name = "🌊 KC SEA HUB",
   LoadingTitle = "KC HUB",
   LoadingSubtitle = "Blox Fruits",
   ConfigurationSaving = {
      Enabled = false
   },
   KeySystem = false
})

---------------------------------------------------
-- TAB
---------------------------------------------------

local Main = Window:CreateTab("⚔️ Chính",4483362458)
local Sea = Window:CreateTab("🌊 Sea Event",4483362458)
local Misc = Window:CreateTab("⚙️ Khác",4483362458)

---------------------------------------------------
-- BIẾN
---------------------------------------------------

_G.FastAttack = false
_G.AutoHaki = false
_G.AutoSea = false

---------------------------------------------------
-- THÔNG BÁO
---------------------------------------------------

Library:Notify({
   Title = "🌊 KC SEA HUB",
   Content = "Script đã bật thành công!",
   Duration = 5,
   Image = 4483362458,
})

---------------------------------------------------
-- TAB CHÍNH
---------------------------------------------------

Main:CreateParagraph({
   Title = "✨ KC HUB",
   Content = "Tổng hợp đánh nhanh & săn Sea Event"
})

-- đánh nhanh
Main:CreateToggle({
   Name = "⚡ Đánh Siêu Nhanh",
   CurrentValue = false,

   Callback = function(v)

      _G.FastAttack = v

      while _G.FastAttack do
         task.wait(0.03)

         pcall(function()

            game:GetService("VirtualUser")
            :Button1Down(Vector2.new(0,0))

            task.wait()

            game:GetService("VirtualUser")
            :Button1Up(Vector2.new(0,0))

         end)
      end
   end,
})

-- auto haki
Main:CreateToggle({
   Name = "🛡️ Tự Động Haki",
   CurrentValue = false,

   Callback = function(v)

      _G.AutoHaki = v

      while _G.AutoHaki do
         task.wait(5)

         pcall(function()

            game:GetService("ReplicatedStorage")
            .Remotes.CommF_:InvokeServer("Buso")

         end)
      end
   end,
})

---------------------------------------------------
-- SEA EVENT
---------------------------------------------------

Sea:CreateParagraph({
   Title = "🌊 Sea Event",
   Content = "Tự động săn quái biển"
})

Sea:CreateToggle({
   Name = "🚢 Tự Động Đi Biển",
   CurrentValue = false,

   Callback = function(v)

      _G.AutoSea = v

      while _G.AutoSea do
         task.wait(1)

         pcall(function()

            local hrp =
            game.Players.LocalPlayer.Character.HumanoidRootPart

            hrp.CFrame =
            hrp.CFrame + Vector3.new(0,0,-700)

         end)
      end
   end,
})

Sea:CreateButton({
   Name = "⛵ Mua Thuyền Guardian",

   Callback = function()

      game:GetService("ReplicatedStorage")
      .Remotes.CommF_:InvokeServer("BuyBoat","Guardian")

   end,
})

---------------------------------------------------
-- KHÁC
---------------------------------------------------

Misc:CreateButton({
   Name = "📱 Giảm Lag",

   Callback = function()

      for i,v in pairs(game:GetDescendants()) do
         pcall(function()

            if v:IsA("ParticleEmitter") then
               v.Enabled = false
            end

            if v:IsA("Trail") then
               v.Enabled = false
            end

         end)
      end

      settings().Rendering.QualityLevel = "Level01"

   end,
})

Misc:CreateButton({
   Name = "🔄 Vào Lại Server",

   Callback = function()

      game:GetService("TeleportService"):Teleport(
      game.PlaceId,
      game.Players.LocalPlayer)

   end,
})

---------------------------------------------------
-- CHỐNG AFK
---------------------------------------------------

local vu = game:GetService("VirtualUser")

game.Players.LocalPlayer.Idled:Connect(function()

   vu:Button2Down(Vector2.new(0,0),
   workspace.CurrentCamera.CFrame)

   task.wait(1)

   vu:Button2Up(Vector2.new(0,0),
   workspace.CurrentCamera.CFrame)

end)
