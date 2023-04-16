local Cache = { DevConfig = {} };
Cache.DevConfig["FindFruitArgumet"] = loadstring(game:HttpGet"https://raw.githubusercontent.com/KangKung02/The-Last-Krypton/master/Back-End/src/public/api/UWU.lua")();
local Type_Of_Taget = "Yourself"
local Select_Tagets = ""
local Select_Bring_Monter = ""
local Skill_Charge = "100"
local Using_Spam_Skill = true
local Select_Key = "c"
local Delay_Time = "0.1"


print(Type_Of_Taget)

local GetingSkillArgumet = function(Arg1)
    if Arg1 == "M_H" then
        local Position;
        if Type_Of_Taget == "Mouse" then
            Position = game.Players.LocalPlayer:GetMouse().Hit;
        elseif Type_Of_Taget == "Yourself" then
            Position = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame;
                    break;
        end
        if not Position then
            Position = game.Players.LocalPlayer:GetMouse().Hit;
        end
        return  Position;
    end    

print(Position)
 
 
