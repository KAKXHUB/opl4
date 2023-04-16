local Cache = { DevConfig = {} };
Cache.DevConfig["FindFruitArgumet"] = loadstring(game:HttpGet"https://raw.githubusercontent.com/KangKung02/The-Last-Krypton/master/Back-End/src/public/api/UWU.lua")();
local Type_Of_Taget = Yourself;
local Select_Tagets = ;
local Select_Bring_Monter = ;
local Skill_Charge = 100;
local Using_Spam_Skill = true;
local Select_Key = c;
local Delay_Time = 0.1;


spawn(function()
    local GetingSkillArgumet = function(Arg1)
        if Arg1 == "M_H" then
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
        elseif Arg1 == "M_T" then
            return game.Players.LocalPlayer:GetMouse().Target;
        elseif Arg1 == "C" then
            return tonumber(Skill_Charge or 100);
        elseif Arg1 == "nil" then
            return false;
        elseif Arg1 == "CM" then
            return "Left";
        elseif Arg1 == "M_H_P" then
            return game.Players.LocalPlayer:GetMouse().Hit.Position;
        elseif Arg1 == "ARM_P" then
            return game.Players.LocalPlayer.Character["Right Arm"].Position;
        elseif Arg1 == "HRP_P" then
            return game.Players.LocalPlayer.Character.HumanoidRootPart.Position;
        elseif Arg1 == "DS_SL" then
            return game.Workspace.UserData["User_"..game.Players.LocalPlayer.UserId].Data.SniperLevel.Value;
        elseif Arg1 == "DS_DL" then
            return game.Workspace.UserData["User_"..game.Players.LocalPlayer.UserId].Data.DefenseLevel.Value;
        elseif Arg1 == "GT" then
            local AllPlayers = {};
            for i, v in pairs(game.Players:GetChildren()) do
                if v.Name ~= game.Players.LocalPlayer.Name and  (game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart").Position - v.Character:FindFirstChild("HumanoidRootPart").Position).magnitude < 1000 then
                    table.insert(AllPlayers, v)
                end
            end
            return AllPlayers;
        elseif Arg1 == "C_GDP" then
            local function GetDotPoint()
                local v45 = game.Players.LocalPlayer.Character.HumanoidRootPart.Position + Vector3.new(0, 1000, 0);
                local v46, v47, v48 = workspace:FindPartOnRay(Ray.new(v45, (game.Players.LocalPlayer:GetMouse().Hit.p - v45).unit * 5000), game.Players.LocalPlayer.Character);
                return v47;
            end;
            return CFrame.new(GetDotPoint());
        end
    end;
    local GetPowerFruitForKey = function(InputKey)
        local Export = {};
        local TableOfKey = {
            A = 1,
            B = 2,
            C = 3,
            D = 4,
            E = 5,
            F = 6
        }
        for _, v in pairs(game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].Data:GetChildren()) do
            if v.Name:find("Basic_DF") and v.Value == string.upper(InputKey) then
                Export[1] = TableOfKey[v.Name:split("")[10]]
                Export[2] = 1
                if v.Name:match("%d") == "2" then
                    Export[1] += 6
                    Export[2] = 2
                end
            end
        end
        return Export;
    end;
    local function GetPosition()
        if Type_Of_Taget == "Mouse" then
            Position = game.Players.LocalPlayer:GetMouse().Hit;
        elseif Type_Of_Taget == "Yourself" then
            Position = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame;
        elseif Type_Of_Taget == "Players" then
            for Name in pairs(Select_Tagets) do
                Position = game.Players[Name].Character.HumanoidRootPart.CFrame;
                break;
            end
        elseif Type_Of_Taget == "Monsters" then
            for _, Value in pairs(game.Workspace.Enemies:GetChildren()) do
                if Select_Bring_Monter[Value] then
                    Position = Value.HumanoidRootPart.CFrame;
                    break;
                end
            end
        end
        return Position or game.Players.LocalPlayer:GetMouse().Hit;
    end
    while wait() do
        pcall(function()
            if  Using_Spam_Skill == true then
            local KeyList = {"Z", "X", "C", "V", "B", "N"};
            local DevilFruit_Name;
            for Key in pairs(Select_Key) do
                if table.find(KeyList, Key) then
                    DevilFruit_Name = game:GetService("Workspace").UserData["User_" .. game.Players.LocalPlayer.UserId].Data.DevilFruit.Value;
                else
                    DevilFruit_Name = game:GetService("Workspace").UserData["User_" .. game.Players.LocalPlayer.UserId].Data.DevilFruit2.Value;
                end
                print(DevilFruit_Name);
                local KeyOfFruit, CountOfFruit = unpack(GetPowerFruitForKey(Key));
                local FuritTypeArgument = Cache.DevConfig["FindFruitArgumet"]:Get(DevilFruit_Name);
                local KeyOfArgument = getsenv(game.Players.LocalPlayer.Character.Powers[DevilFruit_Name])["VTC"];
                game:GetService("Players").LocalPlayer.Character.Powers[DevilFruit_Name].RemoteEvent:FireServer(
                    KeyOfArgument,
                    string.format("%sPower%s", DevilFruit_Name, KeyOfFruit),
                    "StartCharging",
                    GetPosition()
                );
                local Args = {KeyOfArgument, string.format("%sPower%s", DevilFruit_Name, KeyOfFruit), "StopCharging"};

                for _, Value in pairs(FuritTypeArgument[string.format("Power%s", (CountOfFruit == 1 and KeyOfFruit) or CountOfFruit == 2 and KeyOfFruit - 6)]) do
                    local Data = GetingSkillArgumet(Value);
                    table.insert(Args, Data);
                end
                game:GetService("Players").LocalPlayer.Character.Powers[DevilFruit_Name].RemoteEvent:FireServer(unpack(Args));
                if game.Players.LocalPlayer.Character.Humanoid.Health <= 0 then
                    [Using_Spam_Skill]:SetValue(false);
                end
            end
            wait(tonumber(Delay_Time or 1));
        end)
    end
end);
