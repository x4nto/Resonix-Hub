local httpService = game:GetService("HttpService")
local request = (http and http.request) or http_request or request or HttpPost

local function getExecutor()
    local name, version
    if identifyexecutor then
        name, version = identifyexecutor()
    end
    return name or "Unknown", version or "N/A"
end

local lib = {}

function lib.report(s_name, s_ver, ui_ver)
    if request then
        local e_name, e_ver = getExecutor()
        local s, _ = pcall(request, {
            Url = "https://stats.sirius.menu/api/v1/events",
            Method = "POST",
            Headers = {
                ["Accept"] = "application/json",
                ["Content-Type"] = "application/json"
            },
            Body = httpService:JSONEncode({
                api_key = "c73e400c5b924302a093be14efccbe0b",
                name = "execution",
                properties = {
                    exec_name = e_name,
                    exec_version = "V"..e_ver,
                    script_name = s_name,
                    script_version = s_ver,
                    ui_version = ui_ver,
                    place_id = game.PlaceId
                }
            })
        })
        if not s then
            warn("Failed to report analytics, please contact the Sirius Development team.")
        end
	else
		warn("Failed to find required function for report, please make a ticket in our discord!")
    end
end


return lib
