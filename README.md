# UIAtlasItemIcons
UIAtlas icons converted to ItemIcons

To use the icons add the UIAtlasItemIcons folder to your games Mods folder (or add the contents of the ItemIcons folder to your own mod's ItemIcons)

v1.0.0 contains the following icons, which are all of the icons used in the vanilla buffs.xml for alpha 15.0 (more will be added as time permits)
* ui_game_symbol_beer
* ui_game_symbol_brokenbone
* ui_game_symbol_campfire
* ui_game_symbol_coffee
* ui_game_symbol_cold
* ui_game_symbol_critical
* ui_game_symbol_death
* ui_game_symbol_drunk
* ui_game_symbol_dysentery
* ui_game_symbol_fire
* ui_game_symbol_food_poisoning
* ui_game_symbol_hot
* ui_game_symbol_hunger
* ui_game_symbol_infection
* ui_game_symbol_map_bed
* ui_game_symbol_medical
* ui_game_symbol_natural_healing
* ui_game_symbol_oxygen
* ui_game_symbol_pills
* ui_game_symbol_radiation
* ui_game_symbol_run
* ui_game_symbol_skull
* ui_game_symbol_smell
* ui_game_symbol_splint
* ui_game_symbol_stunned
* ui_game_symbol_tea
* ui_game_symbol_thirst
* ui_game_symbol_wet


To use these icons and also be able to use any icons from the ItemIcon atlas (and icons added the ItemIcons folder in a mod within the Mods folder) **atlas="ItemIconAtlas"** needs to be added in 3 places.

If buffs.xml you can for example change icon="ui_game_symbol_drunk" to icon="beer" and it will use the icon for the beer item. Note that the icon will get squished flat a bit. If you want the aspect ratio to be correct, the icon should be 64x64 pixels at the shape you want, then resize the icon to 116x80 and save as a .png to your Mods/Modname/ItemIcons folder.

Replace the **BuffPopoutList** window with the following (in windows.xml):

```
		<rect name="hud" pos="93,124" side="left" controller="BuffPopoutList" pivot="BottomLeft" >
			<panel width="168" height="43" name="item" visible="false" pivot="right" disableautobackground="true" pos="70, 0" >
				<sprite depth="3" pos="0,0" name="Background" sprite="ui_game_popup" height="43" width="162" pivot="center" flip="Horizontally" color="[transparent]" />
				<sprite depth="4" name="Icon" atlas="ItemIconAtlas" size="36,32" pos="-58,0" pivot="center" color="[transparent]"/>
				<label depth="6" name="TextContent" pos="0,0" font_size="28" color="[white]" justify="center" height="30" pivot="center"/>
			</panel>
		</rect>
```

Replace the **buffInfoPanel** window with the following (in windows.xml):

```
  <window name="buffInfoPanel" width="603" height="427" controller="BuffInfoWindow" anchor="CenterTop" panel="Center">
    <panel name="header" height="43" depth="1" backgroundspritename="ui_game_panel_header">
      <sprite depth="2" name="windowIcon" style="icon32px" pos="4,-5" atlas="ItemIconAtlas" sprite="{bufficon|once}"/>
      <label style="header.name" text="{buffname|once}"/>
    </panel>
    <rect name="contentBuffInfo" height="381" depth="1" pos="0,-46">
      <rect>
        <sprite depth="5" name="backgroundMain" sprite="menu_empty3px" width="603" height="381" color="[black]" type="sliced" fillcenter="false"/>
        <sprite depth="1" name="background" color="[black]" type="sliced" visible="false" sprite="menu_empty3px" fillcenter="false"/>
        <sprite depth="8" name="backgroundMain" sprite="menu_empty3px" pos="0,0" width="153" height="153" color="[black]" type="sliced" fillcenter="false"/>
        <sprite depth="1" pos="2,-3" name="preview" width="150" height="148" color="[darkGrey]" type="sliced"/>
        <sprite depth="3" name="itemPreview" width="100" height="100" atlas="ItemIconAtlas" sprite="{bufficon|once}" pos="27,-27" foregroundlayer="true"/>
        <sprite depth="8" name="backgroundMain" sprite="menu_empty3px" pos="0,-150" width="153" height="231" color="[black]" type="sliced" fillcenter="false"/>
        <grid name="itemActions" rows="4" cols="1" pos="3,-153" width="148" height="100%" cell_width="147" cell_height="42" controller="ItemActionList" repeat_content="true">
          <item_action_entry/>
        </grid>
        <sprite depth="3" name="fillerBackground" pos="3,-321" height="57" width="147" color="[mediumGrey]" type="sliced"/>
        <rect depth="1" pos="153,-3" name="description" width="447" height="195">
          <sprite depth="3" name="backgroundMain" sprite="menu_empty3px" pos="-3,3" width="453" height="201" color="[black]" type="sliced" fillcenter="false"/>
          <sprite depth="1" color="[mediumGrey]" type="sliced" globalopacity="true"/>
          <label depth="3" name="statText" pos="5,-6" width="443" text="{buffstats}"/>
        </rect>
        <rect depth="2" pos="153,-200" name="description" width="447" height="104">
          <sprite depth="1" color="[darkGrey]" type="sliced" globalopacity="true"/>
          <label depth="3" name="descriptionText" pos="6,-5" text="{buffdescription|once}" width="440"/>
        </rect>
        <grid rows="1" cols="6" pos="153,-306" cell_width="75" cell_height="75" repeat_content="true" controller="BuffItemList">
          <buff_item name="0"/>
        </grid>
      </rect>
    </rect>
  </window>
```

Finally replace **active_buff_entry** with the following (in controls.xml):

```
  <active_buff_entry>
    <panel height="43" controller="ActiveBuffEntry" width="314" style="press" sound="[recipe_click]" on_hover="true" disableautobackground="true" on_scroll="true">
      <sprite depth="2" name="backgroundMain" sprite="menu_empty3px" pos="-3,3" width="320" height="49" color="[black]" type="sliced" fillcenter="false"/>
      <sprite depth="0" name="background" color="[darkGrey]" type="sliced" height="45" width="316" pos="-1,1"/>
      <sprite depth="2" name="Icon" atlas="ItemIconAtlas" sprite="{bufficon|once}" style="icon32px" pos="5,-5"/>
      <label depth="2" pos="45,-8" width="280" height="30" text="{buffname|once}  [DECEA3]{buffdisplayinfo}[-]" font_size="28" pivot="topleft"/>
    </panel>
  </active_buff_entry>
```

Credit for the **atlas="ItemIconAtlas"** changes to Alphado-Jaki, DnaJur and n2n1.
