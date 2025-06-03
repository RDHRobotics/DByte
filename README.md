# USB D-Byte (BadUSB) Documentation
## 📚 Table of Contents
- [Specs USB D-Byte](#specs-usb-d-byte)
- [Scripting](#scripting)
  - [Basics](#basics)
  - [Functions](#functions)
  - [Keys](#keys)
  - [Mouse](#mouse)
- [Credits](#credits)

---

## Specs USB D-Byte
* Dimensions: 38mm x 16.5mm x 6.5mm
* Dual-core 133 MHz 32-bit CPU
* 16 MB SPI flash (15 MB accessible via USB)
* 2 Position Mode Switch (Attack & Setup)
* USB-A plug
* Reset & boot button

## Scripting
### Basics

:::note
USB D-Bytes's script language is compatible with Ducky Script (1.0). However, some functions and keys were added or expanded.
You can find a great Ducky Script quick reference at [docs.hak5.org](https://docs.hak5.org/hak5-usb-rubber-ducky/ducky-script-quick-reference).
:::

## Basic rules:
* A single space separates the keys
* All keys as part of the same line get pressed and released simultaneously
* To write text, use the `STRING` function
* Upper and lower case matters!

| Example | Explanation |
| ------- | ------------ |
| `WINDOWS R` | Press the Windows key and the R key simultaneously |
| `STRING Hello World` | Write "Hello World" |

## Example Script:

```
REM Hello World Example Script
DEFAULTDELAY 200
DELAY 1000
GUI r
STRING notepad
ENTER
DELAY 1000
STRING Hello World!
```

| Line | Explanation |
| ---- | ------------ |
| `REM This is a comment` | Comment something. |
| `DEFAULTDELAY 200` | Set the default delay between each line to 200 milliseconds. |
| `DELAY 1000` | Wait 1 seconds. |
| `GUI r` | Press the Windows key and the R key simultaneously to open the run window. |
| `STRING notepad` | Type "notepad". |
| `ENTER` | Press enter key to launch the Windows Notepad application. |
| `DELAY 1000` | Wait 1 seconds. |
| `STRING Hello World!` | Type "Hello World!" into the newly opened notepad window. |

## Functions

### Main Functions

| Command | Example | Description |
| ------- | ------- | ----------- |
| `#` or `REM` | `# Hello World!` | Comment |
| `DEFAULTDELAY` or `DEFAULT_DELAY` | `DEFAULTDELAY 200` | Time in milliseconds between every command |
| `DELAY` | `DELAY 1000` | Delay in milliseconds |
| `STRING` | `STRING Hello World!` | Types the following text |
| `STRINGLN` | `STRINGLN Hello World!` | Like STRING but presses enter at the end |
| `REPEAT` or `REPLAY` | `REPEAT 3` | Repeats the previous line n times |

:point_down: **More functions below**

### Keyboard Layout

:::tip
You can also change the default keyboard layout in the [preferences.json](/docs/preferences). That way, you don't have to use LOCALE in your script.
:::

Use `LOCALE` to change the keyboard layout. This is necessary for everyone who's not using the US keyboard.  
Otherwise, your BadUSB might type the wrong characters.

Here's an example using the German keyboard layout:
```
LOCALE DE
STRING Gänsefüßchen
```

### Available Keyboard Layouts

| Region | Standard Layout | Mac Layout | Note |
| ------ | --------------- | ---------- | ---- |
| Belgium 🇧🇪 | `BE` | `BE_MAC` | |
| Bulgaria 🇧🇬 | `BG` | `BG_MAC` | |
| Canada 🇨🇦 | `CA-CM`, `CA-FR` | `CA-FR_MAC` | |
| Switzerland 🇨🇭 | `CH-DE`, `CH-FR` | `CH-DE_MAC`, `CH-FR_MAC` | |
| Czech Republic 🇨🇿 | `CZ` | `CZ_MAC` | |
| Germany 🇩🇪 | `DE` | `DE_MAC` | |
| Denmark 🇩🇰 | `DK` | `DK_MAC` | |
| Estonia 🇪🇪 | `EE` | `EE_MAC` | |
| Spain 🇪🇸 | `ES` | `ES_MAC` | |
| Latin-America 🌎 | `ES-LA` | `ES-LA_MAC` | |
| Finland 🇫🇮 | `FI` | `FI_MAC` | |
| France 🇫🇷 | `FR` | `FR_MAC` | |
| United Kingdom 🇬🇧 | `GB` | `GB_MAC` | |
| Greece 🇬🇷 | `GR` | `GR_MAC` | |
| Croatia 🇭🇷 | `HR` | `HR_MAC` | Since v1.2.1 |
| Hungary 🇭🇺 | `HU` | `HU_MAC` | |
| Ireland 🇮🇪 | `IE` | - | |
| India 🇮🇳 | `IN` | `IN_MAC` | |
| Iceland 🇮🇸 | `IS` | `IS_MAC` | |
| Italy 🇮🇹 | `IT` | `IT_MAC` | |
| Latvia 🇱🇻 | `LT` | `LT_MAC` | |
| Lithuania 🇱🇹 | `LV` | `LV_MAC` | |
| Netherlands 🇳🇱 | `NL` | `NL_MAC` | |
| Norway 🇳🇴 | `NO` | `NO_MAC` | |
| Poland 🇵🇱 | `PL` | `PL_MAC` | |
| Brazil 🇧🇷 | `PT-BR` | `PT-BR_MAC` | |
| Portugal 🇵🇹 | `PT` | `PT_MAC` | |
| Romania 🇷🇴 | `RO` | `RO_MAC` | |
| Russia 🇷🇺 | `RU` | `RU_MAC` | |
| Sweden 🇸🇪 | `SE` | `SE_MAC` | |
| Slovenia 🇸🇮 | `SI` | `SI_MAC` | |
| Slovakia 🇸🇰 | `SK` | `SK_MAC` | |
| Turkey 🇹🇷 | `TR` | `TR_MAC` | |
| Ukraine 🇺🇦 | `UA` | `UA_MAC` | |
| United States 🇺🇸 | `US` | `US_MAC` | |

## Multi-Line Comments

If you have a lot to say, you can use multi-line comments using `###`:
```
###
The quick brown 
fox jumps over 
the lazy dog
###
```

## Large Strings

For longer texts, use `LSTRING_BEGIN` and `LSTRING_END`. 
Everything between those two commands, including linebreaks, gets typed out:

```
LSTRING_BEGIN
The quick brown 
fox jumps over 
the lazy dog
LSTRING_END
```

## Loops

To repeat one or more lines, you can use `LOOP_BEGIN` and `LOOP_END`, which works just like a for-loop: 
```
LOOP_BEGIN 3
STRING Hello 
DELAY 1000
STRINGLN World!
LOOP_END
```

## Imports

With `IMPORT`, You can start running another script from within a script! This is particularly useful if you want to split your script into multiple files for better readability - instead of having one gigantic script.

```
IMPORT second_script.txt
```

## LED

Control the onboard LED with the `LED` function.
You can either set the color (`R`, `G`, or `B`) and mode (`SOLID`, `SLOW`, `FAST`, or `OFF`) like this:
```
LED R SOLID
LED G SLOW
LED B FAST
```

Or you can set a specific RGB color value (0-255) like this:
```
LED 42 13 37
```

And optionally, you can also set a blink interval in milliseconds (r,g,b, blink):
```
LED 42 13 37 500
```

## Custom Keycodes

The `KEYCODE` function sends specified keycodes to the target computer. You can use it to press any key or combination possible. 
This is particularly useful if a key is not specified in the script language.

This example presses shift and a, resulting in an "A":
```
KEYCODE 0x02 0x04
```

The first argument specifies the modifiers (like shift, ctrl, or alt). The second argument is a key; you can specify up to 6 keys.
Values can be in decimal or hexadecimal:  
`KEYCODE modifier key1 [key2] [key3] [key4] [key5] [key6]`

## Keys

### Standard Keys

| Key |
| --- |
| `a` - `z` |
| `A` - `Z` |
| `0` - `9` |
| `F1` - `F12` |

## Modifier Keys

| Key |
| --- |
| `CTRL` or `CONTROL` |
| `SHIFT` |
| `ALT` |
| `GUI` or `WINDOWS` or `COMMAND` |

## Other Keys

| Key |
| --- |
| `ENTER` |
| `MENU` or `APP`|
| `DELETE` |
| `HOME` |
| `INSERT` |
| `PAGEUP` |
| `PAGEDOWN` |
| `UP` or `UPARROW` |
| `DOWN` or `DOWNARROW` |
| `LEFT` or `LEFTARROW` |
| `RIGHT` or `RIGHTARROW` |
| `TAB` |
| `END` |
| `ESC` or `ESCAPE` |
| `SPACE` |
| `PAUSE` or `BREAK` |
| `CAPSLOCK` |
| `NUMLOCK` |
| `PRINTSCREEN` |
| `SCROLLLOCK` |

## Numpad Keys

| Key |
| --- |
| `NUM_0` - `NUM_9` |
| `NUM_ASTERIX` |
| `NUM_ENTER` |
| `NUM_MINUS` |
| `NUM_DOT` |
| `NUM_PLUS` |
### Mouse

| Command | Example | Description |
| ------- | ------- | ----------- |
| `MOVE x y` or `MOUSE x y` | `MOVE 100 0` | Move the mouse cursor |
| `CLICK button` or `MOUSE_CLICK button` | `CLICK 1` | Click a mouse button |
| `PRESS button` or `MOUSE_PRESS button` | `PRESS 2` | Keep pressing a mouse button |
| `RELEASE button` or `MOUSE_RELEASE button` | `RELEASE 2` | Release a mouse button |
| `SCROLL v h` or `MOUSE_SCROLL v h` | `SCROLL -10 0` | Scroll vertically or horizontally |

## Mouse Buttons

| Button | Description |
| ------ | ----------- |
| `0` | Left button |
| `1` | Right button |
| `2` | Middle button |
| `3` | Backward button |
| `4` | Forward button |

## Credits

This project is based on [USB Nova](https://github.com/SpacehuhnTech/USBNova) by SpacehuhnTech.  
Firmware and hardware have been modified under the terms of the MIT and CERN-OHL-P-2.0 licenses.

Thank you to the open-source community for making innovation accessible to all.
