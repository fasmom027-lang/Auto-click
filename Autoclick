repeat task.wait() until game:IsLoaded()

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

troll = {""}
intheGame = false
_G.Mobile_752 = false

if _G.AutoClickerStart_Welp then
	local oldGui = playerGui:FindFirstChild("AutoGui")
	if oldGui then oldGui:Destroy() end
	local oldCoreGui = game:GetService("CoreGui"):FindFirstChild("AutoGui")
	if oldCoreGui then oldCoreGui:Destroy() end
end
_G.AutoClickerStart_Welp = true

local touchGui = playerGui:FindFirstChild("TouchGui")

local function setScreen()
	local guiGame = playerGui:FindFirstChild("ScreenGui")
	if not guiGame then return end

	local promoFrame = guiGame:FindFirstChild("PromoFrame")
	if promoFrame then promoFrame:Destroy() end

	local coinFrame = guiGame:FindFirstChild("CoinFrame")
	if coinFrame then
		coinFrame.Position = UDim2.new(0.86, 0, 0.3, 0)
	end
end

RunService.RenderStepped:Connect(function()
	if _G.Mobile_752 == true then
		setScreen()
	end
end)

player.Chatted:Connect(function(msg)
	local prefix = "/e"
	local cmd = "cmd"
	local argsMsg = msg:split(" ")
	if argsMsg[1] == prefix and argsMsg[2] and argsMsg[2]:lower() == cmd and argsMsg[3] then
		local args = { [1] = argsMsg[3]:lower() }
		local remotes = ReplicatedStorage:FindFirstChild("Remotes")
		if remotes and remotes:FindFirstChild("PromoRewards") then
			remotes.PromoRewards:FireServer(unpack(args))
		end
	end
end)

if touchGui then
	_G.Mobile_752 = true
	touchGui.Name = "TouchGui1"
	task.spawn(function()
		while task.wait(0.25) do
			if touchGui and touchGui.Parent then
				touchGui.Name = "TouchGui1"
				local controlFrame = touchGui:FindFirstChild("TouchControlFrame")
				if controlFrame then
					for _, v in ipairs(controlFrame:GetChildren()) do
						if v:IsA("GuiObject") then
							v.Visible = true
						end
					end
				end
			end
		end
	end)
end

local function hookCharacter(char)
	intheGame = false
	local hum = char:WaitForChild("Humanoid")
	hum.Died:Connect(function()
		intheGame = false
	end)
end

if player.Character then
	task.spawn(hookCharacter, player.Character)
end
player.CharacterAdded:Connect(hookCharacter)

player:WaitForChild("Backpack").ChildAdded:Connect(function()
	if _G.Mobile_752 == true then
		intheGame = true
	end
end)

RunService.RenderStepped:Connect(function()
	local shiftlock = playerGui:FindFirstChild("Shiftlock")
	if shiftlock then
		local imgBtn = shiftlock:FindFirstChild("ImageButton")
		if imgBtn then
			imgBtn.Visible = true
		end
	end
end)

-- ==========================================
-- ألوان التصميم والخط العربي الواضح
-- ==========================================
local Theme = {
	WindowBg   = Color3.fromRGB(16, 15, 20),
	RedGlow    = Color3.fromRGB(235, 42, 48),
	RedDark    = Color3.fromRGB(115, 18, 22),
	TileBg     = Color3.fromRGB(28, 28, 35),
	TileBorder = Color3.fromRGB(82, 80, 92),
	TextWhite  = Color3.fromRGB(255, 255, 255),
	TextMuted  = Color3.fromRGB(185, 190, 205),
	TextBlue   = Color3.fromRGB(108, 178, 255),
	GreenGlow  = Color3.fromRGB(52, 214, 134),
	BlueGlow   = Color3.fromRGB(45, 145, 255),
}

local ArabicFont = Font.new(
	"rbxasset://fonts/families/SourceSansPro.json",
	Enum.FontWeight.Bold,
	Enum.FontStyle.Normal
)

local function addCorner(inst, radius)
	local c = Instance.new("UICorner")
	c.CornerRadius = UDim.new(0, radius or 10)
	c.Parent = inst
	return c
end

local function addStroke(inst, color, thickness, transparency)
	local s = Instance.new("UIStroke")
	s.Color = color or Theme.TileBorder
	s.Thickness = thickness or 1.4
	s.Transparency = transparency or 0
	s.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
	s.Parent = inst
	return s
end

-- ==========================================
-- بناء الواجهة
-- ==========================================
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "AutoGui"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game:GetService("CoreGui")

local eqToolObj = Instance.new("ObjectValue")
eqToolObj.Name = "eqTool"
eqToolObj.Parent = ScreenGui

local dataFolder = Instance.new("Folder")
dataFolder.Name = "data"
dataFolder.Parent = ScreenGui

local reachValueObj = Instance.new("NumberValue")
reachValueObj.Name = "ReachDistance"
reachValueObj.Value = 7
reachValueObj.Parent = dataFolder

-- أزرار التبديل السريع للأدوات (نفس مكانها الأصلي بالضبط)
local toolsFrame = Instance.new("Frame")
toolsFrame.Name = "Tools"
toolsFrame.BorderSizePixel = 0
toolsFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
toolsFrame.AnchorPoint = Vector2.new(1, 1)
toolsFrame.Size = UDim2.new(0, 100, 0, 40)
toolsFrame.Position = UDim2.new(0.86, 0, 0.75, 0)
toolsFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
toolsFrame.BackgroundTransparency = 1
toolsFrame.Parent = ScreenGui

local toolsList = Instance.new("UIListLayout")
toolsList.HorizontalAlignment = Enum.HorizontalAlignment.Right
toolsList.Padding = UDim.new(0, 5)
toolsList.FillDirection = Enum.FillDirection.Horizontal
toolsList.Parent = toolsFrame

local function createToolSlot(slotName, fallbackIcon)
	local slot = Instance.new("Frame")
	slot.Name = slotName
	slot.BorderSizePixel = 0
	slot.BackgroundColor3 = Color3.fromRGB(36, 36, 44)
	slot.AnchorPoint = Vector2.new(0.5, 0.5)
	slot.Size = UDim2.new(1, 0, 1, 0)
	slot.Position = UDim2.new(0, 40, 0.1, 0)
	slot.BorderColor3 = Color3.fromRGB(0, 0, 0)
	slot.Parent = toolsFrame

	local aspect = Instance.new("UIAspectRatioConstraint")
	aspect.AspectRatio = 1.2
	aspect.Parent = slot

	addCorner(slot, 8)
	addStroke(slot, Color3.fromRGB(107, 107, 107), 1.5)

	local eqBool = Instance.new("BoolValue")
	eqBool.Name = "Eq"
	eqBool.Parent = slot

	local imgBtn = Instance.new("ImageButton")
	imgBtn.Name = "ImageButton"
	imgBtn.BorderSizePixel = 0
	imgBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	imgBtn.AnchorPoint = Vector2.new(0.5, 0.5)
	imgBtn.Image = fallbackIcon or "rbxassetid://15317582625"
	imgBtn.Size = UDim2.new(0.75, 0, 0.75, 0)
	imgBtn.BackgroundTransparency = 1
	imgBtn.BorderColor3 = Color3.fromRGB(0, 0, 0)
	imgBtn.Position = UDim2.new(0.5, 0, 0.5, 0)
	imgBtn.Parent = slot

	local toolObj = Instance.new("ObjectValue")
	toolObj.Name = "Tool"
	toolObj.Parent = slot

	return slot
end

local potionFrame = createToolSlot("1Potions", "rbxassetid://15317582625")
local pickaxeFrame = createToolSlot("2Pickaxe", "rbxassetid://15317582625")

-- علامة (+) في منتصف الشاشة
local crosshair = Instance.new("Frame")
crosshair.Name = "CenterCrosshair"
crosshair.AnchorPoint = Vector2.new(0.5, 0.5)
crosshair.Position = UDim2.fromScale(0.5, 0.5)
crosshair.Size = UDim2.new(0, 20, 0, 20)
crosshair.BackgroundTransparency = 1
crosshair.Visible = false
crosshair.Parent = ScreenGui

local hBar = Instance.new("Frame")
hBar.AnchorPoint = Vector2.new(0.5, 0.5)
hBar.Position = UDim2.fromScale(0.5, 0.5)
hBar.Size = UDim2.new(0, 12, 0, 2)
hBar.BackgroundColor3 = Theme.TextWhite
hBar.BorderSizePixel = 0
hBar.Parent = crosshair
addCorner(hBar, 999)

local vBar = Instance.new("Frame")
vBar.AnchorPoint = Vector2.new(0.5, 0.5)
vBar.Position = UDim2.fromScale(0.5, 0.5)
vBar.Size = UDim2.new(0, 2, 0, 12)
vBar.BackgroundColor3 = Theme.TextWhite
vBar.BorderSizePixel = 0
vBar.Parent = crosshair
addCorner(vBar, 999)

local centerDot = Instance.new("Frame")
centerDot.AnchorPoint = Vector2.new(0.5, 0.5)
centerDot.Position = UDim2.fromScale(0.5, 0.5)
centerDot.Size = UDim2.new(0, 4, 0, 4)
centerDot.BackgroundColor3 = Theme.BlueGlow
centerDot.BorderSizePixel = 0
centerDot.Parent = crosshair
addCorner(centerDot, 999)

-- زر إعادة فتح النافذة بعد الإغلاق بـ X
local reopenBtn = Instance.new("TextButton")
reopenBtn.Name = "ReopenHubBtn"
reopenBtn.Size = UDim2.new(0, 88, 0, 26)
reopenBtn.Position = UDim2.new(0.5, -44, 0, 12)
reopenBtn.BackgroundColor3 = Theme.WindowBg
reopenBtn.BackgroundTransparency = 0.15
reopenBtn.Text = "AUTO HUB"
reopenBtn.TextColor3 = Theme.TextWhite
reopenBtn.FontFace = ArabicFont
reopenBtn.TextSize = 13
reopenBtn.Visible = false
reopenBtn.Parent = ScreenGui
addCorner(reopenBtn, 8)
addStroke(reopenBtn, Theme.RedGlow, 1.4, 0.1)

-- النافذة الرئيسية (حجم أصغر ومضغوط)
local mainWindow = Instance.new("Frame")
mainWindow.Name = "MainPanel"
mainWindow.AnchorPoint = Vector2.new(0.5, 0.5)
mainWindow.Size = UDim2.new(0, 295, 0, 325)
mainWindow.Position = UDim2.new(0.5, 0, 0.5, 0)
mainWindow.BackgroundColor3 = Theme.WindowBg
mainWindow.BackgroundTransparency = 0.12
mainWindow.BorderSizePixel = 0
mainWindow.Parent = ScreenGui
addCorner(mainWindow, 18)

local outerGlowHalo = Instance.new("Frame")
outerGlowHalo.Name = "OuterGlow"
outerGlowHalo.Size = UDim2.new(1, 8, 1, 8)
outerGlowHalo.Position = UDim2.new(0, -4, 0, -4)
outerGlowHalo.BackgroundTransparency = 1
outerGlowHalo.ZIndex = 0
outerGlowHalo.Parent = mainWindow
addCorner(outerGlowHalo, 21)
addStroke(outerGlowHalo, Theme.RedGlow, 2.5, 0.45)

addStroke(mainWindow, Theme.RedGlow, 2, 0.08)

-- شريط العنوان العلوي (قابل للسحب)
local header = Instance.new("Frame")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 44)
header.Position = UDim2.new(0, 0, 0, 0)
header.BackgroundTransparency = 1
header.Parent = mainWindow

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, -76, 1, 0)
titleLabel.Position = UDim2.new(0, 38, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "AUTO HUB"
titleLabel.TextColor3 = Theme.TextWhite
titleLabel.FontFace = ArabicFont
titleLabel.TextSize = 17
titleLabel.Parent = header

local closeBtn = Instance.new("TextButton")
closeBtn.Name = "CloseButton"
closeBtn.Size = UDim2.new(0, 28, 0, 28)
closeBtn.Position = UDim2.new(1, -38, 0, 8)
closeBtn.BackgroundTransparency = 1
closeBtn.Text = "✕"
closeBtn.TextColor3 = Theme.TextWhite
closeBtn.FontFace = ArabicFont
closeBtn.TextSize = 16
closeBtn.Parent = header

local topDivider = Instance.new("Frame")
topDivider.Size = UDim2.new(1, -24, 0, 1)
topDivider.Position = UDim2.new(0, 12, 0, 45)
topDivider.BackgroundColor3 = Theme.RedDark
topDivider.BackgroundTransparency = 0.45
topDivider.BorderSizePixel = 0
topDivider.Parent = mainWindow

local midDivider = Instance.new("Frame")
midDivider.Size = UDim2.new(0, 1, 1, -60)
midDivider.Position = UDim2.new(0.5, 0, 0, 52)
midDivider.BackgroundColor3 = Theme.RedDark
midDivider.BackgroundTransparency = 0.55
midDivider.BorderSizePixel = 0
midDivider.Parent = mainWindow

-- ==========================================
-- العمود الأيسر: 4 سرعات بأسماء واضحة وأيقونات
-- ==========================================
local leftCol = Instance.new("Frame")
leftCol.Name = "LeftColumn"
leftCol.Size = UDim2.new(0.5, -16, 1, -60)
leftCol.Position = UDim2.new(0, 11, 0, 52)
leftCol.BackgroundTransparency = 1
leftCol.Parent = mainWindow

local leftLayout = Instance.new("UIListLayout")
leftLayout.Padding = UDim.new(0, 7)
leftLayout.FillDirection = Enum.FillDirection.Vertical
leftLayout.Parent = leftCol

local function createSpeedTile(cardName, arabicLabel, defaultNum, iconText)
	local tile = Instance.new("Frame")
	tile.Name = cardName
	tile.Size = UDim2.new(1, 0, 0, 60)
	tile.BackgroundColor3 = Theme.TileBg
	tile.BackgroundTransparency = 0.25
	tile.BorderSizePixel = 0
	tile.Parent = leftCol
	addCorner(tile, 11)
	local stroke = addStroke(tile, Theme.TileBorder, 1.3, 0.2)

	local lbl = Instance.new("TextLabel")
	lbl.Size = UDim2.new(0.76, 0, 0, 18)
	lbl.Position = UDim2.new(0.06, 0, 0, 4)
	lbl.BackgroundTransparency = 1
	lbl.Text = arabicLabel
	lbl.TextColor3 = Theme.TextMuted
	lbl.FontFace = ArabicFont
	lbl.TextSize = 12
	lbl.TextXAlignment = Enum.TextXAlignment.Left
	lbl.Parent = tile

	local iconLbl = Instance.new("TextLabel")
	iconLbl.Size = UDim2.new(0.2, 0, 0, 18)
	iconLbl.Position = UDim2.new(0.78, 0, 0, 4)
	iconLbl.BackgroundTransparency = 1
	iconLbl.Text = iconText
	iconLbl.TextColor3 = Theme.TextWhite
	iconLbl.FontFace = ArabicFont
	iconLbl.TextSize = 13
	iconLbl.Parent = tile

	local box = Instance.new("TextBox")
	box.Name = "TextBox"
	box.Size = UDim2.new(0.88, 0, 0, 30)
	box.Position = UDim2.new(0.06, 0, 0, 24)
	box.BackgroundTransparency = 1
	box.Text = tostring(defaultNum)
	box.TextColor3 = Theme.TextBlue
	box.FontFace = ArabicFont
	box.TextSize = 18
	box.TextXAlignment = Enum.TextXAlignment.Left
	box.ClearTextOnFocus = false
	box.Parent = tile

	local speedVal = Instance.new("NumberValue")
	speedVal.Name = "Speed"
	speedVal.Value = defaultNum / 100
	speedVal.Parent = tile

	return speedVal, box, stroke
end

local blockSpeedVal, _, blockStroke = createSpeedTile("blockSpeed", "سرعة البلوكات", 10, "◴")
local swordSpeedVal, _, swordStroke = createSpeedTile("SwordSpeed", "سرعة السيف", 10, "❖")
local bowSpeedVal, _, bowStroke     = createSpeedTile("BowSpeed", "سرعة القوس", 10, "◈")
local axeSpeedVal, _, axeStroke     = createSpeedTile("AxeSpeed", "سرعة الفأس", 10, "↗")

-- ==========================================
-- العمود الأيمن: Aim bot | Auto jump | سرعة الريتش Reach | تفعيل | Auto
-- ==========================================
local rightCol = Instance.new("Frame")
rightCol.Name = "RightColumn"
rightCol.Size = UDim2.new(0.5, -16, 1, -60)
rightCol.Position = UDim2.new(0.5, 5, 0, 52)
rightCol.BackgroundTransparency = 1
rightCol.Parent = mainWindow

local rightLayout = Instance.new("UIListLayout")
rightLayout.Padding = UDim.new(0, 7)
rightLayout.FillDirection = Enum.FillDirection.Vertical
rightLayout.Parent = rightCol

-- 1) Aim bot
local aimTile = Instance.new("Frame")
aimTile.Name = "AimBotCard"
aimTile.Size = UDim2.new(1, 0, 0, 54)
aimTile.BackgroundColor3 = Theme.TileBg
aimTile.BackgroundTransparency = 0.25
aimTile.BorderSizePixel = 0
aimTile.Parent = rightCol
addCorner(aimTile, 11)
local aimStroke = addStroke(aimTile, Theme.TileBorder, 1.3, 0.2)

local aimBtn = Instance.new("TextButton")
aimBtn.Name = "AimBotButton"
aimBtn.Size = UDim2.new(1, 0, 1, 0)
aimBtn.BackgroundTransparency = 1
aimBtn.Text = "Aim bot   ◎"
aimBtn.TextColor3 = Theme.TextWhite
aimBtn.FontFace = ArabicFont
aimBtn.TextSize = 14
aimBtn.Parent = aimTile

-- 2) Auto jump
local jumpTile = Instance.new("Frame")
jumpTile.Name = "AutoJumpCard"
jumpTile.Size = UDim2.new(1, 0, 0, 68)
jumpTile.BackgroundColor3 = Theme.TileBg
jumpTile.BackgroundTransparency = 0.25
jumpTile.BorderSizePixel = 0
jumpTile.Parent = rightCol
addCorner(jumpTile, 11)
local jumpStroke = addStroke(jumpTile, Theme.TileBorder, 1.3, 0.2)

local jumpBtn = Instance.new("TextButton")
jumpBtn.Name = "AutoJumpButton"
jumpBtn.Size = UDim2.new(1, 0, 1, 0)
jumpBtn.BackgroundTransparency = 1
jumpBtn.Text = "Auto jump   ↑"
jumpBtn.TextColor3 = Theme.TextWhite
jumpBtn.FontFace = ArabicFont
jumpBtn.TextSize = 14
jumpBtn.Parent = jumpTile

-- 3) سرعة الريتش Reach (مع اسم واضح + رقم 7 + شريط)
local reachTile = Instance.new("Frame")
reachTile.Name = "ReachCard"
reachTile.Size = UDim2.new(1, 0, 0, 60)
reachTile.BackgroundColor3 = Theme.TileBg
reachTile.BackgroundTransparency = 0.25
reachTile.BorderSizePixel = 0
reachTile.Parent = rightCol
addCorner(reachTile, 11)
local reachStroke = addStroke(reachTile, Theme.TileBorder, 1.3, 0.2)

local reachBtn = Instance.new("TextButton")
reachBtn.Name = "ReachButton"
reachBtn.Size = UDim2.new(1, 0, 0, 24)
reachBtn.Position = UDim2.new(0, 0, 0, 3)
reachBtn.BackgroundTransparency = 1
reachBtn.Text = "سرعة الريتش · Reach"
reachBtn.TextColor3 = Theme.TextWhite
reachBtn.FontFace = ArabicFont
reachBtn.TextSize = 12
reachBtn.Parent = reachTile

local reachBarBg = Instance.new("Frame")
reachBarBg.Size = UDim2.new(0.88, 0, 0, 22)
reachBarBg.Position = UDim2.new(0.06, 0, 0, 31)
reachBarBg.BackgroundTransparency = 1
reachBarBg.Parent = reachTile

local reachTicks = Instance.new("TextLabel")
reachTicks.Size = UDim2.new(0.42, 0, 1, 0)
reachTicks.Position = UDim2.new(0, 0, 0, 0)
reachTicks.BackgroundTransparency = 1
reachTicks.Text = "| | | |"
reachTicks.TextColor3 = Color3.fromRGB(135, 138, 150)
reachTicks.FontFace = ArabicFont
reachTicks.TextSize = 10
reachTicks.TextXAlignment = Enum.TextXAlignment.Left
reachTicks.Parent = reachBarBg

local reachBox = Instance.new("TextBox")
reachBox.Name = "ReachValueBox"
reachBox.Size = UDim2.new(0.22, 0, 1, 0)
reachBox.Position = UDim2.new(0.4, 0, 0, 0)
reachBox.BackgroundTransparency = 1
reachBox.Text = "7"
reachBox.TextColor3 = Theme.TextWhite
reachBox.FontFace = ArabicFont
reachBox.TextSize = 13
reachBox.ClearTextOnFocus = false
reachBox.Parent = reachBarBg

local reachTrack = Instance.new("Frame")
reachTrack.Size = UDim2.new(0.34, 0, 0, 5)
reachTrack.Position = UDim2.new(0.65, 0, 0.5, -2.5)
reachTrack.BackgroundColor3 = Color3.fromRGB(60, 62, 72)
reachTrack.BorderSizePixel = 0
reachTrack.Parent = reachBarBg
addCorner(reachTrack, 999)

local reachFill = Instance.new("Frame")
reachFill.Size = UDim2.new(0.35, 0, 1, 0)
reachFill.BackgroundColor3 = Color3.fromRGB(235, 65, 45)
reachFill.BorderSizePixel = 0
reachFill.Parent = reachTrack
addCorner(reachFill, 999)

-- 4) تفعيل | Auto
local auto = Instance.new("Frame")
auto.Name = "auto"
auto.Size = UDim2.new(1, 0, 0, 58)
auto.BackgroundColor3 = Theme.TileBg
auto.BackgroundTransparency = 0.22
auto.BorderSizePixel = 0
auto.Parent = rightCol
addCorner(auto, 11)
local autoStroke = addStroke(auto, Theme.GreenGlow, 1.8, 0.1)

local autoBtn = Instance.new("TextButton")
autoBtn.Name = "F"
autoBtn.Size = UDim2.new(0.72, 0, 1, 0)
autoBtn.Position = UDim2.new(0.05, 0, 0, 0)
autoBtn.BackgroundTransparency = 1
autoBtn.Text = "تفعيل | Auto"
autoBtn.TextColor3 = Theme.TextWhite
autoBtn.FontFace = ArabicFont
autoBtn.TextSize = 14
autoBtn.TextXAlignment = Enum.TextXAlignment.Left
autoBtn.Parent = auto

local pillSwitch = Instance.new("Frame")
pillSwitch.Size = UDim2.new(0, 30, 0, 15)
pillSwitch.Position = UDim2.new(1, -36, 0.5, -7.5)
pillSwitch.BackgroundColor3 = Color3.fromRGB(20, 46, 82)
pillSwitch.BorderSizePixel = 0
pillSwitch.Parent = auto
addCorner(pillSwitch, 999)
addStroke(pillSwitch, Theme.BlueGlow, 1.3, 0.2)

local pillKnob = Instance.new("Frame")
pillKnob.Size = UDim2.new(0, 11, 0, 11)
pillKnob.Position = UDim2.new(0, 17, 0.5, -5.5)
pillKnob.BackgroundColor3 = Theme.TextBlue
pillKnob.BorderSizePixel = 0
pillKnob.Parent = pillSwitch
addCorner(pillKnob, 999)

local startVal = Instance.new("BoolValue")
startVal.Name = "Start"
startVal.Value = false
startVal.Parent = auto

-- ==========================================
-- إغلاق/إعادة فتح وسحب النافذة
-- ==========================================
closeBtn.MouseButton1Click:Connect(function()
	mainWindow.Visible = false
	reopenBtn.Visible = true
end)

reopenBtn.MouseButton1Click:Connect(function()
	mainWindow.Visible = true
	reopenBtn.Visible = false
end)

local dragging = false
local dragInput, dragStart, startPos

header.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = mainWindow.Position

		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

header.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		local delta = input.Position - dragStart
		mainWindow.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

-- ==========================================
-- منطق Reach الفعلي + Aim bot + Auto jump
-- ==========================================
local reachEnabled = false
local originalSizes = {}

local function restoreReachParts()
	for part, oldSize in pairs(originalSizes) do
		if part and part.Parent then
			part.Size = oldSize
		end
		originalSizes[part] = nil
	end
end

local function updateReachHitboxes()
	if not reachEnabled then
		restoreReachParts()
		return
	end

	local char = player.Character
	local root = char and char:FindFirstChild("HumanoidRootPart")
	if not root then return end

	local reachDist = math.clamp(reachValueObj.Value, 1, 25)
	local activeParts = {}

	for _, plr in ipairs(Players:GetPlayers()) do
		if plr ~= player and plr.Character then
			local enemyRoot = plr.Character:FindFirstChild("HumanoidRootPart")
			if enemyRoot then
				local dist = (enemyRoot.Position - root.Position).Magnitude
				if dist <= reachDist + 8 then
					if not originalSizes[enemyRoot] then
						originalSizes[enemyRoot] = enemyRoot.Size
					end
					enemyRoot.Size = Vector3.new(reachDist, reachDist, reachDist)
					activeParts[enemyRoot] = true
				end
			end
		end
	end

	for part, oldSize in pairs(originalSizes) do
		if not activeParts[part] then
			if part and part.Parent then
				part.Size = oldSize
			end
			originalSizes[part] = nil
		end
	end
end

local function updateReachBar(val)
	local ratio = math.clamp(val / 20, 0.08, 1)
	TweenService:Create(reachFill, TweenInfo.new(0.15), {
		Size = UDim2.new(ratio, 0, 1, 0)
	}):Play()
end

reachBox.FocusLost:Connect(function()
	local num = tonumber(reachBox.Text)
	if num == nil or num <= 0 then
		reachBox.Text = tostring(reachValueObj.Value)
		return
	end
	reachValueObj.Value = num
	updateReachBar(num)
	updateReachHitboxes()
end)

reachBtn.MouseButton1Click:Connect(function()
	local num = tonumber(reachBox.Text)
	if num and num > 0 then
		reachValueObj.Value = num
		updateReachBar(num)
	end

	reachEnabled = not reachEnabled
	reachBtn.Text = reachEnabled and "Reach · ON" or "سرعة الريتش · Reach"
	TweenService:Create(reachStroke, TweenInfo.new(0.15), {
		Color = reachEnabled and Theme.GreenGlow or Theme.TileBorder
	}):Play()

	if not reachEnabled then
		restoreReachParts()
	else
		updateReachHitboxes()
	end
end)

RunService.Heartbeat:Connect(function()
	if reachEnabled then
		updateReachHitboxes()
	end
end)

local aimBotEnabled = false
aimBtn.MouseButton1Click:Connect(function()
	aimBotEnabled = not aimBotEnabled
	crosshair.Visible = aimBotEnabled
	TweenService:Create(aimStroke, TweenInfo.new(0.15), {
		Color = aimBotEnabled and Theme.BlueGlow or Theme.TileBorder
	}):Play()
end)

local autoJumpEnabled = false
jumpBtn.MouseButton1Click:Connect(function()
	autoJumpEnabled = not autoJumpEnabled
	TweenService:Create(jumpStroke, TweenInfo.new(0.15), {
		Color = autoJumpEnabled and Theme.GreenGlow or Theme.TileBorder
	}):Play()
end)

RunService.Heartbeat:Connect(function()
	if not autoJumpEnabled then return end
	local char = player.Character
	local hum = char and char:FindFirstChildOfClass("Humanoid")
	if hum and hum.Health > 0 and hum.FloorMaterial ~= Enum.Material.Air then
		hum:ChangeState(Enum.HumanoidStateType.Jumping)
		hum.Jump = true
	end
end)

-- ==========================================
-- منطق الأوتو كليكر والسرعات والـ Reach
-- ==========================================
local cooldowns = {
	["block"] = blockSpeedVal,
	["sword"] = swordSpeedVal,
	["bow"]   = bowSpeedVal,
	["axe"]   = axeSpeedVal,
}

for _, speedVal in pairs(cooldowns) do
	local box: TextBox = speedVal.Parent:WaitForChild("TextBox")
	box.FocusLost:Connect(function()
		local num = tonumber(box.Text)
		if num == nil or num / 100 <= 0 then
			box.Text = tostring(speedVal.Value * 100)
			return
		end
		speedVal.Value = num / 100
		local stroke = speedVal.Parent:FindFirstChildOfClass("UIStroke")
		if stroke then
			TweenService:Create(stroke, TweenInfo.new(0.2), { Color = Theme.GreenGlow }):Play()
			task.delay(0.35, function()
				TweenService:Create(stroke, TweenInfo.new(0.25), { Color = Theme.TileBorder }):Play()
			end)
		end
	end)
end

local function getAimTarget()
	local maxDist = reachEnabled and math.max(reachValueObj.Value, 1) or 25
	local cam = workspace.CurrentCamera
	if not cam then return player:GetMouse().Target end

	local vp = cam.ViewportSize
	local unitRay = cam:ViewportPointToRay(vp.X * 0.5, vp.Y * 0.5)
	local params = RaycastParams.new()
	params.FilterType = Enum.RaycastFilterType.Exclude
	if player.Character then
		params.FilterDescendantsInstances = { player.Character }
	end

	local res = workspace:Raycast(unitRay.Origin, unitRay.Direction * maxDist, params)
	if res then
		return res.Instance
	end
	return aimBotEnabled and nil or player:GetMouse().Target
end

local function clickTool()
	local tool = eqToolObj.Value
	if tool == nil then return end

	local cdVal = cooldowns[tool.Name:lower()]
	local waitTime = (cdVal and cdVal.Value > 0) and cdVal.Value or 0.1
	local target = getAimTarget()

	if tool.Name == "Sword" then
		tool:Activate()
		task.wait(waitTime)
	elseif tool.Name == "Bow" then
		task.spawn(function()
			local srv = tool:FindFirstChild("ServerControl")
			if srv and srv:IsA("RemoteFunction") then
				srv:InvokeServer(true)
				srv:InvokeServer(false)
			end
		end)
		task.wait(waitTime)
	elseif tool.Name == "Axe" then
		if target == nil then return end
		local remote = tool:FindFirstChild("RemoteEvent")
		if remote and remote:IsA("RemoteEvent") then
			remote:FireServer(target)
		end
		tool:Activate()
		task.wait(waitTime)
	elseif tool.Name == "Block" then
		local remote = tool:FindFirstChild("RemoteEvent")
		if remote and remote:IsA("RemoteEvent") and target then
			remote:FireServer(target)
		end
		tool:Activate()
		task.wait(waitTime)
	elseif tool:FindFirstChild("drink") or tool.Name == "Shield" then
		tool:Activate()
		task.wait(0.05)
	end
end

local function updateAutoState()
	local active = startVal.Value
	TweenService:Create(pillKnob, TweenInfo.new(0.18), {
		Position = active and UDim2.new(0, 2, 0.5, -5.5) or UDim2.new(0, 17, 0.5, -5.5),
		BackgroundColor3 = active and Theme.GreenGlow or Theme.TextBlue
	}):Play()
	TweenService:Create(autoStroke, TweenInfo.new(0.18), {
		Color = active and Theme.GreenGlow or Theme.BlueGlow
	}):Play()
end

autoBtn.MouseButton1Click:Connect(function()
	startVal.Value = not startVal.Value
end)

UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.E then
		startVal.Value = not startVal.Value
	end
end)

startVal.Changed:Connect(updateAutoState)
updateAutoState()

task.spawn(function()
	while task.wait(0.05) do
		local char = player.Character
		eqToolObj.Value = char and char:FindFirstChildOfClass("Tool") or nil
	end
end)

-- ==========================================
-- إصلاح التعرف على البوشن والأدوات السريعة
-- ==========================================
local function isPotionTool(item: Tool)
	local lowerName = item.Name:lower()
	if lowerName == "shield"
		or lowerName:find("potion", 1, true)
		or lowerName:find("drink", 1, true)
		or lowerName:find("heal", 1, true)
	then
		return true
	end

	for _, desc in ipairs(item:GetDescendants()) do
		local dName = desc.Name:lower()
		if dName:find("drink", 1, true)
			or dName:find("potion", 1, true)
			or dName:find("heal", 1, true)
		then
			return true
		end
	end

	return false
end

local function isAxeTool(item: Tool)
	local lowerName = item.Name:lower()
	return lowerName == "axe" or lowerName:find("axe", 1, true) ~= nil or lowerName:find("pick", 1, true) ~= nil
end

local function refreshToolSlots()
	local foundPotion = nil
	local foundAxe = nil

	local function scanContainer(container)
		if not container then return end
		for _, item in ipairs(container:GetChildren()) do
			if item:IsA("Tool") then
				if isPotionTool(item) then
					foundPotion = foundPotion or item
				elseif isAxeTool(item) then
					foundAxe = foundAxe or item
				end
			end
		end
	end

	scanContainer(player:FindFirstChild("Backpack"))
	scanContainer(player.Character)

	potionFrame.Tool.Value = foundPotion
	potionFrame.Visible = (foundPotion ~= nil)

	pickaxeFrame.Tool.Value = foundAxe
	pickaxeFrame.Visible = (foundAxe ~= nil)
end

task.spawn(function()
	while task.wait(0.2) do
		refreshToolSlots()
	end
end)

local function updateSlotStroke(frame: Frame, active: boolean)
	local stroke = frame:FindFirstChildOfClass("UIStroke")
	if stroke then
		TweenService:Create(stroke, TweenInfo.new(0.25), {
			Color = active and Theme.GreenGlow or Color3.fromRGB(170, 87, 88)
		}):Play()
	end
end

local function syncEquippedStates()
	for _, child in ipairs(toolsFrame:GetChildren()) do
		if child:IsA("Frame") then
			local eqBool = child:FindFirstChild("Eq")
			local toolObj = child:FindFirstChild("Tool")
			if eqBool and toolObj then
				local isEquipped = (eqToolObj.Value ~= nil and eqToolObj.Value == toolObj.Value)
				eqBool.Value = isEquipped
				updateSlotStroke(child, isEquipped)
			end
		end
	end
end

eqToolObj.Changed:Connect(syncEquippedStates)

for _, child in ipairs(toolsFrame:GetChildren()) do
	if child:IsA("Frame") then
		local btn: ImageButton = child:WaitForChild("ImageButton")
		local eqBool: BoolValue = child:WaitForChild("Eq")
		local toolObj: ObjectValue = child:WaitForChild("Tool")

		local function updateIcon()
			local currentTool = toolObj.Value
			if currentTool and currentTool:IsA("Tool") then
				if currentTool.TextureId ~= "" then
					btn.Image = currentTool.TextureId
				else
					btn.Image = "rbxassetid://15317582625"
				end
				child.Visible = true
			else
				child.Visible = false
			end
		end

		toolObj.Changed:Connect(updateIcon)
		updateIcon()

		btn.MouseButton1Click:Connect(function()
			local targetTool = toolObj.Value
			if not targetTool or not targetTool:IsA("Tool") then
				child.Visible = false
				return
			end

			local char = player.Character
			local backpack = player:FindFirstChild("Backpack")
			if not char or not backpack then return end

			if targetTool.Parent == char then
				targetTool.Parent = backpack
				eqBool.Value = false
				updateSlotStroke(child, false)
			else
				for _, equipped in ipairs(char:GetChildren()) do
					if equipped:IsA("Tool") then
						equipped.Parent = backpack
					end
				end
				targetTool.Parent = char
				eqBool.Value = true
				updateSlotStroke(child, true)
			end
		end)
	end
end

task.spawn(function()
	while true do
		if startVal.Value and eqToolObj.Value ~= nil then
			clickTool()
		end
		task.wait()
	end
end)

print("Loaded Real Reach AUTO HUB!!")
