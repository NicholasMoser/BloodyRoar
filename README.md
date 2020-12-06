# Bloody Roar Extreme

Investigating some things about the GameCube title Bloody Roar Extreme

## Wall Durability

In Bloody Roar Extreme, you can slam your opponent into a wall to break it. After it breaks you can ring them out from there. Most professional players of the game feel that the default durability is far too low. This causes some people to prefer playing with wall destruction off. Current estimates says that the wall breaks in around 2 or so hits. They all seem to break in around the same amount of hits.

## Wall Durability Decomp

Wall damage seems to occur at instruction 0x80047d68:
![Wall Break](/wall_break.PNG?raw=true "Wall Break")

After setting the damage, it is immediately checked against the health of the wall, `*(short *)(puVar2 + 2)`. The health for all walls in the game seem to be 0x100, but are actually set by the seq parser. Seems like the  health might be set at 0x8000e900, however it's not obvious where this value is coming from.

## Increase Wall Durability Code

```gecko
04047d90 38A00200
```

The above code will give the wall 2x durability. The `200` at the end of the code is the health of all walls in the game. It is `100` by default, therefore `200` is twice as strong. It may have a max of `FFFF` since it is casted to a short.

## Extended Debug Mode

Bloody Roar has a code to enable debug mode during matches in-game:

```gecko
0405aedc 60000000
0400ad24 4803fde1
```

When this code is enabled, there also appears to be an **extended** debug menu. You can get to it by highlighting Options in the main menu, hold `L + R`, and hit `A`. For all of the functionality to work you'll need to use an unpacked version of the game, i.e. all fpack files have been decompressed.

When you hit `Start` in this menu, it will bring up the debug menu.

![Debug Menu Pause](/debug_menu_pause.PNG?raw=true "Debug Menu Pause")

If a different menu is desired, see the codes below:

- [Training Mode Pause](#training-mode-pause)
- [Battle Mode Pause](#battle-mode-pause)
- [No Menu Pause](#no-menu-pause)

### Features

- [NORMAL TEST](#normal-test)
- [GAME TEST](#game-test)
- [FACE EDIT](#face-edit)
- [SEQ EDIT](#seq-edit)
- [TXG VIEWER](#txg-viewer)
- [MEMORY CARD](#txg-viewer)
- [MOVIE TEST](#movie-test)

### Normal Test

This mode has no practical purpose, it likely was an early test demo.

### Game Test

This mode contains some functionality

It is recommended to change **DEBUG** to 0 on the second menu so that the screen isn't blocked by CPU/RAM data.

- `Z + B` = Bone Control
- `Z + Y` = Nothing (Calls method at 800974e4)
- `Z + C-stick up` = Invert colors
- `Z + C-stick down` = Normal colors (revert inverted colors)
- `Z + C-stick left` = Add blur
- `Z + c-stick right` = Add spiral blur
- `C-stick up` = Restart match and show battle intro
- `C-stick down` = Restart match
- `C-stick left` = P1 win animation
- `C-stick right` = P2 win animation

### Face Edit

It is recommended to change **DEBUG** to 0 on the second menu so that the screen isn't blocked by CPU/RAM data.

When in the FACE EDIT menu in-game, `L` and `R` will zoom in and out. Once you hit EDIT, `L` will bring up a [face animation tester](https://imgur.com/a/GTtPXFZ).

- `Z + B` = Bone Control
- `Z + Y` = Face Edit
- `Z + C-stick up` = Invert colors
- `Z + C-stick down` = Normal colors (revert inverted colors)
- `Z + C-stick left` = Add blur
- `Z + c-stick right` = Add spiral blur
- `C-stick up` = Restart match and show battle intro
- `C-stick down` = Restart match

### SEQ Edit

Doesn't appear to have any additional functionality.

- `Z + B` = Bone Control
- `Z + Y` = Nothing (Calls method at 800974e4)
- `Z + C-stick up` = Invert colors
- `Z + C-stick down` = Normal colors (revert inverted colors)
- `Z + C-stick left` = Add blur
- `Z + c-stick right` = Add spiral blur
- `C-stick up` = Restart match and show battle intro
- `C-stick down` = Restart match
- `C-stick left` = P1 win animation
- `C-stick right` = P2 win animation

### TXG Viewer

A viewer for TXG texture files.

### Memory Card

Allows you to read and write to the GameCube memory card.

### Movie Test

Allows you to play the h4m movies contained in the game.

### Other Pause Menus

#### Training Mode Pause

```gecko
0405aedc 60000000
0400ad14 4804207d
```

![Training Mode Pause](/training_mode_pause.PNG?raw=true "Training Mode Pause")

#### Battle Mode Pause

```gecko
0405aedc 60000000
0400ad14 480419d1
```

![Battle Mode Pause](/battle_mode_pause.PNG?raw=true "Battle Mode Pause")

#### No Menu Pause

```gecko
0405aedc 60000000
0400ad14 60000000
```

![No Menu Pause](/no_menu_pause.PNG?raw=true "No Menu Pause")
