local roundTime = 300 -- 5 minutes
local intermissionTime = 60 -- 1 minute intermission
local playersRemaining = 0

-- Function to start the round
local function startRound()
    print("Round started!")
    playersRemaining = #game.Players:GetPlayers() -- Track number of active players
    
    -- Countdown timer
    for i = roundTime, 1, -1 do
        wait(1)
        print("Time left: " .. i .. " seconds")
        
        -- Check if only one player is left
        if playersRemaining <= 1 then
            print("A player has won the round!")
            break
        end
    end
    
    print("Round over!")
    startIntermission()
end

-- Function for intermission between rounds
local function startIntermission()
    print("Intermission started!")
    
    for i = intermissionTime, 1, -1 do
        wait(1)
        print("Intermission time left: " .. i .. " seconds")
    end
    
    -- Start a new round after intermission
    startRound()
end

-- Function to reduce the number of remaining players when a player is eliminated
local function onPlayerEliminated(player)
    playersRemaining = playersRemaining - 1
    if playersRemaining <= 1 then
        print("Round winner: " .. player.Name)
    end
end

-- Connect player elimination to the elimination function
game.Players.PlayerRemoving:Connect(onPlayerEliminated)

-- Start the first round
startRound()
