## functions
* **[log(string)](#log)**
* **[sleep(int ms)](#sleep)**
* **[printps(string)](#printps)**
* **[set_fps_limit(float)](#set_fps_limit)**
* **[send_packet(int type, string packet)](#send_packet)**
* **[send_packet_raw(table game_packet_t, bool to_client = false)](#send_packet_raw)**
* **[get_ping()](#get_ping)**
* **[get_world()](#get_world)**
* **[get_players()](#get_players)**
* **[get_inventory()](#get_inventory)**
* **[get_local_player()](#get_local_player)**
* **[get_item_info_manager()](#get_item_info_manager)**
* **[warp(string world name)](#warp)**
* **[drop(int item_id, int count)](#drop)**
* **[say(string text)](#say)**

**World & player info**
* **[get_tile(int x, int y)](#get_tile)**
* **[get_tiles([table item_ids])](#get_tiles)**
* **[get_player_info(int user_id)](#get_player_info)**
* **[get_object_info(int unique_id)](#get_object_info)**
* **[get_objects(int x, int y)](#get_objects)**
* **[get_gems_count(int x, int y)](#get_gems_count)**
* **[has_world_access()](#has_world_access)**
* **[has_any_access()](#has_any_access)**
* **[reconnect()](#reconnect)**
* **[get_item_count(int item_id)](#get_item_count)**
* **[get_inventory_item(int item_id)](#get_inventory_item)**
* **[get_item_info(int item_id)](#get_item_info)**
* **[get_item_info_by_name(string name)](#get_item_info_by_name)**

**Actions**
* **[paint_tile(int x, int y, int color)](#paint_tile)**
* **[highlight_tile(int x, int y)](#highlight_tile)**
* **[item_activate(int item_id)](#item_activate)**
* **[send_punch(int x, int y)](#send_punch)**
* **[enter_door(int x, int y)](#enter_door)**
* **[remove_item(int item_id, int count)](#remove_item)**
* **[dropall([string type])](#dropall)**
* **[collect([int range])](#collect)**
* **[wear_visual(int item_id)](#wear_visual)**
* **[set_wear_visual(int item_id, bool worn)](#set_wear_visual)**
* **[is_wearing_visual(int item_id)](#is_wearing_visual)**

**Effects & feedback**
* **[on_text_overlay(string text)](#on_text_overlay)**
* **[on_add_notification(string text)](#on_add_notification)**
* **[on_talk_bubble(string text)](#on_talk_bubble)**
* **[on_particle_effect(int id, vec2f pos [, int count])](#on_particle_effect)**

**Packets, variants & misc**
* **[send_varlist(table varlist [, int netid])](#send_varlist)**
* **[send_country_state(string badge)](#send_country_state)**
* **[get_vec2i(int x, int y)](#get_vec2i)**
* **[get_vec2f(float x, float y)](#get_vec2f)**
* **[add_log(string text)](#add_log)**
* **[srand()](#srand)**
* **[run_file([string file_name])](#run_file)**
* **[stop_file([string file_name])](#stop_file)**

> Most functions have an alias with the same meaning — lowerCamel (`getWorld`) and/or PascalCase
> (`GetWorld`). The aliases are listed under each function below.

### log
```lua
-- logs to growtopia console
log("Hello Nora!")
```

### sleep
```lua
sleep(1337) -- sleeps 1337 milliseconds
```

### printps
```lua
-- prints to console colorful like growtopia's game console
printps("`9Hello `@Nora```c!``.")
```

### set_fps_limit
```lua
-- sets fps limit of growtopia app
set_fps_limit(90) -- sets max fps to 90
set_fps_limit(0) -- sets max fps unlimited
```

### send_packet
```lua
-- sends packet to game
send_packet(2, "action|input\n|text|Hello Nora!")
```

### send_packet_raw
```lua
-- sends raw packet to game
packet = {}
packet.type = game_packet_type.state -- or packet.type_int = 0
packet.flags = packet_flag.facing_right -- or packet.flags_int = 48
send_packet_raw(packet) 
```

### get_ping
**aliases:** `GetPing`
```lua
-- logs your connection ping
log("`9your current ping:`` `@" .. get_ping() .. "``.")
```

### get_world
**aliases:** `getWorld`, `GetWorld`
```lua
-- logs your world name
log("`9current world name:`` `@" .. get_world().name .. "``.")
```

### get_players
**aliases:** `GetPlayers`
```lua
-- prints players name in world
for _, player in ipairs(get_players()) do
    printps(player.name)
end
```

### get_inventory
**aliases:** `GetInventory`
```lua
-- prints inventory item's id and count
for _, item in ipairs(get_inventory()) do
    printps("item id, count: " .. item.item_id ..", ".. item.count)
end
```

### get_local_player
**aliases:** `getLocalPlayer`, `GetLocalPlayer`
```lua
-- logs local player name
log("`9local player name:`` `@" .. get_local_player().name .. "``.")
```

### get_item_info_manager
**aliases:** `GetItemInfoManager`
```lua
-- logs item id (2) name 'Dirt' 
item_info_manager = get_item_info_manager()
log("`9item id (2) name:`` `@" .. item_info_manager.get_item(2).name .. "``.")
```

### warp
```lua
-- warps to world
warp("norabetter")
```

### drop
```lua
-- drops all inventory
item_info_manager = get_item_info_manager()
for _, item in ipairs(get_inventory()) do
     item_info = item_info_manager.get_item(item.item_id)
     if item_info.flags ~= item_flag.untradeable then -- checks item untradeable or not
        drop(item.item_id, item.count)
     end
end
```

### say
**aliases:** `chat`, `talk`, `Chat`, `Talk`

Says something in the world.
```lua
say("hello")
chat("hello") -- same function
```

---

## World & player info

### get_tile
**aliases:** `getTile`, `GetTile`

Returns the [tile_t](structs.md#tile_t) at `x, y`, or `nil` when there is no world or no tile there.
```lua
-- gets the tile at x, y (same as get_world().tile_map:get_tile(x, y))
local tile = get_tile(5, 7)
if tile ~= nil then
    printps("foreground id: " .. tile.fg .. ", flags: " .. tile.flags)
end
```

> The result points at the live tile, not a copy — read what you need from it, do not hold it across
> a world change.

### get_tiles
**aliases:** `getTiles`, `GetTiles`

Every tile whose foreground **or** background matches one of the ids in `item_ids`. With no argument
it returns every tile in the world.
```lua
for _, tile in ipairs(get_tiles({ 756 })) do   -- all dice
    printps("dice at " .. tile.pos.x .. ", " .. tile.pos.y)
end
get_tiles() -- every tile in the world
```

> Each call returns fresh **copies** of the tiles, so what you get is a snapshot taken when you
> called it, and a script that calls this in a loop grows the game's memory. Prefer `get_tile(x, y)`
> when you only need one tile, and do not call `get_tiles()` with no argument inside a loop.

### get_player_info
**aliases:** `getPlayerInfo`
```lua
-- returns the player with that user id, or nil if they are not in the world
local player = get_player_info(123456)
if player ~= nil then
    printps(player.name .. " is here, country: " .. player.country)
end
```

### get_object_info
**aliases:** `getObjectInfo`

Returns an `object_t` (`world_object_t` in the docs), or `nil`.
```lua
local object = get_object_info(oid) -- oid as printed by object.oid
if object ~= nil then
    printps("object id: " .. object.id .. ", count: " .. object.count)
end
```

### get_objects
**aliases:** `getObjects`

Returns every `object_t` standing on the tile `x, y`.
```lua
-- prints what is lying on tile (10, 10)
for _, object in ipairs(get_objects(10, 10)) do
    printps("object id: " .. object.id .. ", count: " .. object.count)
end
```

### get_gems_count
**aliases:** `getGemsCount`

Gems summed over the **whole tile** at `x, y` (not just one drop).
```lua
-- prints the gems on tile (12, 4)
printps("`9gems on tile:`` `@" .. get_gems_count(12, 4) .. "``.")
```

### has_world_access
**aliases:** `hasWorldAccess`, `HasWorldAccess`
```lua
-- true when you have build access on the current world
if has_world_access() then
    printps("`2you can build here``")
end
```

### has_any_access
**aliases:** `hasAnyAccess`, `HasAnyAccess`

True for build access **or** wrench access.
```lua
if has_any_access() then
    printps("`2you have access``")
end
```

### reconnect
**aliases:** `Reconnect`, `reconnect_server`

Re-sends the login redirect the client captured (`OnSendToServer`).
```lua
reconnect()
```

### get_item_count
**aliases:** `getItemCount`, `GetItemCount`

Count of an item in your inventory, taken from the item manager.
```lua
printps("`9dirt:`` `@" .. get_item_count(2) .. "``.")
```

### get_inventory_item
```lua
local item = get_inventory_item(2)
if item ~= nil then
    printps("dirt: " .. item.count)
end
```

### get_item_info
```lua
local info = get_item_info(2)
if info ~= nil then
    printps("id 2 is " .. info.name)
end
```

### get_item_info_by_name
```lua
local info = get_item_info_by_name("Dirt")
if info ~= nil then
    printps("Dirt's id is " .. info.id)
end
```

---

## Actions

> Coordinates below are **tile** coordinates, `x, y`.

### paint_tile
**aliases:** `paintTile`, `PaintTile`

Takes a number or a `tile_flag` value.
```lua
paint_tile(5, 7, tile_flag.red)   -- same as paint_tile(5, 7, 0x2000)
paint_tile(5, 7, tile_flag.green)
```

> **Client side only.** This changes the tile colour on *your* screen. It does not change the world
> for anyone else and the server is never told. It also does nothing if there is no tile at `x, y`.

### highlight_tile
**aliases:** `highlightTile`, `HighlightTile`

Selects a tile the way clicking it does.
```lua
highlight_tile(5, 7)
```

> Also client side only — nothing is sent to the server.

### item_activate
**aliases:** `item_active`, `activate_item`, `ActivateItem`, `ItemActivate`

Uses an item from your inventory (this one is a real server request).
```lua
item_activate(2) -- uses dirt
```

### send_punch
**aliases:** `punch_tile`
```lua
send_punch(5, 7)
```

> Not the same as `punch(x, y)`, which places item 18 (the fist) with `place`.

### enter_door
```lua
enter_door(5, 7)
```

### remove_item
```lua
remove_item(2, 200) -- removes 200 dirt from the inventory view
```

### dropall
**aliases:** `dropAll`, `DropAll`

Known types: `none`, `seeds`, `surgery`, `crime`, `cards`, `startopia`, `clothes`.
```lua
dropall("seeds")
dropall() -- everything
```

### collect
Picks up dropped items around you.
```lua
collect(3)  -- within 3 tiles
collect()   -- uses the collect range from the settings
```

### wear_visual
**aliases:** `wear`, `Wear`

> **Toggles** the item, and only for your own client.

```lua
wear_visual(2150)
```

### set_wear_visual
Wears or removes the item in both directions (idempotent) and asks the server to do it, so other
players see it. Refuses to wear an item you do not own.
```lua
set_wear_visual(2150, true)  -- wear
set_wear_visual(2150, false) -- remove
```

### is_wearing_visual
```lua
if is_wearing_visual(2150) then
    printps("`9you are wearing it``")
end
```

---

## Effects & feedback

### on_text_overlay
```lua
on_text_overlay("`2hello world``")
on_text_overlay("`2hello``", net_id) -- as if that player said it
```

### on_add_notification
```lua
on_add_notification("`9something happened``")
```

### on_talk_bubble
```lua
on_talk_bubble("hi")
```

### on_particle_effect
```lua
on_particle_effect(181, get_local_player().pos)              -- gems above you
on_particle_effect(181, vec2f.new(320.0, 640.0), 25)         -- with a count
```

---

## Packets, variants & misc

### send_varlist
**aliases:** `sendVarlist`, `send_variantlist`, `send_variant_list`, `send_var_list`, `send_vl`,
`send_variant`, `SendVariantList`, `SendVarList`
```lua
varlist = {}
varlist[0] = "OnTextOverlay"
varlist[1] = "`2sent from lua``"
send_varlist(varlist)
```

> This does **not** go to the server: it is handed back to the client's own packet handler, so it
> triggers client side handlers (overlays, dialogs, effects) for you only.

### send_country_state
**aliases:** `send_badge`, `sendBadge`, `set_country_state`, `setCountryState`, `sendCountryState`

Sets the badge shown next to your name. A raw token is accepted with or without the wrapper:
```lua
send_country_state("donor")           -- wrapped to country|showGuild|donor for you
send_country_state("|showGuild|donor")
send_country_state(nil)               -- clears it
```

Tokens: `master`, `maxLevel`, `donor`, `ccBadge`, `ttBadge`.

> Client side only, like `send_varlist` — only you see it.

### get_vec2i
### get_vec2f
```lua
local tile = get_vec2i(5, 7)
local pos  = get_vec2f(160.0, 224.0)
```
There is also a constructor form, which does not allocate:
```lua
local tile = vec2i.new(5, 7)
local pos  = vec2f.new(160.0, 224.0)
```

### add_log
```lua
add_log("written to the nora log") -- only when packet logging is on
```

### srand
```lua
srand() -- seeds the random generator with the current time
```

### run_file
**aliases:** `runFile`

Runs another script. With no argument it re-runs the current one.
```lua
run_file("other_script.lua")
run_file()
```

### stop_file
**aliases:** `stopFile`

Stops a script. With no argument it stops the current one — the usual way to end a loop script.
```lua
stop_file("other_script.lua")
stop_file()
```
