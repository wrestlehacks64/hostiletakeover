# Log 08 - Game Intro

Took a break from editing graphics today to explore the Game Intro.

A lot of ROM hacks just change the Wrestler ID + Animation, and then maybe edit some overlays. Still feels like the same old game to me.

I want to rewrite the entire intro, but need to learn how it works.

Split into two sections :

**Section A**

This handles the camera angle, camera speed, overlays, scene length, and sound effects.

Example of the "Truck Driving Downhill - Scene 3"

```
800D4F14: 02BC0081
800D4F18: 00030001
800D4F1C: 00000000
800D4F20: 00000000
800D4F24: 00000000
800D4F28: 00000000
800D4F2C: 02000085

02BC = Length of the scene
0081 = Camera (messes up Truck position)
0003 = Scene number 
0001 = Truck setting 
00 00 00 00 x 4
0200 =
0085 = 

```
The 00 00 00 00  blocks are used as pointers to **Section B** information. 

This is the Hogan on Stage example 

```
800D5080: 0087008B
800D5084: 00080011
800D5088: 800D3A18
800D508C: 00000203
800D5090: 00000000
800D5094: 00000000
800D5098: 0C000080

0087 - Frame Length
008B - Camera
0008 - Overlay/Scene
0011 - Location modifier (Stage, Ring, etc)
800D3A18 points to the character animation data.

```

**Section B**

This handles the wrestlers, animations, and their locations.

Hogan on the Stage (Scene 08)

```
800D3A18: 0201000A
800D3A1C: 1D1B0000
800D3A20: 00000000
800D3A24: FEC00800
800D3A28: 00100000
800D3A2C: 02030000
800D3A30: FFFA0032
800D3A34: 00000000
800D3A38: FF9C0800
800D3A3C: 00010000
```

This section has been well documented by others, just curiousity pulled me into learning how the whole intro process was pieced together. 

I'm going to stop before I get too deep into this, but I'm glad to know the basics. 









