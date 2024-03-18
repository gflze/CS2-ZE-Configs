# GFLClan CS2 ZE Configs

| Sync Status |
|:-----------:|
| [![Sync Files To Main Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-main.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) [![Sync Files To Test Server](https://github.com/gflze/CS2-ZE-Configs/actions/workflows/ci-master-test.yml/badge.svg)](https://github.com/gflze/CS2-ZE-Configs/actions) |


A collection of the Stripper and map configs used on GFL's CS2 ZE server.

Everything in this repository is auto-synced to our main/test servers on a new commit/push.

# How to Contribute

For making any of these configs, you'll need to use [Source 2 Viewer](https://valveresourceformat.github.io/) to view entity lumps, and optionally [CS2ServerGUI](https://github.com/Source2ZE/CS2ServerGUI) for live debugging. You can also compare maps with current configs in this repository and see how things have already been done if you're looking for functional examples of things.

**_IMPORTANT:_** Make sure the filename of the config matches the map name on the server.

## Stripper

Stripper is quite a complicated beast, and unfortunately a single template is not really going to help you too much. You can find documentation on the config format in the [StripperCS2 Readme](https://github.com/Source2ZE/StripperCS2?tab=readme-ov-file#configuration). If you have any questions regarding stripper creation, you can always join our [#mapping channel](https://discord.gg/zh2CVSM) on Discord for assistance.

## Map Configs

These are basic CS2 config files containing cvars/commands that get executed on map start.

Some common GFL plugin cvars that you may want to adjust are listed below with their functionalities.
```
```