# Changelogs

## Release 0.42
    [+] added account switcher (save accounts and switch between them, with optional fingerprint)
    [+] added accounts page (add / edit / remove accounts, fill from current login)
    [+] added vend buy page (fast buy, fast restock, fast withdraw, buy what you can afford, price check)
    [+] added exploit page (marker / door / portal find, stop at the tile or walk to it)
    [+] added lua functions for building, tiles, items and effects, see [functions](functions.md)
    [+] added get_tile(x, y) and get_tiles({ ids }) to read tiles from a script
    [+] added alias names for lua functions (lowerCamel, PascalCase), e.g. getWorld() works like get_world()
    [+] added vec2i.new(x, y) and vec2f.new(x, y) so scripts can build vectors themselves
    [+] added send_country_state(badge) / send_badge(badge) for the country badge
    [~] fixed lua scripts deleting themselves when run from the script list
    [~] fixed a script disappearing from the list taking the wrong entry with it
    [~] fixed lua editor missing colors for many functions
    [~] fixed /master not turning off, and "reset all titles" not resetting
    [~] fixed /showgems always showing 0
    [~] fixed /showgems only working the first time it was used

## Release 0.3
    [+] added special talk between nora users
    [+] added hosting page (still on development)
    [+] added mod detector page (only for vip users)
    [+] added auto updater (no more waiting for new update)
    [+] added auto remove visual items from your inventory when close visual clothes
    [+] added visuals (player esp, object esp, weather esp, placed item esp [placed block/background esp])
    [~] re-organized cheats & settings page
    [~] fixed visuals (no more any issues)

## Beta 0.2.5
    [+] Added links of casinos (rudys/ju it will auto go to their casinos)
    [+] Added Auto Login (you gotta click checkbox and save your config as default.cfg)
    [~] fixed some logic issues
    
## Beta 0.2.4
    [+] Updated gui backend for latest growtopia
    [~] structure update
    
## Beta 0.2.3
    [+] multiple growtopia fix (mutex)
    [~] fixed website loader downloader issue
    [~] fixed features such as wrench pull
    [~] fixed dialog issues

## Beta 0.2.2
    [+] account login
    [+] launched internal count will be showen in growtopia's window name<br>
    [+] after you login with your account there'll be dialog for code that can be used at #code for gain role<br>
    [~] website's 80-90% finished last things common things such as lua docs etc
    
## Beta 0.2.1
    [+] text editor (executor) added ctrl + backspace working well
    [~] text editor (executor) colors such as '[[ ]]' '--[[ ]]' fixed

    
## Beta 0.2.0
    [+] added ping watermark also watermarks shown at right bottom at the moment<br>
    [+] now if you explore vend worlds you will help our database of vend locator<br>
    [+] added user checker in world if has nora user shows you<br>
    [+] nora logger added button to open terminal<br>
    [~] nora logger fixed extra line '\n' when copying


## 0.1.9
- **vend locator update**
- **redesigned pages**

## 0.1.8
- **improvements about automation, fixed mem leak**
- **added auto nian (Currently have these automations: nian, farm, store buy, surg, crime, party)**

## 0.1.7
- **flags, types initialization**

## 0.1.6 
- **added timer and transformer library**

## 0.1.5
- **added structures such as: player_items_t, net_object_manager_t, item_info_manager_t, item_info_t, vec2<uint8_t>, vec3f, vec4f**
- **run_file(string file_name)** (runs script of that file)
- **stop_file(string file_name)** (stops script of that file)
- **get_item_info(int item_id)** (returns item_info_t struct by item id)
- **get_item_info_by_name(string name)** (returns item_info_t struct by name)
- **printps(string text)** (prints colored text like growtopia)
- **warp(string world)**
- **drop(int item_id, item_count)**
- **get_player(int net_id)** (returns player in world by net id)
- **get_nom()** (returns net object manager)
- **get_inventory()** (returns player_items_t struct)
- **get_local_player()** (returns local player (net avatar) struct) 
- **get_item_info_manager()** (returns item_info_manager_t struct)
- **send_varlist(varlist)** 

## 0.1.4
- **added structures such as: world_t, world_tile_map_t, world_object_map_t, tile_collision_type, tile_flag, tile_extra, tile_t, object_t**
- **get_world()** 
- **get_world().name** 
- **get_world().version** 
- **get_world().tile_map** 
- **get_world().tile_map.tiles**
- **get_world().object_map** 
- **get_world().object_map.objects** 

## 0.1.3
- **added structures such as: net_avatar_t, body_parts_t, body_part_type**
- **say(string text)** -- can work with: chat(string), talk(string)
- **wrench(int x, int y)**
- **punch(int x, int y, bool animation = false)**
- **place(int x, int y, int item_id, bool animation = false, bool to_client = false)**
- **find_path(int x, int y)** -- can work with teleport(x, y)
- **run_thread(function)**
- **remove_callback(string callback_name)** -- can work with remove_hook(string)
- **remove_callbacks()** -- can work with remove_hooks();
- **add_callback(string callback_name, callback_type (ON_VARIANT_LIST, ON_GAME_PACKET...), function)** -- can work with add_hook(string, callback_type, function)

## 0.1.2
- **added structures such as: net_avatar_t, body_parts_t, body_part_type**
- **say(string text)** -- can work with: chat(string), talk(string)
- **wrench(int x, int y)**
- **punch(int x, int y, bool animation = false)**
- **place(int x, int y, int item_id, bool animation = false, bool to_client = false)**
- **find_path(int x, int y)** -- can work with teleport(x, y)
- **run_thread(function)**
- **remove_callback(string callback_name)** -- can work with remove_hook(string)
- **remove_callbacks()** -- can work with remove_hooks();
- **add_callback(string callback_name, callback_type (ON_VARIANT_LIST, ON_GAME_PACKET...), function)** -- can work with add_hook(string, callback_type, function)

## 0.1.1
- **added structures such as: game_packet_t, game_packet_type, vec2i, vec2f**
- **log(string)**
- **sleep(int ms)**
- **send_packet(int type, string packet)**
- **send_packet_raw(game_packet_t, bool to_client = false)**
