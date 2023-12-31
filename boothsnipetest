local osclock = os.clock()
repeat task.wait() until game:IsLoaded()

setfpscap(10)
game:GetService("RunService"):Set3dRenderingEnabled(false)
local Booths_Broadcast = game:GetService("ReplicatedStorage").Network:WaitForChild("Booths_Broadcast")
local Players = game:GetService('Players')
local getPlayers = Players:GetPlayers()
local PlayerInServer = #getPlayers
local http = game:GetService("HttpService")
local ts = game:GetService("TeleportService")
local rs = game:GetService("ReplicatedStorage")
local playerID

if not snipeNormalPets then
    snipeNormalPets = false
end

local vu = game:GetService("VirtualUser")
Players.LocalPlayer.Idled:connect(function()
   vu:Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
   task.wait(1)
   vu:Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
end)

for i = 1, PlayerInServer do
   for ii = 1,#alts do
        if getPlayers[i].Name == alts[ii] and alts[ii] ~= Players.LocalPlayer.Name then
            jumpToServer()
        end
    end
end

local function processListingInfo(uid, gems, item, version, shiny, amount, boughtFrom, boughtStatus, mention)
    local gemamount = Players.LocalPlayer.leaderstats["💎 Diamonds"].Value
    local snipeMessage ="||".. Players.LocalPlayer.Name .. "||"
    local weburl, webContent, webcolor
    if version then
        if version == 2 then
            version = "Rainbow "
        elseif version == 1 then
            version = "Golden "
        end
    else
       version = ""
    end

    if boughtStatus then
	    webcolor = tonumber(0x00ff00)
	    weburl = webhook
        snipeMessage = snipeMessage .. " CALDI!! "
	    if mention then 
            webContent = "<@".. userid ..">"
        else
	        webContent = ""
	    end
	    if normalwebhook then
	        weburl = normalwebhook
	    end
    else
	    webcolor = tonumber(0xff0000)
	    weburl = webhookFail
	    snipeMessage = snipeMessage .. " failed to snipe a "
    end
    
    snipeMessage = snipeMessage .. "**" .. version
    
    if shiny then
        snipeMessage = snipeMessage .. " Shiny "
    end
    
    snipeMessage = snipeMessage .. item .. "**"
    
    local message1 = {
        ['content'] = webContent,
        ['embeds'] = {
            {
		        ["author"] = {
			        ["name"] = "Erdogan",
			        ["icon_url"] = "https://cdn.discordapp.com/attachments/828296500513341452/1190667547079610368/indir.jpg?ex=65a2a290&is=65902d90&hm=b8b7df3148c306cd3b117f70d435b35e10eb1444dddfa1f0a72e9a5eb89ebca8&",
		        },
                ['title'] = snipeMessage,
                ["color"] = webcolor,
                ["timestamp"] = DateTime.now():ToIsoDate(),
                ['fields'] = {
                    {
                        ['name'] = "__Price:__",
                        ['value'] = tostring(gems) .. " 💎",
                    },
                    {
                        ['name'] = "__Bought from:__",
                        ['value'] = "||"..tostring(boughtFrom).."|| ",
                    },
                    {
                        ['name'] = "__Amount:__",
                        ['value'] = tostring(amount) .. "x"
                    }
                }
            }
        }
    }
    
    local message2 = {
        ['content'] = webContent,
        ['embeds'] = {
            {
		        ["author"] = {
			        ["name"] = "Erdogan",
			        ["icon_url"] = "https://cdn.discordapp.com/attachments/828296500513341452/1190667547079610368/indir.jpg?ex=65a2a290&is=65902d90&hm=b8b7df3148c306cd3b117f70d435b35e10eb1444dddfa1f0a72e9a5eb89ebca8&",
		        },
                ['title'] = snipeMessage,
                ["color"] = webcolor,
                ["timestamp"] = DateTime.now():ToIsoDate(),
                ['fields'] = {
                    {
                        ['name'] = "__Price:__",
                        ['value'] = tostring(gems) .. " 💎",
                    },
                    {
                        ['name'] = "__Bought from:__",
                        ['value'] = "||"..tostring(boughtFrom).."|| ",
                    },
                    {
                        ['name'] = "__Amount:__",
                        ['value'] = tostring(amount) .. "x"
                    }
                }
            }
        }
    }
    
    local encodeMessage1 = http:JSONEncode(message1)
    local encodeMessage2 = http:JSONEncode(message2)
    
    http:PostAsync(weburl, encodeMessage1)
    http:PostAsync(weburl, encodeMessage2)
end
