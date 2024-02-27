# HiIT-JS_Puzzle
## 9Piece Edge Puzzle
Een puzzle met 9 stukken, elk stuk heeft 4 halve tekeningen/symbolen, waarvan de andere helft op een ander puzzlestuk staat.
Het doel is om een 3x3 vlak te leggen, waar alle tekeningen/symbolen volledig zijn. i.e De bovenhelft aan de onderheft van het symbool.

## Het doel van deze opdracht is als volgt:
### versie 1.
+ Maak een klik-sleep speelveld om Puzzlestukken in het 3x3 Grid te slepen: Klik/sleep, rotatie
+ Maak een GameManager die controleert of het Puzzle stuk op een geldige plek ligt en bij extend of de puzzle opgelost is.

### versie 2.
+ Maak een hints systeem, waar een mogelijke volgende stap wordt laten zien.

### versie 3.
+ autocomplete door gamemanager. Los de puzzle op door de pc

## Functionality Scetch
We start with an empty 3x3 Grid and 9 Puzzle Pieces. Each Piece has 4 halfs of a symbols, the other half is on the other pieces.
To Finish the Puzzle, we want to connect all Pieces with a Head and Body half, without a mismatch of symbolhalves.
In short: all connecting pieces should create a complete symbol.

1. Choose Piece on Position
2. Find empty neighbor and connect a possible Piece
3. Find all empty neighbors and connect the possible Pieces
4. Find a Piece that fits the Current Empty Tile
5. If no Piece Found: Restart. 
If Piece Found: Solved. 

## Board & Pieces
### Board
**Row:** [0/2] 
**Cell:** [0/2]
**Occupied:** [True/False]

### Pieces
**uID:** [Pieces][Sides][Types][Variant]
+ Piece: [0/8] 
+ Side: [0/3]
+ Type: [0/3] 
+ Variant: [-1/1]

**uPos:** [Row][Cell][Rotation]
+ Row: [0/2]
+ Cell: [0/2]
+ Rotation: [0/3]

**Possible Positions Array:** [Priority][Piece0][Piece1][~]
+ Priority: [0/8] = Priority given to a Piece for a specific place on the board
+ Piece[] = Connecting Piece 1
+ Piece[] = Connecting Piece 2
+ ...more Pieces that connect..

## Pieces Array Adress Legend
### Pieces 
0 <img alt='Piece#00' src='src/img/IMG00.jpg' width='50' />
1 <img alt='Piece#01' src='src/img/IMG01.jpg' width='50' />
2 <img alt='Piece#02' src='src/img/IMG02.jpg' width='50' />
3 <img alt='Piece#03' src='src/img/IMG03.jpg' width='50' />
4 <img alt='Piece#04' src='src/img/IMG04.jpg' width='50' />
5 <img alt='Piece#05' src='src/img/IMG05.jpg' width='50' />
6 <img alt='Piece#06' src='src/img/IMG06.jpg' width='50' />
7 <img alt='Piece#07' src='src/img/IMG07.jpg' width='50' />
8 <img alt='Piece#08' src='src/img/IMG08.jpg' width='50' />
### Sides: (arguments 1-4: Same behaviour as CSS Borders?)
+ 0 Top
+ 1 Right
+ 2 Bottom
+ 3 Left
### Types:
+ 0 Goldfish
+ 1 Seahorse
+ 2 Octopus
+ 3 RedFish
### Variants:
+ -1 Head
+ 1 Body

#### Array adress:
<img alt='Piece#00' src='src/img/IMG00.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
0011 | 0 | 0 | 1 | 1
0121 | 0 | 1 | 2 | 1
0210 | 0 | 2 | 1 | 0
0331 | 0 | 3 | 3 | 1

<img alt='Piece#01' src='src/img/IMG01.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
1020 | 1 | 0 | 2 | 0
1101 | 1 | 1 | 0 | 1
1231 | 1 | 2 | 3 | 1
1330 | 1 | 3 | 3 | 0

<img alt='Piece#02' src='src/img/IMG02.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
2020 | 2 | 0 | 2 | 0
2100 | 2 | 1 | *0* | *0*
2230 | 2 | 2 | 3 | 0
2300 | 2 | 3 | *0* | *0*

<img alt='Piece#03' src='src/img/IMG03.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
3010 | 3 | 0 | 1 | 0
3100 | 3 | 1 | 0 | 0
3201 | 3 | 2 | 0 | 1
3331 | 3 | 3 | 3 | 1

<img alt='Piece#04' src='src/img/IMG04.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
4021 | 4 | 0 | 2 | 1
4101 | 4 | 1 | 0 | 1
4211 | 4 | 2 | *1* | *1*
4311 | 4 | 3 | *1* | *1*

<img alt='Piece#05' src='src/img/IMG05.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
5000 | 5 | 0 | 0 | 0
5121 | 5 | 1 | 2 | 1
5201 | 5 | 2 | 0 | 1
5331 | 5 | 3 | 3 | 1

<img alt='Piece#06' src='src/img/IMG06.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
6010 | 6 | 0 | *1* | *0*
6130 | 6 | 1 | 3 | 0
6220 | 6 | 2 | 2 | 0
6310 | 6 | 3 | *1* | *0*

<img alt='Piece#07' src='src/img/IMG07.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
7011 | 7 | 0 | 1 | 1
7130 | 7 | 1 | 3 | 0
7220 | 7 | 2 | 2 | 0
7321 | 7 | 3 | 2 | 1

<img alt='Piece#08' src='src/img/IMG08.jpg' width='100' />
 uID | piece | side | type | variant
----:|:-----:|:----:|:----:|:-------
8020 | 8 | 0 | 2 | 0
8130 | 8 | 1 | 3 | 0
8210 | 8 | 2 | 1 | 0
8301 | 8 | 3 | 0 | 1

## Pieces Location Adress Legend
**Row:** [0/2] 
**Cell:** [0/2] 
**Rotation:** [0/3]

### Position:
| Cell | 0 | 1 | 2 |
|:-:|:-:|:-:|:-:|
|Row | 00 | 01 | 02 |
|Row | 00 | 01 | 02 |
|Row | 00 | 01 | 02 |
 
### Rotation: 
+ 0 = 0°
+ 1 = 90°
+ 2 = 180°
+ 3 = 270°

### Location Adress
uID | X | Y | Rot 
---:|:-:|:-:|:---
000 | 0 | 0 | 0 
010 | 0 | 1 | 0 
020 | 0 | 2 | 0 
100 | 1 | 0 | 0 
110 | 1 | 1 | 0 
120 | 1 | 2 | 0 
200 | 2 | 0 | 0 
210 | 2 | 1 | 0 
220 | 2 | 2 | 0 

## Checks & Priority
Input Request: [0/8][0/3][0/2][-1/1]
Select a Starting Piece
 With Starting Rotation
 On Starting Row
 And Starting Cell
Save to [Previous Request Array]

[Input Rquest Array] Starting Piece with Rotation, on Row and Cell Position
[Previous Request Array] Save to help users try new input
[Unoccupied Positions Array] Array of empty Positions
[Current Board Status] State of the Board, filled with the placed Pieces.

> We look through all the Unoccupied Tiles []
> We look through all the Unused Pieces []
> We Select a starting Piece00, with a rotation on a Starting position.
> We Remove the Tile from the Unused Tiles []
> We Remove the Piece00 form the Unused Pieces []
> //We Add the PieceData [] to the TableState []

> Step First Neighbor
> Next we decide which Tile to select.
> We look at all Unoccupied Tiles []
> We select a Tile, with X+1/-1 or Y+1/-1
> We Save each Tile as a Possible Position []

> Next we decide which piece to play next.
> We look at all Unused Pieces []
> We search for the negative Variant of the previous Piece00 Symbols []
> also using Rotations
> We Save each Piece01 as a Possible Choice []

> Step Second Neighbors
> We check if the hypothetical neighbours can connect in the current state

> We go through all Possible Choices[] on Possible Position[]
> We Look at each Neighbor tile
> We choose a fitting piece
> Next we check all Neighbors

> For each Possible Choice we check 
> If the can +Priority for the Possible Choice [Piece]
> If the can't -Priority for the Possible Choice [Piece]

> Step Third Neigbors
> All Neighbor Pieces01 created corners, these corners need to corrospond with an unused Piece.
> If this is not possible the Neighbor Pieces01 get -Priority each
> If this is possible the Neighbors Pieces01 and Piece00 get +Priority each: A complete 2x2 square has been created. 

> Step Priority Check 
> We Select a Possible Choice with the Highest Priority Ranking
> PriorityRank Ranking of the Piece, Higher Priority Rank is greater chance of selection.
> We create a hypothetical choice and try and complete the 3x3 square.
> If not possible either -priority or Add to Impossible Array
> If possible Solved. Add to Solved Array.
> Apply hypothetical positions and rotations to pieces

### Checks:
```
Check the Neighborhood for Unoccupied Tiles. Save these Tiles to the Unoccupied Positions Array.
// TABLE CHECK ()
For (Row < 2)
 For (Cell < 2)
 // OCCUPATION CHECK ()
If ([Row+X][Cell+Y][Occupied = False])
 Add to [Unoccupied Positions Array]

Select a New Piece
 Option 1. Based on User Input
 Option 2. Based on Array Position (Next Piece)
 Option 3. Based on First Symbol (Top Symbol Variant)
 Option 4. Based on Priority Rating

Rotate a Piece to connect to another piece with the same symbol
// ROTATION CHECK ()
For (Rotation < 3)
If ([Row][Cell] [Piece][Side][Type] == [Row][Cell][Rotation] [Piece][Side][Type])

Check if the Type is the Same, next check if the variant is the negative of the other.
// TYPE CHECK ()
If ([Piece][Side][Type] == [Piece][Side][Type])
// VARIANT CHECK ()
 If ([Variant] *-1 [Variant])
= Complete Symbol: Increase Priority

// TABLE CHECK ()
For (Row < 2)
 For (Cell < 2)

// GetCellState (xRow, yCell)
Return (isOccupied, [PieceData])
// SetCellState (xRow, yCell, isOccupied, [PieceData])
_isOccupied = isOccupied
_[PieceData] = [PieceData]

// 
```

### Priority: 
 +Pri = if a piece connects to another piece (Range: 1-4)
 -Pri = if no connects (Range: 1-4)
 
 +Pri = if connected pieces connect to another piece (Range: 1 + 8)
 -Pri = if no connects (Range: 1-4)

With Priority of 8 = Found 1 Solved State
