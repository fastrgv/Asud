
![screenshot](https://github.com/fastrgv/Asud/blob/main/menu.png)

Menu Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/l-pairs3.png)
Linked-Pairs Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/keyCellTrace.png)
Bad Key Cell Screen


![screenshot](https://github.com/fastrgv/Asud/blob/main/badXC.png)

Bad Xcycle: remove 3 @ (2,2)

![screenshot](https://github.com/fastrgv/Asud/blob/main/hiddenPairs.png)

Hidden Pairs

---------------------------------------------------------------------------


Here is the link to the latest release, which includes all source:

https://github.com/fastrgv/Asud/releases/download/v1.2.3/sud1jun24.7z


* On OSX, Keka works well for 7Z files. The command-line for Keka is:
	* /Applications/Keka.app/Contents/MacOS/Keka --cli 7z x (filename.7z)


===============================================================================






# ASUD: Ada Sudoku Assistant


## Most recent changes



**ver 1.2.3 -- 01jun2024**

* Refined global KeyCell function to match strategy used for selected-cell version.
* Added 9 distinct Set Equivalence Theory overlays.
* Corrected drawing so that any removable digits are now always seen in cyan color.
* Now prohibit saving erroneous puzzle states.
* Improved messaging in terminal window.


**ver 1.2.2 -- 17may2024**

* Significantly improved KeyCell function now finds the simplest removable-digit chains.


**ver 1.2.1 -- 14may2024**

* Improved terminal messages.
* Improved transitions between auto-candidate and manual mode.
* Reduced external file usage.
* Improved the Kcell removable-digit search algorithm.
* Minor change to key maps...
	* (u)-key : Undo last assert.
	* (.)-key : search for unique singles.


**ver 1.2.0 -- 03may2024**

* Enabled 8-level-undo for assertions.
* Decluttered root directory by putting helper files elsewhere.
* Save now preserves mode, too.


More revision history is at end of this file.

-----------------------------------------------------------------

### Terminology

A given cell belongs to 3 "houses": its row, its column, its 3x3 box.
In X-sudoku, a cell could also belong to a 4th house: the diagonal.
Saying cells can "see" each other means they share a house.
Singles are cells with all digits but one eliminated. A single also
refers to a candidate digit that is unique in one of its houses,
even if its cell has other candidates listed.



## Introduction

ASUD is a sudoku assistant tool designed to help with manually solving Sudoku puzzles.
It handles routine tasks so you can focus on more advanced puzzle solving strategies.

For example, some routine, but tedious tasks are:

* noticing single occurrences of a digit within a house
* removing a singleton digit from all other cells in a house
* finding hidden pairs, triples & quads, etc.

In each of the 81 cells, all candidate digits can be shown. The working goal is to
facilitate the removal of as many candidate digits as possible.

Algorithms have been added to detect and display hidden (or naked) pairs, triples, & quads,
whose display can be toggled.

The default display shows automatically calculated candidate digits in the center of each cell. 
For simple puzzles, one can toggle a Manual mode that just shows manually-inserted pen or pencil mark numerals.

Sudoku fans that get stuck will find that this app can help 
them to get a new perspective, using any PC or laptop.
This package includes executables that run on Windows, OSX, and Linux.
All source code, build scripts & resources are included.


## Features

* F.O.S.S. (Free Open Source Software);
* runs on Windows, OSX, & Linux;  Linux binary runs on many distros!
* uses GLFW3;
* works on HiDPI displays;
* no installation;
* no dependencies;
* simply unzip in your Downloads directory, or to a flash drive, and run.

------------------------------------------------


## Control Keys:

* mouse-click 	=> select/Deselect one of 81 cells from among 9x9 array to edit

* [1..9]-key	=> toggle candidate numeral n in selected cell (aka "pencil" mark)

* [ctrl]+[1..9] => assert a single numeral n in selected cell (aka "Pen" mark)

* [u]-key		=> Undo most recent pen-mark (assertion); Limited to 8 most recent.
					The number of remaining Undo's is written to the terminal window.

* [esc]-key		=> Quit

* [h]-key		=> toggle this key Help menu

* [m]-key		=> toggles between Auto-candidate and Manual-candidate mode.
						Manual mode shows only manually entered candidates (pencil-marks)
						or manually asserted unique singles (pen-marks)
						and disables advanced function keys: {a,n,u,p,t,q,x,y,c,k,l,d}

* [s]-key		=> Save puzzle state for later restart

* [r]-key		=> Restore (using data from previous save)

* [f]-key		=> Flush: If no cell is selected, then for every cell with a unique single digit,
						remove it from all other cells in its 3 houses.
						If a cell with a single digit is selected, it flushes just that cell,

------------------------- auto-candidate-mode ftns below ---------------------------------------

* [.]-key		=> search for, assert, & flush: cells with a single candidate, and houses
						with a single occurrence of a given digit.

* [a]-key		=> toggle: hilight Aligned Box Digit Doubles (Red) with Cyan deletables.
* [n]-key		=> toggle: hilight Nonaligned Box Digit Doubles (Purple)...utility doubtful.


* [b]-key		=> toggle a Brute-Force solver to find & show [first] solution

* [p]-key=> view toggle: Pairs: 1) hidden-box, 2) hidden-row, 3) hidden-col, 4) naked-R/C/B, 5) Off

* [t]-key=> view toggle: Triples: 1) hidden-box, 2) hidden-row, 3) hidden-col, 4) naked-R/C/B, 5) Off

* [q]-key=> view toggle: Quads: 1) hidden-box, 2) hidden-row, 3) hidden-col, 4) naked-R/C/B, 5) Off

* [x]-key		=> toggle: Xwing (shows only 1st-found; cyan implies removable)

* [y]-key		=> toggle: Ywing (shows only 1st-found)

* [c]-key		=> toggle: xCycle (shows only 1st-found, searches bad, then good)

* [l]-key		=> toggle: multiple Linked-pairs-chains hilighted with alternating Red/Blue colors

* [d]-key		=> toggle: hilight Digit-Doubles: 1) box, 2) row, 3) col, 4) Off

* [k]-key		=> toggle: Key-Cell test: If no cell selected, tests all cells until contradiction is found.
					**You may select a cell first, to limit Key-Cell test to selected cell.**

--------------------------------------------------------------------------


Notes:

* The last 12 view-toggles are mutually exclusive: activating one deactivates others.
* Linked-Pairs (l-key): each digit might have multiple chains of related pairs that are cycled 
thru in order; (you can make a quick exit by pressing a different view-toggle key).
* Key-Cell test (k-key): performs Key-Cell test on all cells in lexicographic order until a contradiction is found. If so, the hypothetical singles are shown in Blue and resulting empty cells in Blue outline. Deleted digits are shown in Orange.
* Digit-Doubles (d-key) shows houses with only 2 aligned, like-digits. Row/Col shows rows and columns with digit-doubles, while Box shows boxes with digit-doubles. Each of these modes highlight the doubles in red, any [assertable] singles in Green, and removable candidates in cyan.

* xCycles looks for contradictory inference chains. Shows only the first found. If found, the first cell in the chain is responsible for the contradiction, so is shown in Cyan as being deletable. If not found, it then searches for consistent chains with deletable cells that see two colors.


--------------------------------------------

## Setup & execution:

Windows users can see additional details in "windows-setup.txt".
Mac users see "osx-setup.txt".

Unzip the archive.  

* On Linux & Windows, 7z [www.7-zip.org] works well for this. The proper command to extract the archive and maintain the directory structure is "7z x filename".

* On OSX, Keka works well for 7Z files. The command-line for Keka is:
	* /Applications/Keka.app/Contents/MacOS/Keka --cli 7z x (filename.7z)

After the archive is unzipped...

Users may then open a terminal window, cd to install-directory, then, at the command line, type the executable name to start the tool. (the command **must** be run from the install-directory) ...

Let {fnam} indicate an optional input file-name. Then

----------------------------------------------------------------------
On OSX type "osud {fnam}"

----------------------------------------------------------------------
In Linux type "lsud {fnam}".

In Linux, you can also use the Windows executable under wine, thusly:
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
one can save the state using the "s" key. This creates the file: frestoreB.txt

To restart, type the executable name with no parameter.





## How to best use this tool:

The 2 primary viewing modes are toggled with the m-key: 
1) auto-candidate (default), and 2) manual-mode (beta-test). 

The manual mode makes easy puzzles more fun by disabling most of the advanced functions. 
Manual mode is very intuitive and similar to typical online sudoku-solving tools,
except it has auto-flush when a single numeral is asserted. Testing for this mode is still ongoing,
so I'm not yet sure that all error conditions are handled well. (In auto-candidate mode, 
simpler puzzles are too easily solved, and much of the fun is lost.)


The remaining descriptions refer to the default auto-candidate mode, for difficult puzzles.

The general strategy for solving any sudoku puzzle is to minimize the candidates within each cell.
After loading a puzzle, you will need to FlushAll, perhaps more than once, in order to
properly initialize the candidates that are displayed. Each flush might expose new singles
that subsequently need flushing, again. The automation of flushes has recently been
reduced to a bare minimum to avoid confusion.

Similarly, the unique singles key (u-key) frequently exposes new (green) singles with each press,
so that mutliple presses might be needed. 

Use the following ASUD-methods to work towards a solution:

* remove candidates using 
	* Digit-Doubles-view
	* Hidden Pairs/Triples/Quad-view
	* Ywing-view
	* Xwing-view
	* Linked-Pairs-view
	* xCycle-view.
* f-key: Flush all dups
* .-key: process all singles: remove other candidates in same cell, then flush.

-----------------------------------------------------------------------------------------------------
The hidden pairs/triples/quads tool allows particularly easy removal of excess candidates.
Simply remove the Cyan digits in each involved cell.

If new digit pairs or singles appear, you might be able to eliminate even more candidates.

**Note that known removable digits are generally displayed using a cyan color**

-----------------------------------------------------------------------------------------------------

### Digit-Doubles/Triples Box View [d-key]

* Aligned Box-Digit-Doubles (pointing-pairs), and Triples (pointing triples) are colored Red.
* Removable digits aligned with pointing-pairs or pointing-triples are Cyan.

-----------------------------------------------------------------------------------------------------

### Digit-Doubles Row/Col View [d-key]

* Aligned Digit-Doubles highlighted in Red.
* If a double occurs within a box, then other like digits in that box are removable (Cyan).
* Occasionally this view might allow you to notice Xwing variants not handled by Xwing-view.

-----------------------------------------------------------------------------------------------------

### Linked-Pairs-View [l-key]
A digit-pair refers to a single house with exactly 2 occurrences of a
particular digit. That means they are strongly connected in the sense that
if one of them is OFF then the other must be ON.
This view shows a chain of digit pairs with alternating colors 
(nominally Red/Blue), where one color represents ON and the other OFF, 
but we don't know which is which. **Note that a chain of digit-pairs may form
a tree structure of related digit-pairs, rather than a linear sequence.**

The Linked-Pairs view allows manual application of the following rules for elimination:

* if any house has 2 digits of same color, that color must represent OFF (to be eliminated).
* if any non-chain digit can "see" itself in both colors, it must be OFF (eliminated).

**Note:  all removable digits have their color changed to Cyan.**

Helpful comments to identify removable digits are printed in the terminal window.
EG [ linked-pairs(3) 1 of 3 ] shows comments like:


LinkedPairs removable dig= 9 @(3,2) can see 2 colors! (2nd rule above).

LinkedPairs box#9, dig= 9...multiple same-color-digits => removable (1st rule)

The current chain of related digit pairs is printed to the terminal,
along with a list of deletable candidates.

Finally, chains that do not result in deletable digits are now skipped.


-----------------------------------------------------------------------------------------------------

### xCycle-View [ c-key ]
This view first looks for contradictory xCycles, which are somewhat similar to linked-pairs.
This inconsistent-xCycle view shows a chain of digits with alternating 
colors, where Blue represents ON and Red is OFF [in the forward direction]. If anything is 
displayed, then the first digit, originally Blue because it was assumed ON, 
shares a house with another Blue, which is contradictory.
Thusly, the first digit in the chain should be removed, indicated by its [new] color Cyan.
The on-screen label shows the cell-coordinates of the first & last cells in the chain;
EG: "xCycle-19-99" indicates the first cell in the chain is at row=1, col=9.
The console terminal lists the logical sequences of digit states.

If that first search fails, it then searches for a consistent x-cycle chain that generates
any [Cyan-colored] deletable cells that can see both Blue & Red colored chain links.
Again, the console terminal lists the logical sequences of digit states.
Note that a consistent sequence can be read backwards if one reverses the color 
interpretations, i.e. Red=On, Blue=Off.

The C-key [cap-C] searches only for consistent X-Cycles. This is mainly for algorithmic testing
because the contradictory X-Cycle search often finds the same deletables, first.


-----------------------------------------------------------------------------------------------------

### Ywing-View [y-key]
Here, the first Ywing found is displayed. A Ywing is a triple of related cells, 
only one of which, the pivot, can see the other two, called the "pincers". 
The 2 pincers intersect at a "target" cell. The pivot has only 2 candidates, 
where either one forces the elimination of a common digit in the target cell.
If no target exists, or it has been removed, then nothing will be displayed.

-----------------------------------------------------------------------------------------------------

### Xwing-View [x-key]
Two digit-pairs are highlighted in CYAN so that any like digits in the same row or column may be removed, shown in RED. Note that Xwings are not displayed unless there are digits to remove.

-----------------------------------------------------------------------------------------------------
One can easily find references online that give more complete definitions of the previous concepts:

* Linked Pairs
* X-cycles
* Xwings
* Ywings


-----------------------------------------------------------------------------------------------------

All the techniques above will only solve the moderately difficult puzzles.
There exists extreme puzzles that require advanced methods and insights...

-----------------------------------------------------------------------------------------------------

### Key-Cell-View [k-key]

**Think of KeyCell as a generalized Ywing algorithm, and use it as such.**

This powerful tool can be used in 2 ways.

---------------------------------------------------------------------------------------------
**Firstly,** if you select a cell before hitting the k-key, then it operates **only** on the selected cell.
It tries asserting each candidate in the cell to find whether it leads to a contradiction
that identifies some deletable digit. Look for a shortest chain of logic by selecting various different 
cells. Short logic chains are much easier to follow and appreciate. If contradictions are found, 
deletable digits are hilighted in a Cyan color. 

---------------------------------------------------------------------------------------------
**Secondly,** the full-powered version is initiated by the same k-key, but without selecting a cell 
first. It searches all cells in lexicographic order until it finds removable digits, or fails.

#### Further details of Key-Cell

If you have reduced the candidates as much as possible with other methods, but still
need help, then use the k-key. This **Key-Cell** test searches the ramifications 
of selecting each digit in each cell, which might lead to a logical contradiction. 
If so, the causal digit is shown in Cyan, indicating it should be removed.
A contradiction eventually appears in the form of a cell that would become empty, outlined in blue,
OR a house that is missing a [orange] digit. The logic sequence for that contradiction appears in the terminal window.

During this test, any values shown in blue (singles) are definitely ON, while values shown in orange
are definitely OFF. The blue & orange values are the result of the hypothesized initial digit.
If a cell contains only orange digits, then it is colored with a blue outline because all
of its digits have been ruled out; AND since an empty cell is a contradiction, the original 
hypothesized digit is shown in a CYAN color.

If no blue cells appear, but some house has a missing digit, that is also a contradiction, which is so indicated in the terminal window, along with the removable cyan digit that caused it.

If no blue cells appear, and no house has a missing digit,
then no contradictions were found and you will have to try something else. 

**Key-Cell** is a generalization of advanced methods (like linked-pairs, 3Dmedusa, 
Alternate-Inference-Chain, Hidden-Unique-Rectangle, etc.), all of which assume a single digit in a 
particular cell, followed by a chain of inferences leading to a contradiction.

The logical sequence of hypothetical new (BLUE) singles followed by the resulting deletions (Orange) is
written to the console window to explain why the blue cells are empty.

EG:

 +3@(1,4): -3@(3,5) -3@(1,7) -3@(1,8) -3@(1,9) -3@(7,4)

 +7@(1,9): -7@(3,9)

etc.

...meaning: if we assume digit 3 in cell @ row=1, col=4 then the consequences are to
remove digit 3 at cells (3,5), (1,7), (1,8), (1,9) & (7,4), each of which are in the same house.
Repeating this process should eventually solve the puzzle, in most cases.
This new Key-Cell test can solve some [but not all] terribly hard puzzles.

All cells are searched in lexicographic order and the first contradiction found is displayed. Typically, each application will expose new contradictions, until solved.

-----------------------------------------------------------------------------------------------------

### Guessing
Most experts consider X-Cycles a valid solution technique. But the essence of contradictory
X-Cycles is to hypothesize a particular digit in a given cell, then test the ramifications. When a
contradiction is reached, the intitial hypothesis is found to be false. Thusly, I would call this a
guessing technique. Same goes for my KeyCell method above.

This is why guessing techniques may be acceptable to some.

That said, I have collected 4 puzzles, so far, that reside in the directory ~/puzzles/impossible/ 
that refuse to be solved using KeyCell alone, without some sort of guessing. And here is a solution methodology for this type:

* choose a cell with a small number of candidates. One works, and the others will eventually fail.

* assert one candidate; then use a combination of KeyCell or X-Cycle tests until reaching either 1) a solution, 2) a failed-puzzle-state, or 3) KeyCell fails to find another deletable digit...

* if a failed puzzle state occurs, you will see one of two things:
	1) one or more empty cells; i.e. where all candidates have been eliminated.
	2) one or more houses are missing some digit.
In either case, use the u-key to Undo the assertion; then assert a different candidate.

* if KeyCell fails to find any more deletable digits, this represents an indeterminate state. The process described here can be recursively repeated by choosing another cell with minimal candidates...

Note that this app allows the last 8 assertions [pen-marks] to be undone.

There are very few sudoku puzzle where more than one [pen-mark] assertion is necessary to reach either a failed puzzle state, or a solution. See ~/puzzles/impossible/ for the most difficult puzzles I've collected.

-----------------------------------------------------------------------------------------------------

## Set Equivalence Theory [SET] overlays

The key-pad numbers 1..9 on a typical keyboard now toggle 8 distinct geometric overlays, each with the property that the numeral-sets contained in each of the 2 colored regions are equal. This knowledge can occasionally [but rarely] help to solve a sudoku.

EG: overlay #1 helps to solve ~/puzzles/extreme/wheel.txt without resorting to KeyCell or guessing.


## Build Requirements:
* systems:  Windows, OSX, or GNU/Linux
* a recent Ada compiler;  eg. GNU-Ada...try this link:
	* https://github.com/alire-project/GNAT-FSF-builds/releases


## Build instructions:

Three [pre-compiled] binary executables are delivered. All are fairly portable. 
Also remember that the Windows binary will run under WINE on Linux.

Thus, for most people, rebuilding is unnecessary.

If you still want to rebuild, install Ada, then execute the following scripts:

* msWin64 =>
	* setpath64.bat
	* wcmp.bat

* linux =>
	* lcmp.sh

* osx =>
	* ocmp.sh

Note that these scripts might need to be adjusted to reference 
your actual installation directory for the 64bit GNU Ada compiler.

-------------------------------------------------------

## Final Notes

1) X-sudoku tools [wsudx.bat,osudx,lsudx] (asudx.adb) with similar capabilities & interface
are also included. In this type of puzzle, each cell can be in either 3 or 4 houses, 
because the 2 diagonals are also houses.

2) Brute-force solvers [susolve/susolvex] are also included under ./bruteForceSolver/. 
They display the first-found solution to the screen:

* wsol.bat {filename} (on Windows)
* lsol  {filename} (on Linux)
* osol  {filename} (on osx)

For X-sudokus use wsolx.bat/lsolx/osolx.

3) A fair variety of puzzles can be found in the directories:

* ./puzzles/?.txt (see descriptions @ bottom for difficulty level)
* ./puzzles/extreme/?.txt
* ./puzzles/impossible/?.txt
* ./puzzles/Xpuz/?.txt


4) Note that this software knows when a bad assertion is made but it does not prevent it, but in the terminal window you will notice a "_?_" symbol.


-------------------------------------------------------------------------

## TBD list:
* Rarely, unhandled aborts might still happen. Save often.
* Input puzzle handling is primitive.
* Keyboard user interface is somewhat spartan.

## Summary:
My original intent in writing this app was merely to avoid the optical drudgery of discovering unique singles or hidden triples/quads. But since then it has evolved to help me tackle ever more formidable puzzles,
Lately I have tried to make the simpler puzzles more fun, too.


----------------------------------------------

## what is special about this project?

Uses the Ada programming language and modern OpenGL methods, with textures, shaders and uniforms.  Compiles and runs on Windows, OSX, and GNU/Linux.

Focusing on portability, transparency, and open source freedom, this project relies exclusively on F.O.S.S. tools:  a thin GLFW3 binding, a thin OpenGL binding, a PNG reader by Stephen Sanguine & Dimitry Anisimkov, and a GNU-Ada compiler.

The linux-build is among very few modern OpenGL apps where a single pre-built executable can run on multiple Linux distros without 3rd party add-ons!

Open source Ada developers are welcome to help improve or extend this app.

Developer or not, Sudoku fans can send comments, suggestions or questions to:
fastrgv@gmail.com

In particular, I would greatly appreciate hearing about any repeatable problems. I only have one tester, me; and I seldom type unexpected keys.


===================================================================
## License

asud itself is covered by the GNU GPL v3 as indicated in the sources:


 Copyright (C) 2024  <fastrgv@gmail.com>

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


**ver 1.1.9 -- 30apr2024**
* Fixed aborts when typing a number without selecting a cell first.

**ver 1.1.8 -- 26apr2024**
* Assertions no longer obstruct manual saves.

**ver 1.1.7 -- 19apr2024**
* No longer aborts when user makes an invalid assertion.

**ver 1.1.6 -- 17apr2024**
* Corrected error in asudx.adb that caused failure when using k-key or b-key.

**ver 1.1.5 -- 16apr2024**
* The (m)-key now toggles a manual-candidate mode, more like typical online sudoku solving tools,
that makes easy puzzles much more fun.

**ver 1.1.4 -- 10oct2023**
* Added commandline build for Mac/OSX (no bundle)...built without using Xcode.
* [20feb24] clarified explanation of KeyCell operation (k-key).

**ver 1.1.3 -- 20sep2023**
* Augmented X-solver to display, not only digit-doubles but triples along the diagonals, as well as any removables they reveal. Shown whenever displaying digit-doubles [d-key] or aligned-digits [a-key].

**ver 1.1.2 -- 16aug2023**
* Removed most automatic flushes so updates & reloads are less confusing.
* Added automatic flush after digit assertion, for more intuitive results.
* Corrected a coding error that caused KeyCell aborts.
* Naked Pairs/Triples/Quads now display Cyan removable digits, if any.
* Improved messages & effectiveness of KeyCell search.

**ver 1.1.1 -- 30jul2023**
* Aligned Box Digit Doubles view (pointing-pairs) now includes aligned box digit triples (pointing-triples), and can be toggled on or off with the a-key.
* Improved console output for consistent x-Cycles.
* Minor change in f-key action.

**ver 1.1.0 -- 26jul2023**
* Fixed HiddenTriples error in ASUDX (lsudx).
* Improved Hidden Quads/Triples/Pairs to distinguish between row/col/box views.
* Now display boxPairs/boxTriples that were previously suppressed (to reduce clutter).

**ver 1.0.9 -- 22jul2023**
* Deleting removable candidates while viewing Linked-Pairs now works as expected.

**ver 1.0.8 -- 19jul2023**
* Minor color changes for greater uniformity.
* Fixed X-Cycle logic for Sudoku-X (lsudx).
* Removed some unused code.
* KeyCell: now shows hypothetically-deleted digits in orange.
* Refined KeyCell terminal output.
* LinkedPairs now displays all deletable digits in Cyan.
* LinkedPairs now skips chains with no deletable digits.

**ver 1.0.7 -- 12jul2023**
* Changed highlight colors;  now more uniform with deletable digits Cyan.
* Hidden pairs/triples/quads now color deletable digits Cyan.
* Better terminal messaging.
* Corrected (generalized) algorithms searching for naked: Pairs/Triples/Quads.
* Pointing-Pairs now shown as Red, Singles as Green, in default mode.
* Changed u-key action; changed k-key action.
* When no inconsistent X-Cycles are found, the search continues by seeking consistent X-Cycles that exhibit deletable digits.


**ver 1.0.6 -- 1jul2023**
* Fixed error in Xsudoku keyboard code.
* Improved action in xCycle-view.
* Added quick [non-modal] method to emplace a single into a selected cell using (ctrl)+(dig)
* Improved the helpfulness of the Digit-Doubles-view by highlighting removable digits.


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


