
![screenshot](https://github.com/fastrgv/Asud/blob/main/menu.png)


# ASUD: Ada Sudoku Assistant

Use the following link to download the latest release, including source code:

https://github.com/fastrgv/Asud/releases/download/v1.0.0/asud.7z


-----------------------------------------------------------------

### First, some terminology:

A given cell belongs to 3 "houses": its row, its column, its 3x3 box.
In X-sudoku, a cell could also belong to a 4th house: the diagonal.
Cells can "see" each other if they are in the same house.
Singletons are cells with all digits but one eliminated.



## Introduction

Pencil & paper Sudoku fans that need help will find that this [free & offline] app can help 
them to identify & eliminate candidate digits, using Windows or Linux.

ASUD is a sudoku assistant tool designed to help with manually solving Sudoku puzzles.
It handles routine tasks so you can focus on more advanced puzzle solving strategies.
In each of the 81 cells, all candidate digits are shown. The working goal is to
facilitate the removal of as many candidate digits (aka pencil marks) as possible.

Algorithms have been added to detect and display (hidden or naked) pairs, triples, & quads,
whose display can be toggled.

In addition to showing all candidate digits in each cell, 
the default display mode shows matching digit-pairs in RED that reside within each 3x3 box.

One can toggle a "minimal" display that just shows a) known singletons, b) box-digit-pairs.
This minimal display could allow easier pattern recognition.

Executables that run [offline] on Windows, and GNU/Linux are delivered.
All source code, build scripts & resources are included.


## Display conventions:

* Colored digits are singles or pairs **within** each 3x3 box;
	allows you to manually delete those digits from the other cells in the same row or column. A single Green digit within a box flags the only occurrence of that digit; 
	so it must be the correct one for its cell.

* CYAN digits can be toggled to show pairs, triples, or quads within each house;
	allows you to manually delete those digits from the other cells of the house.
	For triples & quads the displays of naked versus hidden have been separated
	to reduce confusion.


## Controls:

* mouse-click 	=> select one of 81 cells from among 9x9 array to edit

* [1..9]-key	=> toggle numeral n within selected cell

* [esc]-key		=> Quit

* [h]-key		=> toggle this key menu

* [s]-key		=> Save puzzle state for later restart

* [r]-key		=> Restore (using data from previous save)


* [f]-key		=> Flush-dups: for each cell with a single digit, this removes it
						from all other cells in its 3 houses.

* [u]-key		=> findUnique: searches all houses
						for a single occurrence of a given digit, then
						removes all other digits in its cell,
						and then performs a Flush operation on its other houses.

* [b]-key		=> toggle a Brute-Force solver to find [first] solution

--------------------------------------------------------------------------

* [m]-key		=> view toggle Minimal: hides unknown candidate digits except for 
						RED & GREEN (might enhance pattern recognition)

* [=]-key		=> view: toggle RED/GREEN coloring of box-digit-pairs/singles (default=ON)

* [p]-key		=> view: triple-toggle Pairs: 1) hidden, 2) naked, 3) off

* [t]-key		=> view: triple-toggle Triples: 1) Hidden, 2) Naked, 3) Off

* [q]-key		=> view: triple-toggle Quads: 1) Hidden, 2) Naked, 3) Off

* [y]-key		=> view: toggle Y-wing (shows only 1st-found)

* [x]-key		=> view: toggle badXcycle (shows only 1st-found)

* [k]-key		=> view: toggle Key-Cell digit-pair test

* [l]-key		=> view: Linked-pairs hilighted with alternating Magenta/Cyan colors

* [d]-key		=> view: toggle Digit-Doubles in rows & columns (for possible Xwings)


Notes:

* Naked triples **within boxes** are NOT shown to reduce clutter. Same for naked quads & naked pairs.
* The last 10 view-toggles are mutually exclusive: activating one deactivates others.
* Linked-Pairs (l-key): each digit might have multiple chains that are cycled thru in order;
	(you can make a quick exit by pressing a different view-toggle key).
* If a bad [contradictory] Xcycle is found, the first/last digits are CYAN, the other digits involved are green.
* Key-Cell test (k-key), for a cell with only 2 candidates, shows one in RED if it leads to logical contradiction. Also shows consequences of the RED digit by showing the resulting singletons in GREEN and the resulting empty cells in a BLUE outline.

--------------------------------------------
## Features

* F.O.S.S. (Free Open Source Software);
* runs [offline] on Windows & Linux;  Linux binary runs on many distros!
* uses GLFW3;
* works on HiDPI displays;
* no installation;
* no dependencies;
* simply unzip in your Downloads directory, or to a flash drive, and run.

------------------------------------------------

## Setup & execution:

Windows users see "windows-setup.txt".

Unzip the archive.  On Windows, 7z [www.7-zip.org] works well for this.
The proper command to extract the archive and maintain the directory structure is "7z x filename".

Users may then open a terminal window, cd to install-directory, then, at the command line, type the executable name to start the tool. (the command **must** be run from the install-directory)

Let {fnam} indicate an optional input file-name...

----------------------------------------------------------------------
In Linux type "lsud {fnam}".

You can also use the Windows executable under wine, thusly:
	* wine binw64/sud.exe {fnam}

----------------------------------------------------------------------
Windows users type:  "wsud.bat {fnam}" or "binw64\sud.exe {fnam}"
 
----------------------------------------------------------------------

## Input Files (normal sudoku):

* If no commandline parameters are passed to the executable, then the previously saved puzzle is restored.

* If one commandline parameter is passed, it must be the name of a [local] valid input file.

In order to create a valid input file, copy the prototype file named "s0.txt" to a filename of your choosing. 
Then edit it to match your puzzle, say sud1.txt. Zeros imply that the value is not known.
So just insert the known puzzle values into their proper positions.

(According to s0.txt, you may notice that the digit entries must be separated by spaces,
and that textual comments after the end are tolerated.)

Then simply type the command name followed by the input file name.

* EG: binw64\sud.exe puzzles\sud1.txt (Win64)
* EG: lsud puzzles/sud1.txt (linux)

...

After working with the tool and eliminating as many candidate digits as possible,
one can save the state using the "s" key. This creates the file: frestore.txt

To restart, type the executable name with no parameter.





## Using the Available Tools:

The general idea for solving a sudoku puzzle is to eliminate candidates in each cell down to one singleton.

Use the following methods to work towards a solution:

* using the default screen, if a cell has a GREEN digit, remove any others in the same cell
* using the default screen,  remove candidates aligned with matching RED digits in a box
* remove candidates using 
	* Pairs-view
	* Triples-view
	* Quad-view
	* Ywing-view
	* Linked-Pairs-view
	* Xcycle-view.
* f-key: Flushdups
* u-key: findUnique

-----------------------------------------------------------------------------------------------------
The hidden pairs/triples/quads tool allows particularly easy removal of excess candidates.
Simply remove the digits in each involved cell that are NOT highlighted.

If new RED or GREEN digits appear, you might be able to eliminate even more candidates.

-----------------------------------------------------------------------------------------------------

### Linked-Pairs
A digit-pair refers to the situation when a single house has exactly 2 occurrences of a
single digit. This view shows a chain of digit pairs with alternating colors, where
one color represents ON and the other OFF, but we don't yet know which is which.
The Linked-Pairs view allows manual application of the following rules for elimination:

* if any house has 2 digits of same color, that color must represent OFF (to be eliminated).
* if any non-colored digit can "see" itself in both colors, it must be OFF (eliminated).

Helpful comments to identify removable digits are printed in the terminal window.
EG [ linked-pairs(3) 1 of 3 ] shows comments like:
"dig@row,col: 3@ 4 2 can see 2 colors!" and
"dig@row,col: 3@ 5 2 can see 2 colors!" (2nd rule above)


-----------------------------------------------------------------------------------------------------

### Bad-Xcycle
This view shows a chain of digits that is similar to, but more general than digit-pairs.
The bad-Xcycle view shows a cyan & green chain of digits, alternating in colors,
where one color represents ON and the other is OFF. If anything is displayed,
then the first digit shares a house with another of the same color, which means that
color must represent OFF. Thusly, the first digit in the chain [CYAN] should be removed.
The on-screen label shows the cell-coordinates of the first & last cells in the chain;
EG: "Xcycle-19-99" indicates the first cell in the chain is at row=1, col=9.

-----------------------------------------------------------------------------------------------------

### Ywing
Here, the first Ywing found is displayed. A Ywing is a triple of related cells, 
only one of which, the pivot, can see the other two, the pincers. 
The 2 pincers intersect at a "target" cell. The pivot has only 2 candidates, 
where either one forces the elimination of a common digit in the target cell.
If no target exists, or it has been removed, then nothing will be displayed.

-----------------------------------------------------------------------------------------------------
The techniques above will only solve the simpler puzzles.
There exists very difficult ones that require advanced methods and insights.

-----------------------------------------------------------------------------------------------------

### Key-Cell
If you have reduced the candidates as much as possible, then you likely have many cells
with only 2 candidates, particularly each cell of a naked pair. For such cells
you can select the cell with the mouse, then use the k-key. This, last-resort
**Key-Cell** test searches the ramifications of selecting one-of-two digits that leads to 
a logical contradiction. If so, the digit is shown in RED, indicating it should be removed.
A contradiction appears in the form of a cell that would become empty outlined in blue,
as well as digits that would become singletons in either GREEN or CYAN. The CYAN 
color is used when a digit appears more than once in the same house. If you cannot understand 
why a blue cell becomes empty, then it may be easier to find why a [would-be-singleton] digit 
appears twice in the same house, and trace the logic for that contradiction.

If no digit appears RED and no blue cells appear, then you will have to try something else. 
**Key-Cell** is a cheap equivalent to a combination of advanced methods like 3Dmedusa, 
Alternate-Inference-Chain, Hidden-Unique-Rectangle, linkedPairs, bad-Xcycles, Ywing, etc.

A logical sequence of deletions followed by their motivating new singletons is
written to the console window to attempt to explain why the blue cells are empty.
EG: "-8 @ 86  <=  +8 @ 46" 
	[ deleted digit 8 @ cell(8,6) because singleton 8 was found @ cell(4,6) ].

-----------------------------------------------------------------------------------------------------

### Guessing
Guessing is easy to do with this app. but make sure to **save the state** BEFORE you resort to it. 
If you do and subsequent Unique or Flush operations lead to some empty cells, 
then you guessed wrong. So then you can easily restore and continue.
Cells where every digit has been eliminated are one manifestation of a contradictory assumption.



----------------------------------------------



## Build Requirements:
* systems:  Windows, or GNU/Linux
* a recent Ada compiler;  eg. GNU-Ada...try this link:

https://github.com/alire-project/GNAT-FSF-builds/releases


## Build instructions:

Two [pre-compiled] binary executables are delivered, one for Windows
and one for linux. Both are fairly portable. Also remember that the
Windows binary will run under WINE on Linux.

Thus, for most people, rebuilding is unnecessary.

If you still want to rebuild, then execute the following scripts:

* msWin64 =>
	* setpath64.bat
	* wcmp.bat

* linux =>
	* lcmp.sh

Note that these scripts might need to be adjusted to reference 
your actual installation directory for 64bit GNU Ada compiler.

-------------------------------------------------------


## Algorithmic Notes

There is an interesting relation between the two algorithms to find 
naked and hidden pairs, triples or quads. The hidden searches are a 
much more formidable problem for humans, yet the algorithmic solution 
is similar and only slightly more complex. In fact, I would call the 
two algorithms mathematical duals...complementary strategies, in some sense.

For those interested, I suggest studying the 2 files

* asud-nakedpairs.adb 
* asud-hiddenpairs.adb.


## Final Notes

1) This app should be considered an in-progress prototype.

2) There is also a prototype X-sudoku tool (asudx) with similar capabilities & interface.
In this type of puzzle, each cell can be in either 3 or 4 houses, 
because the 2 diagonals are also houses.

3) Brute-force solvers [susolve/susolvex] are also included under ./bruteForceSolver/. 
They display the first-found solution to the screen:

* wsol.bat {filename} (on Windows)
* susolve  {filename} (on Linux)

For X-sudokus use wsolx.bat/susolvex.

-------------------------------------------------------------------------

## TBD list:
* Input puzzle handling is primitive.
* No Xwing, swordfish or 3Dmedusa highlights, is yet provided. However Digit-Doubles-view (d-key) might help finding Xwings, and KeyDigit (k-key) will, FTTB, provide another way to eliminate candidates.
* You will probably find that the sparse user interface works differently than mainstream apps, but still can be helpful, nevertheless, and ASUD is free. (I was not inclined to purchase a mainstream app for evaluation!)

----------------------------------------------

## what is special about this project?

Uses the Ada programming language and modern OpenGL methods, with textures, shaders and uniforms.  Compiles and runs on Windows and GNU/Linux.

Focusing on portability, transparency, and open source freedom, this project relies exclusively on F.O.S.S. tools:  a thin GLFW3 binding, a thin OpenGL binding, a PNG reader by Stephen Sanguine & Dimitry Anisimkov, and a GNU-Ada compiler.

The linux-build is among very few modern OpenGL apps where a single pre-built executable can run on multiple Linux distros without 3rd party add-ons!

Open source Ada developers are welcome to help improve or extend this app.

Developer or not, Sudoku fans can send comments, suggestions or questions to:
fastrgv@gmail.com



===================================================================
## License

asud itself is covered by the GNU GPL v3 as indicated in the sources:


 Copyright (C) 2023  <fastrgv@gmail.com>

 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.

 You may read the full text of the GNU General Public License
 at <http://www.gnu.org/licenses/>.

-------------------------------------------------

## Download Sites for all my puzzles, games & apps:

I have written many other interesting games, puzzles, and tools, that can be found at the following sites:

* https://github.com/fastrgv?tab=repositories
* https://www.indiedb.com/members/fastrgv/games
* https://fastrgv.itch.io
* https://sourceforge.net/u/fastrgv/profile/
* https://gamejolt.com/@fastrgv/games

A standalone sokoban solver, and a morse code tool are only found at the SourceForge or GitHub sites.

-------------------------------------------------


## Revision History:


**ver 1.0.0 -- 25may2023**

* Initial release.
