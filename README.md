
![screenshot](https://github.com/fastrgv/Asud/blob/main/menu.png)

Menu Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/l-pairs3.png)
Linked-Pairs Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/badKeyCell.png)
Bad Key Cell Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/badXcycle_sudx.png)

Bad Xcycle: remove 3 @ (2,2)

---------------------------------------------------------------------------


Here is the link to the latest release, which includes all source:

https://github.com/fastrgv/Asud/releases/download/v1.0.5/sud28jun23.7z

===============================================================================




# ASUD: Ada Sudoku Assistant


## Most recent changes


**ver 1.0.6 -- 1jul2023**

* Fixed serious error in Xsudoku keyboard code.
* Improved action in xCycle-view.
* Standard (minimal) view now also shows non-aligned box pairs in blue.
* Added quick [non-modal] method to emplace a single into a selected cell using (ctrl)+(dig)
* Improved the helpfulness of the Digit-Doubles-view by highlighting removable digits.

More revision history is at end of this file.

-----------------------------------------------------------------

### First, some terminology:

A given cell belongs to 3 "houses": its row, its column, its 3x3 box.
In X-sudoku, a cell could also belong to a 4th house: the diagonal.
Saying cells can "see" each other means they share a house.
Singles are cells with all digits but one eliminated. A single also
refers to a candidate digit that is unique in one of its houses,
even if its cell has other candidates.



## Introduction

ASUD is a sudoku assistant tool designed to help with manually solving Sudoku puzzles.
It handles routine tasks so you can focus on more advanced puzzle solving strategies.

For example, some of the routine and somewhat tedious tasks are:

* noticing single occurrences of a digit within some house
* removing a singleton digit from all visible cells
* noticing whether a digit is removable in a given circumstance
* finding hidden triples & quads, etc.

In each of the 81 cells, all candidate digits can be shown. The working goal is to
facilitate the removal of as many candidate digits (aka pencil marks) as possible.

Algorithms have been added to detect and display (hidden or naked) pairs, triples, & quads,
whose display can be toggled.

The default display shows all candidate digits in each cell. However, one can toggle a 
minimal "standard" display that just shows a) known singles, b) box-digit-pairs.
This minimal display could allow easier pattern recognition.

Pencil & paper Sudoku fans that get stuck will find that this app can help 
them to get a new perspective, using any PC or laptop.
This package includes executables that run on Windows, and Linux.
All source code, build scripts & resources are included.




## Controls:

* mouse-click 	=> select/Deselect one of 81 cells from among 9x9 array to edit

* [1..9]-key	=> toggle candidate numeral n within selected cell

* [ctrl]+[1..9] => assert numeral n within selected cell

* [esc]-key		=> Quit

* [h]-key		=> toggle this key menu

* [s]-key		=> Save puzzle state for later restart

* [r]-key		=> Restore (using data from previous save)

* [f]-key		=> Flush-dups: after selecting a cell with a single candidate digit,
						remove it from all other cells in its 3 houses.

* [F]-key		=> Flush-All: for every cell with a single digit,
						remove it from all other cells in its 3 houses.

* [u]-key		=> showUniques: displays in green any digit unique to a house.

* [U]-key		=> processUniques: searches all houses
						for a single occurrence of a given digit, then
						removes all other candidate digits in its cell,
						and then performs a Flush operation on its other houses.

* [b]-key		=> toggle a Brute-Force solver to find & show [first] solution

--------------------------------------------------------------------------

* [m]-key		=> view toggle Minimal: hides unknown candidate digits except for 
						aligned-box-doubles (Red), singles(Green), & non-aligned-box-doubles(Blue).

* [p]-key		=> view toggle: Pairs: 1) hidden, 2) naked, 3) Off

* [t]-key		=> view toggle: Triples: 1) Hidden, 2) Naked, 3) Off

* [q]-key		=> view toggle: Quads: 1) Hidden, 2) Naked, 3) Off

* [x]-key		=> view toggle: Xwing (shows only 1st-found; red implies removable)

* [y]-key		=> view toggle: Ywing (shows only 1st-found)

* [c]-key		=> view toggle: bad-xCycle (shows only 1st-found)

* [k]-key		=> view toggle: Key-Cell digit test of one selected cell

* [K]-key		=> view toggle: Key-Cell test of all cells until contradiction found

* [l]-key		=> view: Linked-pairs hilighted with alternating Magenta/Cyan colors

* [d]-key		=> view toggle: Digit-Doubles: 1) box, 2) row, 3) col, 4) Off

--------------------------------------------------------------------------
and for Sudoku-X...

* [d]-key		=> view toggle: Digit-Doubles: 1) X(Diag), 2) B(box), 3) R(row), 4) C(col), 5) Off


Notes:

* Naked triples **within boxes** are NOT shown to reduce clutter. Same for naked quads & naked pairs.
* The last 10 view-toggles are mutually exclusive: activating one deactivates others.
* Linked-Pairs (l-key): each digit might have multiple chains that are cycled thru in order;
	(you can make a quick exit by pressing a different view-toggle key).
* If a bad [contradictory] Xcycle is found, the first/last digits are Green, the other digits involved alternate between Red(off) and Green(on).
* Key-Cell test (k-key): for any selected cell, shows one candidate digit in RED if it leads to logical contradiction. Also shows consequences of the RED digit by showing the resulting singles in GREEN and the resulting empty cells in a BLUE outline.
* Key-Cell test (K-key): performs Key-Cell test on all cells in lexicographic order until a contradiction is found.
* Digit-Doubles (d-key) shows houses with only 2 like-digits. Row/Col shows rows and columns with digit-doubles, while Box shows boxes with digit-doubles. Each of these modes highlight the doubles in red, any singles in green, and removable candidates in cyan.


--------------------------------------------
## Features

* F.O.S.S. (Free Open Source Software);
* runs on Windows & Linux;  Linux binary runs on many distros!
* uses GLFW3;
* works on HiDPI displays;
* no installation;
* no dependencies;
* simply unzip in your Downloads directory, or to a flash drive, and run.

------------------------------------------------

## Setup & execution:

Windows users can see additional details in "windows-setup.txt".

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

## Input Files:

* If no commandline parameters are passed to the executable, then the previously saved puzzle is restored.

* If one commandline parameter is passed, it must be the relative path to a valid input file.

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





## How to use:

The general idea for solving any sudoku puzzle is to eliminate candidates in each cell down to one single.

Use the following ASUD-methods to work towards a solution:

* using the Unique screen (u-key), if a cell has a GREEN digit, remove any others in the same cell; then flush.
* remove candidates using 
	* Digit-Doubles-view
	* Hidden Pairs/Triples/Quad-view
	* Ywing-view
	* Xwing-view
	* Linked-Pairs-view
	* xCycle-view.
* F-key: Flush all dups
* U-key: process all [Unique] singles

-----------------------------------------------------------------------------------------------------
The hidden pairs/triples/quads tool allows particularly easy removal of excess candidates.
Simply remove the digits in each involved cell that are NOT highlighted.

If new RED pairs or GREEN singles appear, you might be able to eliminate even more candidates.

-----------------------------------------------------------------------------------------------------

### Digit-Doubles Box View

* Doubles highlighted in Red, any singles in Green.
* Removable like digits aligned with box-pairs (pointing-pairs) are highlighted (Cyan).

-----------------------------------------------------------------------------------------------------

### Digit-Doubles Row/Col View

* Doubles highlighted in Red, any singles in Green.
* If a double occurs within a box, then other like digits in that box are removable and highlighted (Cyan).
* You might also notice Xwing variants not handled by Xwing-view.

-----------------------------------------------------------------------------------------------------

### Linked-Pairs-View
A digit-pair refers to a single house with exactly 2 occurrences of a
particular digit. This view shows a chain of digit pairs with alternating colors, where
one color represents ON and the other OFF, but we don't yet know which is which.
The Linked-Pairs view allows manual application of the following rules for elimination:

* if any house has 2 digits of same color, that color must represent OFF (to be eliminated).
* if any non-colored digit can "see" itself in both colors, it must be OFF (eliminated).

Helpful comments to identify removable digits are printed in the terminal window.
EG [ linked-pairs(3) 1 of 3 ] shows comments like:

row:3, dig= 3...multiple magenta digits; must be Off, thus removable (1st rule above).

removable dig= 9 @(3,2) can see 2 colors! (2nd rule above).


-----------------------------------------------------------------------------------------------------

### Bad-xCycle-View
Similar to linked-pairs, the bad-Xcycle view shows a chain of digits with alternating 
colors, where Green represents ON and Red is OFF. If anything is displayed,
then the first Green digit shares a house with another, which is contradictory.
Thusly, the first digit in the chain should be removed.
The on-screen label shows the cell-coordinates of the first & last cells in the chain;
EG: "Xcycle-19-99" indicates the first cell in the chain is at row=1, col=9.

-----------------------------------------------------------------------------------------------------

### Ywing-View
Here, the first Ywing found is displayed. A Ywing is a triple of related cells, 
only one of which, the pivot, can see the other two, called the "pincers". 
The 2 pincers intersect at a "target" cell. The pivot has only 2 candidates, 
where either one forces the elimination of a common digit in the target cell.
If no target exists, or it has been removed, then nothing will be displayed.

-----------------------------------------------------------------------------------------------------

### Xwing-View
Two digit-pairs are highlighted in CYAN so that any like digits in the same row or column may be removed, shown in RED. Note that Xwings are not displayed unless there are digits to remove.

-----------------------------------------------------------------------------------------------------
All the techniques above will only solve the simpler puzzles.
There exists very difficult ones that require advanced methods and insights...

-----------------------------------------------------------------------------------------------------

### Key-Cell-View
If you have reduced the candidates as much as possible with other methods, but still
need help, you can select any cell with the mouse, then use the k-key. This, last-resort
**Key-Cell** test searches the ramifications of selecting each digit in the cell, which might lead
to a logical contradiction. If so, the digit is shown in RED, indicating it should be removed.
A contradiction eventually appears in the form of a cell that would become empty, outlined in blue.
The logic sequence for that contradiction appears in the terminal window.

If no blue cells appear, then no contradictions were found and you will have to try something else. 
**Key-Cell** is a cheap equivalent to a combination of advanced methods (like 3Dmedusa, 
Alternate-Inference-Chain, Hidden-Unique-Rectangle, etc.), all of which assume a single in a cell, 
followed by a chain of inferences leading to a contradiction.

A logical sequence of new singles followed by the resulting deletions is
written to the console window to explain why the blue cells are empty.

EG:
======================= if we assert: +3@(1,4)...

 -3@(3,5)  -3@(1,7)  -3@(1,8)  -3@(1,9)  -3@(7,4)

 +7@(1,9)...  -7@(3,9) 
etc.

...meaning: if we assume digit 3 in cell @ row=1, col=4 then the consequences are to
remove digit 3 at cells (3,5), (1,7), (1,8), (1,9) & (7,4)
which are in the same house.

After removing one red digit as recommended by the Key-Cell test, you should flush its cell.
If new singles appear, you should flush again with F-key.
Repeating this process should eventually solve the puzzle, in most cases.

This new Key-Cell test can solve some [but not all] terribly hard puzzles.

The [capital] K-key does not require selecting a cell; it searches all cells
in lexicographic order and stops at the first contradiction found. Typically, each application
will expose new contradictions, until solved.

-----------------------------------------------------------------------------------------------------




## Build Requirements:
* systems:  Windows, or GNU/Linux
* a recent Ada compiler;  eg. GNU-Ada...try this link:
	* https://github.com/alire-project/GNAT-FSF-builds/releases


## Build instructions:

Two [pre-compiled] binary executables are delivered, one for Windows
and one for linux. Both are fairly portable. Also remember that the
Windows binary will run under WINE on Linux.

Thus, for most people, rebuilding is unnecessary.

If you still want to rebuild, install Ada, then execute the following scripts:

* msWin64 =>
	* setpath64.bat
	* wcmp.bat

* linux =>
	* lcmp.sh

Note that these scripts might need to be adjusted to reference 
your actual installation directory for the 64bit GNU Ada compiler.

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

1) There is also a prototype X-sudoku tool lsudx (asudx.adb) with similar capabilities & interface.
In this type of puzzle, each cell can be in either 3 or 4 houses, 
because the 2 diagonals are also houses.

2) Brute-force solvers [susolve/susolvex] are also included under ./bruteForceSolver/. 
They display the first-found solution to the screen:

* wsol.bat {filename} (on Windows)
* susolve  {filename} (on Linux)

For X-sudokus use wsolx.bat/susolvex.

-------------------------------------------------------------------------

## TBD list:
* Input puzzle handling is primitive.
* User interface is spartan.
* Could be better at facilitating the human discovery process.

## Summary:
My original intent in writing this app was to avoid the optical drudgery of discovering unique singles or hidden triples/quads. But since then I have watched some inspiring videos on how a Sudoku tool could enhance the fun of puzzle solving. Watch for future releases!

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

**ver 1.0.5 -- 28jun2023**

* Simplified Digit-Doubles display. Now easier to spot deletable candidates.
* Added Xwing view.
* Clarified xCycle view to show alternating on/off colors.

**ver 1.0.4 -- 23jun2023**

* Added K-key to perform Key-Cell test on every cell until a contradiction is found.
* Decluttered & minimized console output for Key-Cell tests.
* Other coding improvements.

**ver 1.0.3 -- 17jun2023**

* Fully expanded Key-Cell test (k-key) to allow selecting any cell.

**ver 1.0.2 -- 12jun2023**

* Improved & expanded Key-Cell test (k-key) now allows selecting cells with either 2 or 3 entries.
* Augmented action of Flush keys: f-key flushes a selected cell; F-key flushes all cells.
* Augmented action of Unique keys: u-key merely displays all singles (green); U-key clears & flushes all singles.

**ver 1.0.1 -- 1jun2023**

* Corrections to documentation.
* Enhancements to displays, keymap.
* Replace "="-key with 3-way d-key for house digit-doubles.
* Improved k-key console-terminal explanations.

**ver 1.0.0 -- 25may2023**

* Initial release.













