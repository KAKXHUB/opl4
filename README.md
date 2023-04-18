local Cache = { DevConfig = {} };
Cache.DevConfig["ListOfRareDveilFruit"] = game:GetService("HttpService"):JSONDecode(game:HttpGet("https://raw.githubusercontent.com/KangKung02/just-bin/main/OPL_LF.json"));

local Detector = {
        ListOfRareFruit = {};
        ListOfNormalFruit = {};
        ListOfNormalBox = {};
        ListOfRareBox = {};
    };

    function Detector:Add(Argument)
        local Content;
        if Argument.IsFruit then
            Content = string.format("Fruit Name : %s, Owner Name : %s, Position : %s, IsRare : %s", Argument.FruitName or "None", Argument.Owner or "None", Argument.Position or "None", (Argument.IsRare and "Yes") or "No");
            if Argument["IsRare"] then
                table.insert(self.ListOfRareFruit, Content);
            else
                table.insert(self.ListOfNormalFruit, Content);
            end
        else
            Content = string.format("Box Name : %s, Owner Name : %s, Position : %s, IsRare : %s", Argument.FruitName or "None", Argument.Owner or "None", Argument.Position or "None", (Argument.IsRare and "Yes") or "No");
            if Argument["IsRare"] then
                table.insert(self.ListOfRareBox, Content);
            else
                table.insert(self.ListOfNormalBox, Content);
            end
        end
    end;

    for _, Players in pairs(game.Players:GetChildren()) do
        if Players.Name ~= game.Players.LocalPlayer.Name then
            for _, Item in pairs(Players.Backpack:GetChildren()) do
                if Item.ClassName == "Tool" and string.match(Item.Name, "Fruit") then
                    Detector:Add({
                        ["FruitName"] = Item.Name;
                        ["Owner"] = Players.Name;
                        ["Position"] = "Backpack";
                        ["IsRare"] = table.find(Cache.DevConfig["ListOfRareDveilFruit"], Item.Name);
                        ["IsFruit"] = true;
                    });
                elseif Item.ClassName == "Tool" and table.find(Cache.DevConfig["ListOfBox"], Item.Name) then
                    Detector:Add({
                        ["FruitName"] = Item.Name;
                        ["Owner"] = Players.Name;
                        ["Position"] = "Backpack";
                        ["IsRare"] = table.find(Cache.DevConfig["ListOfRareBox"], Item.Name);
                        ["IsFruit"] = false;
                    });
                end
            end

            for _, Item in pairs(Players.Character:GetChildren()) do
                if Item.ClassName == "Tool" and string.match(Item.Name, "Fruit") then
                    Detector:Add({
                        ["FruitName"] = Item.Name;
                        ["Owner"] = Players.Name;
                        ["Position"] = "Hand";
                        ["IsRare"] = table.find(Cache.DevConfig["ListOfRareDveilFruit"], Item.Name);
                        ["IsFruit"] = true;
                    });
                elseif Item.ClassName == "Tool" and table.find(Cache.DevConfig["ListOfBox"], Item.Name) then
                    Detector:Add({
                        ["FruitName"] = Item.Name;
                        ["Owner"] = Players.Name;
                        ["Position"] = "Hand";
                        ["IsRare"] = table.find(Cache.DevConfig["ListOfRareBox"], Item.Name);
                        ["IsFruit"] = false;
                    });
                end
            end
        end
    end

    for _, Item in pairs(game.Workspace:GetChildren()) do
        if Item.ClassName == "Tool" and table.find(Cache.DevConfig["ListOfBox"], Item.Name) then
            Detector:Add({
                ["FruitName"] = Item.Name;
                ["Owner"] = "None";
                ["Position"] = "Ground";
                ["IsRare"] = table.find(Cache.DevConfig["ListOfRareBox"], Item.Name);
                ["IsFruit"] = false;
            });
        end
    end

    for _, Item in pairs(game.Workspace.Trees.Tree.Model:GetChildren()) do
        if Item.ClassName == "Tool" and string.match(Item.Name, "Fruit") then
            Detector:Add({
                ["FruitName"] = Item.Name;
                ["Position"] = "Ground";
                ["IsRare"] = table.find(Cache.DevConfig["ListOfRareDveilFruit"], Item.Name);
                ["IsFruit"] = true;
            });
        end
    end

    for _, Path in pairs(game:GetService("Workspace").Island14.PedestalSpots:GetChildren()) do
        for _, Item in pairs(Path:GetChildren()) do
            if Item.ClassName == "Tool" and string.match(Item.Name, "Fruit") then
                Detector:Add({
                    ["FruitName"] = Item.Name;
                    ["Position"] = "Pedestal";
                    ["IsRare"] = table.find(Cache.DevConfig["ListOfRareDveilFruit"], Item.Name);
                    ["IsFruit"] = true;
                });
            end
        end
    end

    for _, Item in pairs(game:GetService("Workspace").Altar.FruitReceptical:GetChildren()) do
        if Item.ClassName == "Tool" and string.match(Item.Name, "Fruit") then
            Detector:Add({
                ["FruitName"] = Item.Name;
                ["Position"] = "Rebirth Pedestal";
                ["IsRare"] = table.find(Cache.DevConfig["ListOfRareDveilFruit"], Item.Name);
                ["IsFruit"] = true;
            });
        end
    end

    print("--------------------------------------->");

    for _, Value in pairs(Detector.ListOfRareFruit) do
        print(string.format("** %s **", Value));
    end
    
    for _, Value in pairs(Detector.ListOfNormalFruit) do
        print(Value);
    end

    for _, Value in pairs(Detector.ListOfRareBox) do
        print(string.format("** %s **", Value));
    end
    
    for _, Value in pairs(Detector.ListOfNormalBox) do
        print(Value);
    end
    print("<---------------------------------------");
