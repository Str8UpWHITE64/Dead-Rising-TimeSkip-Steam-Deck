# Dead-Rising-TimeSkip-Steam-Deck
## Goal
To speedrun Dead Rising 1 on the Steam Deck
## Disclosure
I do not take any responsibility for any issues that are caused by following this guide.  While the instructions I have laid out are fairly simple, there is still a small degree of Linux experience that is nice to have.  If you have any questions, feel free to open an issue here or message me.  
## Why this is different than on Windows

With the Steam Deck running Linux, getting games that require mods to talk to eachother is a bit more complex.  The Steam Deck, which runs SteamOS, uses Proton (Steam's fork of Wine) to run Windows EXEs.  When an EXE is run using Proton, a container (called a prefix) is created to house all of the dependencies and files needed for that program to run.  So, when you run a program using Proton, a container is made and locked off from the rest of the system.  This is done so that the program doesnt install files outside of the container and risk screwing up the file system.  When you launch a game on the Steam Deck through Steam, it first creates the prefix, starts the program, then it locks the prefix.  

Dead Rising's TimeSkip mod is used to skip all of the wasted time in the game waiting around for the next mission.  Without the mod, Speedrunning the game is not really possible.  The game's time progresses based off of real time, so no matter how fast you complete a mission, you still have to wait for a timer to tick down before you can continue.  The TimeSkip mod fixes that by injecting into the game, reading the current time, and when it notices that a mission has completed it changes the in-game time to skip ahead to when the next mission is ready to start.

In order to utilize the TimeSkip mod, as well as a program to track time when speedrunning, we need to make it so both the game and our programs all run inside the same prefix.  To do this we first have to have Steam create the prefix, then we stop it before it runs the game and we have it run a script instead.  

## Issues
### Bike Skip
With this setup you will be able to speedrun the game fairly normally in Desktop Mode.  I was able to do the normal Timeskip catagory with BikeSkip. When you add OBS into the mix, the performance dip drops too low to be able to do BikeSkip.  I was seeing 85-110FPS with OBS in the area with the BikeSkip.  Unless another screen recording utility comes along that has less of an impact on performance, I dont see this a catagory that is viable to run on the Steam Deck.  Any other catagory without BikeSkip should work.

### Gaming Mode
You are able to use the TimeSkip mod in Gaming mode, but you are not able to use OBS or LiveSplit.  OBS doesn't launch in Gaming Mode and LiveSplit causes things to lock up.  I see there being two options for speedrunning this game on the Deck: 

* A. Run for practice in Gaming Mode without LiveSplit and without OBS
* B. Speedrun in Desktop Mode.  

If you choose option A, leave out any intruction below with LiveSplit in it or create a second script file that you can swap with the first if you want to switch between.  

### Battery Life
I have not tested the battery life while running the game at uncapped framerate, but I have to assume it wont last very long.  With it running the game, the TimeSkip mod, LiveSplit, and OBS (if trying to record runs) that is a lot of power being used.  
# Installation
I highly recommend a keyboard and mouse for this. Typing and navigating Desktop Mode is a pain without them.
## Files

[Dead Rising](https://store.steampowered.com/app/427190/DEAD_RISING/)

[LiveSplit](https://livesplit.org/downloads/)

["Dead Rising Speedrunning Skip Tool (Up-To-Date)" and "Updated Autosplitter by Edge"](https://www.speedrun.com/dr1/resources).


## Setup
* In Gaming Mode, tap the Options Button on the bottom right of the Steam Deck, opposite of the Steam Button.
* In Performance, turn on Advanced View, and set the FPS limit to off. 
* Go into Desktop Mode on the Steam Deck.  This can be done by tapping the Steam button, going down to Power, then choosing "Switch to Desktop Mode"
* Download the files listed above.
* Open up Dolphin, the File Manager, and navigate to your Dead Rising folder.  For me that is in `/run/media/mmcblk0p1/steamapps/common/Dead Rising/`
* Copy the TimeSkip mod EXE and the contents of the LiveSplit folder into the Dead Rising folder.

#### Create the Script
Open Konsole and navigate into the Dead Rising folder:

`cd /run/media/mmcblk0p1/steamapps/common/Dead\ Rising/`

Create the script:

`nano script`

In the new empty prompt:

`#!/bin/bash`

`"/home/deck/.local/share/Steam/steamapps/common/Proton 7.0/proton" run DeadRising.exe & "/home/deck/.local/share/Steam/steamapps/common/Proton 7.0/proton" run DeadRisingSpeedrunningSkipTool.exe & "/home/deck/.local/share/Steam/steamapps/common/Proton 7.0/proton" run LiveSplit.exe`

On your keyboard click 'ctrl' and 'x'.  It will ask you if you want to save the file, hit 'Y' then 'Enter'.

Change the permissions of the script to allow it to be executed.

`chmod 755 script`

#### Set Steam Launch Option
* Open Steam and navigate to your Library
* Right click on Dead Rising
* Click Properties

In General, at the bottom, you should see Launch Options with an empty box below it. Enter:

`./script && echo %command% >/dev/null`


## Closing
This should get everything set up to run the three programs at once through Steam.  You should test it before returning to Gaming Mode in case something isnt setup properly.  When Dead Rising is up and running, you should be able to hit "Connect" in the TimeSkip mod window and it should say connected.  When you start a game it should track the time properly.  

If you choose to run the game without LiveSplit and OBS through Gaming Mode, you can switch between the active top window by hitting the Steam button and switching between the TimeSkip mod window and the game window.  

I wont go through how to set up the autosplitter option in LiveSplit, because there are tutorials for that on YouTube.  Just run Dead Rising from Steam after doing the whole setup listed above, and make changes in the LiveSplit window that comes up with the game.  I've noticed its a little slow to start, but it runs fine and auto-splits correctly.  

# Credit
Thanks to Souzooka for creating the TimeSkip mod as well as giving some pointers for getting it to work on the Deck.  [Here](https://github.com/Souzooka) is a link to his Github.
