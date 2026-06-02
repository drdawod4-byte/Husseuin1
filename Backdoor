-- [[ HUSSEIN ARCHITECT - SYSTEM SERVER-SIDE (SS) ADMIN ]]
-- حقوق الملكية: المطور حسين 🛡️

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local CoreGui = game:GetService("CoreGui")

print("--- [HUSSEIN SS] جارٍ قنص السيرفر والبحث عن منفذ SS تفعيلي ---")

-- قائمة بأشهر الريموتات (Backdoors) التي تسمح بتشغيل أكواد SS
local SS_Remotes = {
    "Handshake", "Remote", "VibeRemote", "Control", "Execute", 
    "ServerAction", "Glitch", "Freeze", "MemeRemote", "HDAdminRemote",
    "LunaRemote", "DexRemote", "Payload", "IronBrewRemote"
}

local MainRemote = nil

-- البحث عن الثغرة في السيرفر
for _, obj in pairs(ReplicatedStorage:GetDescendants()) do
    if obj:IsA("RemoteEvent") or obj:IsA("RemoteFunction") then
        for _, name in pairs(SS_Remotes) do
            if string.find(obj.Name, name) then
                MainRemote = obj
                break
            end
        end
    end
    if MainRemote then break end
end

-- دالة تشغيل لوحة التحكم والأوامر (تفتح وتعمل فقط إذا وُجدت ثغرة SS)
local function LaunchSSAdmin()
    local ScreenGui = Instance.new("ScreenGui")
    pcall(function() ScreenGui.Parent = CoreGui or LocalPlayer:WaitForChild("PlayerGui") end)
    ScreenGui.Name = "Hussein_SS_Admin"

    -- اللوحة الرئيسية
    local MainFrame = Instance.new("Frame", ScreenGui)
    MainFrame.Size = UDim2.new(0, 400, 0, 250)
    MainFrame.Position = UDim2.new(0.5, -200, 0.4, -125)
    MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
    MainFrame.BorderSizePixel = 2
    MainFrame.Active = true
    MainFrame.Draggable = true

    -- عنوان اللوحة
    local Title = Instance.new("TextLabel", MainFrame)
    Title.Size = UDim2.new(1, 0, 0, 40)
    Title.Text = "لوحة المطور حسين SS 🛡️"
    Title.TextColor3 = Color3.fromRGB(255, 100, 100)
    Title.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
    Title.TextSize = 16
    Title.Font = Enum.Font.SourceSansBold

    -- مربع نصي لكتابة اسم الضحية
    local NameInput = Instance.new("TextBox", MainFrame)
    NameInput.Size = UDim2.new(0, 280, 0, 35)
    NameInput.Position = UDim2.new(0.5, -140, 0, 65)
    NameInput.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
    NameInput.TextColor3 = Color3.fromRGB(255, 255, 255)
    NameInput.PlaceholderText = "اكتب اسم اللاعب هنا..."
    NameInput.Text = ""
    NameInput.TextSize = 14
    NameInput.Font = Enum.Font.SourceSans

    -- زر أمر القتل (Kill)
    local KillBtn = Instance.new("TextButton", MainFrame)
    KillBtn.Size = UDim2.new(0, 130, 0, 35)
    KillBtn.Position = UDim2.new(0.5, -145, 0, 120)
    KillBtn.BackgroundColor3 = Color3.fromRGB(150, 30, 30)
    KillBtn.Text = "إعدام (Kill)"
    KillBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    KillBtn.TextSize = 14
    KillBtn.Font = Enum.Font.SourceSansBold

    -- زر أمر التطير (Fling / Launch)
    local FlingBtn = Instance.new("TextButton", MainFrame)
    FlingBtn.Size = UDim2.new(0, 130, 0, 35)
    FlingBtn.Position = UDim2.new(0.5, 15, 0, 120)
    FlingBtn.BackgroundColor3 = Color3.fromRGB(150, 100, 30)
    FlingBtn.Text = "تطير (Fling)"
    FlingBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    FlingBtn.TextSize = 14
    FlingBtn.Font = Enum.Font.SourceSansBold

    -- نص الحالة بالأسفل
    local StatusLabel = Instance.new("TextLabel", MainFrame)
    StatusLabel.Size = UDim2.new(1, 0, 0, 30)
    StatusLabel.Position = UDim2.new(0, 0, 0, 180)
    StatusLabel.Text = "الحالة: متصل بالسيرفر بنجاح عبر " .. MainRemote.Name
    StatusLabel.TextColor3 = Color3.fromRGB(50, 200, 50)
    StatusLabel.BackgroundTransparency = 1
    StatusLabel.TextSize = 14

    -- دالة البحث عن اللاعب المستهدف بالاسم المختصر
    local function GetTarget()
        local text = string.lower(NameInput.Text)
        for _, p in pairs(Players:GetPlayers()) do
            if string.sub(string.lower(p.Name), 1, #text) == text then
                return p
            end
        end
        return nil
    end

    -- برمجية زر القتل (Kill SS)
    KillBtn.MouseButton1Click:Connect(function()
        local target = GetTarget()
        if target and target.Character then
            -- إرسال كود برميجي مباشر ينفذه السيرفر لقتل الضحية
            local code = string.format("game.Players['%s'].Character:BreakJoints()", target.Name)
            MainRemote:FireServer(code)
            StatusLabel.Text = "تم إرسال أمر القتل لـ " .. target.Name
        else
            StatusLabel.Text = "🚨 لم يتم العثور على اللاعب!"
        end
    end)

    -- برمجية زر التطير (Fling SS)
    FlingBtn.MouseButton1Click:Connect(function()
        local target = GetTarget()
        if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
            -- إرسال كود للسيرفر يرمي اللاعب في السماء بسرعة خارقة
            local code = string.format("game.Players['%s'].Character.HumanoidRootPart.Velocity = Vector3.new(0, 5000, 0)", target.Name)
            MainRemote:FireServer(code)
            StatusLabel.Text = "تم تطير اللاعب " .. target.Name
        else
            StatusLabel.Text = "🚨 لم يتم العثور على اللاعب!"
        end
    end)
end

-- التحقق النهائي وتشغيل اللوحة
if MainRemote then
    warn("🛡️ كفو! تم اختراق السيرفر وتأكيد منفذ الـ SS.")
    LaunchSSAdmin()
else
    print("-----------------------------------------")
    print("🛡️ نظام المطور حسين SS:")
    print("• النتيجة: السيرفر محمي بالكامل ولا يحتوي على ثغرات SS مفتوحة.")
    print("• نصيحة: جرب تشغيل السكربت في مابات تحتوي على موديلات مجانية كثيرة.")
    print("-----------------------------------------")
end
