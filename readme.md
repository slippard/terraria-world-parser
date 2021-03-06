<!--
  Title: terraria world parser
  Description: Terraria world file parser
  Author: cokolele
  Tags: terraria, world file, file structure, file dumper, file format, documentation, data, parsing, parser, map viewer, tool, javascript, node, browser
  -->

# Terraria world parser

Terraria world file parser written in javascript

\- supports only maps generated in 1.3.5.3

Feel free to contribute 🌳

## Usage 

```javascript
const terrariaWorldParser = require("terraria-world-parser.js");

//node
let world = new terrariaWorldParser("Canvas.wld");
//browser
let world = await new terrariaWorldParser(worldFile);

world = world.parse();

const name = world.header.mapName;
const size = world.header.maxTilesX + "x" + world.header.maxTilesY;
console.log( `Size of ${name} is ${size}`);
```

## Functions:

*node class constructor* **new terrariaWorldParser( path )**  
*browser class constructor* **new terrariaWorldParser( file )**  

 \- Opens/loads the file, doesn't parse it yet

*instance method* **parse( sections )**  

 \- *string array* **sections** parameter specifies world file sections that will be parsed  
 &nbsp;&nbsp;&nbsp;- by default all sections are parsed (if you don't define parameter)  
 &nbsp;&nbsp;&nbsp;- sections: FileFormatHeader, Header, WorldTiles, Chests, Signs, NPCs, TileEntities, WeightedPressurePlates, TownManager  
 \- Parses the file  
 \- Returns an object

## Return object:

***object* fileFormatHeader**

Type | Variable | Description
--- | --- | ---
*int32* | version | map file version (not game version)
*7 bytes string* | magicNumber | magic number for file format
*int8* | fileType | file format type (relogic uses more formats than .wld)
*uint32* | revision | how many times this map was opened ingame
*uint64* | favorite | is map favorite (always 0)
*int32 array* | pointers | memory pointers for sections
*bool array* | importants | tile frame important for blocks (animated, big sprite, more variants...)<br>\- contains *null*s instead of *false*s<br>\- array entry number == block id

***object* header**

Type | Variable | Description
--- | --- | ---
*string* | mapName | name of the map
*string* | seedText | seed of the map
*uint64* | worldGeneratorVersion | version of the world generator, returns 8 bytes array because node.js doesn't natively support 32+ bit value reads
*int64* | creationTime | time of creation (created with C# Datetime.ToBinary()), returns 8 bytes array (^)
*guid* | guid | guid of the map, returns 16 bytes array (^)
*int32 array* | killCount | kill counter of the enemies (array index == enemy id probably)
*int32* | worldId | id of the world, used as name of the .map file
*int32* | leftWorld | map dimesion in pixels (1 tile = 16 pixels)
*int32* | rightWorld | ^
*int32* | topWorld | ^
*int32* | bottomWorld | ^
*int32* | maxTilesX | map dimension x in tiles
*int32* | maxTilesY | map dimension y in tiles
*int32* | spawnTileX | position x of the spawn point
*int32* | spawnTileY | position y of the spawn point
*int32* | dungeonX | position x of the dungeon base
*int32* | dungeonY | position y of the dungeon base
*int32 array* | treeX | ?
*int32 array* | treeStyle | ?
*int32 array* | caveBackX | ?
*int32 array* | caveBackStyle | ?
*int32* | iceBackStyle | ?
*int32* | jungleBackStyle | ?
*int32* | hellBackStyle | ?
*double* | worldSurface | y dimension where ground level starts
*double* | rockLayer | y dimension where cavern level starts
*bool* | expertMode | expert mode map
*bool* | hardMode | is map hardmode
*int32* | oreTier1 | what is <tier 1> hardmore ore (block id)
*int32* | oreTier2 | ^
*int32* | oreTier3 | ^
*bool* | crimson | is world crimson
*int32* | altarCount | how many altars exists
*bool* | shadowOrbSmashed | has been shadow orb (crimson hearts count too probably) smashed
*int8* | shadowOrbCount | how many shadow orbs (crimson hearts ?) exists
*double* | tempTime | current time
*bool* | tempDayTime | is day time
*bool* | spawnMeteor | ?
*int8* | moonType | ?
*bool* | tempRaining | is currently raining
*int32* | tempRainTime | current rain time
*float* | tempMaxRain | ?
*int32* | cloudBGActive | ?
*double* | cloudBGAlpha | ?
*int16* | numClouds | ?
*float* | windSpeedSet | ?
*float* | windSpeed | ?
*bool* | Temp_Sandstorm_Happening | is sandstorm happening
*int32 | Temp_Sandstorm_TimeLeft | time left to sandstorm end
*float* | Temp_Sandstorm_Severity | current severity of the sandstorm
*float* | Temp_Sandstorm_IntendedSeverity | (? max / average) intented severity of the sandstorm
*int32* | tempMoonPhase | moon phase (probably)
*bool* | tempBloodMoon | is blood moon happening
*bool* | tempEclipse | is eclipse happening
*bool* | eclipse | is eclipse happening (^ copied)
*int32* | invasionDelay | ?
*int32* | invasionSize | ?
*int32* | invasionSizeStart | ?
*int32* | invasionType | type of an event
*double* | invasionX | ?
*double* | slimeRainTime | ?
*int32* | tempCultistDelay | ?
*bool* | tempPartyManual | ?
*bool* | tempPartyGenuine | ?
*int32* | tempPartyCooldown | party event cooldown
*int32 array* | tempPartyCelebratingNpcs | NPCs currently celebrating
*bool* | TowerActiveSolar | is solar pillar up
*bool* | TowerActiveVortex | is vortex pillar up
*bool* | TowerActiveNebula | is nebula pillar up
*bool* | TowerActiveStardust | is stardust pillar up
*bool* | LunarApocalypseIsUp | is lunar event active
*bool* | downedBoss1 | has been <boss 1> killed
*bool* | downedBoss2 | ^
*bool* | downedBoss3 | ^
*bool* | downedQueenBee | ^
*bool* | downedMechBoss1 | ^
*bool* | downedMechBoss2 | ^
*bool* | downedMechBoss3 | ^
*bool* | downedMechBossAny | ^
*bool* | downedPlantBoss | ^
*bool* | downedGolemBoss | ^
*bool* | downedSlimeKing | ^
*bool* | downedGoblins | ^
*bool* | downedClown | ^
*bool* | downedFrost | ^
*bool* | downedPirates | ^
*bool* | downedFishron | ^
*bool* | downedMartians | ^
*bool* | downedAncientCultist | ^
*bool* | downedMoonlord | ^
*bool* | downedHalloweenKing | ^
*bool* | downedHalloweenTree | ^
*bool* | downedChristmasIceQueen | ^
*bool* | downedChristmasSantank | ^
*bool* | downedChristmasTree | ^
*bool* | downedTowerSolar | ^
*bool* | downedTowerVortex | ^
*bool* | downedTowerNebula | ^
*bool* | downedTowerStardust | ^
*bool* | DD2Event_DownedInvasionT1 | is Old One's Army <tier 1> downed
*bool* | DD2Event_DownedInvasionT2 | ^
*bool* | DD2Event_DownedInvasionT3 | ^
*bool* | savedGoblin | is \<goblin> saved
*bool* | savedWizard | ^
*bool* | savedMech | ^
*bool* | savedAngler | ^
*bool* | savedStylist | ^
*bool* | savedTaxCollector | ^
*bool* | savedBartender | ^ (Tavernkeep)
*int8* | setBG0 | ?
*int8* | setBG1 | ?
*int8* | setBG2 | ?
*int8* | setBG3 | ?
*int8* | setBG4 | ?
*int8* | setBG5 | ?
*int8* | setBG6 | ?
*int8* | setBG7 | ?
*int8* | sundialCooldown | cooldown of the Enchanted Sundial
*bool* | fastForwardTime | ?
*string array* | anglerWhoFinishedToday | ?
*int32* | anglerQuest | id of the current angler quest (probably)

***2d object array* worldTiles**

Type | Variable | Description
--- | --- | ---
*byte / unint16* | blockId | block id
*int16* | frameX | frame x (tile frame important)
*int16* | frameY | frame y (^)
*int8* | wallId | wall id
*string* | hammered | edited block (half, TR, TL, BR, BL)
*object* : | colors |
\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | block | painted block
\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | wall | painted wall
*object* : | liquid |
\|&nbsp;&nbsp;&nbsp;&nbsp;*string* | type | liquid type (water, lava, honey)
\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | amount | amount
*object* : | wiring |
\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | hasActuator | contains actuator
\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | actuated | is actuated
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | wires |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | red | contains red wire
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | blue | contains blue wire
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | green | contains green wire
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | yellow | contains yellow wire

***object* chestsData**

Type | Variable | Description
--- | --- | ---
*int16* | chestsCount | number of chests in the world
*int16* | chestSpace | number of slots for chests, 40 as for version 1.3.5.3
*number* | overflow | number of overflowing slots
*object array* : | chests |
\|&nbsp;&nbsp;&nbsp;&nbsp;*string* | name | name of the chest
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | x | position x of the chest
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | y | position y of the chest
\|&nbsp;&nbsp;&nbsp;&nbsp;*object array* : | items |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | stack | stack of the item
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | id | id of the item
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | prefix | id of the prefix for the item (modifier)

***object* signsData**

Type | Variable | Description
--- | --- | ---
*int16* | signsCount | number of signs in the world
*object array* : | signs |
\|&nbsp;&nbsp;&nbsp;&nbsp;*string* | text | text of the sign
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | x | position x of the sign
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | y | position y of the sign

***object array* npcsData**

Type | Variable | Description
--- | --- | ---
*int32* | id | id of an npc
*string* | npc | type of an npc
*string* | name | name of an npc
*bool* | homeless | is homeless
*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;*float* | x | position x of an npc
\|&nbsp;&nbsp;&nbsp;&nbsp;*float* | y | position y of an npc
*object* : | homePosition |
\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | x | position x of npc's home
\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | y | position y of npc's home

***object* tileEntities**

Type | Variable | Description
--- | --- | ---
*int32* | tileEntitiesCount | number of tile entities in the world
*object array* : | tileEntities |
\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | id | ID of the tile entity
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | x | position x of the tile entity
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | y | position y of the tile entity
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | targetDummy |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | npc | ?
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | itemFrame |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | itemId | ID of the framed item
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | prefix | prefix of the framed item (modifier)
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int16* | stack | stack of the framed item
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | logicSensor |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int8* | logicCheck | type of the logic check (probably)
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*bool* | on | is on


***object* pressurePlates**

Type | Variable | Description
--- | --- | ---
*int32* | pressurePlatesCount | number of pressurePlates in the world
*object array* : | pressurePlates |
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | x | position x of the pressurePlate
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | y | position y of the pressurePlate

***object* townManager**

Type | Variable | Description
--- | --- | ---
*int32* | roomsCount | number of rooms in the world
*object array* : | rooms |
\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | npcId | ID of an NPC
\|&nbsp;&nbsp;&nbsp;&nbsp;*object* : | position |
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | x | position x of the room
\|&nbsp;&nbsp;&nbsp;&nbsp;\|&nbsp;&nbsp;&nbsp;&nbsp;*int32* | y | position y of the room