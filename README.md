local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Rayfield/main/source"))()

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
   Content = "Hub đã bật thành công!",
   Duration = 5
})

---------------------------------------------------
-- ĐÁNH NHANH
---------------------------------------------------

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

---------------------------------------------------
-- AUTO HAKI
---------------------------------------------------

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

Sea:CreateToggle({
   Name = "🌊 Tự Động Đi Biển",
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

---------------------------------------------------
-- MUA THUYỀN
---------------------------------------------------

Sea:CreateButton({
   Name = "⛵ Mua Thuyền Guardian",

   Callback = function()

      game:GetService("ReplicatedStorage")
      .Remotes.CommF_:InvokeServer("BuyBoat","Guardian")

   end,
})

---------------------------------------------------
-- GIẢM LAG
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

---------------------------------------------------
-- REJOIN
---------------------------------------------------

Misc:CreateButton({
   Name = "🔄 Vào Lại Server",

   Callback = function()

      game:GetService("TeleportService"):Teleport(
      game.PlaceId,
      game.Players.LocalPlayer)

   end,
})

---------------------------------------------------
-- ANTI AFK
---------------------------------------------------

local vu = game:GetService("VirtualUser")

game.Players.LocalPlayer.Idled:Connect(function()

   vu:Button2Down(Vector2.new(0,0),
   workspace.CurrentCamera.CFrame)

   task.wait(1)

   vu:Button2Up(Vector2.new(0,0),
   workspace.CurrentCamera.CFrame)

end)
