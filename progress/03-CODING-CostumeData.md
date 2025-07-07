# Log 03 - Coding / Costume Data

I am eager to begin modding these characters, but first, I wanted to compile all of the costume data in the game. This will give me a better grasp of how each attire is constructed and coded. As many wrestlers share the same assets *(ex. boots, wristbands, etc)*, I will need to properly recode certain attires and need the structure.

I created a spreadsheet to document the following : 

- Attire Graphics
  - Body Type M
  - Body Type L
  - Body Type XL
  - Body Type S
  - Body Type Other
- Attire Polygons
- Head / Mask Shapes

Reading the memory, I learned that this block started with Body Size Medium - 1 (Sting Singlet). Each Attire Graphic block is 48 bits.

```
PAL = That specific texture palette
GRA = That specific texture graphic
- SHAPE CATEGORY
- WAIST PAL
- WAIST GRA
- STOMACH PAL
- STOMACH GRA
- CHEST PAL
- CHEST GRA
- LOWER LEFT LEG PAL
- LOWER LEFT LEG GRA
- UPPER L LEG PAL
- UPPER L LEG GRA
- LEFT FOOT PAL
- LEFT FOOT GRA
- LEFT HAND PAL
- LEFT HAND GRA
- LEFT FINGERS PAL
- LEFT FINGERS GRA
- LOWER LEFT ARM PAL
- LOWER LEFT ARM GRA
- UPPER LEFT ARM PAL
- UPPER LEFT ARM GRA
- LOWER RIGHT LEG PAL
- LOWER RIGHT LEG GRA
- UPPER RIGHT LEG PAL
- UPPER RIGHT LEG GRA
- RIGHT FOOT PAL
- RIGHT FOOT GRA
- LOWER RIGHT ARM PAL
- LOWER RIGHT ARM GRA
- RIGHT HAND PAL
- RIGHT HAND GRA
- RIGHT FINGERS PAL
- RIGHT FINGERS GRA
- UPPER RIGHT ARM PAL
- UPPER RIGHT ARM GRA
- END
```

Using "Copy -> Gameshark Code", I was able to copy and paste the data quickly.

![costumedata](https://github.com/user-attachments/assets/6aae259f-ba35-4531-b2ed-2ad7d57ddcdf)

In the old days, it would be typing each individual address + value in a notepad file just to share on eZboard. A member named "DOOMSDAY EWF" archived a lot of Attire + Arena addreses for these games. Must have been a lot of work.

Attire Polygons were half the size of the graphics, but maintained a similar pattern.
```
WAIST
STOMACH
CHEST
LOWER LEFT LEG
UPPER LEG LEG
LEFT FOOT
LEFT HAND
LEFT FINGERS
LOWER LEFT ARM
UPPER LEFT ARM
LOWER RIGHT LEG
UPPER RIGHT LEG
RIGHT FOOT
LOWER RIGHT ARM
RIGHT HAND
RIGHT FINGERS
UPPER RIGHT ARM
END
```

Head/Mask followed this pattern : 
```
NECK SHAPE
FACE SHAPE
HEAD SHAPE
NECK PAL
NECK GRA
FACE PAL
FACE GRA
HAIR PAL
HAIR GRA
RIP PAL
RIP GRA
SKIN COLOR
```

I learned that I had a total of 129 in-game heads to use for this project. There's a patch of open-space nearby which I should be able to use for a few more (The planned goal is 170). But, I need to make sure it works for playing the ROM on other devices before going too far. Open-space can be delicate and I don't want to lock this project to emulators.

After compiling all of this data, I think I'm ready to start my first attire. 
