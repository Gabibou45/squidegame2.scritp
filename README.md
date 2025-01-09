local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Squid Game",
   Icon = 0, -- Icon in Topbar. Can use Lucide Icons (string) or Roblox Image (number). 0 to use no icon (default).
   LoadingTitle = "Squid Game",
   LoadingSubtitle = "by Gabibou",
   Theme = "Default", -- Check https://docs.sirius.menu/rayfield/configuration/themes

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false, -- Prevents Rayfield from warning when the script has a version mismatch with the interface

   ConfigurationSaving = {
      Enabled = true,
      FolderName = nil, -- Create a custom folder for your hub/game
      FileName = "Big Hub"
   },

   Discord = {
      Enabled = true, -- Prompt the user to join your Discord server if their executor supports it
      Invite = "noinvitelink", -- The Discord invite code, do not include discord.gg/. E.g. discord.gg/ ABCD would be ABCD
      RememberJoins = true -- Set this to false to make them join the discord every time they load it up
   },

KeySystem = true, -- Set this to true to use our key system
   KeySettings = {
      Title = "squide game key",
      Subtitle = "Key System",
      Note = "join the discord for Get key: https://discord.gg/R2c3Z8BXzf", -- Use this to tell the user how to get a key
      FileName = "https://lootdest.org/s?VW70YiGT", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = false, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"Squide 332211222211222211"} -- List of keys that will be accepted by the system, can be RAW file links (pastebin, github etc) or simple strings ("hello","key22")
   }
})

local PlayerTab = Window:CreateTab("Player", 4483362458) -- Title, Image
local otherTab = Window:CreateTab("Other", 4483362458)

-- LocalPlayer is the player running the script
local player = game.Players.LocalPlayer

local Label = PlayerTab:CreateLabel("Gamepass Give", 4483362458, Color3.fromRGB(255, 0, 255), false) -- Title, Icon, Color, IgnoreTheme

-- Toggle button for Double Jumps
local ToggleDoubleJump = PlayerTab:CreateToggle({
   Name = "Double Jumps",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
      -- Define the function to toggle the double jump
      local function toggleDoubleJump()
          local doubleJump = player:FindFirstChild("DoubleJump")
          if doubleJump and doubleJump:IsA("BoolValue") then
              doubleJump.Value = not doubleJump.Value
              -- Optionally, update the UI to reflect the change
              if doubleJump.Value then
                  print("Double Jump Enabled") 
              else
                  print("Double Jump Disabled")
              end
          else
              warn("La propriété DoubleJump n'a pas été trouvée ou n'est pas un BoolValue.")
          end
      end
      -- Call the function to toggle the Double Jump state
      toggleDoubleJump()
   end,
})

-- Button to Toggle Double Speed
local ButtonDoubleSpeed = PlayerTab:CreateButton({
   Name = "Toggle Double Speed",
   Callback = function()
      local function toggleDoubleSpeed()
          -- Check if the player has the DoubleSpeed property
          local doubleSpeed = player:FindFirstChild("DoubleSpeed")
          if not doubleSpeed then
              -- Create the attribute if it doesn't exist
              doubleSpeed = Instance.new("NumberValue")
              doubleSpeed.Name = "DoubleSpeed"
              doubleSpeed.Parent = player
              doubleSpeed.Value = 1 -- Default value (normal speed)
          end

          -- Toggle the double speed value
          if doubleSpeed.Value == 2 then
              doubleSpeed.Value = 1
              print("Double Speed Disabled")
          else
              doubleSpeed.Value = 2
              print("Double Speed Enabled")
          end
      end
      -- Call the function to toggle the Double Speed state
      toggleDoubleSpeed()
   end,
})

-- Button to Toggle Double Speed
local ButtonDoubleSpeed = PlayerTab:CreateButton({
   Name = "Give TeleportGun",
   Callback = function()
      local function toggleDoubleSpeed()
          -- Check if the player has the DoubleSpeed property
          local doubleSpeed = player:FindFirstChild("TeleportGun")
          if not doubleSpeed then
              -- Create the attribute if it doesn't exist
              doubleSpeed = Instance.new("NumberValue")
              doubleSpeed.Name = "TeleportGun"
              doubleSpeed.Parent = player
              doubleSpeed.Value = 0 -- Default value (normal speed)
          end

          -- Toggle the double speed value
          if doubleSpeed.Value == 1 then
              doubleSpeed.Value = 0
              print("TeleportGun Disabled")
          else
              doubleSpeed.Value = 1
              print("TeleportGun Enabled")
          end
      end
      -- Call the function to toggle the Double Speed state
      toggleDoubleSpeed()
   end,
})

local Button = otherTab:CreateButton({
   Name = "Dev",
   Callback = function()
  loadstring(game:HttpGet("https://raw.githubusercontent.com/infyiff/backup/main/dex.lua"))()
   end,
})

local Button = otherTab:CreateButton({
   Name = "Fly V3🔥",
   Callback = function()
  loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.txt"))()

warn("F L Y   G U I   V 3 🔥")
   end,
})

local Label = PlayerTab:CreateLabel("Esp", 4483362458, Color3.fromRGB(0, 255, 255), false)

local Toggle = PlayerTab:CreateToggle({
   Name = "Glasse esp",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
  
   -- Localisation du dossier contenant tous les modèles
local parentFolder = game.Workspace.BrigePartFolder

-- Parcours des enfants du dossier parent
for _, model in pairs(parentFolder:GetChildren()) do
    -- Vérifier si l'objet est un modèle
    if model:IsA("Model") then
        -- Parcours des parts dans le modèle
        for _, part in pairs(model:GetChildren()) do
            -- Vérification que c'est une BasePart et qu'il n'a pas de sous-dossier "TouchInterest"
            if part:IsA("BasePart") and not part:FindFirstChild("TouchInterest") then
                -- Changer la couleur de la part en rouge
                part.BrickColor = BrickColor.new("Bright red")
            end
        end
    end
end
   end,
})

-- Fonction pour appliquer un Highlight aux joueurs
function togglePlayerVisibilityThroughWalls(enable)
    -- Récupérer tous les joueurs
    local players = game:GetService("Players"):GetPlayers()

    -- Parcourir tous les joueurs
    for _, player in ipairs(players) do
        if player.Character and player.Character:FindFirstChild("Head") then
            local character = player.Character
            -- Si le toggle est activé, ajouter un Highlight pour les rendre visibles à travers les murs
            if enable then
                -- Appliquer un effet Highlight aux personnages
                local highlight = character:FindFirstChildOfClass("Highlight")
                
                -- Si le personnage n'a pas encore de Highlight, en créer un
                if not highlight then
                    highlight = Instance.new("Highlight")
                    highlight.Parent = character
                    highlight.Adornee = character
                    highlight.FillColor = Color3.fromRGB(255, 0, 0)  -- Couleur rouge pour l'effet
                    highlight.OutlineColor = Color3.fromRGB(255, 255, 255)  -- Couleur de contour blanche
                    highlight.FillTransparency = 0.5  -- Transparence de l'intérieur
                    highlight.OutlineTransparency = 0.3  -- Transparence du contour
                end
            else
                -- Supprimer l'effet Highlight lorsque le toggle est désactivé
                local highlight = character:FindFirstChildOfClass("Highlight")
                if highlight then
                    highlight:Destroy()  -- Retirer le Highlight pour réinitialiser l'effet
                end
            end
        end
    end
end

-- Créer le Toggle pour activer/désactiver l'affichage des joueurs à travers les murs
local Toggle = PlayerTab:CreateToggle({
   Name = "Voir les Joueurs à travers les murs",  -- Nom du Toggle
   CurrentValue = false,  -- Valeur initiale (désactivée, joueurs non visibles à travers les murs)
   Flag = "Toggle1",  -- Un identifiant unique pour la configuration
   Callback = function(Value)
       -- Lorsque le Toggle est activé ou désactivé
       -- La variable "Value" est vraie si le toggle est activé, sinon elle est fausse
       if Value then
           -- Activer la visibilité des joueurs à travers les murs
           togglePlayerVisibilityThroughWalls(true)
       else
           -- Désactiver la visibilité à travers les murs
           togglePlayerVisibilityThroughWalls(false)
       end
   end,
})

-- Rafraîchir toutes les 10 secondes pour s'assurer que tous les joueurs sont visibles
while true do
    -- Vérifier si le Toggle est activé, et appliquer la mise à jour
    if Toggle.CurrentValue then
        togglePlayerVisibilityThroughWalls(true)
    end

    -- Attendre 10 secondes avant de rafraîchir
    wait(10)
end
