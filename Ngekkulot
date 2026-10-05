-- ============================================
-- CAT HUB v2.0 — GUI TEST BUILD
-- ============================================

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")
local localPlayer = Players.LocalPlayer
local playerGui = localPlayer:WaitForChild("PlayerGui")

-- ============ CONFIG ============
local DISCORD_LINK = "https://discord.gg/FJK6QzNnf7"
local CAT_IMAGE_ID = "85043883236326"
local DC_IMAGE_ID  = "10367063084"
local FAV_FILE     = "cathub_fav_" .. localPlayer.UserId .. ".json"

-- ============ PALETTE ============
local COL_BG       = Color3.fromRGB(10, 15, 30)
local COL_PANEL    = Color3.fromRGB(18, 25, 45)
local COL_SIDEBAR  = Color3.fromRGB(15, 20, 38)
local COL_CARD     = Color3.fromRGB(25, 35, 60)
local COL_ACCENT   = Color3.fromRGB(30, 100, 230)
local COL_GLOW     = Color3.fromRGB(64, 128, 255)
local COL_TEXT     = Color3.fromRGB(255, 255, 255)
local COL_SUBTEXT  = Color3.fromRGB(150, 170, 200)
local COL_MUTED    = Color3.fromRGB(100, 115, 140)
local COL_STAR     = Color3.fromRGB(255, 200, 60)
local COL_GREEN    = Color3.fromRGB(80, 220, 130)

-- ============ FAVORITES SYSTEM ============
local favorites = {}

local function loadFavorites()
    favorites = {}
    if readfile and isfile then
        local ok, exists = pcall(function() return isfile(FAV_FILE) end)
        if ok and exists then
            local ok2, content = pcall(function() return readfile(FAV_FILE) end)
            if ok2 and content then
                local ok3, data = pcall(function() return HttpService:JSONDecode(content) end)
                if ok3 and type(data) == "table" then
                    favorites = data
                end
            end
        end
    end
end

local function saveFavorites()
    if writefile then
        pcall(function()
            writefile(FAV_FILE, HttpService:JSONEncode(favorites))
        end)
    end
end

loadFavorites()

-- ============ SCREEN GUI ============
local gui = Instance.new("ScreenGui")
gui.Name = "CatHubGUI"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = playerGui

-- ============ MAIN WINDOW ============
local main = Instance.new("Frame")
main.Name = "Main"
main.Size = UDim2.fromOffset(560, 380)
main.Position = UDim2.new(0.5, -280, 0.5, -190)
main.BackgroundColor3 = COL_BG
main.BorderSizePixel = 0
main.Active = true
main.Parent = gui

local uiScale = Instance.new("UIScale")
local vp = workspace.CurrentCamera.ViewportSize
uiScale.Scale = math.min(1, (vp.X - 20) / 560, (vp.Y - 20) / 380)
uiScale.Parent = main

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 12)
mainCorner.Parent = main

local mainStroke = Instance.new("UIStroke")
mainStroke.Color = COL_GLOW
mainStroke.Thickness = 1.5
mainStroke.Transparency = 0.2
mainStroke.Parent = main

task.spawn(function()
    while main.Parent do
        local t1 = TweenService:Create(mainStroke,
            TweenInfo.new(1.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
            { Transparency = 0.55, Thickness = 2.5 })
        t1:Play(); t1.Completed:Wait()
        local t2 = TweenService:Create(mainStroke,
            TweenInfo.new(1.2, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
            { Transparency = 0.2, Thickness = 1.5 })
        t2:Play(); t2.Completed:Wait()
    end
end)

-- ============ HEADER ============
local header = Instance.new("Frame")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 55)
header.BackgroundColor3 = COL_PANEL
header.BorderSizePixel = 0
header.Parent = main

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 12)
headerCorner.Parent = header

-- Cat circle
local catCircle = Instance.new("Frame")
catCircle.Size = UDim2.fromOffset(42, 42)
catCircle.Position = UDim2.fromOffset(12, 7)
catCircle.BackgroundColor3 = COL_ACCENT
catCircle.BorderSizePixel = 0
catCircle.Parent = header

local catCorner = Instance.new("UICorner")
catCorner.CornerRadius = UDim.new(1, 0)
catCorner.Parent = catCircle

local catStroke = Instance.new("UIStroke")
catStroke.Color = COL_GLOW
catStroke.Thickness = 1.5
catStroke.Parent = catCircle

local catImage = Instance.new("ImageLabel")
catImage.Size = UDim2.new(1, -6, 1, -6)
catImage.Position = UDim2.fromOffset(3, 3)
catImage.BackgroundTransparency = 1
catImage.Image = "rbxthumb://type=Asset&id="..CAT_IMAGE_ID.."&w=420&h=420"
catImage.ScaleType = Enum.ScaleType.Crop
catImage.Parent = catCircle

local catImageCorner = Instance.new("UICorner")
catImageCorner.CornerRadius = UDim.new(1, 0)
catImageCorner.Parent = catImage

-- Title
local title = Instance.new("TextLabel")
title.BackgroundTransparency = 1
title.Position = UDim2.fromOffset(64, 6)
title.Size = UDim2.new(0.5, 0, 0, 20)
title.Font = Enum.Font.GothamBold
title.TextSize = 16
title.TextColor3 = COL_TEXT
title.TextXAlignment = Enum.TextXAlignment.Left
title.Text = "cat hub"
title.Parent = header

local subtitle = Instance.new("TextLabel")
subtitle.BackgroundTransparency = 1
subtitle.Position = UDim2.fromOffset(64, 26)
subtitle.Size = UDim2.new(0.5, 0, 0, 16)
subtitle.Font = Enum.Font.Gotham
subtitle.TextSize = 10
subtitle.TextColor3 = COL_SUBTEXT
subtitle.TextXAlignment = Enum.TextXAlignment.Left
subtitle.Text = "universal"
subtitle.Parent = header

-- Search bar (top right)
local searchFrame = Instance.new("Frame")
searchFrame.Name = "SearchFrame"
searchFrame.Size = UDim2.fromOffset(140, 28)
searchFrame.Position = UDim2.new(1, -250, 0, 13)
searchFrame.BackgroundColor3 = COL_CARD
searchFrame.BorderSizePixel = 0
searchFrame.Parent = header

local searchCorner = Instance.new("UICorner")
searchCorner.CornerRadius = UDim.new(0, 6)
searchCorner.Parent = searchFrame

local searchBox = Instance.new("TextBox")
searchBox.Size = UDim2.new(1, -12, 1, 0)
searchBox.Position = UDim2.fromOffset(6, 0)
searchBox.BackgroundTransparency = 1
searchBox.Font = Enum.Font.Gotham
searchBox.TextSize = 10
searchBox.TextColor3 = COL_TEXT
searchBox.PlaceholderText = "Search scripts..."
searchBox.PlaceholderColor3 = COL_MUTED
searchBox.Text = ""
searchBox.TextXAlignment = Enum.TextXAlignment.Left
searchBox.ClearTextOnFocus = false
searchBox.Parent = searchFrame

-- Minimize
local minimizeBtn = Instance.new("TextButton")
minimizeBtn.Size = UDim2.fromOffset(28, 28)
minimizeBtn.Position = UDim2.new(1, -74, 0, 13)
minimizeBtn.BackgroundTransparency = 1
minimizeBtn.Text = "-"
minimizeBtn.Font = Enum.Font.GothamBold
minimizeBtn.TextSize = 18
minimizeBtn.TextColor3 = COL_TEXT
minimizeBtn.AutoButtonColor = false
minimizeBtn.Parent = header

-- Close
local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.fromOffset(28, 28)
closeBtn.Position = UDim2.new(1, -38, 0, 13)
closeBtn.BackgroundTransparency = 1
closeBtn.Text = "X"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 14
closeBtn.TextColor3 = COL_TEXT
closeBtn.AutoButtonColor = false
closeBtn.Parent = header

-- ============ SIDEBAR ============
local sidebar = Instance.new("Frame")
sidebar.Name = "Sidebar"
sidebar.Size = UDim2.new(0, 130, 1, -71)
sidebar.Position = UDim2.fromOffset(8, 63)
sidebar.BackgroundColor3 = COL_SIDEBAR
sidebar.BorderSizePixel = 0
sidebar.Parent = main

local sidebarCorner = Instance.new("UICorner")
sidebarCorner.CornerRadius = UDim.new(0, 10)
sidebarCorner.Parent = sidebar

local sidebarList = Instance.new("Frame")
sidebarList.Size = UDim2.new(1, 0, 0, 240)
sidebarList.BackgroundTransparency = 1
sidebarList.Parent = sidebar

local sidebarLayout = Instance.new("UIListLayout")
sidebarLayout.Padding = UDim.new(0, 4)
sidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
sidebarLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
sidebarLayout.Parent = sidebarList

local sidebarPad = Instance.new("UIPadding")
sidebarPad.PaddingTop = UDim.new(0, 8)
sidebarPad.Parent = sidebarList

local function makeNavButton(text, order)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -12, 0, 30)
    btn.BackgroundColor3 = COL_CARD
    btn.BackgroundTransparency = 1
    btn.Text = text
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 10
    btn.TextColor3 = COL_SUBTEXT
    btn.AutoButtonColor = false
    btn.LayoutOrder = order
    btn.Parent = sidebarList

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = btn

    return btn
end

local homeBtn     = makeNavButton("Home", 1)
local scriptBtn   = makeNavButton("Script", 2)
local serverBtn   = makeNavButton("Server", 3)
local settingsBtn = makeNavButton("Settings", 4)
local creditBtn   = makeNavButton("Credit", 5)
local aboutBtn    = makeNavButton("About", 6)

homeBtn.BackgroundTransparency = 0
homeBtn.BackgroundColor3 = COL_ACCENT
homeBtn.TextColor3 = COL_TEXT

-- ============ PROFILE CARD (bottom of sidebar) ============
local profileCard = Instance.new("Frame")
profileCard.Size = UDim2.new(1, -12, 0, 100)
profileCard.Position = UDim2.new(0, 6, 1, -106)
profileCard.BackgroundColor3 = COL_CARD
profileCard.BorderSizePixel = 0
profileCard.Parent = sidebar

local profileCorner = Instance.new("UICorner")
profileCorner.CornerRadius = UDim.new(0, 8)
profileCorner.Parent = profileCard

local avatar = Instance.new("ImageLabel")
avatar.Size = UDim2.fromOffset(32, 32)
avatar.Position = UDim2.fromOffset(8, 8)
avatar.BackgroundColor3 = COL_ACCENT
avatar.BorderSizePixel = 0
avatar.Parent = profileCard

local avatarCorner = Instance.new("UICorner")
avatarCorner.CornerRadius = UDim.new(1, 0)
avatarCorner.Parent = avatar

pcall(function()
    avatar.Image = Players:GetUserThumbnailAsync(
        localPlayer.UserId,
        Enum.ThumbnailType.HeadShot,
        Enum.ThumbnailSize.Size100x100
    )
end)

local userName = Instance.new("TextLabel")
userName.BackgroundTransparency = 1
userName.Position = UDim2.fromOffset(46, 8)
userName.Size = UDim2.new(1, -52, 0, 14)
userName.Font = Enum.Font.GothamBold
userName.TextSize = 10
userName.TextColor3 = COL_TEXT
userName.TextXAlignment = Enum.TextXAlignment.Left
userName.TextTruncate = Enum.TextTruncate.AtEnd
userName.Text = localPlayer.Name
userName.Parent = profileCard

local userHandle = Instance.new("TextLabel")
userHandle.BackgroundTransparency = 1
userHandle.Position = UDim2.fromOffset(46, 22)
userHandle.Size = UDim2.new(1, -52, 0, 12)
userHandle.Font = Enum.Font.Gotham
userHandle.TextSize = 9
userHandle.TextColor3 = COL_SUBTEXT
userHandle.TextXAlignment = Enum.TextXAlignment.Left
userHandle.TextTruncate = Enum.TextTruncate.AtEnd
userHandle.Text = "@"..localPlayer.Name
userHandle.Parent = profileCard

local discordBtn = Instance.new("TextButton")
discordBtn.Size = UDim2.new(1, -16, 0, 34)
discordBtn.Position = UDim2.new(0, 8, 1, -42)
discordBtn.BackgroundColor3 = Color3.fromRGB(88, 101, 242)
discordBtn.Text = ""
discordBtn.AutoButtonColor = false
discordBtn.BorderSizePixel = 0
discordBtn.Parent = profileCard

local dcCorner = Instance.new("UICorner")
dcCorner.CornerRadius = UDim.new(0, 6)
dcCorner.Parent = discordBtn

local dcIcon = Instance.new("ImageLabel")
dcIcon.Size = UDim2.fromOffset(20, 20)
dcIcon.Position = UDim2.fromOffset(6, 7)
dcIcon.BackgroundTransparency = 1
dcIcon.Image = "rbxthumb://type=Asset&id="..DC_IMAGE_ID.."&w=420&h=420"
dcIcon.Parent = discordBtn

local dcText = Instance.new("TextLabel")
dcText.BackgroundTransparency = 1
dcText.Position = UDim2.fromOffset(30, 0)
dcText.Size = UDim2.new(1, -36, 1, 0)
dcText.Font = Enum.Font.GothamBold
dcText.TextSize = 9
dcText.TextColor3 = COL_TEXT
dcText.TextXAlignment = Enum.TextXAlignment.Left
dcText.TextTruncate = Enum.TextTruncate.AtEnd
dcText.Text = "Join"
dcText.Parent = discordBtn

-- ============ CONTENT AREA ============
local content = Instance.new("Frame")
content.Size = UDim2.new(1, -146, 1, -71)
content.Position = UDim2.fromOffset(138, 63)
content.BackgroundTransparency = 1
content.Parent = main

-- ============ HOME PAGE ============
local homePage = Instance.new("Frame")
homePage.Size = UDim2.fromScale(1, 1)
homePage.BackgroundTransparency = 1
homePage.Visible = true
homePage.Parent = content

-- Welcome panel
local welcomePanel = Instance.new("Frame")
welcomePanel.Size = UDim2.new(1, 0, 0, 70)
welcomePanel.Position = UDim2.fromOffset(0, 0)
welcomePanel.BackgroundColor3 = COL_PANEL
welcomePanel.BorderSizePixel = 0
welcomePanel.Parent = homePage

local wpCorner = Instance.new("UICorner")
wpCorner.CornerRadius = UDim.new(0, 8)
wpCorner.Parent = welcomePanel

local wpTitle = Instance.new("TextLabel")
wpTitle.BackgroundTransparency = 1
wpTitle.Position = UDim2.fromOffset(12, 8)
wpTitle.Size = UDim2.new(1, -24, 0, 18)
wpTitle.Font = Enum.Font.GothamBold
wpTitle.TextSize = 12
wpTitle.TextColor3 = COL_TEXT
wpTitle.TextXAlignment = Enum.TextXAlignment.Left
wpTitle.Text = "Hello, "..localPlayer.Name.."!"
wpTitle.Parent = welcomePanel

local wpLine = Instance.new("TextLabel")
wpLine.BackgroundTransparency = 1
wpLine.Position = UDim2.fromOffset(12, 28)
wpLine.Size = UDim2.new(1, -24, 0, 14)
wpLine.Font = Enum.Font.Gotham
wpLine.TextSize = 10
wpLine.TextColor3 = COL_SUBTEXT
wpLine.TextXAlignment = Enum.TextXAlignment.Left
wpLine.Text = "Thanks for using cat hub."
wpLine.Parent = welcomePanel

local wpLine2 = Instance.new("TextLabel")
wpLine2.BackgroundTransparency = 1
wpLine2.Position = UDim2.fromOffset(12, 44)
wpLine2.Size = UDim2.new(1, -24, 0, 14)
wpLine2.Font = Enum.Font.Gotham
wpLine2.TextSize = 10
wpLine2.TextColor3 = COL_SUBTEXT
wpLine2.TextXAlignment = Enum.TextXAlignment.Left
wpLine2.Text = "Enjoy the scripts!"
wpLine2.Parent = welcomePanel

-- Current Game panel
local gamePanel = Instance.new("Frame")
gamePanel.Size = UDim2.new(1, 0, 0, 100)
gamePanel.Position = UDim2.fromOffset(0, 78)
gamePanel.BackgroundColor3 = COL_PANEL
gamePanel.BorderSizePixel = 0
gamePanel.Parent = homePage

local gpCorner = Instance.new("UICorner")
gpCorner.CornerRadius = UDim.new(0, 8)
gpCorner.Parent = gamePanel

local gpHeader = Instance.new("TextLabel")
gpHeader.BackgroundTransparency = 1
gpHeader.Position = UDim2.fromOffset(12, 6)
gpHeader.Size = UDim2.new(1, -24, 0, 16)
gpHeader.Font = Enum.Font.GothamBold
gpHeader.TextSize = 10
gpHeader.TextColor3 = COL_GLOW
gpHeader.TextXAlignment = Enum.TextXAlignment.Left
gpHeader.Text = "CURRENT GAME"
gpHeader.Parent = gamePanel

local gpGame = Instance.new("TextLabel")
gpGame.BackgroundTransparency = 1
gpGame.Position = UDim2.fromOffset(12, 26)
gpGame.Size = UDim2.new(1, -24, 0, 18)
gpGame.Font = Enum.Font.GothamBold
gpGame.TextSize = 13
gpGame.TextColor3 = COL_TEXT
gpGame.TextXAlignment = Enum.TextXAlignment.Left
gpGame.Text = "Loading..."
gpGame.Parent = gamePanel

local gpOnline = Instance.new("TextLabel")
gpOnline.BackgroundTransparency = 1
gpOnline.Position = UDim2.fromOffset(12, 48)
gpOnline.Size = UDim2.new(1, -24, 0, 14)
gpOnline.Font = Enum.Font.Gotham
gpOnline.TextSize = 10
gpOnline.TextColor3 = COL_SUBTEXT
gpOnline.TextXAlignment = Enum.TextXAlignment.Left
gpOnline.Text = "Players online: --"
gpOnline.Parent = gamePanel

local gpServer = Instance.new("TextLabel")
gpServer.BackgroundTransparency = 1
gpServer.Position = UDim2.fromOffset(12, 62)
gpServer.Size = UDim2.new(1, -24, 0, 14)
gpServer.Font = Enum.Font.Gotham
gpServer.TextSize = 10
gpServer.TextColor3 = COL_SUBTEXT
gpServer.TextXAlignment = Enum.TextXAlignment.Left
gpServer.Text = "Current server: -- players"
gpServer.Parent = gamePanel

local gpStatus = Instance.new("TextLabel")
gpStatus.BackgroundTransparency = 1
gpStatus.Position = UDim2.fromOffset(12, 78)
gpStatus.Size = UDim2.new(1, -24, 0, 14)
gpStatus.Font = Enum.Font.GothamBold
gpStatus.TextSize = 10
gpStatus.TextColor3 = COL_GREEN
gpStatus.TextXAlignment = Enum.TextXAlignment.Left
gpStatus.Text = "Status: Supported"
gpStatus.Parent = gamePanel

-- Favorites panel
local favPanel = Instance.new("Frame")
favPanel.Size = UDim2.new(1, 0, 0, 110)
favPanel.Position = UDim2.fromOffset(0, 186)
favPanel.BackgroundColor3 = COL_PANEL
favPanel.BorderSizePixel = 0
favPanel.Parent = homePage

local fpCorner = Instance.new("UICorner")
fpCorner.CornerRadius = UDim.new(0, 8)
fpCorner.Parent = favPanel

local fpHeader = Instance.new("TextLabel")
fpHeader.BackgroundTransparency = 1
fpHeader.Position = UDim2.fromOffset(12, 6)
fpHeader.Size = UDim2.new(1, -24, 0, 16)
fpHeader.Font = Enum.Font.GothamBold
fpHeader.TextSize = 10
fpHeader.TextColor3 = COL_GLOW
fpHeader.TextXAlignment = Enum.TextXAlignment.Left
fpHeader.Text = "FAVORITES"
fpHeader.Parent = favPanel

local favListFrame = Instance.new("Frame")
favListFrame.Size = UDim2.new(1, 0, 1, -26)
favListFrame.Position = UDim2.fromOffset(0, 26)
favListFrame.BackgroundTransparency = 1
favListFrame.Parent = favPanel

local favListLayout = Instance.new("UIListLayout")
favListLayout.Padding = UDim.new(0, 4)
favListLayout.Parent = favListFrame

local favPad = Instance.new("UIPadding")
favPad.PaddingLeft = UDim.new(0, 12)
favPad.PaddingRight = UDim.new(0, 12)
favPad.Parent = favListFrame

local favEmpty = Instance.new("TextLabel")
favEmpty.BackgroundTransparency = 1
favEmpty.Position = UDim2.fromOffset(12, 30)
favEmpty.Size = UDim2.new(1, -24, 0, 20)
favEmpty.Font = Enum.Font.Gotham
favEmpty.TextSize = 9
favEmpty.TextColor3 = COL_MUTED
favEmpty.TextXAlignment = Enum.TextXAlignment.Left
favEmpty.Text = "Star scripts to add them here."
favEmpty.Parent = favPanel

-- Favorites refresh function
local favRunFunctions = {}  -- filled later sa script page

local function refreshFavorites()
    -- clear existing rows
    for _, child in ipairs(favListFrame:GetChildren()) do
        if child:IsA("Frame") then child:Destroy() end
    end

    if #favorites == 0 then
        favEmpty.Visible = true
        return
    end
    favEmpty.Visible = false

    for _, name in ipairs(favorites) do
        local row = Instance.new("Frame")
        row.Size = UDim2.new(1, -4, 0, 28)
        row.BackgroundColor3 = COL_CARD
        row.BorderSizePixel = 0
        row.Parent = favListFrame

        local rCorner = Instance.new("UICorner")
        rCorner.CornerRadius = UDim.new(0, 6)
        rCorner.Parent = row

        local label = Instance.new("TextLabel")
        label.BackgroundTransparency = 1
        label.Position = UDim2.fromOffset(10, 0)
        label.Size = UDim2.new(1, -110, 1, 0)
        label.Font = Enum.Font.GothamBold
        label.TextSize = 10
        label.TextColor3 = COL_TEXT
        label.TextXAlignment = Enum.TextXAlignment.Left
        label.Text = name
        label.Parent = row

        -- Star (remove)
        local starBtn = Instance.new("TextButton")
        starBtn.Size = UDim2.fromOffset(28, 22)
        starBtn.Position = UDim2.new(1, -94, 0.5, -11)
        starBtn.BackgroundColor3 = COL_BG
        starBtn.Text = "★"
        starBtn.Font = Enum.Font.GothamBold
        starBtn.TextSize = 13
        starBtn.TextColor3 = COL_STAR
        starBtn.AutoButtonColor = false
        starBtn.BorderSizePixel = 0
        starBtn.Parent = row

        local sbCorner = Instance.new("UICorner")
        sbCorner.CornerRadius = UDim.new(0, 5)
        sbCorner.Parent = starBtn

        -- Run
        local runBtn = Instance.new("TextButton")
        runBtn.Size = UDim2.fromOffset(56, 22)
        runBtn.Position = UDim2.new(1, -64, 0.5, -11)
        runBtn.BackgroundColor3 = COL_ACCENT
        runBtn.Text = "RUN"
        runBtn.Font = Enum.Font.GothamBold
        runBtn.TextSize = 9
        runBtn.TextColor3 = COL_TEXT
        runBtn.AutoButtonColor = false
        runBtn.BorderSizePixel = 0
        runBtn.Parent = row

        local rbCorner = Instance.new("UICorner")
        rbCorner.CornerRadius = UDim.new(0, 5)
        rbCorner.Parent = runBtn

        starBtn.MouseButton1Click:Connect(function()
            for i, n in ipairs(favorites) do
                if n == name then
                    table.remove(favorites, i)
                    break
                end
            end
            saveFavorites()
            refreshFavorites()
            if _G.CatHubRefreshStars then _G.CatHubRefreshStars() end
        end)

        runBtn.MouseButton1Click:Connect(function()
            if favRunFunctions[name] then
                task.spawn(favRunFunctions[name])
            end
        end)
    end
end

-- ============ LIVE: TOTAL PLAYERS ONLINE ============
task.spawn(function()
    while gui.Parent do
        pcall(function()
            local url = "https://games.roblox.com/v1/games?universeIds="..tostring(game.GameId)
            local res = game:HttpGet(url)
            local data = HttpService:JSONDecode(res)
            if data.data and data.data[1] then
                local playing = data.data[1].playing
                gpOnline.Text = "Players online: "..tostring(playing)
                gpGame.Text = data.data[1].name or "Unknown Game"
            end
        end)
        task.wait(30)
    end
end)

-- ============ LIVE: CURRENT SERVER PLAYERS ============
local function updateServerCount()
    local count = #Players:GetPlayers()
    gpServer.Text = "Current server: "..count.." players"
end

Players.PlayerAdded:Connect(updateServerCount)
Players.PlayerRemoving:Connect(updateServerCount)
updateServerCount()

refreshFavorites()

-- ============ SCRIPT PAGE ============
local scriptPage = Instance.new("Frame")
scriptPage.Size = UDim2.fromScale(1, 1)
scriptPage.BackgroundTransparency = 1
scriptPage.Visible = false
scriptPage.Parent = content

-- View 1: game list
local gameListView = Instance.new("Frame")
gameListView.Size = UDim2.fromScale(1, 1)
gameListView.BackgroundTransparency = 1
gameListView.Visible = true
gameListView.Parent = scriptPage

local glTitle = Instance.new("TextLabel")
glTitle.BackgroundTransparency = 1
glTitle.Position = UDim2.fromOffset(0, 0)
glTitle.Size = UDim2.new(1, 0, 0, 22)
glTitle.Font = Enum.Font.GothamBold
glTitle.TextSize = 14
glTitle.TextColor3 = COL_TEXT
glTitle.TextXAlignment = Enum.TextXAlignment.Left
glTitle.Text = "Script"
glTitle.Parent = gameListView

local glLayout = Instance.new("UIListLayout")
glLayout.Padding = UDim.new(0, 6)
glLayout.SortOrder = Enum.SortOrder.LayoutOrder
glLayout.Parent = gameListView

local glPad = Instance.new("UIPadding")
glPad.PaddingTop = UDim.new(0, 30)
glPad.Parent = gameListView

local function makeGameBtn(name, order)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -4, 0, 38)
    btn.BackgroundColor3 = COL_PANEL
    btn.Text = "  "..name
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 11
    btn.TextColor3 = COL_TEXT
    btn.TextXAlignment = Enum.TextXAlignment.Left
    btn.AutoButtonColor = false
    btn.BorderSizePixel = 0
    btn.LayoutOrder = order
    btn.Parent = gameListView

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 8)
    corner.Parent = btn

    return btn
end

local stealBtn  = makeGameBtn("Steal an Egg", 1)
local bloxBtn   = makeGameBtn("Blox Fruits", 2)
local petBtn    = makeGameBtn("Pet Simulator 99", 3)
local bladeBtn  = makeGameBtn("Blade Ball", 4)

-- View 2: Steal an Egg view
local scriptDetailView = Instance.new("Frame")
scriptDetailView.Size = UDim2.fromScale(1, 1)
scriptDetailView.BackgroundTransparency = 1
scriptDetailView.Visible = false
scriptDetailView.Parent = scriptPage

local backBtn = Instance.new("TextButton")
backBtn.Size = UDim2.fromOffset(60, 24)
backBtn.Position = UDim2.fromOffset(0, 0)
backBtn.BackgroundColor3 = COL_CARD
backBtn.Text = "< Back"
backBtn.Font = Enum.Font.GothamBold
backBtn.TextSize = 10
backBtn.TextColor3 = COL_TEXT
backBtn.AutoButtonColor = false
backBtn.BorderSizePixel = 0
backBtn.Parent = scriptDetailView

local backCorner = Instance.new("UICorner")
backCorner.CornerRadius = UDim.new(0, 6)
backCorner.Parent = backBtn

local sdTitle = Instance.new("TextLabel")
sdTitle.BackgroundTransparency = 1
sdTitle.Position = UDim2.fromOffset(70, 0)
sdTitle.Size = UDim2.new(1, -70, 0, 24)
sdTitle.Font = Enum.Font.GothamBold
sdTitle.TextSize = 12
sdTitle.TextColor3 = COL_TEXT
sdTitle.TextXAlignment = Enum.TextXAlignment.Left
sdTitle.Text = "Steal an Egg"
sdTitle.Parent = scriptDetailView

-- Search (only in this view)
local detailSearch = Instance.new("Frame")
detailSearch.Size = UDim2.new(1, 0, 0, 26)
detailSearch.Position = UDim2.fromOffset(0, 30)
detailSearch.BackgroundColor3 = COL_CARD
detailSearch.BorderSizePixel = 0
detailSearch.Parent = scriptDetailView

local dsCorner = Instance.new("UICorner")
dsCorner.CornerRadius = UDim.new(0, 6)
dsCorner.Parent = detailSearch

local dsBox = Instance.new("TextBox")
dsBox.Size = UDim2.new(1, -12, 1, 0)
dsBox.Position = UDim2.fromOffset(6, 0)
dsBox.BackgroundTransparency = 1
dsBox.Font = Enum.Font.Gotham
dsBox.TextSize = 10
dsBox.TextColor3 = COL_TEXT
dsBox.PlaceholderText = "Search scripts..."
dsBox.PlaceholderColor3 = COL_MUTED
dsBox.Text = ""
dsBox.TextXAlignment = Enum.TextXAlignment.Left
dsBox.ClearTextOnFocus = false
dsBox.Parent = detailSearch

-- Tabs
local tabHolder = Instance.new("Frame")
tabHolder.Size = UDim2.new(1, 0, 0, 26)
tabHolder.Position = UDim2.fromOffset(0, 62)
tabHolder.BackgroundTransparency = 1
tabHolder.Parent = scriptDetailView

local function makeTab(text, x, w)
    local b = Instance.new("TextButton")
    b.Size = UDim2.fromOffset(w, 26)
    b.Position = UDim2.fromOffset(x, 0)
    b.BackgroundColor3 = COL_CARD
    b.Text = text
    b.Font = Enum.Font.GothamBold
    b.TextSize = 9
    b.TextColor3 = COL_TEXT
    b.AutoButtonColor = false
    b.BorderSizePixel = 0
    b.Parent = tabHolder

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 6)
    c.Parent = b
    return b
end

local tabKey      = makeTab("KEY", 0, 70)
local tabKeyless  = makeTab("KEYLESS", 74, 70)
local tabVisuals  = makeTab("VISUALS", 148, 70)

tabKey.BackgroundColor3 = COL_ACCENT

-- Script list
local scriptList = Instance.new("ScrollingFrame")
scriptList.Size = UDim2.new(1, 0, 1, -92)
scriptList.Position = UDim2.fromOffset(0, 92)
scriptList.BackgroundTransparency = 1
scriptList.BorderSizePixel = 0
scriptList.ScrollBarThickness = 3
scriptList.ScrollBarImageColor3 = COL_ACCENT
scriptList.CanvasSize = UDim2.fromOffset(0, 0)
scriptList.AutomaticCanvasSize = Enum.AutomaticSize.Y
scriptList.Parent = scriptDetailView

local slLayout = Instance.new("UIListLayout")
slLayout.Padding = UDim.new(0, 5)
slLayout.Parent = scriptList

-- ============ HUB DATA ============
local KEY_HUBS = {
    {"Clover Hub", "https://cloverhub.app/clover.lua"},
    {"Ajjans Hub", "https://api.luarmor.net/files/v4/loaders/359e97f8618e9008afe5f496184ebb7c.lua"},
    {"Big Foot", "https://raw.githubusercontent.com/hanniii1/Loader/refs/heads/main/BFLoader.lua"},
    {"Speed Hub", "https://raw.githubusercontent.com/AhmadV99/Speed-Hub-X/main/Speed%20Hub%20X.lua"},
    {"Zeroin Hub", "https://zeroinhub.com/api/script"},
    {"Quantumq Onyx", "https://raw.githubusercontent.com/flazhy/QuantumOnyx/refs/heads/main/QuantumOnyx.lua"},
    {"Axonic", "https://raw.githubusercontent.com/Kenniel123/Steal-A-Egg/refs/heads/main/Steal%20A%20Egg"},
    {"Night Hub", "https://raw.githubusercontent.com/WhiteX1208/Scripts/refs/heads/main/StealAnEggs.luau"},
    {"On Hub", "https://raw.githubusercontent.com/davizin713/ONhub/refs/heads/main/script.lua"},
    {"NEOX HUB", "https://raw.githubusercontent.com/hassanxzayn-lua/NEOXHUBMAIN/refs/heads/main/loader"},
    {"RIFT GOHA", "https://raw.githubusercontent.com/Dodoyung24/script-core/main/Steal-An-Egg"},
    {"ATHER HUB", "https://api.luarmor.net/files/v3/loaders/2529a5f9dfddd5523ca4e22f21cceffa.lua"},
    {"VANITY HUB", "https://vanityscript.xyz/loader"},
    {"RONIX HUB", "https://api.luarmor.net/files/v3/loaders/fda9babd071d6b536a745774b6bc681c.lua"},
    {"UNREXL", "https://raw.githubusercontent.com/unrexl/Scripts/refs/heads/main/StealaEgg"},
    {"WADIDIS HUB", "https://api.jnkie.com/api/v1/luascripts/public/809c81e15814d1c016f44d9fe56587f5f38c55a97f203f11bc1a3f7cc3725c5f/download"},
    {"H4XSCRIPTS", "https://raw.githubusercontent.com/H4xScripts/Loader/refs/heads/main/loader.lua"},
    {"THAN HUB", "https://api.luarmor.net/files/v4/loaders/d1c82862a093e64c6bd82bb6d6f7a46b.lua"},
    {"YANTO HUB", "https://raw.githubusercontent.com/YantoRoblox/Script-Free-YantoHUB/refs/heads/main/YantoHUB"},
    {"CHIYO HUB", "https://raw.githubusercontent.com/kaisenlmao/loader/refs/heads/main/chiyo.lua"},
    {"OMG HUB", "https://raw.githubusercontent.com/Omgshit/Scripts/main/MainLoader.lua"},
    {"UNKNOWN HUB", "https://unknownhub.win/api/projects/54474b4c5d5a4f459909c4cb70e7b4f3/loader"},
    {"AIRFLOW", "https://airflowscript.com/loader"},
    {"SOLIX HUB", "https://raw.githubusercontent.com/bao8jl/solixhub/main/loader"},
    {"ZERO IMPACT", "https://www.zeroimpact.online/raw/loader"},
    {"SNOWY HUB", "https://flowauth.net/v1/ui/a87f00d9adf63658655fcd02ab86a4ef.lua"},
    {"NEMESIS HUB", "https://raw.githubusercontent.com/x2zu/loader/main/freeloader.lua"},
    {"ZHENN SPAWNER", "https://raw.githubusercontent.com/ZhennHub/PetSpawner/refs/heads/main/lua"},
    {"KEXXE HUB", "https://raw.githubusercontent.com/premiumbuddy/kex/refs/heads/main/kexxxx"},
    {"NOVA HUB", "https://raw.githubusercontent.com/NovaHubRBLX/NovaHub/refs/heads/main/novahub.lua"},
    {"SPORTSCLUB HUB", "https://loader.sportsclub.fun/loader.luau"},
    {"SCRIPTVERSE HUB", "https://scriptversekey.xyz/s/steal-an-egg"},
    {"GS HUB", "https://gist.githubusercontent.com/spiritualgaming1123-beep/46ef55c5f8284e076aafc5ebd12233f4/raw/5b24749c3931c1838a76e64c9af508dcdd03700a/gistfile1.lua"},
    {"PROBEST", "https://api.jnkie.com/api/v1/luascripts/public/0199b576f5c2d5a34159f0f9f4e1de0a566b4d1da5b1cfa5d2f71ade9bdcaa24/download"},
    {"SAIOPS HUB", "https://api.saiops.cc/scripts/Steal-An-Egg-Script.lua"},
    {"NEVERLOSE", "https://raw.githubusercontent.com/inrate1337/NeverloseLoaderRoblox/refs/heads/main/main.luau"},
    {"CRYSTALIZED HUB", "https://api.jnkie.com/api/v1/luascripts/public/a62237c6a75399adc9add4151ebeeb91c1f965fab665a650dcbc699a5622b37f/download"},
    {"OCTOPUS HUB", "https://www.octopushub.xyz/loader"},
    {"JINHUB", "https://jinhub.my.id/scripts/Universal.lua"},
    {"OVERFLOW", "https://overflow.cx/loader.lua"},
    {"SOLVEXGUI", "https://raw.githubusercontent.com/Solvexxxx/Scripts/refs/heads/main/SolvexGUI_SAE.lua"},
    {"SAKURA HUB", "https://flowauth.net/v1/ui/d00ec69382de97372fc9559efc722298.lua"},
    {"FORGE HUB", "https://cdn.forgehub.store/loader"},
    {"BASEMENT HUB", "https://thebsmt.xyz/BSMT"},
    {"KALI HUB", "https://kalihub.xyz/loader.lua"},
    {"CORE HUB", "https://getcore.lol/loader.lua"},
    {"APEL HUB", "https://apelhub.com/loader.lua"},
    {"PANDA HUB", "https://raw.githubusercontent.com/Muhammad6196/Project-Infinity-X/refs/heads/main/main.lua"},
    {"FISHY", "https://jnkie.com/loaders/fishyhub"},
    {"VIVID LUA", "https://vivid.vividhub.workers.dev/loader.lua"},
    {"REZZY HUB", "https://raw.githubusercontent.com/Roman666Cabj/Nether/refs/heads/main/RezzyStealAnEgg.lua"},
    {"ZNEX HUB", "https://api.jnkie.com/api/v1/luascripts/public/181cfe2bd5df35ce78607b5ffb37c6666abd76eda11ff33b0f24a1b2d8ee935f/download"},
    {"ASVARA HUB", "https://raw.githubusercontent.com/asvraRoblox/stealegg/refs/heads/main/main"},
    {"SHADOW HUB", "https://pastebin.com/raw/QAvDbBKa"},
    {"KING VYPER", "https://kingvypers.site/raw/TrialLoader"},
    {"HIP HUB", "https://hiphub.cloud/api/script-roblox/loader"},
    {"POTATO HUB", "https://raw.githubusercontent.com/potatohub67/potatoscripts/refs/heads/main/stealaegg.lua"},
}

local KEYLESS_HUBS = {
    {"Bypass Speed", "https://rawscripts.net/raw/Steal-An-Egg-bypass-anti-cheat-224212"},
    {"Nasi Rendang", "https://www.nrlscript.com/raw/y9BUU6LkVW"},
    {"Miranda Hub", "https://api.luarmor.net/files/v4/loaders/7891557d7950ed56a7d1d8f57b66ad4d.lua"},
    {"Lennon Hub", "https://raw.githubusercontent.com/lennonxscripts/lennonhubv4/refs/heads/main/stealanegg"},
    {"Foxname", "https://raw.githubusercontent.com/caomod2077/Script/refs/heads/main/Fn-stealanegg.lua"},
    {"Mcrzhub", "https://flowauth.net/v1/loaders/3c4e87ed34813171b0f8d53a108a7d88.lua"},
    {"VXEZES", "https://vxezestudio.online/api/scripts/script_G5CGjqj2X3rOS/stream/init"},
    {"Anti Guard", "https://api.getpolsec.com/scripts/hosted/6582551b42d21c6b7eb55f1d76d8d50ce53cb35592093d6615b5e83437594dc0.lua"},
    {"Lkz", "https://api.luarmor.net/files/v4/loaders/65bf3459d87ba3ac46350e154b640929.lua"},
    {"Decode", "https://raw.githubusercontent.com/ItzYumi/Decode/refs/heads/main/DE%3ACODE.lua"},
    {"Blxyo Hub", "https://flowauth.net/v1/loaders/69d3463240384f3a73fbe32c178093a2.lua"},
    {"Hoshi Hub", "https://hoshihub.site/loader.lua"},
    {"Sena Hub", "https://senahub.xyz/raw/loader"},
    {"Vincetore", "https://raw.githubusercontent.com/idk953072-crypto/Steal-an-Egg/refs/heads/main/vincitore"},
    {"Chilli Hub", "https://raw.githubusercontent.com/tienkhanh1/spicy/main/Chilli.lua"},
    {"Tsuo", "https://raw.githubusercontent.com/Tsuo7/TsuoHub/main/stealanegg"},
    {"Ouroboros", "https://raw.githubusercontent.com/joustingmatch/Ouroboros/main/loader.lua"},
    {"VOIDHUB", "https://voidon.top/api/loader/main"},
    {"LIMBO HUB", "https://limbohub.my.id/loader.lua"},
    {"OXIDE HUB", "https://raw.githubusercontent.com/xulfo/Oxide-Loader/main/Main.lua"},
    {"PULSE HUB", "https://raw.githubusercontent.com/PulseZax/Loader/refs/heads/main/.lua"},
    {"YARHM HUB", "https://yarhm.com"},
    {"MONARCHH", "https://raw.githubusercontent.com/nobuxy/monarch.win/refs/heads/main/Monarch.lua"},
    {"DIVINE EGG", "https://raw.githubusercontent.com/SynergyNetworkz/VULN/refs/heads/main/STEALANEGG.lua"},
    {"TOKINU", "https://raw.githubusercontent.com/Tokinu-Scripts/Steal-An-Egg/refs/heads/main/Instant/Tp"},
    {"NEVA HUB", "https://raw.githubusercontent.com/VEZ2/NEVAHUB/main/2"},
    {"LEVON HUB", "https://pastefy.app/nasHhfko/raw"},
    {"PET SPAWNER", "https://raw.githubusercontent.com/bugxiefun/roblox-scripts/refs/heads/main/rblxscripts-stealanegg-spawner"},
    {"VALINC HUB", "https://api.valincsyndicate.com/v1/releases/5502cba03703f4a3628d522d396b80d8.lua"},
    {"CIAO HUB HOP", "https://pastefy.app/YoZocJ8O/raw"},
    {"RONNEI HUB", "https://raw.githubusercontent.com/elonmod/skibidi/refs/heads/main/Ronneihub-keyless.lua"},
    {"PROJECT-MADARA", "https://raw.githubusercontent.com/IsThisMe01/Project-Madara/refs/heads/main/stealanegg"},
    {"TOOLBOX", "https://raw.githubusercontent.com/Abdullahking20/loader-lua/main/loader"},
    {"CITRA HUB", "https://raw.githubusercontent.com/gilgameshfate59/ohbfoosk8tid/main/CitraLoader.lua"},
    {"VSN", "https://raw.githubusercontent.com/NetNullv1/VSN/refs/heads/main/HUB"},
    {"BK HUB", "https://api.luarmor.net/files/v4/loaders/9ee4edde227ac85f50872bf9e4226508.lua"},
    {"AXURS", "https://raw.githubusercontent.com/XE3Scripts/Axur-sGamesHub/refs/heads/main/StealAnEgg"},
    {"WIS HUB", "https://api.wishub.cloud/files/loader.lua"},
    {"SOFTKILLZ", "https://pastebin.com/raw/ZuEBwb5K"},
}

local VISUAL_HUBS = {
    {"Animation", "https://rawscripts.net/raw/Universal-Script-Free-animations-112111"},
    {"Spawner", "https://raw.githubusercontent.com/bugxiefun/roblox-scripts/refs/heads/main/rblxscripts-stealanegg-spawner"},
    {"Admin Panel", "https://api.jnkie.com/api/v1/luascripts/public/f6851ba0a3fc126430592a97d523d7c05b632f607eefb582f11353b9ef77a38f/download"},
    {"UNIVERS GRAPHICS", "https://raw.githubusercontent.com/Uranus197/-Univers-Hub-Graphics-Script-/refs/heads/main/UniversHub"},
    {"Shader", "https://pastebin.com/raw/Zpaf00Nu"},
    {"Shader1", "https://raw.githubusercontent.com/randomstring0/pshade-ultimate/refs/heads/main/src/cd.lua"},
    {"Avatar Changer", "https://raw.githubusercontent.com/Unknown-ugc/Unknown/refs/heads/main/Avatar%20change"},
    {"Pet Spawner", "https://api.luarmor.net/files/v4/loaders/d8f1c691a58edb11ef782849f80e9b61.lua"},
}

-- ============ SCRIPT BUTTON FACTORY ============
local currentList = {}  -- for search

local function makeScriptRow(name, url)
    local row = Instance.new("Frame")
    row.Name = name
    row.Size = UDim2.new(1, -4, 0, 32)
    row.BackgroundColor3 = COL_PANEL
    row.BorderSizePixel = 0
    row.Parent = scriptList

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = row

    local label = Instance.new("TextLabel")
    label.BackgroundTransparency = 1
    label.Position = UDim2.fromOffset(10, 0)
    label.Size = UDim2.new(1, -110, 1, 0)
    label.Font = Enum.Font.GothamBold
    label.TextSize = 9
    label.TextColor3 = COL_TEXT
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.TextTruncate = Enum.TextTruncate.AtEnd
    label.Text = name
    label.Parent = row

    -- Star
    local star = Instance.new("TextButton")
    star.Size = UDim2.fromOffset(26, 22)
    star.Position = UDim2.new(1, -92, 0.5, -11)
    star.BackgroundColor3 = COL_BG
    star.Text = "★"
    star.Font = Enum.Font.GothamBold
    star.TextSize = 12
    star.AutoButtonColor = false
    star.BorderSizePixel = 0
    star.Parent = row

    local starCorner = Instance.new("UICorner")
    starCorner.CornerRadius = UDim.new(0, 5)
    starCorner.Parent = star

    local isFav = table.find(favorites, name) ~= nil
    star.TextColor3 = isFav and COL_STAR or COL_MUTED

    star.MouseButton1Click:Connect(function()
        local found = table.find(favorites, name)
        if found then
            table.remove(favorites, found)
            star.TextColor3 = COL_MUTED
        else
            table.insert(favorites, name)
            star.TextColor3 = COL_STAR
        end
        saveFavorites()
        refreshFavorites()
    end)

    -- Run
    local run = Instance.new("TextButton")
    run.Size = UDim2.fromOffset(56, 22)
    run.Position = UDim2.new(1, -62, 0.5, -11)
    run.BackgroundColor3 = COL_ACCENT
    run.Text = "RUN"
    run.Font = Enum.Font.GothamBold
    run.TextSize = 9
    run.TextColor3 = COL_TEXT
    run.AutoButtonColor = false
    run.BorderSizePixel = 0
    run.Parent = row

    local runCorner = Instance.new("UICorner")
    runCorner.CornerRadius = UDim.new(0, 5)
    runCorner.Parent = run

    local function runFn()
        pcall(function()
            loadstring(game:HttpGet(url))()
        end)
    end

    run.MouseButton1Click:Connect(function()
        task.spawn(runFn)
    end)

    -- Store for favorites run
    favRunFunctions[name] = runFn

    return row
end

local function clearScriptList()
    for _, c in ipairs(scriptList:GetChildren()) do
        if c:IsA("Frame") then c:Destroy() end
    end
end

local function showList(list)
    clearScriptList()
    currentList = list
    for _, item in ipairs(list) do
        makeScriptRow(item[1], item[2])
    end
end

-- Tab handlers
tabKey.MouseButton1Click:Connect(function()
    tabKey.BackgroundColor3 = COL_ACCENT
    tabKeyless.BackgroundColor3 = COL_CARD
    tabVisuals.BackgroundColor3 = COL_CARD
    showList(KEY_HUBS)
    dsBox.Text = ""
end)

tabKeyless.MouseButton1Click:Connect(function()
    tabKeyless.BackgroundColor3 = COL_ACCENT
    tabKey.BackgroundColor3 = COL_CARD
    tabVisuals.BackgroundColor3 = COL_CARD
    showList(KEYLESS_HUBS)
    dsBox.Text = ""
end)

tabVisuals.MouseButton1Click:Connect(function()
    tabVisuals.BackgroundColor3 = COL_ACCENT
    tabKey.BackgroundColor3 = COL_CARD
    tabKeyless.BackgroundColor3 = COL_CARD
    showList(VISUAL_HUBS)
    dsBox.Text = ""
end)

-- Search filter
dsBox:GetPropertyChangedSignal("Text"):Connect(function()
    local q = string.lower(dsBox.Text or "")
    for _, row in ipairs(scriptList:GetChildren()) do
        if row:IsA("Frame") then
            local nameLower = string.lower(row.Name)
            if q == "" or string.find(nameLower, q, 1, true) then
                row.Visible = true
            else
                row.Visible = false
            end
        end
    end
end)

-- Navigation
stealBtn.MouseButton1Click:Connect(function()
    gameListView.Visible = false
    scriptDetailView.Visible = true
    showList(KEY_HUBS)
end)

backBtn.MouseButton1Click:Connect(function()
    scriptDetailView.Visible = false
    gameListView.Visible = true
end)

-- Placeholder handlers (other games)
bloxBtn.MouseButton1Click:Connect(function() end)
petBtn.MouseButton1Click:Connect(function() end)
bladeBtn.MouseButton1Click:Connect(function() end)

-- ============ SERVER PAGE ============
local serverPage = Instance.new("Frame")
serverPage.Size = UDim2.fromScale(1, 1)
serverPage.BackgroundTransparency = 1
serverPage.Visible = false
serverPage.Parent = content

local srvTitle = Instance.new("TextLabel")
srvTitle.BackgroundTransparency = 1
srvTitle.Position = UDim2.fromOffset(0, 0)
srvTitle.Size = UDim2.new(1, 0, 0, 22)
srvTitle.Font = Enum.Font.GothamBold
srvTitle.TextSize = 14
srvTitle.TextColor3 = COL_TEXT
srvTitle.TextXAlignment = Enum.TextXAlignment.Left
srvTitle.Text = "Server"
srvTitle.Parent = serverPage

local srvLayout = Instance.new("UIListLayout")
srvLayout.Padding = UDim.new(0, 5)
srvLayout.Parent = serverPage

local srvPad = Instance.new("UIPadding")
srvPad.PaddingTop = UDim.new(0, 30)
srvPad.Parent = serverPage

for i = 1, 6 do
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1, -4, 0, 32)
    b.BackgroundColor3 = COL_PANEL
    b.Text = "Server "..i.."  - FULL"
    b.Font = Enum.Font.GothamBold
    b.TextSize = 10
    b.TextColor3 = COL_TEXT
    b.AutoButtonColor = false
    b.BorderSizePixel = 0
    b.LayoutOrder = i
    b.Parent = serverPage

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 6)
    c.Parent = b
end

-- ============ SETTINGS PAGE ============
local settingsPage = Instance.new("Frame")
settingsPage.Size = UDim2.fromScale(1, 1)
settingsPage.BackgroundTransparency = 1
settingsPage.Visible = false
settingsPage.Parent = content

local stTitle = Instance.new("TextLabel")
stTitle.BackgroundTransparency = 1
stTitle.Position = UDim2.fromOffset(0, 0)
stTitle.Size = UDim2.new(1, 0, 0, 22)
stTitle.Font = Enum.Font.GothamBold
stTitle.TextSize = 14
stTitle.TextColor3 = COL_TEXT
stTitle.TextXAlignment = Enum.TextXAlignment.Left
stTitle.Text = "Settings"
stTitle.Parent = settingsPage

local stPlaceholder = Instance.new("TextLabel")
stPlaceholder.BackgroundTransparency = 1
stPlaceholder.Position = UDim2.fromOffset(0, 30)
stPlaceholder.Size = UDim2.new(1, 0, 1, -30)
stPlaceholder.Font = Enum.Font.Gotham
stPlaceholder.TextSize = 11
stPlaceholder.TextColor3 = COL_MUTED
stPlaceholder.TextXAlignment = Enum.TextXAlignment.Left
stPlaceholder.TextYAlignment = Enum.TextYAlignment.Top
stPlaceholder.Text = "Settings will be added here.\n\n• Color change\n• Song ID\n• Transparency slider"
stPlaceholder.Parent = settingsPage

-- ============ CREDIT PAGE ============
local creditPage = Instance.new("Frame")
creditPage.Size = UDim2.fromScale(1, 1)
creditPage.BackgroundTransparency = 1
creditPage.Visible = false
creditPage.Parent = content

local crTitle = Instance.new("TextLabel")
crTitle.BackgroundTransparency = 1
crTitle.Position = UDim2.fromOffset(0, 0)
crTitle.Size = UDim2.new(1, 0, 0, 22)
crTitle.Font = Enum.Font.GothamBold
crTitle.TextSize = 14
crTitle.TextColor3 = COL_TEXT
crTitle.TextXAlignment = Enum.TextXAlignment.Left
crTitle.Text = "Credit"
crTitle.Parent = creditPage

local crThank = Instance.new("TextLabel")
crThank.BackgroundTransparency = 1
crThank.Position = UDim2.fromOffset(0, 30)
crThank.Size = UDim2.new(1, 0, 0, 40)
crThank.Font = Enum.Font.Gotham
crThank.TextSize = 10
crThank.TextColor3 = COL_TEXT
crThank.TextXAlignment = Enum.TextXAlignment.Left
crThank.TextYAlignment = Enum.TextYAlignment.Top
crThank.Text = "THANK YOU\nThank you for using cat hub!"
crThank.Parent = creditPage

local crSpecial = Instance.new("TextLabel")
crSpecial.BackgroundTransparency = 1
crSpecial.Position = UDim2.fromOffset(0, 78)
crSpecial.Size = UDim2.new(1, 0, 0, 16)
crSpecial.Font = Enum.Font.GothamBold
crSpecial.TextSize = 10
crSpecial.TextColor3 = COL_TEXT
crSpecial.TextXAlignment = Enum.TextXAlignment.Left
crSpecial.Text = "SPECIAL THANKS TO"
crSpecial.Parent = creditPage

local tiktokList = {
    {"@official_mneil", "https://www.tiktok.com/@official_mneil"},
    {"@noah_dump5", "https://www.tiktok.com/@noah_dump5"},
    {"@_johnxines", "https://www.tiktok.com/@_johnxines"},
    {"@kenn50921", "https://www.tiktok.com/@kenn50921"},
}

for i, tk in ipairs(tiktokList) do
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -4, 0, 24)
    btn.Position = UDim2.fromOffset(0, 98 + (i - 1) * 28)
    btn.BackgroundColor3 = COL_PANEL
    btn.Text = "  "..tk[1]
    btn.Font = Enum.Font.GothamBold
    btn.TextSize = 9
    btn.TextColor3 = COL_GLOW
    btn.TextXAlignment = Enum.TextXAlignment.Left
    btn.AutoButtonColor = false
    btn.BorderSizePixel = 0
    btn.Parent = creditPage

    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, 5)
    c.Parent = btn

    btn.MouseButton1Click:Connect(function()
        if setclipboard then setclipboard(tk[2]) end
    end)
end

local crOwnerLabel = Instance.new("TextLabel")
crOwnerLabel.BackgroundTransparency = 1
crOwnerLabel.Position = UDim2.fromOffset(0, 220)
crOwnerLabel.Size = UDim2.new(1, 0, 0, 16)
crOwnerLabel.Font = Enum.Font.GothamBold
crOwnerLabel.TextSize = 10
crOwnerLabel.TextColor3 = COL_TEXT
crOwnerLabel.TextXAlignment = Enum.TextXAlignment.Left
crOwnerLabel.Text = "OWNER"
crOwnerLabel.Parent = creditPage

local crOwner = Instance.new("TextLabel")
crOwner.BackgroundTransparency = 1
crOwner.Position = UDim2.fromOffset(0, 240)
crOwner.Size = UDim2.new(1, 0, 0, 20)
crOwner.Font = Enum.Font.GothamBold
crOwner.TextSize = 11
crOwner.TextColor3 = COL_GLOW
crOwner.TextXAlignment = Enum.TextXAlignment.Left
crOwner.Text = "CHRIS"
crOwner.Parent = creditPage

-- ============ ABOUT PAGE ============
local aboutPage = Instance.new("Frame")
aboutPage.Size = UDim2.fromScale(1, 1)
aboutPage.BackgroundTransparency = 1
aboutPage.Visible = false
aboutPage.Parent = content

local abTitle = Instance.new("TextLabel")
abTitle.BackgroundTransparency = 1
abTitle.Position = UDim2.fromOffset(0, 0)
abTitle.Size = UDim2.new(1, 0, 0, 22)
abTitle.Font = Enum.Font.GothamBold
abTitle.TextSize = 14
abTitle.TextColor3 = COL_TEXT
abTitle.TextXAlignment = Enum.TextXAlignment.Left
abTitle.Text = "About"
abTitle.Parent = aboutPage

local abScroll = Instance.new("ScrollingFrame")
abScroll.Position = UDim2.fromOffset(0, 30)
abScroll.Size = UDim2.new(1, 0, 1, -30)
abScroll.BackgroundTransparency = 1
abScroll.BorderSizePixel = 0
abScroll.ScrollBarThickness = 3
abScroll.ScrollBarImageColor3 = COL_ACCENT
abScroll.CanvasSize = UDim2.fromOffset(0, 0)
abScroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
abScroll.Parent = aboutPage

local abText = Instance.new("TextLabel")
abText.BackgroundTransparency = 1
abText.Position = UDim2.fromOffset(0, 0)
abText.Size = UDim2.new(1, -8, 0, 0)
abText.AutomaticSize = Enum.AutomaticSize.Y
abText.Font = Enum.Font.Gotham
abText.TextSize = 10
abText.TextColor3 = COL_TEXT
abText.TextXAlignment = Enum.TextXAlignment.Left
abText.TextYAlignment = Enum.TextYAlignment.Top
abText.TextWrapped = true
abText.Text = [[ABOUT • v2.0

CAT HUB
Version 2.0

━━━━━━━━━━━━━━━━━━
V2.0 • MAJOR UPDATE
━━━━━━━━━━━━━━━━━━

[+] NEW GUI
• Modern dark theme with blue accents
• Cat logo circle in header
• Profile card with avatar & Discord link
• Sidebar navigation (6 tabs)

[+] NEW FEATURES
• Live player count (game + server)
• Favorites system (saved per player)
• Search bar in Script view
• Back button for navigation
• Smooth animations & transitions

[+] SCRIPT UPDATES
• 87+ hubs organized by category
• Star button to save favorites
• Auto-detect current game

━━━━━━━━━━━━━━━━━━

⚠️ This script is 100% FREE!
If you PAID for it, you got scammed.
Report the seller on Discord.

Thank you for using cat hub.
]]
abText.Parent = abScroll

-- ============ NAV SWITCHING ============
local allPages = {
    [homeBtn]     = homePage,
    [scriptBtn]   = scriptPage,
    [serverBtn]   = serverPage,
    [settingsBtn] = settingsPage,
    [creditBtn]   = creditPage,
    [aboutBtn]    = aboutPage,
}

local allNavs = {homeBtn, scriptBtn, serverBtn, settingsBtn, creditBtn, aboutBtn}

local function setActive(activeBtn)
    for _, b in ipairs(allNavs) do
        b.BackgroundTransparency = 1
        b.BackgroundColor3 = COL_CARD
        b.TextColor3 = COL_SUBTEXT
    end
    activeBtn.BackgroundTransparency = 0
    activeBtn.BackgroundColor3 = COL_ACCENT
    activeBtn.TextColor3 = COL_TEXT
end

local function showPage(page)
    homePage.Visible = false
    scriptPage.Visible = false
    serverPage.Visible = false
    settingsPage.Visible = false
    creditPage.Visible = false
    aboutPage.Visible = false
    page.Visible = true
end

for btn, page in pairs(allPages) do
    btn.MouseButton1Click:Connect(function()
        setActive(btn)
        showPage(page)

        -- Reset script view to game list
        if page == scriptPage then
            gameListView.Visible = true
            scriptDetailView.Visible = false
        end
    end)
end

-- Nav hover
for _, b in ipairs(allNavs) do
    b.MouseEnter:Connect(function()
        if b.BackgroundColor3 ~= COL_ACCENT then
            b.BackgroundTransparency = 0.7
            b.BackgroundColor3 = COL_CARD
        end
    end)
    b.MouseLeave:Connect(function()
        if b.BackgroundColor3 ~= COL_ACCENT then
            b.BackgroundTransparency = 1
        end
    end)
end

-- Refresh stars helper (para sa favorites removal sync)
_G.CatHubRefreshStars = function()
    for _, row in ipairs(scriptList:GetChildren()) do
        if row:IsA("Frame") then
            local name = row.Name
            local star = nil
            for _, c in ipairs(row:GetChildren()) do
                if c:IsA("TextButton") and c.Text == "★" then
                    star = c
                    break
                end
            end
            if star then
                local isFav = table.find(favorites, name) ~= nil
                star.TextColor3 = isFav and COL_STAR or COL_MUTED
            end
        end
    end
end

-- ============ DISCORD COPY ============
local copiedTimeout = false
discordBtn.MouseButton1Click:Connect(function()
    if copiedTimeout then return end
    copiedTimeout = true

    if setclipboard then setclipboard(DISCORD_LINK)
    elseif syn and syn.write_clipboard then syn.write_clipboard(DISCORD_LINK)
    elseif toclipboard then toclipboard(DISCORD_LINK) end

    local original = dcText.Text
    dcText.Text = "Copied!"
    task.wait(1.5)
    dcText.Text = original
    copiedTimeout = false
end)

discordBtn.MouseEnter:Connect(function()
    TweenService:Create(discordBtn, TweenInfo.new(0.2),
        { BackgroundColor3 = Color3.fromRGB(105, 120, 255) }):Play()
end)

discordBtn.MouseLeave:Connect(function()
    TweenService:Create(discordBtn, TweenInfo.new(0.2),
        { BackgroundColor3 = Color3.fromRGB(88, 101, 242) }):Play()
end)

-- ============ CLOSE ============
closeBtn.MouseButton1Click:Connect(function()
    gui:Destroy()
end)

closeBtn.MouseEnter:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.15),
        { BackgroundColor3 = Color3.fromRGB(200, 60, 70), BackgroundTransparency = 0.3 }):Play()
end)

closeBtn.MouseLeave:Connect(function()
    TweenService:Create(closeBtn, TweenInfo.new(0.15),
        { BackgroundTransparency = 1 }):Play()
end)

-- ============ MINIMIZE ============
local isMinimized = false
minimizeBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    main.Visible = not isMinimized
end)

minimizeBtn.MouseEnter:Connect(function()
    TweenService:Create(minimizeBtn, TweenInfo.new(0.15),
        { BackgroundColor3 = COL_CARD, BackgroundTransparency = 0.3 }):Play()
end)

minimizeBtn.MouseLeave:Connect(function()
    TweenService:Create(minimizeBtn, TweenInfo.new(0.15),
        { BackgroundTransparency = 1 }):Play()
end)

-- ============ DRAG WINDOW ============
local dragging = false
local dragStart, startPos

header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = main.Position
    end
end)

UIS.InputChanged:Connect(function(input)
    if dragging and (
        input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch
    ) then
        local delta = input.Position - dragStart
        main.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1
    or input.UserInputType == Enum.UserInputType.Touch then
        dragging = false
    end
end)

-- ============ FADE-IN ============
main.BackgroundTransparency = 1
header.BackgroundTransparency = 1
sidebar.BackgroundTransparency = 1
profileCard.BackgroundTransparency = 1
welcomePanel.BackgroundTransparency = 1
gamePanel.BackgroundTransparency = 1
favPanel.BackgroundTransparency = 1

TweenService:Create(main,        TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(header,      TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(sidebar,     TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(profileCard, TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(welcomePanel,TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(gamePanel,   TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()
TweenService:Create(favPanel,    TweenInfo.new(0.5), { BackgroundTransparency = 0 }):Play()

print("[cat hub] v2.0 TEST BUILD loaded")
print("[cat hub] Favorite file:", FAV_FILE)
