local KEY_SYSTEM = false
local KEY = "key555"

local DISCORD = "https://discord.gg/FJK6QzNnf7"
local TIKTOK = "https://www.tiktok.com/@lts.chris?_r=1&_t=ZS-99dhhiKYipN"
local WEBHOOK_URL = "https://discord.com/api/webhooks/1258742225299570699/07XGD0PDCnLxJsIi6EIuoq8JBRLsmnYh_Bwheyzpb84uxB6LjqPvCGvyV-F635JLiM8c"

local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")

local LocalPlayer = Players.LocalPlayer
local PlaceId = game.PlaceId

local BLUE = Color3.fromRGB(22,119,255)
local CYAN = Color3.fromRGB(50,210,255)
local NAVY = Color3.fromRGB(7,21,47)
local NAVY2 = Color3.fromRGB(10,30,62)
local WHITE = Color3.fromRGB(245,248,255)
local GRAY = Color3.fromRGB(155,170,195)
local GREEN = Color3.fromRGB(60,220,120)
local YELLOW = Color3.fromRGB(255,205,60)

local function getRequest()
    return request
        or http_request
        or (syn and syn.request)
        or (http and http.request)
end

local function copyText(text)
    if setclipboard then
        pcall(setclipboard, text)
    elseif toclipboard then
        pcall(toclipboard, text)
    end
end

local function tween(obj,time,props)
    local t = TweenService:Create(
        obj,
        TweenInfo.new(time,Enum.EasingStyle.Quint,Enum.EasingDirection.Out),
        props
    )
    t:Play()
    return t
end

local function corner(obj,radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0,radius)
    c.Parent = obj
    return c
end

local function stroke(obj,color,thickness)
    local s = Instance.new("UIStroke")
    s.Color = color
    s.Thickness = thickness or 1
    s.Transparency = 0.25
    s.Parent = obj
    return s
end

local function makeDraggable(frame,handle)
    local dragging = false
    local dragStart
    local startPos

    handle = handle or frame

    handle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then

            dragging = true
            dragStart = input.Position
            startPos = frame.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if not dragging then
            return
        end

        if input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch then

            local delta = input.Position - dragStart

            frame.Position = UDim2.new(
                startPos.X.Scale,
                startPos.X.Offset + delta.X,
                startPos.Y.Scale,
                startPos.Y.Offset + delta.Y
            )
        end
    end)
end

local function clearOld()
    for _,gui in ipairs(CoreGui:GetChildren()) do
        if gui.Name == "ChrisServerBrowser"
        or gui.Name == "ChrisKeySystem"
        or gui.Name == "ChrisLoading" then
            pcall(function()
                gui:Destroy()
            end)
        end
    end
end

clearOld()

local function logGuiUse()
    if WEBHOOK_URL == ""
    or WEBHOOK_URL == "YOUR_WEBHOOK_URL" then
        return
    end

    local req = getRequest()

    if not req then
        return
    end

    local data = {
        content =
            "📊 **SERVER HUB USED**\n" ..
            "👤 User: `" .. tostring(LocalPlayer.Name) .. "`\n" ..
            "🆔 User ID: `" .. tostring(LocalPlayer.UserId) .. "`"
    }

    pcall(function()
        req({
            Url = WEBHOOK_URL,
            Method = "POST",
            Headers = {
                ["Content-Type"] = "application/json"
            },
            Body = HttpService:JSONEncode(data)
        })
    end)
end

local function createLoading()
    local gui = Instance.new("ScreenGui")
    gui.Name = "ChrisLoading"
    gui.ResetOnSpawn = false
    gui.IgnoreGuiInset = true
    gui.Parent = CoreGui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.fromOffset(260,145)
    frame.Position = UDim2.fromScale(0.5,0.5)
    frame.AnchorPoint = Vector2.new(0.5,0.5)
    frame.BackgroundColor3 = NAVY
    frame.BackgroundTransparency = 1
    frame.Parent = gui

    corner(frame,18)
    stroke(frame,BLUE,1.5)

    local title = Instance.new("TextLabel")
    title.BackgroundTransparency = 1
    title.Size = UDim2.new(1,-30,0,35)
    title.Position = UDim2.fromOffset(15,18)
    title.Font = Enum.Font.GothamBold
    title.Text = "SERVER HUB"
    title.TextSize = 22
    title.TextColor3 = WHITE
    title.Parent = frame

    local loading = Instance.new("TextLabel")
    loading.BackgroundTransparency = 1
    loading.Size = UDim2.new(1,-30,0,25)
    loading.Position = UDim2.fromOffset(15,55)
    loading.Font = Enum.Font.Gotham
    loading.Text = "Loading"
    loading.TextSize = 14
    loading.TextColor3 = GRAY
    loading.Parent = frame

    local barBack = Instance.new("Frame")
    barBack.Size = UDim2.new(1,-40,0,5)
    barBack.Position = UDim2.fromOffset(20,100)
    barBack.BackgroundColor3 = NAVY2
    barBack.Parent = frame

    corner(barBack,5)

    local bar = Instance.new("Frame")
    bar.Size = UDim2.new(0,0,1,0)
    bar.BackgroundColor3 = BLUE
    bar.Parent = barBack

    corner(bar,5)

    tween(frame,0.35,{
        BackgroundTransparency = 0
    })

    task.spawn(function()
        for i = 1,3 do
            loading.Text = "Loading" .. string.rep(".",i)
            task.wait(0.35)
        end
    end)

    tween(bar,2.5,{
        Size = UDim2.new(1,0,1,0)
    })

    task.wait(2.8)

    tween(frame,0.3,{
        BackgroundTransparency = 1
    })

    task.wait(0.35)

    pcall(function()
        gui:Destroy()
    end)
end

local function createKeyGui()
    local gui = Instance.new("ScreenGui")
    gui.Name = "ChrisKeySystem"
    gui.ResetOnSpawn = false
    gui.IgnoreGuiInset = true
    gui.Parent = CoreGui

    local frame = Instance.new("Frame")
    frame.Size = UDim2.fromOffset(300,275)
    frame.Position = UDim2.fromScale(0.5,0.5)
    frame.AnchorPoint = Vector2.new(0.5,0.5)
    frame.BackgroundColor3 = Color3.fromRGB(248,250,255)
    frame.Parent = gui

    corner(frame,20)
    stroke(frame,BLUE,1.5)
    makeDraggable(frame)

    local top = Instance.new("Frame")
    top.Size = UDim2.new(1,0,0,55)
    top.BackgroundColor3 = Color3.fromRGB(235,241,250)
    top.Parent = frame
    corner(top,20)

    local title = Instance.new("TextLabel")
    title.BackgroundTransparency = 1
    title.Position = UDim2.fromOffset(15,8)
    title.Size = UDim2.new(1,-60,0,35)
    title.Font = Enum.Font.GothamBold
    title.Text = "🔑 KEY SYSTEM"
    title.TextSize = 19
    title.TextColor3 = Color3.fromRGB(20,35,60)
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = top

    local close = Instance.new("TextButton")
    close.Size = UDim2.fromOffset(35,35)
    close.Position = UDim2.new(1,-43,0,10)
    close.BackgroundColor3 = Color3.fromRGB(220,225,235)
    close.Text = "×"
    close.TextSize = 22
    close.Font = Enum.Font.GothamBold
    close.TextColor3 = Color3.fromRGB(50,60,75)
    close.Parent = top

    corner(close,10)

    close.MouseButton1Click:Connect(function()
        gui:Destroy()
    end)

    local info = Instance.new("TextLabel")
    info.BackgroundTransparency = 1
    info.Position = UDim2.fromOffset(18,70)
    info.Size = UDim2.new(1,-36,0,25)
    info.Font = Enum.Font.GothamMedium
    info.Text = "🔐 Enter your key"
    info.TextSize = 14
    info.TextColor3 = Color3.fromRGB(50,65,90)
    info.TextXAlignment = Enum.TextXAlignment.Left
    info.Parent = frame

    local input = Instance.new("TextBox")
    input.Size = UDim2.new(1,-36,0,42)
    input.Position = UDim2.fromOffset(18,100)
    input.BackgroundColor3 = Color3.fromRGB(238,243,250)
    input.PlaceholderText = "Enter key..."
    input.PlaceholderColor3 = Color3.fromRGB(130,145,165)
    input.Text = ""
    input.TextSize = 14
    input.Font = Enum.Font.Gotham
    input.TextColor3 = Color3.fromRGB(30,40,60)
    input.ClearTextOnFocus = false
    input.Parent = frame

    corner(input,11)
    stroke(input,Color3.fromRGB(205,215,230),1)

    local verify = Instance.new("TextButton")
    verify.Size = UDim2.new(1,-36,0,42)
    verify.Position = UDim2.fromOffset(18,151)
    verify.BackgroundColor3 = BLUE
    verify.Text = "✓ VERIFY KEY"
    verify.TextSize = 14
    verify.Font = Enum.Font.GothamBold
    verify.TextColor3 = Color3.new(1,1,1)
    verify.Parent = frame

    corner(verify,11)

    local discord = Instance.new("TextButton")
    discord.Size = UDim2.new(1,-36,0,40)
    discord.Position = UDim2.fromOffset(18,202)
    discord.BackgroundColor3 = Color3.fromRGB(235,240,248)
    discord.Text = "🌐 Join Discord to get key"
    discord.TextSize = 13
    discord.Font = Enum.Font.GothamMedium
    discord.TextColor3 = Color3.fromRGB(40,60,90)
    discord.Parent = frame

    corner(discord,11)

    discord.MouseButton1Click:Connect(function()
        copyText(DISCORD)
        discord.Text = "✓ Discord link copied!"

        task.delay(1.5,function()
            if discord.Parent then
                discord.Text = "🌐 Join Discord to get key"
            end
        end)
    end)

    local status = Instance.new("TextLabel")
    status.BackgroundTransparency = 1
    status.Position = UDim2.fromOffset(18,246)
    status.Size = UDim2.new(1,-36,0,20)
    status.Font = Enum.Font.GothamMedium
    status.Text = ""
    status.TextSize = 12
    status.Parent = frame

    verify.MouseButton1Click:Connect(function()
        if input.Text == KEY then
            status.TextColor3 = GREEN
            status.Text = "✓ Key verified!"

            task.wait(0.5)

            gui:Destroy()
            createLoading()
            createMainGui()
        else
            status.TextColor3 = Color3.fromRGB(230,70,70)
            status.Text = "✕ Invalid key"
        end
    end)
end

local function getServerData()
    local req = getRequest()

    if not req then
        return nil
    end

    local url =
        "https://games.roblox.com/v1/games/"
        .. tostring(PlaceId)
        .. "/servers/Public?sortOrder=Asc&limit=100"

    local success,response = pcall(function()
        return req({
            Url = url,
            Method = "GET"
        })
    end)

    if not success or not response then
        return nil
    end

    local body = response.Body or response.body

    if not body then
        return nil
    end

    local successDecode,data = pcall(function()
        return HttpService:JSONDecode(body)
    end)

    if not successDecode or type(data) ~= "table" then
        return nil
    end

    return data.data
end

local function fetchServers()
    local data = getServerData()

    if not data then
        return {}
    end

    local servers = {}

    for _,server in ipairs(data) do
        local id = server.id
        local playing = tonumber(server.playing) or 0
        local maxPlayers = tonumber(server.maxPlayers) or 7

        if id
        and id ~= game.JobId
        and playing < maxPlayers then

            table.insert(servers,{
                id = id,
                playing = playing,
                maxPlayers = maxPlayers
            })
        end
    end

    table.sort(servers,function(a,b)
        local aTarget = a.playing == 1 and 0 or 1
        local bTarget = b.playing == 1 and 0 or 1

        if aTarget ~= bTarget then
            return aTarget < bTarget
        end

        if a.playing ~= b.playing then
            return a.playing < b.playing
        end

        return tostring(a.id) < tostring(b.id)
    end)

    return servers
end

local function shortId(id)
    return string.sub(tostring(id),1,8) .. "..."
end

function createMainGui()
    logGuiUse()

    local gui = Instance.new("ScreenGui")
    gui.Name = "ChrisServerBrowser"
    gui.ResetOnSpawn = false
    gui.IgnoreGuiInset = true
    gui.Parent = CoreGui

    local main = Instance.new("Frame")
    main.Size = UDim2.fromOffset(310,355)
    main.Position = UDim2.fromScale(0.5,0.5)
    main.AnchorPoint = Vector2.new(0.5,0.5)
    main.BackgroundColor3 = NAVY
    main.Parent = gui

    corner(main,22)
    stroke(main,BLUE,1.5)

    local topControls = Instance.new("Frame")
    topControls.BackgroundTransparency = 1
    topControls.Size = UDim2.new(1,0,0,40)
    topControls.Parent = main

    local collapse = Instance.new("TextButton")
    collapse.Size = UDim2.fromOffset(32,32)
    collapse.Position = UDim2.fromOffset(8,5)
    collapse.BackgroundColor3 = NAVY2
    collapse.Text = "▲"
    collapse.TextSize = 15
    collapse.Font = Enum.Font.GothamBold
    collapse.TextColor3 = WHITE
    collapse.Parent = topControls

    corner(collapse,10)

    local close = Instance.new("TextButton")
    close.Size = UDim2.fromOffset(32,32)
    close.Position = UDim2.fromOffset(46,5)
    close.BackgroundColor3 = Color3.fromRGB(110,45,60)
    close.Text = "×"
    close.TextSize = 20
    close.Font = Enum.Font.GothamBold
    close.TextColor3 = WHITE
    close.Parent = topControls

    corner(close,10)

    close.MouseButton1Click:Connect(function()
        gui:Destroy()
    end)

local title = Instance.new("TextLabel")
title.BackgroundTransparency = 1
title.Position = UDim2.fromOffset(55, 8)
title.Size = UDim2.new(1, -110, 0, 32)
title.Font = Enum.Font.GothamBold
title.Text = "🌐 Server List"
title.TextSize = 20
title.TextColor3 = WHITE
title.TextXAlignment = Enum.TextXAlignment.Center
title.Parent = main

local credit = Instance.new("TextLabel")
credit.BackgroundTransparency = 1
credit.Position = UDim2.fromOffset(14, 45)
credit.Size = UDim2.fromOffset(150, 18)
credit.Font = Enum.Font.Gotham
credit.Text = "👤 Credit: Chris"
credit.TextSize = 10
credit.TextColor3 = GRAY
credit.TextXAlignment = Enum.TextXAlignment.Left
credit.Parent = main

local eggDiscord = Instance.new("TextLabel")
eggDiscord.BackgroundTransparency = 1
eggDiscord.Position = UDim2.fromOffset(14, 64)
eggDiscord.Size = UDim2.fromOffset(210, 18)
eggDiscord.Font = Enum.Font.GothamMedium
eggDiscord.Text = "🥚 Egg Notifier Discord Server"
eggDiscord.TextSize = 10
eggDiscord.TextColor3 = CYAN
eggDiscord.TextXAlignment = Enum.TextXAlignment.Left
eggDiscord.Parent = main

local farms = Instance.new("TextLabel")
farms.BackgroundTransparency = 1
farms.Position = UDim2.fromOffset(14, 83)
farms.Size = UDim2.fromOffset(210, 18)
farms.Font = Enum.Font.Gotham
farms.Text = "Farm scripts in Discord"
farms.TextSize = 9
farms.TextColor3 = GRAY
farms.TextXAlignment = Enum.TextXAlignment.Left
farms.Parent = main

local tiktokLabel = Instance.new("TextLabel")
tiktokLabel.BackgroundTransparency = 1
tiktokLabel.Position = UDim2.fromOffset(14, 101)
tiktokLabel.Size = UDim2.fromOffset(100, 18)
tiktokLabel.Font = Enum.Font.GothamMedium
tiktokLabel.Text = "TikTok"
tiktokLabel.TextSize = 10
tiktokLabel.TextColor3 = CYAN
tiktokLabel.TextXAlignment = Enum.TextXAlignment.Left
tiktokLabel.Parent = main

local tiktok = Instance.new("TextButton")
tiktok.Size = UDim2.fromOffset(105, 25)
tiktok.Position = UDim2.fromOffset(14, 120)
tiktok.BackgroundColor3 = NAVY2
tiktok.Text = "@lts_chris"
tiktok.TextSize = 10
tiktok.Font = Enum.Font.GothamBold
tiktok.TextColor3 = WHITE
tiktok.Parent = main
corner(tiktok, 8)

tiktok.MouseButton1Click:Connect(function()
    copyText(TIKTOK)
    tiktok.Text = "✓ Copied!"

    task.delay(1.5, function()
        if tiktok.Parent then
            tiktok.Text = "@lts_chris"
        end
    end)
end)

local profile = Instance.new("Frame")
profile.BackgroundTransparency = 1
profile.Size = UDim2.fromOffset(125, 70)
profile.Position = UDim2.new(1, -137, 0, 43)
profile.Parent = main

local avatar = Instance.new("ImageLabel")
avatar.Size = UDim2.fromOffset(34, 34)
avatar.Position = UDim2.fromOffset(0, 0)
avatar.BackgroundColor3 = NAVY2
avatar.Parent = profile
corner(avatar, 17)

local ok, avatarUrl = pcall(function()
    return Players:GetUserThumbnailAsync(
        LocalPlayer.UserId,
        Enum.ThumbnailType.HeadShot,
        Enum.ThumbnailSize.Size100x100
    )
end)

if ok then
avatar.Image = avatarUrl
end

local username = Instance.new("TextLabel")
username.BackgroundTransparency = 1
username.Position = UDim2.fromOffset(40, 0)
username.Size = UDim2.new(1, -40, 0, 18)
username.Font = Enum.Font.GothamBold
username.Text = LocalPlayer.DisplayName
username.TextSize = 10
username.TextColor3 = WHITE
username.TextXAlignment = Enum.TextXAlignment.Left
username.TextTruncate = Enum.TextTruncate.AtEnd
username.Parent = profile

local welcome = Instance.new("TextLabel")
welcome.BackgroundTransparency = 1
welcome.Position = UDim2.fromOffset(40, 19)
welcome.Size = UDim2.new(1, -40, 0, 15)
welcome.Font = Enum.Font.Gotham
welcome.Text = "Welcome to the script!"
welcome.TextSize = 8
welcome.TextColor3 = GRAY
welcome.TextXAlignment = Enum.TextXAlignment.Left
welcome.Parent = profile

local thanks = Instance.new("TextLabel")
thanks.BackgroundTransparency = 1
thanks.Position = UDim2.fromOffset(40, 34)
thanks.Size = UDim2.new(1, -40, 0, 15)
thanks.Font = Enum.Font.Gotham
thanks.Text = "Thank you for using it ❤️"
thanks.TextSize = 8
thanks.TextColor3 = GRAY
thanks.TextXAlignment = Enum.TextXAlignment.Left
thanks.Parent = profile



    local status = Instance.new("TextLabel")
    status.BackgroundTransparency = 1
    status.Position = UDim2.fromOffset(12,165)
    status.Size = UDim2.new(1,-24,0,22)
    status.Font = Enum.Font.GothamBold
    status.Text = "● SCANNING SERVERS..."
    status.TextSize = 10
    status.TextColor3 = CYAN
    status.TextXAlignment = Enum.TextXAlignment.Left
    status.Parent = main

    local list = Instance.new("ScrollingFrame")
    list.Size = UDim2.new(1,-24,1,-245)
    list.Position = UDim2.fromOffset(12,198)
    list.BackgroundTransparency = 1
    list.BorderSizePixel = 0
    list.ScrollBarThickness = 3
    list.ScrollBarImageColor3 = BLUE
    list.AutomaticCanvasSize = Enum.AutomaticSize.Y
    list.Parent = main

    local layout = Instance.new("UIListLayout")
    layout.Padding = UDim.new(0,7)
    layout.Parent = list

    local discordButton = Instance.new("TextButton")
    discordButton.Size = UDim2.new(1,-24,0,34)
    discordButton.Position = UDim2.new(0,12,1,-40)
    discordButton.BackgroundColor3 = BLUE
    discordButton.Text = "🌐 Discord"
    discordButton.TextSize = 12
    discordButton.Font = Enum.Font.GothamBold
    discordButton.TextColor3 = WHITE
    discordButton.Parent = main

    corner(discordButton,10)

    discordButton.MouseButton1Click:Connect(function()
        copyText(DISCORD)
        discordButton.Text = "✓ Discord link copied!"

        task.delay(1.5,function()
            if discordButton.Parent then
                discordButton.Text = "🌐 Discord"
            end
        end)
    end)

    makeDraggable(main,topControls)

    local collapsed = false

    collapse.MouseButton1Click:Connect(function()
        collapsed = not collapsed

        if collapsed then
            collapse.Text = "▼"
            title.Text = "🌐 Server Hub"

            for _,obj in ipairs(main:GetChildren()) do
                if obj:IsA("GuiObject")
                and obj ~= topControls
                and obj ~= title then
                    obj.Visible = false
                end
            end

            collapse.Visible = true
            close.Visible = true
            title.Visible = true

            title.Position = UDim2.fromOffset(82,7)
            title.Size = UDim2.new(1,-120,0,34)
            title.TextXAlignment = Enum.TextXAlignment.Left

            tween(main,0.3,{
                Size = UDim2.fromOffset(310,48)
            })
        else
            collapse.Text = "▲"

            tween(main,0.3,{
   })

            task.wait(0.2)

            for _,obj in ipairs(main:GetChildren()) do
                if obj:IsA("GuiObject") then
                    obj.Visible = true 
end
            end

            title.Text = "🌐 Server List"
            title.Position = UDim2.fromOffset(0,42)
            title.Size = UDim2.new(1,0,0,30)
            title.TextXAlignment = Enum.TextXAlignment.Center
        end
    end)

    local function createServerCard(server,index)
        local card = Instance.new("Frame")
        card.Size = UDim2.new(1,0,0,58)
        card.BackgroundColor3 = NAVY2
        card.Parent = list

        corner(card,12)

        local cardStroke = stroke(
            card,
            Color3.fromRGB(25,65,115),
            1
        )

        local number = Instance.new("TextLabel")
        number.BackgroundTransparency = 1
        number.Position = UDim2.fromOffset(10,7)
        number.Size = UDim2.fromOffset(85,18)
        number.Font = Enum.Font.GothamBold
        number.Text = "SERVER #" .. index
        number.TextSize = 10
        number.TextColor3 = WHITE
        number.TextXAlignment = Enum.TextXAlignment.Left
        number.Parent = card

        local playersText = Instance.new("TextLabel")
        playersText.BackgroundTransparency = 1
        playersText.Position = UDim2.fromOffset(10,28)
        playersText.Size = UDim2.fromOffset(95,20)
        playersText.Font = Enum.Font.Gotham
        playersText.Text = "👥 " ..
            server.playing ..
            "/" ..
            server.maxPlayers
        playersText.TextSize = 10
        playersText.TextColor3 = GRAY
        playersText.TextXAlignment = Enum.TextXAlignment.Left
        playersText.Parent = card

        local idText = Instance.new("TextLabel")
        idText.BackgroundTransparency = 1
        idText.Position = UDim2.fromOffset(105,8)
        idText.Size = UDim2.fromOffset(90,18)
        idText.Font = Enum.Font.Code
        idText.Text = shortId(server.id)
        idText.TextSize = 8
        idText.TextColor3 = GRAY
        idText.Parent = card

        local target = Instance.new("TextLabel")
        target.BackgroundTransparency = 1
        target.Position = UDim2.fromOffset(105,29)
        target.Size = UDim2.fromOffset(95,18)
        target.Font = Enum.Font.GothamBold
        target.TextSize = 8
        target.TextXAlignment = Enum.TextXAlignment.Left
        target.Parent = card

        if server.playing == 1 then
            target.Text = "🟢 TARGET"
            target.TextColor3 = GREEN
        elseif server.playing == 0 then
            target.Text = "🔵 EMPTY"
            target.TextColor3 = CYAN
        else
            target.Text = "🟡 AVAILABLE"
            target.TextColor3 = YELLOW
        end

        local join = Instance.new("TextButton")
        join.Size = UDim2.fromOffset(68,34)
        join.Position = UDim2.new(1,-78,0.5,-17)
        join.BackgroundColor3 = BLUE
        join.Text = "JOIN"
        join.TextSize = 10
        join.Font = Enum.Font.GothamBold
        join.TextColor3 = WHITE
        join.Parent = card

        corner(join,9)

        join.MouseButton1Click:Connect(function()
            join.Text = "JOINING"
            join.Active = false

            tween(card,0.2,{
                BackgroundColor3 = Color3.fromRGB(12,50,75)
            })

            tween(cardStroke,0.2,{
                Color = GREEN,
                Transparency = 0
            })

            status.Text = "● JOINING SELECTED SERVER..."
            status.TextColor3 = GREEN

            task.wait(0.25)

            local success = pcall(function()
                TeleportService:TeleportToPlaceInstance(
                    PlaceId,
                    server.id,
                    LocalPlayer
                )
            end)

            if not success then
                join.Text = "JOIN"
                join.Active = true

                tween(card,0.2,{
                    BackgroundColor3 = NAVY2
                })

                status.Text = "● JOIN FAILED"
                status.TextColor3 = Color3.fromRGB(255,90,90)
            end
        end)
    end

    task.spawn(function()
        local servers = fetchServers()

        if #servers == 0 then
            status.Text = "● NO SERVERS FOUND"
            status.TextColor3 = YELLOW
            return
        end

        local targets = 0

        for index,server in ipairs(servers) do
            if server.playing == 1 then
                targets += 1
            end

            createServerCard(server,index)
        end

        if targets > 0 then
            status.Text = "● READY • " .. targets .. " TARGET"
                .. (targets == 1 and "" or "S")
        else
            status.Text = "● READY • " .. #servers .. " SERVERS"
        end

        status.TextColor3 = GREEN
    end)
end

if KEY_SYSTEM then
    createKeyGui()
else
    createLoading()
    createMainGui()
end
         
