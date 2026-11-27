# Game HUD assets

`inventory/` and `minimap/` contain the PNG resources supplied in `rpg-inventory-assets.zip` and `rpg-minimap-assets.zip`. The original images are preserved.

The runtime skin is `client/src/assets/rpg-game.css`. Inventory and quickbar use a 36px source slice; the tooltip uses 20px. The nameplate uses `35 56 fill`. Round frames retain their aspect ratio and the map canvas is clipped to the inside of the ring.

The three supplied item icons map to `vest`, `axe` and `staff`. Other equipment keeps its existing sprite icon; character portraits use the player's actual equipped appearance.
