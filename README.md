# Free Key System UI
Simple free key system (because of that obfuscated)

Created in 1 hour

- Draggable (pc only)
- Save Key
- Animations
- Debug mode
- Environment check
- Very fast

*All verification is on your script side (cracking by lib side is impossible)*

##	▶ Screenshots ◀
![Screenshot 1](https://github.com/OopssSorry/LuaU-Free-Key-System-UI/blob/main/image1.png)
![Screenshot 2](https://github.com/OopssSorry/LuaU-Free-Key-System-UI/blob/main/image2.png)

**Supported Services:**
- [Key Guardian](https://github.com/OopssSorry/LuaU-Free-Key-System-UI?tab=readme-ov-file#-for-keyguardian-)
- [KeyRBLX](https://github.com/OopssSorry/LuaU-Free-Key-System-UI?tab=readme-ov-file#-for-keyrblx-)
- Pelican Development *soon*

##	▶ Example ◀
```lua
local KeySystem = loadstring(game:HttpGet("https://raw.githubusercontent.com/OopssSorry/LuaU-Free-Key-System-UI/main/source.lua"))()
local KeyValid = false
local response = KeySystem:Init({
	Debug=false, -- <bool> Prints some output in console when true
	Title="ExampleHub | Key System", -- <string or nil> Title of key system
	Description=nil, -- <string or nil> Description of key system
	Link="", -- <string> String to get key
	Discord="test", -- <string or nil> Button to join your discord server
	SaveKey=false, -- <bool or nil> Just auto save key
	Verify=function(key) -- <function> Verify is key valid
		if key=="1234" then
      KeyValid=true
			return true
		else
			return false
		end
	end,
	GuiParent = game.CoreGui, -- <object or nil> :3
})

if not response or not KeyValid then return end
-- HERE YOUR SCRIPT
```

##	▶ [For KeyGuardian](https://keyguardian.org) ◀
```lua
local KeyValid,KeyPremium, KeysystemLibrary, KeyGuardLibrary = false,false,loadstring(game:HttpGet("https://raw.githubusercontent.com/OopssSorry/LuaU-Free-Key-System-UI/main/source.lua"))(),loadstring(game:HttpGet("https://cdn.keyguardian.org/library/v1.0.0.lua"))()

KeyGuardLibrary.Set({
	publicToken = "your publicToken",
	privateToken = "your privateToken",
	trueData = "your trueData",
	falseData = "your falseData",
})

-- https://github.com/OopssSorry/LuaU-Free-Key-System-UI
local KSresponse = KeysystemLibrary:Init({
	Title="ExampleHub",  -- TITLE HERE
	
	SaveKey=true, 
	Debug=false, 
	Link=KeyGuardLibrary.getLink(), 
	Verify=function(key) 
		if KeyGuardLibrary.validateDefaultKey(key) then
			KeyValid=true
		elseif KeyGuardLibrary.validatePremiumKey(key) then
			KeyValid,KeyPremium=true,true
		end;
		return KeyValid
	end,
}) 

-- return nil on closing key system
if not KSresponse or not KeyValid then return end 

-- YOUR SCRIPT HERE

-- Example of checking is user have a premium:
if KeyPremium then
	print("Key is premium!")
end
```

##	▶ [For KeyRBLX](https://keyrblx.com) ◀
```lua
local HashLibrary = loadstring(game.HttpGet("https://raw.githubusercontent.com/Egor-Skriptunoff/pure_lua_SHA/master/sha2.lua"))()
local KeyValid,KeyPremium, KeysystemLibrary, KeyRblx = false,false,loadstring(game:HttpGet("https://raw.githubusercontent.com/OopssSorry/LuaU-Free-Key-System-UI/main/source.lua"))(), loadstring(game.HttpGet("https://raw.githubusercontent.com/MaGiXxScripter0/keysystemv2api/master/version2_1.lua"))()

local true_ = HashLibrary.sha1("YourTrueData")
local false_ = HashLibrary.sha1("YourFalseData")

-- https://github.com/OopssSorry/LuaU-Free-Key-System-UI
local KSresponse = KeysystemLibrary:Init({
	Title="ExampleHub",  -- TITLE HERE
	
	SaveKey=true, 
	Debug=false, 
	Link=KeyGuardLibrary.getLink(), 
	Verify=function(key) 
		local def, prem = KeyRblx.VerifyDefaultKey(key), KeyRblx.VerifyPremiumKey(key)
		def, prem = KeyLibrary.XORDecode(def), KeyLibrary.XORDecode(prem)
		if true_==def then
			KeyValid=true
		elseif true_==prem then
			KeyValid,KeyPremium=true,true
		end;
		return KeyValid
	end,
}) 

-- return nil on closing key system
if not KSresponse or not KeyValid then return end 

-- YOUR SCRIPT HERE

-- Example of checking is user have a premium:
if KeyPremium then
	print("Key is premium!")
end
```
