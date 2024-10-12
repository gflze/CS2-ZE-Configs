# GFL CS2 Zombie Escape Configs

| Sync Status |
|:-----------:|
| [![Sync Files To Main Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-main.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) [![Sync Files To Test Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-test.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) |


A collection of the EntWatch, Stripper and map configs used on GFL Zombie Escape.

Everything in this repository is auto-synced to our main/test servers on a new commit/push.

# How to Contribute

For making any of these configs, you'll need to use [Source 2 Viewer](https://valveresourceformat.github.io/) to view entity lumps, and optionally [CS2ServerGUI](https://github.com/Source2ZE/CS2ServerGUI) for live debugging. You can also compare maps with current configs in this repository and see how things have already been done if you're looking for functional examples of things.

**_IMPORTANT:_** Make sure the name of the folder/config matches the map name on the server.

## EntWatch

Find entity classnames that start with `weapon_` as a starting point for creating these. For each item you're going to want a new block in the root array. The format is available below.

```jsonc
[
    {
        "name": "Item Name",            // Name of item that appears in chat
        "shortname": "Short Name",      // Name of item that appears on the HUD
        "hammerid": "",                 // Hammerid of the weapon entity
        "message": true,                // Whether to show pickup/drop messages in chat
        "ui": true,                     // Whether to show this item on the HUD
        "transfer": true,               // Whether to allow this item to be transferred
        "color": "",                    // Color of the item for chat messages (see list of colors)
        "triggers": [""],               // Array of hammerids of any triggers that this item is associated with
        "handlers": [
            {
                "type": "button",           // "button", "game_ui", or "counter"
                "hammerid": "",             // hammerid of the entity
                "event": "OnPressed",       // Name of the output
                "mode": 2,                  // Mode of the handler
                                            //    0/1 = None
                                            //    2 = Cooldown,               3 = MaxUses
                                            //    4 = MaxUsesWithCooldown,    5 = CooldownAfterUses
                                            //    6 = CounterDown,            7 = CounterUp
                "cooldown": 60,             // Cooldown duration if mode = 2,4,5
                "maxuses": 0,               // Maxuses if mode = 3,4,5
                "message": true,            // Whether to show when this is used in chat
                "ui": true                  // Whether to track this handler on the HUD
            }
        ]
    }
]
```

### EntWatch Color List

Grouped colors are just different aliases for the same color.

- `white`, `default`
- `darkred`
- `team`
- `green`
- `lightgreen`
- `olive`
- `red`
- `gray`, `grey`
- `yellow`
- `silver`
- `blue`
- `darkblue`
- `purple`, `pink`
- `red2`
- `orange`, `gold`

## Stripper

Stripper is quite a complicated beast, and unfortunately a single template is not really going to help you too much. You can find documentation on the config format in the [StripperCS2 Readme](https://github.com/Source2ZE/StripperCS2?tab=readme-ov-file#configuration). If you have any questions regarding stripper creation, you can always join our [#mapping channel](https://discord.gg/zh2CVSM) on Discord for assistance.

## Map Configs

These are basic CS2 config files containing cvars/commands that get executed on map start.

Some common GFL plugin cvars that you may want to adjust are listed below with their functionalities.
```
zr_infect_spawn_mz_ratio	// Ratio of all Players to Mother Zombies to be spawned at round start
zr_infect_spawn_type 0		// Enables classic spawn for the map
zr_infect_spawn_time_max	// Maximum time in which Mother Zombies should be picked, after round start
zr_infect_spawn_time_min	// Minimum time in which Mother Zombies should be picked, after round start
```