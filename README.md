# ZX81-Runaway-Car
A simple low res game in 1K

I decided a while ago to try and write a game in 1K on the ZX81. Needless to say it had to be in Z80 machine code to stand any chance of doing anything reasonable (ish) in such a limited space! So I bought a few books, asked a few questions (mostly about the memory layout of the zeddy and how to minimise byte usage) and ended up with Runaway Car! 

Its a simple game where you need to avoid the oil spills and collect brake fluid. Every time you hit an oil spill you lose a lot of brake fluid and even if you avoid them all you still lose some every time the screen scrolls down. If you brake fluid level gets low an engine warning light comes on! 
Use pretty much any key on the left of the keyboard to move left, and any on the right to move right. The further you travel the faster it gets.

Overview of features: - 

 . Selectable difficulty level (1 to 9) which determines the starting speed
 . Engine warning light
 . Collectable brake fluid
 . Obstacles to avoid 
 . Increasing difficulty
 . High score
 . Joystick support for the ZXpand with AY add-on
 . Crash animation (sort of)
 . Instructions
 . Runs is 1K!!!
 
There are a couple of issues - the random obstacle generation is not as random as I would like and there is a flicker on the car redraw as the screen scrolls down. But even so not too bad for 1K I guess.

The initialisation process fills the screen with black characters (inverted space) and a middle white line. Originally the road was white with a black vertical border but changing to the current layout meant that I could do away with the border and save the screen height * 2 bytes!

The main process is to draw a number of random oil spills on the top line of the screen and then continuously scroll the top line down a line. Every time the top line is scrolled down a new line is created. As the screen memory maps 1:1 for the characters being displayed just moving the bytes in the display file moves the screen so no separate array is required to hold the position of spills.

When a line gets to the bottom of the screen the position of the car is retained and compared to the line being moved down. If the character moving down is a spill a larger amount of brake fluid is removed otherwise 1 is removed. When brake fluid goes below a set level the warning light comes on. When it gets to zero there is a crahs animation and the game ends. Press a number to restart at the appropriate speed.
