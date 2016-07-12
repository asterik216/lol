if GetObjectName(GetMyHero()) ~= "Riven" then return end

local ver = "0.17"

if not FileExist(COMMON_PATH.. "Analytics.lua") then
  DownloadFileAsync("https://raw.githubusercontent.com/LoggeL/GoS/master/Analytics.lua", COMMON_PATH .. "Analytics.lua", function() end)
end

require("Analytics")

Analytics("Eternal Riven", "Toshibiotro", true)
    end
end


require ("DamageLib")
require ("OpenPredict")
require("MapPositionGOS")

if FileExist(COMMON_PATH.."MixLib.lua") then
 require('MixLib')
else
 PrintChat("MixLib not found. Please wait for download.")
 DownloadFileAsync("https://raw.githubusercontent.com/VTNEETS/NEET-Scripts/master/MixLib.lua", COMMON_PATH.."MixLib.lua", function() PrintChat("Downloaded MixLib. Please 2x F6!") return end)
end

local RivenMenu = Menu("Riven", "Riven")
RivenMenu:SubMenu("Combo", "Combo")
RivenMenu.Combo:Boolean("CQ", "Use Q", true)
RivenMenu.Combo:Boolean("CW", "Use W", true)
RivenMenu.Combo:Boolean("CE", "Use E", true)
RivenMenu.Combo:Boolean("CR", "Use R", true)
RivenMenu.Combo:Slider("RC", "Min Enemy HP to Cast R",60,1,100,1)
RivenMenu.Combo:Boolean("CH", "Use R Hydra", true)
RivenMenu.Combo:Boolean("CTH", "Use T Hydra", true)
RivenMenu.Combo:Boolean("YGB", "Use GhostBlade", true)


local skinMeta = {["Riven"] = {"Classic", "Redeemed", "Crimson Elite", "Battle Bunny", "Championship", "Dragonblade", "Arcade"}}
RivenMenu.SkinChanger:DropDown('skin', myHero.charName.. " Skins", 1, skinMeta[myHero.charName], HeroSkinChanger, true)
RivenMenu.SkinChanger.skin.callback = function(model) HeroSkinChanger(myHero, model - 1) print(skinMeta[myHero.charName][model] .." ".. myHero.charName .. " Loaded!") end

function WDmg(unit) return CalcDamage(myHero,unit, 20 + 30 * GetCastLevel(myHero,_W) + GetBonusDmg(myHero) * 1, 0) end
function QDmg(unit) return CalcDamage(myHero,unit, -10 + 20 * GetCastLevel(myHero,_Q) + (myHero.totalDamage) * ((35 + 5 * GetCastLevel(myHero, _Q)) * 0.01), 0) end
function AAB(unit) return CalcDamage(myHero, unit, myHero.totalDamage + (myHero.totalDamage * 0.25)) end
function EShield(myHero) return (60 + 30 * GetCastLevel(myHero, _E) + GetBonusDmg(myHero)) end
local RStats = {delay = 0.025, range = 1100, radius = 100, speed = 1600}
local QCast = 0
local target = GetCurrentTarget()
local UltOn = GetCastName(myHero, _R):lower():find("rivenizunablade")
local Move = {delay = 0.5, speed = math.huge, width = 50, range = math.huge}

OnTick(function ()
	
	local movePos = GetPrediction(target,Move).castPos
	local mousePos = GetMousePos()
	target = GetCurrentTarget()
	local IDamage = (50 + (20 * GetLevel(myHero)))
	local RDmg = getdmg("R",target,myHero,GetCastLevel(myHero, _R))
	local YGB = GetItemSlot(myHero, 3142)
	local RHydra = GetItemSlot(myHero, 3074)
	local Tiamat = GetItemSlot(myHero, 3077)
	UltOn = GetCastName(myHero, _R):lower():find("rivenizunablade")
	
	if RivenMenu.Misc.AL.UAL:Value() and RivenMenu.Misc.AL.ALQ:Value() and not RivenMenu.Misc.AL.ALE:Value() then
		spellorder = {_Q, _E, _W, _Q, _Q, _R, _Q, _E, _Q, _E, _R, _E, _E, _W, _W, _R, _W, _W}	
		if GetLevelPoints(myHero) > 0 then
			LevelSpell(spellorder[GetLevel(myHero) + 1 - GetLevelPoints(myHero)])
		end
	end
	
	if RivenMenu.Misc.AL.UAL:Value() and RivenMenu.Misc.AL.ALE:Value() and not RivenMenu.Misc.AL.ALQ:Value() then
		spellorder = {_E, _Q, _W, _E, _E, _R, _E, _Q, _E, _Q, _R, _Q, _Q, _W, _W, _R, _W, _W}
		if GetLevelPoints(myHero) > 0 then
			LevelSpell(spellorder[GetLevel(myHero) + 1 - GetLevelPoints(myHero)])
		end
	end	
	
	if Mix:Mode() == "Combo" then
	
		if RivenMenu.Combo.CR:Value() and Ready(_R) and ValidTarget(target, 600) and not UltOn then
			if Ready(_Q) and GetCurrentHP(target) >= RivenMenu.Combo.RC:Value() or EnemiesAround(myHero, 700) > 1 then
				CastSpell(_R)
			end
		end	
		
		if RivenMenu.Combo.YGB:Value() and YGB > 0 and Ready(YGB) and ValidTarget(target, 600) then
			CastSpell(YGB)
		end
		
		if RivenMenu.Combo.CW:Value() and Ready(_W) and ValidTarget(target, GetCastRange(myHero, _W)) then
			CastSpell(_W)
		end

		if RivenMenu.Combo.CE:Value() and Ready(_E) and ValidTarget(target, 325) then
			CastSkillShot(_E, mousePos)
		end	
	end	


				end
			end
		end
	end

	if GetTeam(unit) == 300 and spell.name:lower():find("attack") and spell.target.isMe then
		if Mix:Mode() == "LaneClear" then
			if RivenMenu.JungleClear.JCE:Value() and Ready(_E) then
				CastSkillShot(_E, GetMousePos())
			end
		end	
	end
	
	if RivenMenu.Combo.CH:Value() and unit.isMe and spell.name:lower():find("attack") then
		if Mix:Mode() == "Combo" or Mix:Mode() == "Harass" then
			if RH > 0 then
				if Ready(RH) and ValidTarget(target, 400) then
					CastSpell(RH)
				end
			end
		end	
	end
	
	if RivenMenu.Combo.CH:Value() and unit.isMe and spell.name:lower():find("attack") then
		if Mix:Mode() == "Combo" or Mix:Mode() == "Harass" then
			if Tiamat > 0 then
				if Ready(Tiamat) and ValidTarget(target, 350) then
					CastSpell(Tiamat)
				end
			end
		end	
	end

	if unit.isMe and spell.name:lower():find("itemtiamatcleave") then
		Mix:ResetAA()
	end	
end)

OnProcessSpellComplete(function(unit,spell)

	local TH = GetItemSlot(myHero, 3748)

	if RivenMenu.Combo.CTH:Value() and unit.isMe and spell.name:lower():find("attack") and spell.target.isHero then
		if Mix:Mode() == "Combo" then
			if TH > 0 then 
				if Ready(TH) and GetCurrentHP(target) > CalcDamage(myHero, target, myHero.totalDamage + (GetMaxHP(myHero) / 10), 0) then
					CastSpell(TH)
					DelayAction(function()
						AttackUnit(spell.target)
					end, spell.windUpTime)
				end
			end
		end
	end
	
	if unit.isMe and spell.name:lower():find("attack") and spell.target.isHero then
		if Mix:Mode() == "Combo" or Mix:Mode() == "Harass" then
			if RivenMenu.Combo.CQ:Value() and Ready(_Q) and ValidTarget(target, GetCastRange(myHero, _Q)) then
				CastSkillShot(_Q, target)	
			end
		end
	end
	
	if unit.isMe and spell.name:lower():find("rivenfengshuiengine") then
		DelayAction(function()
			if WindWall == nil or GetDistance(myHero, WindWall) > 1100 then
				CastSkillShot(_R, target)
			end		
		end, 14.9)
	end	
end) 


OnCreateObj(function(object)
	if RivenMenu.Misc.GSQ:Value() then
		if object and GetObjectBaseName(object) and GetOrigin(object) and GetDistance(object) < 1000 then
			if GetObjectBaseName(object):find("Riven_Base_Q_") and GetObjectBaseName(object):find("_detonate") and GetDistance(object) < 225 then
				if Mix:Mode() == "Combo" or	Mix:Mode() == "Harass" or Mix:Mode() == "LaneClear" then
					CastEmote(EMOTE_DANCE)
					for delay = 15,(GetLatency()*2.5) do
						DelayAction(function()
							Mix:ResetAA()
						end, delay)
					end	
				end	
			end
		end
	end
	
	if object.isSpell and object.spellName:lower():find("yasuowmovingwallmisl") and object.spellOwner.team == 300 - GetTeam(myHero) then
        WindWall = object
    end
end)

OnDeleteObj(function(object)
	if object.isSpell and object.spellName:lower():find("yasuowmovingwallmisl") and object.spellOwner.team == 300 - GetTeam(myHero) then
        WindWall = nil
	end
end)	

OnUpdateBuff(function(unit,buff)
	if unit.isMe and buff.Name:lower():find("riventricleave") then 
		QCast = buff.Count
	end
end)

OnRemoveBuff(function(unit,buff)
	if unit.isMe and buff.Name:lower():find("riventricleave") then 
		QCast = 0
	end
end)		

OnProcessWaypoint(function(unit, waypointProc)
	if unit.isHero and waypointProc.dashspeed > unit.ms and not unit.isMe and unit.team == 300 - myHero.team then
		local dashTargetPos = waypointProc.position
		if RivenMenu.AGC.AGCW:Value() then	
			if GetDistance(myHero, dashTargetPos) < GetCastRange(myHero, _W) and Ready(_W) then
				DelayAction(function()
					CastSpell(_W)
				end, (GetDistance(myHero, unit) / waypointProc.dashspeed) - 0.267)	
			end	
		end
	end
end)

print("Thank You For Using Eternal Riven, Have Fun :D")
