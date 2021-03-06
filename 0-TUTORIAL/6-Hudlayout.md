# Hudlayout.res

Hudlayout.res controls the positioning and size of most panels (with some notable exceptions, such as health), and can be used for hud elements that are always visible ingame (notably, hud crosshairs or transparent viewmodels). It is found in the folder:
```
scripts/hudlayout.res
```

## Controlling Panels

Panels controlled by hudlayout (which is the majority of ones visible ingame) can be repositioned and resized. For example, one of the first panels inside hudlayout.res controls the ammo panel:
```
	HudWeaponAmmo
	{
		"fieldName" "HudWeaponAmmo"
		"visible" "1"
		"enabled" "1"
		"xpos"	"r95"	[$WIN32]
		"xpos_minmode"	"r85"	[$WIN32]
		"ypos"	"r55"	[$WIN32]
		"ypos_minmode"	"r36"	[$WIN32]
		"xpos"	"r131"	[$X360]
		"ypos"	"r77"	[$X360]
		"wide"	"94"
		"tall"	"45"
	}
```
If we cut out the excess, it becomes a bit more simple:
```
	HudWeaponAmmo
	{
		"fieldName" "HudWeaponAmmo"
		"visible" "1"
		"enabled" "1"
		"xpos"	"r95"
		"ypos"	"r55"
		"wide"	"94"
		"tall"	"45"
	}
```
Changing the xpos and ypos will move the ammo panel, which effectively moves everything contained in the hudammoweapons.res file.

A bit less intuitively, changing the wide and tall values will change the max size of the ammo panel. If something inside hudammoweapons.res is larger, or appears outside of that max size, it will be cut off and not visible. For this reason, some huds will choose to make their hudammoweapons.res control all positioning, and have their ammo panel in hudlayout cover the entire screen (doing this without adjusting hudammoweapons.res will result in your ammo being in the top right corner):
```
	HudWeaponAmmo
	{
		"fieldName" "HudWeaponAmmo"
		"visible" "1"
		"enabled" "1"
		"xpos"	"0"
		"ypos"	"0"
		"wide"	"f0"
		"tall"	"480"
	}
```

## Special Panels

Some panels in hudlayout don't have their own file, and are controlled entirely within hudlayout. One of the best examples of this is the killfeed (confusingly called the death notice in hudlayout):
```
	HudDeathNotice
	{
		"fieldName" "HudDeathNotice"
		"visible" "1"
		"enabled" "1"
		"xpos"	 "r640"	[$WIN32]
		"ypos"	 "18"	[$WIN32]
		"xpos"	 "r672"	[$X360]
		"ypos"	 "35"	[$X360]
		"wide"	 "628"
		"tall"	 "468"

		"MaxDeathNotices" "4"
		"IconScale"	  "0.35"
		"LineHeight"	  "16"
		"LineSpacing"	  "4"
		"CornerRadius"	  "3"
		"RightJustify"	  "1"	// If 1, draw notices from the right
		
		"TextFont"		"Default"
		
		"TeamBlue"		"HUDBlueTeamSolid"
		"TeamRed"		"HUDRedTeamSolid"
		"IconColor"		"HudWhite"
		"LocalPlayerColor"	"HUDBlack"

		"BaseBackgroundColor"	"46 43 42 220"		[$WIN32]
		"LocalBackgroundColor"	"245 229 196 200"	[$WIN32]
		"BaseBackgroundColor"	"32 32 32 255"		[$X360]
		"LocalBackgroundColor"	"0 0 0 255"		[$X360]
	}
```
As you notice, there is a lot here that doesn't exist on any other panel. The xpos, ypos, wide, tall all control the panel positioning and bounds, like it did with ammo.