# Log 02 - Roster Coding

I opened the ROM in Hex Editor Neo today and jumped down to the section which handles the data for default wrester information.

*I don't know how markup will translate to mobile website, as I'm only updating via desktop.*

Each wreslter has bio data for the following : 
- Name / Short Name / Short Only
- Height
- Weight
- Taunts (Moved)
- Camera Movement
- Manager / Accompanied By
- Ring Taunt Type
- Pyro Type

Sting example.  
```
RAM : 80038E60
OFF : C00
R0M : 39a60
```

```
3c 53 74 69 6e 67 3e 00 00 00 00 00 36 27 33 22
00 00 00 00 32 35 32 6c 62 73 2e 00 00 00 00 00
00 01 01 00 1d 0e 1d 34 80 03 8e 60 80 03 8e 6c
80 03 8e 74 0b 00 02 60 00 00 00 00
```

```
<Sting> : 3c 53 74 69 6e 67 3e
 Height : 36 27 33 22 (6'3")
  Break : 00 00 00 00
 Weight : 32 35 32 6c 62 73 2e 00 (252lbs.)
  Break : 00 00 00 00
    ID1 : 00 01
    ID2 : 01 xx
S-Taunt : 1D0E
R-Taunt : 1D34

  Name Point : 80 03 8e 60
Height Point : 80 03 8e 6c
Weight Point : 80 03 8e 74

 Camera : 0b
Manager : 00
Ent Type: 02
   Pyro : 60

End Break: 00 00 00 00
```

Names can be split in different ways :

```
Full Name
<Short Name> (+ Long Name)
{Short Name Only}
```
**Breaks** are used to keep run-off on the text. Without a 00 separating Height + Weight, the text can continue on their on-screen profile info. Ex : 6'1"252lbs.

**S-Taunt** is the animation that they would do on the stage. I believe this was eventually hardcoded into the moveset as changing them has no effect.

**R-Taunt** is the animation that they would do in the ring. Like the Stage Taunt, it was hardcoded into the wrestler moveset. 

**Camera** changes the POV of the on-stage entrance. I didn't test out all the values yet, but it decides whether the camera pans left/right, straight forward, etc. 

**Manager** decides who accompanies the wrestler to the ring. It follows the ID2 and there's no way to change between Attire 1-4 of that manager. *Maybe?*

**Ent Type** is classified how they enter the ring and where they stand during their in-ting taunt. 

```
00 - Walk + Center of Ring
01 - Run  + Center of Ring
02 - Walk + Turnbuckle Face Crowd
03 - Run  + Turnbuckle Face Crowd
04 - Walk + Turnbuckle Face Ring
05 - Run  + Turnbuckle Face Ring
etc.
```

 **Pyro** decides what type of fireworks they get. Booker T. gets flames (40), Goldberg gets standard fireworks (11), etc. 

Most of this information will come in handy later when refining the characters. It'll also be helpful for future Revenge projects. 

**Pointers** point to 1) the beginning of the name, 2) wrestler height, 3) wrestler weight. They must point to an address ending in 0, 4, 8, or C, *or the game might crash?*. 

Started with a blank spreadsheet, set up with :
- ROM Address 
- RAM Address
- ID Point
- Wrestler Name
- Default ROM Address
- New ID Point

Here's a picture, it makes no sense, but worked.
![roster-spreadsheet](https://github.com/user-attachments/assets/96150fc3-986b-42aa-a0c7-c028538fb869)

You don't need a full 00 00 00 00 break between the name/height/weight. As long as there is one 00 to end the data **and then** you can start a new line on a 0/4/8/C address, you can crunch the profile data to make space for longer names.

Default Sting :
![defaultsting](https://github.com/user-attachments/assets/4b852180-d868-4903-a1cd-846484c0e5f5)

New Sting : 
![editsting](https://github.com/user-attachments/assets/28f024bc-5989-46b2-ab85-86cbb4bf1354)

You save ~8 extra bits of space where you can start GIANT a little earlier.

But because of that shift, I had to rewrite the pointers for NAME, WEIGHT, HEIGHT. This was a quick calculation taking the rom address and subtracting C00. This is where that spreadsheet above came in handy.

If you squeeze/expand the wrestler data using this method, you have to make sure their new ID address is changed in the **ROSTER LAYOUT** data after the final character's bio section.

![wrestlerblocks](https://github.com/user-attachments/assets/e63fa878-a754-4dd3-878f-5dcb78ed5435)

This is later used to properly build stables. 

After rewriting my entire roster with their proper names, I actually had 312 total bits of empty space.

The stable pointers weren't locked into a specific address. With my empty space, I pulled the wrestlers up 4 lines. This allowed me to stack extra wrestlers in my stables without worrying about overflow and limitations. 

These wrestlers also need their own ID2. If two or more slots share the same value, there can be crashing when editing names or during gameplay. It goes up to hex-49 / dec-73 total characters, which is enough for the game.

And every character needs to be accounted for in the Stable Data, even if they are a manager. 

During this process, there was one thing I didn't like : Two name splits were exclusive to the Kanyon/Mortis and AKI Man / THQ Man slots. I'll have to figure that out later because I need to split HOLLYWOOD & HULKSTER, and maybe expand some shared slot info.

This was tedious, but I think it was needed. I didn't want to squeeze names into their maximum slot -- *ex: Hacksaw Jim Duggan referred to as only "Duggan"*.


