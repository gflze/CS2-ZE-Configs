# GFL CS2 Zombie Escape Configs

| Sync Status |
|:-----------:|
| [![Sync Files To Main Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-main.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) [![Sync Files To Test Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-test.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) |


A collection of the EntWatch, BossHUD, Stripper and map configs used on GFL Zombie Escape.

Everything in this repository is auto-synced to our main/test servers on a new commit/push.

# How to Contribute

For making any of these configs, you'll need to use [Source 2 Viewer](https://valveresourceformat.github.io/) to view entity lumps, and optionally [CS2ServerGUI](https://github.com/Source2ZE/CS2ServerGUI) for live debugging. You can also compare maps with current configs in this repository and see how things have already been done if you're looking for functional examples of things.

**_IMPORTANT:_** Make sure the name of the folder/config matches the map name on the server.

## EntWatch

Find entity classnames that start with `weapon_` as a starting point for creating these. For each item you're going to want a new block in the root array. The format is available below.

```jsonc
[
    {
        "name": "Item Name",        // Name of item that appears in chat
        "shortname": "Short Name",  // Name of item that appears on the HUD
        "hammerid": "",             // Hammerid of the weapon entity
        "message": true,            // Whether to show pickup/drop messages in chat
        "ui": true,                 // Whether to show this item on the HUD
        "transfer": true,           // Whether to allow this item to be transferred (this auto detects false for knife items)
        "color": "",                // Color of the item for chat messages (see list of colors)
        "triggers": [""],           // Array of hammerids of any triggers that this item is associated with
        "templated": true,          // Whether the entity of this handler is templated with the item weapon, (auto detected if not specified)
        "handlers": [
            {
                "name": "Handler",     // extra name to show in chat when used e.g. XXX has used Item Name (Handler)
                "type": "button",      // "button",
                                       // "counterdown" - counter stops OnHitMin
                                       // "counterup" - counter stops OnHitMax
                                       // (anything else is ignored)
                "hammerid": "",        // hammerid of the entity
                "event": "OnPressed",  // Name of the output, counterup/down types always force "OutValue"
                "mode": 2,             // Mode of the handler
                                        //   0/1 = None
                                        //   2 = Cooldown,           3 = MaxUses (cooldown between each)
                                        //   4 = CooldownAfterUses,  5 = CounterValue
                "offset": [5,-9],      // ADDS the specified offset to counter values, 
                                        // First number is counter value, Second is counter max
                "cooldown": 60,        // Cooldown duration if mode = 2,3,4
                "maxuses": 0,          // Maxuses if mode = 3,4
                "message": true,       // Whether to show when this is used in chat
                "ui": true,            // Whether to track this handler on the HUD
                "templated": true      // Whether the entity of this handler is templated with the item weapon, 
            }                          //  (this will attempt to auto detect if not specified)
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

## BossHUD

Find entity classnames that are either `math_counter`, `func_breakable`, or `func_physbox` as a starting point for creating these. For each boss and NPC, you're going to want a new block in the root array. The format is available below.

```jsonc
[
    {
        "name":             "",     // Name of boss that appears in hud
        "breakable":        "",     // Targetname/Hammerid of breakable
        "counter":          "",     // Targetname/Hammerid of counter
        "iterator":         "",     // OPTIONAL - Targetname/Hammerid of hp iterator (segments)
        "backup":           "",     // OPTIONAL - Targetname/Hammerid of hp backup

        "trigger":                  // OPTIONAL - Specifies the event that triggers the boss
        {
            "ent":          "",     // (string) Targetname/Hammerid of entity
            "output":       "",     // (string) Output of entity
            "delay":        0.0     // OPTIONAL - (float) Delay after output that starts boss
        },

        "showtrigger":              // OPTIONAL - Specifies event that starts displaying boss health
        {
            "ent":          "",     // (string) Targetname/Hammerid of entity
            "output":       "",     // (string) Output of entity
            "delay":        0.0     // OPTIONAL - (float) Delay after event that shows boss health
        },

        "killtrigger":              // OPTIONAL - Specifies event that force kills the boss
        {
            "ent":          "",     // (string) Targetname/Hammerid of entity
            "output":       "",     // (string) Output of entity
            "delay":        0.0     // OPTIONAL - (float) Delay after event that force kills boss
        },

        "hurttrigger":              // OPTIONAL - Specifies event that is considered as damaging the boss
        {
            "ent":          "",     // (string) Targetname/hammerid of entity
            "output":       ""      // (string) Output of entity
        },

        "reversecounter":   false,  // OPTIONAL - (bool) Whether counter should be reversed
        "reverseiterator":  false,  // OPTIONAL - (bool) Whether iterator should be reversed
        "hitmarkeronly":    false,  // OPTIONAL - (bool) Whether only hitmarkers should be shown when hitting boss
        "minorhud":         false,  // OPTIONAL - (bool) Whether boss should should be displayed as no-bar hud variant
        "multitrigger":     false,  // OPTIONAL - (bool) Whether boss can be triggered multiple times (multiple instances)
        "namefixup":        false,  // OPTIONAL - (bool) Whether boss is templated and has name fixup
        "showbeaten":       true,   // OPTIONAL - (bool) Whether top boss damage should be displayed after boss death
        "timeout":          0.0,    // OPTIONAL - (float) Specify time before boss health is hidden after taking no damage
        "offset":           0.0     // OPTIONAL - (float) Specify amount of health to ADD to displayed health (negative to subtract)
    },
]
```

## MusicName

Keys are the soundevent names, they're based off of the maps `soundevents_addon.vsndevts_c` file. Values are what gets displayed ingame, please keep them in `Artist - Song Title` format, and split separate songs with commas. For unknown songs, keep the value empty.

An example config is available below.

```jsonc
{
    "soundevent1":                                  "Artist - Song Title",
    "soundevent2":                                  "Artist 2 - Song Title 2, Artist 3 - Song Title 3",
    "soundevent3":                                  "Artist 3 - Song Title 4/Song Title 5/Song Title 6",

    "music.rick_astley_never_gonna_give_you_up":    "Rick Astley - Never Gonna Give You Up",
    "mako.music.Lv4_2_Pendulum_The_Fountain":       "Pendulum - The Fountain"
}
```

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

## AdminRoom

Very basic, there is a single `adminroom.jsonc` file with map name keys & coordinate values for admin rooms that !adminroom can teleport to, an example entry is `"ExampleMap1": [123, 456, 789]`.