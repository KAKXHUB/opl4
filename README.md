local Cache = { DevConfig = {} };
Cache.DevConfig["FindFruitArgumet"] = loadstring(game:HttpGet"https://raw.githubusercontent.com/KangKung02/The-Last-Krypton/master/Back-End/src/public/api/UWU.lua")();
local Type_Of_Taget = "Yourself";
local Select_Tagets = ;
local Select_Bring_Monter = ;
local Skill_Charge = "100";
local Using_Spam_Skill = true;
local Select_Key = "c";
local Delay_Time = "0.1";

local Position;
if Type_Of_Taget == "Mouse" then
    Position = game.Players.LocalPlayer:GetMouse().Hit;
elseif Type_Of_Taget == "Yourself" then
    Position = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame;
elseif Type_Of_Taget == "Players" then
    for Name in pairs(Select_Tagets) do
        local Ply =  game.Players[Name];
        if Ply and Ply.Character and Ply.Character:FindFirstChild("HumanoidRootPart") and Ply.Character:FindFirstChild("Humanoid") and Ply.Character.Humanoid.Health > 0 then
            Position = Ply.Character.HumanoidRootPart.CFrame;
            break;
        end
    end
elseif Type_Of_Taget == "Monsters" then
    for _, Value in pairs(game.Workspace.Enemies:GetChildren()) do
        if Select_Bring_Monter[Value.Name] and Value:FindFirstChild("HumanoidRootPart") and Value:FindFirstChild("Humanoid") and Value.Humanoid.Health > 0 then
            Position = Value.HumanoidRootPart.CFrame;
            break;
        end
    end
end
if not Position then
    Position = game.Players.LocalPlayer:GetMouse().Hit;
end
return  Position;

print(Position)
