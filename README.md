> If this project helped you, please consider leaving some stars [on the Github](https://github.com/Derec-Mods)! 

[![Support me on Ko-fi](https://cdn.jsdelivr.net/npm/@intergrav/devins-badges@3/assets/compact/donate/kofi-singular-alt_vector.svg)](https://ko-fi.com/derexxd) 

# Trading Hall Optimizer

![image](https://github.com/user-attachments/assets/2716b281-48a6-4a1a-9305-0560684d4e0f)

This plugin was originally created by [mja00](https://github.com/mja00) as Villager Lobotomizer, whom I worked with on the original project. This project is a revival and continuation fork, maintained to provide modern version support, fix tricky confinement scenarios, and optimize performance across newer Paper and Folia servers.

## Description 

Trading Hall Optimizer is a Paper/Folia plugin that eliminates server lag caused by villager AI in trading halls. When villagers are confined in trading stalls or cells, their pathfinding and goal selectors are disabled ("lobotomized") while preserving normal trading, profession restocks, experience leveling, and Hero of the Village gifts.

## Features
* **Automatic AI Disabling:** Shuts off AI for villagers confined to trading stalls, drastically reducing tick lag on survival servers.
* **Full Trading Functionality:** Maintains vanilla trading, experience leveling, demand updates, and scheduled restocks.
* **Configurable Restocks:** Automatic restocking on a configurable interval with optional randomization and workstation proximity checks.
* **Hero of the Village Support:** Lobotomized villagers still grant gifts to heroes within line of sight.
* **Name Tag Controls:** Tag villagers with `nobrain` to force-lobotomize or `alwaysbrain` to keep them active.
* **Sound & Visual Feedback:** Supports custom or profession-specific restock sounds and level-up celebrations.
* **Folia Support:** Built with region-aware and entity-safe schedulers for Paper and Folia compatibility.
* **Trading Enforcement:** Optional setting to prevent players from trading with roaming, unconfined villagers.
* **Diagnostic & Debug Tools:** In-depth `/lobotomy debug` inspection showing precise block-by-block confinement decisions.

## Commands
* `/lobotomy info` - Shows counts and percentages of active and lobotomized villagers.
* `/lobotomy debug` - Inspects the targeted villager and displays a detailed block-by-block confinement report.
* `/lobotomy debug toggle` - Toggles console transition logging for debugging.
* `/lobotomy wake` - Restores AI to the targeted villager.
* `/lobotomy reload` - Reloads the configuration and re-evaluates all tracked villagers.
* `/lobotomy uninstall` - Guides safe uninstallation by restoring AI to all villagers.

## Special Villager Names
* Name a villager with `nobrain` to force AI to stay disabled.
* Name a villager with `alwaysbrain` to prevent it from ever being lobotomized (configurable in `always-active-names`).

## Configuration

```yaml
#Configuration version - DO NOT MODIFY MANUALLY
config-version: 7

#List of names that will always keep villagers active (case-insensitive)
always-active-names:
  - "alwaysbrain"

#Interval between trapped checks, in ticks, for active villagers
check-interval: 150

#Interval between trapped checks, in ticks, for inactive villagers
inactive-check-interval: 150

#Interval between villager trade restocks, in milliseconds
restock-interval: 540000

#Range (in milliseconds) before restock-interval to start random restock checks. If set to 0, restocking is not randomized. Values equal to or greater than restock-interval are capped to it, so the threshold is randomized across the whole interval (anywhere from immediately up to restock-interval).
restock-random-range: 0

#Whether to only lobotomize villagers with jobs
only-lobotomize-villagers-with-professions: false

#Whether to only lobotomize villagers that have been traded at least once
only-lobotomize-villagers-with-experience: false

#Whether to lobotomize villagers in boats/minecarts. Does not apply to villagers riding on non-vehicle entities like horses.
always-lobotomize-villagers-in-vehicles: false

#Whether to make lobotomized villagers silent. When enabled, villagers will be muted when their AI is disabled.
silent-lobotomized-villagers: false

#The sound to play when a villager restocks. Leave empty ("") for default sounds.
#A list of sounds can be found at https://jd.papermc.io/paper/io/papermc/paper/registry/keys/SoundEventKeys.html
#Use the name found in the description column, e.g. "entity.villager.celebrate" for the sound played when a villager restocks.
restock-sound: ""

#The sound played when a villager is leveled up. Leave empty ("") for no sound.
level-up-sound: "entity.villager.celebrate"

#Debug mode. Prints debug messages to the console.
debug: false

#Chunk debug mode. Prints debug messages related to chunks
chunk-debug: false

#To ignore villagers stuck in doors, set this to true.
ignore-villagers-stuck-in-doors: false

#To not lobotomize villagers surrounded by non-solid blocks, set this to true.
ignore-non-solid-blocks: false

#To check if there is a roof above a villager before lobotomizing, set this to true. The roof can be directly above its head or one block higher.
check-roof: true

#Create teams for debugging purposes. This will create colored teams for inactive and active villagers. We use this to color their glowing effect.
create-debug-teams: false

#Disable the update checker. You can disable this if you don't want to be notified about updates.
#Note: this is only read when the plugin loads; changing it requires a server restart (a /lobotomy reload will not re-run the update check).
disable-update-checker: false

#Disable chunk forced Villager updating. This'll stop breaking blocks in a chunk from triggering Villagers in the chunk to be updated.
disable-chunk-villager-updates: false

#Prevent trading with unlobotomized villagers. When enabled, players can only trade with villagers that have been lobotomized.
prevent-trading-with-unlobotomized-villagers: false

#Message that is sent to players when they try to trade with an unlobotomized villager. Supports MiniMessage.
unlobotomized-villager-trade-message: "<red>You cannot trade with unlobotomized villagers!</red> <yellow>This villager needs to be lobotomized first.</yellow>"

#Persist lobotomized state across chunk unloads and server restarts. When enabled, lobotomized villagers stay lobotomized, so there is no lag spike while they are re-evaluated after a chunk load or a reboot.
#Run '/lobotomy uninstall' before removing the plugin. Deleting the jar on its own leaves those villagers without AI, because nothing is left to restore them.
persist-lobotomized-state: true

#Let lobotomized villagers give Hero of the Village gifts, which their disabled AI otherwise prevents. Like vanilla, a villager's gift timer (30s after it loads, then 30s-5.5min between gifts) runs while it can see a hero within 16 blocks; once it is done the villager turns to the hero and throws the gift (from vanilla's loot tables) when the hero is within 5 blocks. If its cell would block the throw, the gift is dropped at the hero's feet instead.
hero-gifts-from-lobotomized-villagers: true
```

## Sound System
* **Default Restock Sounds:** When `restock-sound` is left empty, villagers use their profession-specific work sounds.
* **Custom Sounds:** Override restock or level-up sounds using standard Minecraft sound keys or custom resource-pack keys.
* **Level-Up Celebrations:** Villagers play celebrations and emit regeneration particles when leveling up trades.

## ❤️ Credits
* **Original Author:** [mja00](https://github.com/mja00)
* **Contributors:** [DerexXD](https://github.com/DereC4)

This project is open-source and licensed under the [MIT License](LICENSE).
