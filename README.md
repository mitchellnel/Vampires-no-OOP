# Vampires-no-OOP
__Note that this project was created without experience with OOP. To view a higher quality version of this same program, please view the code at the [Vampires](https://github.com/mitchellnel/Vampires) repository__

#### Concepts:
* Classes and objects
* Member functions
* Dynamic allocation of memory
* Memory leaks

The assignment is to complete a prototype of a game that uses character-based graphics. The game is to utilise vials of poisoned blood to exterminate the vampires that have overrun Pauley Pavilion.

In the game, the player (indicated by @) is located in a rectangular arena filled with vampires (usually indicated by V).

<img width="586" alt="vampires" src="https://user-images.githubusercontent.com/56947176/94786434-8bb15600-0403-11eb-934e-0d3b2ddd880d.png">

At each turn, the user selects an action for the player to take:
*	Either move one step in a N, S, E or W direction
*	Or drop a poisoned vial without moving

The player takes their action first, and then each vampire moves one step in a random direction.

If a vampire moves onto a grid point occupied by the player, the player will die from the vampire’s bite. Also, if the player moves to a grid point occupied by a vampire, the player is bitten and dies.

An empty grid point is indicated by a single dot ( . ).

If a vampire lands on a grid point with a poisoned vial (indicated by \*), it drinks the blood in the vial.

The first time a vampire drinks a vial of poisoned blood, it slows down; it moves every other turn. I.e. it won’t move on its next turn, and then the turn after it moves, and the turn after that it doesn’t move etc.

The second time a vampire drinks a vial of poisoned blood, it dies.

If a poisoned vampire moves to a grid point with both the player and a vial of poisoned blood, it drinks the blood in the vial, and just before it dies, bites that player, killing both the vampire and the player.

At each turn, the player may take one of these actions:
1.	Move one step N, S, E or W, and do not drop a vial of poisoned blood.
    1.	If the player attempts to move out of the arena (e.g. while on the bottom row, attempts to move south), the player does not move, and does not drop a vial.
    2.	If the player moves to a grid point currently occupied by a vampire, the player dies.
2.	Do not move, but attempt to drop a vial of poisoned blood.
    1.	If there is already a vial of poisoned blood at that grid point, no additional vials are dropped; a grid point may have at most one vial of poisoned blood.
    2.	The player has an unlimited supply of poisoned blood vials.
    
The game allows the user to select the players action:
* n/s/e/w for movement, or x for dropping a poisoned blood vial
* if the user just hits enter, with no character input, the computer selects the player’s move

After the player moves, it is the vampires’ turn. Each vampire has an opportunity to move uniquely.

A vampire that has previously drunk a vial of poisoned blood will not move if it attempted to move on the previous turn.

Otherwise, it will pick a random direction (N, S, E or W) with equal (25% each) probability. The vampire moves one step in that direction if it can. 

If the vampire attempts to move off of the grid, it does not move. (This still counts as a poisoned vampire’s attempt to move, so it won’t move on the next turn)

More than one vampire can occupy the same grid point. In this case, instead of V, the display will show a digit character indicating the number of vampires at that point (e.g. 4 == four vampires, and 9 == 9 vampires or more).

If after a vampire moves, it occupies the same grid point as the player (regardless if there is a vial of poisoned blood at that point), the player dies.

If the vampire lands on a grid point with a dropped poisoned blood vial, it drinks the blood, and the vial is no longer part of the game (grid point changes from * back to . ). If this is the second vial of poisoned blood that the vampire has drunk, it dies.

If more than one vampire lands on a spot that started the turn with a poisoned blood vial on it, only one of them drinks the vial of poisoned blood.

## Classes
The programme skeleton defines four classes that represent the four kinds of objects that this programme works with:
Game
*	To create a game, you specify a number of rows and columns, and the number of vampires to start with
*	The Game object creates an appropriately sized Arena, and populates it with the Player and the Vampires
*	A round of the game may be played

Arena
*	When an Arena object of a particular size is created, it has no positions occupied by Vampires or the Player
*	In the Arena coordinate system, row 1, column 1 is the upper-leftmost position that can be occupied by a Vampire or a Player. E.g. In an Arena created with 10 rows and 20 columns, the lower-rightmost position that could be occupied would be row 10, column 20.
* You may tell an Arena object to put a poisoned blood vial at a particular position
*	You may ask an Arena object whether there’s a poisoned blood vial at a particular position
*	You may tell an Arena object to create a Vampire at a particular position
*	You may tell an Arena object to create a Player at a particular position
*	You may tell an Arena object to have all the Vampires in it make their move
*	You may ask an Arena object its size, how many Vampires are at a particular position, and how many Vampires altogether are in the Arena
*	You may ask an Arena object for access to its Player
*	An Arena object may be displayed on the screen, showing the locations of the Vampires (indicated by V or a digit), the player (indicated by @), and the poisoned blood vials (\*), along with other status information

Player
*	A Player is created at some position (using the Arena coordinate system)
*	You may tell a Player to move in a direction, or to drop a poisoned blood vial
*	You may tell a Player that it has died
*	You may ask a Player for its position and its alive/dead status

Vampire
*	A Vampire is created at some position (using the Arena coordinate system)
*	You may tell a Vampire to move
*	You may ask a Vampire object for its position and its alive/dead status
