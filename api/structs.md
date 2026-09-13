## Structs

* **[vec2<uint8_t>](#vec2uint8_t)**
* **[vec2i](#vec2i)**
* **[vec2f](#vec2f)**
* **[vec3f](#vec3f)**
* **[vec4f](#vec4f)**
* **[tile_t](#tile_t)**
* **[tile_extra_t](#tile_extra_t)**
* **[tile_extra_type](#tile_extra_type)**
* **[world_object_t](#world_object_t)**
* **[world_object_map_t](#world_object_map_t)**
* **[world_tile_map_t](#world_tile_map_t)**
* **[inventory_item_t](#inventory_item_t)**
* **[player_items_t](#player_items_t)**
* **[world_t](#world_t)**
* **[net_avatar_t](#net_avatar_t)**
* **[body_parts_t](#body_parts_t)**
* **[item_info_t](#item_info_t)**
* **[game_packet_t](#game_packet_t)**

### Enums
* **[tile_flag](#tile_flag)**
* **[item_flag](#item_flag)**
* **[body_part_type](#body_part_type)**
* **[tile_collision_type](#tile_collision_type)**
* **[packet_flag](#packet_flag)**
* **[game_packet_type](#game_packet_type)**

---

### vec2<uint8_t>
| Description | Name | Type |
|:------------|:----:|:-----|
| X-coordinate | **x** | uint8_t |
| Y-coordinate | **y** | uint8_t |

---

### vec2i
| Description | Name | Type |
|:------------|:----:|:-----|
| X-coordinate | **x** | int |
| Y-coordinate | **y** | int |

Create one with `vec2i.new(x, y)` or `get_vec2i(x, y)`.

---

### vec2f
| Description | Name | Type |
|:------------|:----:|:-----|
| X-coordinate | **x** | float |
| Y-coordinate | **y** | float |

Create one with `vec2f.new(x, y)` or `get_vec2f(x, y)`.

---

### vec3f
| Description | Name | Type |
|:------------|:----:|:-----|
| X-coordinate | **x** | float |
| Y-coordinate | **y** | float |
| Z-coordinate | **z** | float |

---

### vec4f
| Description | Name | Type |
|:------------|:----:|:-----|
| X-coordinate | **x** | float |
| Y-coordinate | **y** | float |
| Z-coordinate | **z** | float |
| W-coordinate | **w** | float |

---

### tile_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Foreground tile ID | **fg** | int |
| Background tile ID | **bg** | int |
| Tile flags | **flags** | [tile_flag](#tile_flag) |
| Tile position | **pos** | [vec2i](#vec2i) |
| Extra tile data | **extra** | [tile_extra_t](#tile_extra_t) |

---

### tile_extra_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Tile extra type | **type** | [tile_extra_type](#tile_extra_type) |
| Item price | **item_price** | int |
| Owner ID | **owner** | int |
| Alpha channel color | **color_a** | int |
| Red channel color | **color_r** | int |
| Green channel color | **color_g** | int |
| Blue channel color | **color_b** | int |
| Label text | **label** | std::string |
| Item ID | **item_id** | int |
| Last updated timestamp | **last_updated_timestamp** | int |
| Growth stage | **growth** | int |
| Fruit count | **fruit_count** | int |
| Access list | **access_list** | std::vector<int> |

---

### world_object_t
In Lua this type is called **object_t** (`get_objects`, `get_object_info`, `world.object_map.objects`).

| Description | Name | Type |
|:------------|:----:|:-----|
| Item ID | **id** | int |
| Object count | **count** | int |
| Object count (same as `count`) | **amount** | int |
| Object flags | **flags** | int |
| Object unique ID | **oid** | int |
| Object position | **pos** | [vec2f](#vec2f) |

---

### world_object_map_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Every object in the world | **objects** | table of [object_t](#world_object_t) |
| Object on a tile | **get_object** | function(int x, int y) -> [object_t](#world_object_t) |
| Object by its unique ID | **get_object_by_oid** | function(int oid) -> [object_t](#world_object_t) |
| Object by item ID | **get_object_by_id** | function(int id) -> [object_t](#world_object_t) |

---

### world_tile_map_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Map size | **size** | [vec2i](#vec2i) |
| Every tile in the world | **tiles** | table of [tile_t](#tile_t) |
| Tile at x, y | **get_tile** | function(int x, int y) -> [tile_t](#tile_t) |
| Tile by index | **get_tile_by_id** | function(int id) -> [tile_t](#tile_t) |

---

### inventory_item_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Item ID | **id** | int |
| Item count | **count** | int |
| Item amount | **amount** | int |
| Item flags | **flags** | int |

---

### player_items_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Check if an item exists | **check_id** | function(int) -> bool |
| Get item count | **get_item_count** | function(int) -> int |
| Get all items | **get_items** | function() -> table |
| Get specific item | **get_item** | function(int) -> [inventory_item_t](#inventory_item_t) |

---

### world_t
| Description | Name | Type |
|:------------|:----:|:-----|
| World version | **version** | int |
| Tile map | **tile_map** | [world_tile_map_t](#world_tile_map_t) |
| Object map | **object_map** | [world_object_map_t](#world_object_map_t) |
| World name | **name** | string |

---

### item_flag
| Description | Name | Value |
|:------------|:----:|:-----:|
| No flag | **none** | `0x0` |
| Flippable item | **flippable** | `0x1` |
| Editable item | **editable** | `0x2` |
| Seedless item | **seedless** | `0x4` |
| Permanent item | **permanent** | `0x8` |
| Item has no drops | **dropless** | `0x10` |
| No self interaction | **no_self** | `0x20` |
| Item has no shadow | **no_shadow** | `0x40` |
| Item is world-locked | **world_locked** | `0x80` |
| Beta item | **beta** | `0x100` |
| Item auto-picks up | **auto_pickup** | `0x200` |
| Modded item | **mod** | `0x400` |
| Random growth item | **rand_grow** | `0x800` |
| Public item | **public_** | `0x1000` |
| Item is in the foreground | **foreground** | `0x2000` |
| Holiday item | **holiday** | `0x4000` |
| Untradeable item | **untradeable** | `0x8000` |

---

### item_info_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Item name | **name** | string |
| Item ID | **id** | int |
| Collision type | **collision_type** | [tile_collision_type](#tile_collision_type) |
| Hits to destroy | **break_hits** | int |
| Clothing type | **clothing_type** | [body_part_type](#body_part_type) |
| Body part | **body_part** | [body_part_type](#body_part_type) |
| Item flags | **flags** | [item_flag](#item_flag) |
| Item rarity | **rarity** | int |
| Item grow time | **grow_time** | int |

---

### net_avatar_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Player name | **name** | string |
| Country | **country** | string |
| Network ID | **net_id** | int |
| User ID | **user_id** | int |
| Facing left | **facing_left** | bool |
| Invisible state | **invis** | bool |
| Moderator status | **mod** | bool |
| Super Moderator status | **smod** | bool |
| Position | **pos** | [vec2f](#vec2f) |
| Tile position | **tile** | [vec2i](#vec2i) |
| Worn clothes — the set the game sends | **clothing_items_original** | [body_parts_t](#body_parts_t) |
| Worn clothes after the substitution pass | **transmutated_clothing_items** | [body_parts_t](#body_parts_t) |
| Old name for `clothing_items_original` | **clothes** | [body_parts_t](#body_parts_t) |
| Old name for `transmutated_clothing_items` | **raw_clothes** | [body_parts_t](#body_parts_t) |

> `clothes` and `raw_clothes` are the old names and still work. Note that `raw_clothes` is **not**
> the untouched set — it gives `transmutated_clothing_items`, the run after the substitution pass.
> Use `clothing_items_original` when you want what you are actually wearing.

---

### body_parts_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Hat slot | **hat** | int |
| Shirt slot | **shirt** | int |
| Pants slot | **pants** | int |
| Shoes slot | **feet** | int |
| Face slot | **face** | int |
| Hand slot | **hands** | int |
| Back slot | **wings** | int |
| Hair slot | **hair** | int |
| Chest item slot | **chest_item** | int |
| Old name for `chest_item` | **neck** | int |

---

### game_packet_t
| Description | Name | Type |
|:------------|:----:|:-----|
| Packet type | **type** | [game_packet_type](#game_packet_type) |
| Packet type | **type_int** | int |
| Object type | **object_type** | int |
| First count value | **count1** | int |
| Second count value | **count2** | int |
| Network ID | **netid** | int |
| Item ID | **item** | int |
| Flags | **flags** | [packet_flag](#packet_flag) |
| Flags | **flags_int** | int |
| Float value 1 | **float1** | float |
| Integer data | **int_data** | int |
| First position | **pos** | [vec2f](#vec2f) |
| Second position | **pos2** | [vec2f](#vec2f) |
| Float value 2 | **float2** | float |
| Tile position | **tile** | [vec2i](#vec2i) |
| Extra data size | **extra_data_size** | int |

---

## Enums

### tile_flag
| Description | Name | Value |
|:------------|:----:|:-----:|
| No flags | **none** | `0x0` |
| Has extra data | **extra_data** | `0x1` |
| Tile is locked | **locked** | `0x2` |
| Spliced tree | **spliced_tree** | `0x4` |
| Tree will drop seed | **tree_will_drop_seed** | `0x8` |
| Tree | **tree** | `0x10` |
| Tile is flipped | **flipped** | `0x20` |
| Tile is enabled (e.g., open for doors, enabled jammers) | **enabled** | `0x40` |
| Public tile | **public_** | `0x80` |
| Has extra frame | **extra_frame** | `0x100` |
| Tile is silenced | **silenced** | `0x200` |
| Water tile | **water** | `0x400` |
| Glue tile | **glue** | `0x800` |
| Fire tile | **fire** | `0x1000` |
| Red tile | **red** | `0x2000` |
| Green tile | **green** | `0x4000` |
| Blue tile | **blue** | `0x8000` |

---

### body_part_type
| Name | Value |
|:-----|:-----:|
| **hat** | `0` |
| **shirt** | `1` |
| **pants** | `2` |
| **shoes** | `3` |
| **face_item** | `4` |
| **hand** | `5` |
| **back** | `6` |
| **hair** | `7` |
| **chest_item** | `8` |
| **neck** | `9` |
| **ances** | `10` |


---

### tile_extra_type
| Description | Name | Value |
|:------------|:----:|:-----:|
| No extra type | **none** | `0` |
| Door tile | **door** | `1` |
| Sign tile | **sign** | `2` |
| Lock tile | **lock** | `3` |
| Tree tile | **tree** | `4` |
| Unknown tile (5) | **unk_5** | `5` |
| Mailbox tile | **mailbox** | `6` |
| Bulletin tile | **bulletin** | `7` |
| Dice tile | **dice** | `8` |
| Provider tile | **provider** | `9` |
| Achievement block | **achievement_block** | `10` |
| Heart monitor | **heart_monitor** | `11` |
| Donation box | **donation_box** | `12` |
| Toy box | **toy_box** | `13` |
| Mannequin tile | **mannequin** | `14` |
| Magic egg tile | **magic_egg** | `15` |
| Game block | **game_block** | `16` |
| Game generator | **game_generator** | `17` |
| Xenonite block | **xenonite** | `18` |
| Dressup tile | **dressup** | `19` |
| Crystal tile | **crystal** | `20` |
| Burglar tile | **burglar** | `21` |
| Spotlight tile | **spotlight** | `22` |
| Display block | **display_block** | `23` |
| Vending machine | **vending_machine** | `24` |
| Fish tank | **fishtank** | `25` |
| Solar tile | **solar** | `26` |
| Forge tile | **forge** | `27` |
| Giving tree | **giving_tree** | `28` |
| Giving tree stump | **giving_tree_stump** | `29` |
| Steam organ | **steam_organ** | `30` |
| Silkworm tile | **silkworm** | `31` |
| Sewing machine | **sewing_machine** | `32` |
| Flag tile | **flag** | `33` |
| Lobster trap | **lobster_trap** | `34` |
| Art canvas | **art_canvas** | `35` |
| Battle cage | **battle_cage** | `36` |
| Pet trainer | **pet_trainer** | `37` |
| Steam engine | **steam_engine** | `38` |
| Lock bot | **lock_bot** | `39` |
| Background weather | **background_weather** | `40` |
| Spirit storage | **spirit_storage** | `41` |
| Data bedrock | **data_bedrock** | `42` |
| Display shelf | **display_shelf** | `43` |
| VIP timer | **vip_timer** | `44` |
| Challenge timer | **challenge_timer** | `45` |
| Unknown tile (46) | **unk_46** | `46` |
| Fish mount | **fish_mount** | `47` |
| Portrait tile | **portrait** | `48` |
| Stuff weather | **stuff_weather** | `49` |
| Fossil prep | **fossil_prep** | `50` |
| DNA machine | **dna_machine** | `51` |
| Trickster tile | **trickster** | `52` |
| Chemtank tile | **chemtank** | `53` |
| Storage tile | **storage** | `54` |
| Oven tile | **oven** | `55` |
| Super music | **super_music** | `56` |
| Geiger charger | **geiger_charger** | `57` |

---

### tile_collision_type
| Description | Name | Value |
|:------------|:----:|:-----:|
| No collision | **none** | `0` |
| Solid collision | **solid** | `1` |
| Jump-through platform | **jump_through** | `2` |
| Gateway tile | **gateway** | `3` |
| Collision when turned off | **if_off** | `4` |
| One-way platform | **one_way** | `5` |
| VIP-only tile | **vip** | `6` |
| Jump-down platform | **jump_down** | `7` |
| Adventure mode tile | **adventure** | `8` |
| Collision when turned on | **if_on** | `9` |
| Faction-specific tile | **faction** | `10` |
| Guild-specific tile | **guild** | `11` |
| Cloud tile | **cloud** | `12` |
| Friends-only entrance | **friends_enterance** | `13` |


---

### packet_flag
| Description | Name | Value |
|:------------|:----:|:-----:|
| No flags | **none** | `0x0` |
| Unknown flag 1 | **unk_0x1** | `0x1` |
| Unknown flag 2 | **unk_0x2** | `0x2` |
| Spawn-related flag | **spawn** | `0x4` |
| Extended flag | **extended** | `0x8` |
| Flipped or facing left | **flipped** / **facing_left** | `0x10` |
| Standing or solid | **standing** / **solid** | `0x20` |
| Unknown combination flag | **unk22** | `0x22` |
| Facing right | **facing_right** | `0x30` |
| Fire damage flag | **fire_damage** | `0x40` |
| Jump flag | **jump** | `0x80` |
| Got killed | **got_killed** | `0x100` |
| Punch flag | **punch** | `0x200` |
| Ghost jump | **ghost_jump** | `0x2ff` |
| Place flag | **place** | `0x400` |
| Tile change flag | **tile_change** | `0x800` |
| Punching combination flag | **punching** | `0xa20` |
| Got punched | **got_punched** | `0x1000` |
| Respawn flag | **respawn** | `0x2000` |
| Object collection | **object_collect** | `0x4000` |
| Trampoline flag | **trampoline** | `0x8000` |
| Damage flag | **damage** | `0x10000` |
| Slide flag | **slide** | `0x20000` |
| Parasol flag | **parasol** | `0x40000` |
| Unknown gravity-related flag | **unk_0x80000** | `0x80000` |
| Swim flag | **swim** | `0x100000` |
| Wall hang flag | **wall_hang** | `0x200000` |
| Start of power-up punch | **power_up_punch_start** | `0x400000` |
| End of power-up punch | **power_up_punch_end** | `0x800000` |
| Unknown tile change flag | **unk_0x1000000** | `0x1000000` |
| Hay cart-related flag | **unk_0x2000000** | `0x2000000` |
| Acid damage-related flag | **on_acid_damage** | `0x4000000` |
| Unknown flag | **unk_0x8000000** | `0x8000000` |
| Acid damage | **acid_damage** | `0x10000000` |

---
### game_packet_type
| Description | Name | Value |
|:------------|:----:|:-----:|
| State update packet | **state** | `0` |
| Call function packet | **call_function** | `1` |
| Update status packet | **update_status** | `2` |
| Tile change request packet | **tile_change_request** | `3` |
| Map data packet | **send_map_data** | `4` |
| Tile update data packet | **send_tile_update_data** | `5` |
| Multiple tile update data packet | **send_tile_update_data_multiple** | `6` |
| Tile activate request packet | **tile_activate_request** | `7` |
| Tile apply damage packet | **tile_apply_damage** | `8` |
| Inventory state packet | **send_inventory_state** | `9` |
| Item activate request packet | **item_activate_request** | `10` |
| Item activate object request packet | **item_activate_object_request** | `11` |
| Tile tree state packet | **send_tile_tree_state** | `12` |
| Modify item inventory packet | **modify_item_inventory** | `13` |
| Item change object packet | **item_change_object** | `14` |
| Lock data packet | **send_lock** | `15` |
| Item database data packet | **send_item_database_data** | `16` |
| Particle effect packet | **send_particle_effect** | `17` |
| Icon state packet | **set_icon_state** | `18` |
| Item effect packet | **item_effect** | `19` |
| Character state packet | **set_character_state** | `20` |
| Ping reply packet | **ping_reply** | `21` |
| Ping request packet | **ping_request** | `22` |
| Got punched packet | **got_punched** | `23` |
| App check response packet | **app_check_response** | `24` |
| App integrity fail packet | **app_integrity_fail** | `25` |
| Disconnect packet | **disconnect** | `26` |
| Battle join packet | **battle_join** | `27` |
| Battle event packet | **battle_event** | `28` |
| Use door packet | **use_door** | `29` |
| Parental controls packet | **send_parental** | `30` |
| Gone fishing packet | **gone_fishin** | `31` |
| Steam packet | **steam** | `32` |
| Pet battle packet | **pet_battle** | `33` |
| NPC interaction packet | **npc** | `34` |
| Special packet | **special** | `35` |
| Particle effect v2 packet | **send_particle_effect_v2** | `36` |
| Active arrow to item packet | **active_arrow_to_item** | `37` |
| Select tile index packet | **select_tile_index** | `38` |
| Player tribute data packet | **send_player_tribute_data** | `39` |
| Set item to quick inventory (FTUE) packet | **ftue_set_item_to_quick_inventory** | `40` |
| PVE NPC packet | **pve_npc** | `41` |
| PVPCard battle packet | **pvpcard_battle** | `42` |
| PVE player damage packet | **pve_apply_player_damage** | `43` |
| PVE NPC position update packet | **pve_npc_position_update** | `44` |
| Extra mods packet | **set_extra_mods** | `45` |
| Tile mod step-on packet | **on_step_on_tile_mod** | `46` |

