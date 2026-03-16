-- SETTINGS
local CORRECT_ANSWER = "Adopt Me"
local HINT_TEXT = "It has pets and trading!"

-- 1. BUILD THE WORLD
local folder = Instance.New("Folder")
folder.Name = "GameMap"
folder.Parent = game.Environment

local floor = Instance.New("Part")
floor.Name = "Floor"
floor.Size = Vector3.New(40, 1, 40)
floor.Position = Vector3.New(0, 0, 0)
floor.Anchored = true
floor.Parent = folder

local door = Instance.New("Part")
door.Name = "WinDoor"
door.Size = Vector3.New(10, 15, 1)
door.Position = Vector3.New(0, 7.5, 18)
door.Anchored = true
door.Color = Color.New(1, 0, 0) -- Red
door.Parent = folder

-- 2. LEADERBOARD & GUESSING
game.Players.PlayerAdded:Connect(function(player)
    local ls = Instance.New("Folder")
    ls.Name = "leaderstats"
    ls.Parent = player
    
    local wins = Instance.New("IntValue")
    wins.Name = "Wins"
    wins.Value = 0
    wins.Parent = ls

    player.Chatted:Connect(function(message)
        local chat = string.lower(message)
        local answer = string.lower(CORRECT_ANSWER)
        
        if chat == answer then
            wins.Value = wins.Value + 1
            door.Transparency = 0.5
            door.CanCollide = false
            wait(5)
            door.Transparency = 0
            door.CanCollide = true
        elseif chat == "hint" then
            print("HINT: " .. HINT_TEXT)
        end
    end)
end)
