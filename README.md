# Maze Game

This is a simple maze game written in Jack. The game generates a maze using an Iterative implementation (with stack).  
The player can move around the maze using the arrow keys. The goal is to reach the finish cell.

References:  
    [Wikipedia](https://en.wikipedia.org/wiki/Maze_generation_algorithm)  
    [Github/hbusul](https://github.com/hbusul/MazeEscaper)  

The following is the documentation for the classes and methods in the game:
## splashScreen.jack

This file contains the `splashScreen` class which is responsible for creating and managing the splash screen of the application. It has two methods:

1. `draw()`: This method is responsible for drawing the splash screen. It first clears the screen, then paints the splash screen, and finally prints the difficulty options for the user to choose from. The difficulty options are "Easy", "Medium", and "Hard". The method uses the `Screen.clearScreen()`, `Output.moveCursor()`, and `Output.printString()` methods to achieve this.

2. `paint(int location)`: This method is responsible for painting the splash screen at the specified memory location. It does this by poking values into the memory at the specified location and the following locations. The method uses the `Memory.poke()` method to achieve this.

## Stack.jack

This file contains the `Stack` class which is a simple implementation of a stack data structure. It has three methods:

1. `new(int size)`: This is the constructor of the `Stack` class. It creates a new stack with the specified size. It uses the `Array.new()` method to create a new array of the specified size.

2. `push(Cell item)`: This method is responsible for adding an item to the top of the stack. If the stack is full, it prints "Stack is full". Otherwise, it adds the item to the top of the stack and increments the stack pointer.

3. `pop()`: This method is responsible for removing and returning the item at the top of the stack. If the stack is empty, it prints "Stack is empty" and returns null. Otherwise, it decrements the stack pointer and returns the item at the top of the stack.

4. `getSize()`: This method returns the number of items in the stack. It does this by returning the value of the stack pointer.

The `Stack` class also has three fields:

- `items`: This is an array that holds the items in the stack.
- `max`: This is the maximum size of the stack.
- `sp`: This is the stack pointer, which points to the top of the stack.

## Cell.jack

This file contains the `Cell` class which represents a cell in the maze. A cell is made up of 4 lines. It has several methods and fields:

### Methods:

1. `new(int row,int colm,int width)`: This is the constructor of the `Cell` class. It creates a new cell at specified x,y of width w. It also initializes the walls of the cell and sets the cell as not visited.

2. `geti()`: This method returns the row number of the cell.

3. `getj()`: This method returns the column number of the cell.

4. `show()`: This method draws the walls of the cell.

5. `highlight()`: This method highlights the cell by drawing a smaller rectangle.

6. `setVisited()`: This method sets the cell as visited.

7. `getVisited()`: This method returns if the cell is visited.

8. `getWall(int index)`: This method returns the wall at the given index.

9. `removeLeftWall()`: This method removes the left wall of the cell.

10. `removeRightWall()`: This method removes the right wall of the cell.

11. `removeTopWall()`: This method removes the top wall of the cell.

12. `removeBottomWall()`: This method removes the bottom wall of the cell.

### Fields:

- `i`: This is the row number of the cell.
- `j`: This is the column number of the cell.
- `w`: This is the width of the cell.
- `walls`: This is an array of walls of the cell.
- `visited`: This is a boolean that indicates if the cell is visited.

## Player.jack

This file contains the `Player` class which is used to create a player object that represents the player in the maze. It has several methods and fields:

### Methods:

1. `new(int i,int j, int width)`: This is the constructor of the `Player` class. It creates a new player with the specified row, column, and width.

2. `draw()`: This method is used to draw the player on the screen.

3. `erase()`: This method is used to erase the player from the screen.

4. `geti()`: This method is used to get the row of the player.

5. `getj()`: This method is used to get the column of the player.

6. `move(int dir,Array Grid,int startRow,int startCol,int rows,int cols)`: This method is used to move the player in the maze.

### Fields:

- `row`: This field is used to store the row of the player.
- `colm`: This field is used to store the column of the player.
- `x`: This field is used to store the x-coordinate of the player.
- `y`: This field is used to store the y-coordinate of the player.
- `w`: This field is used to store the width of the player.


## Main.jack

This file contains the `Main` class which is the entry point of the application. It contains the main game loop and the logic for creating the maze and moving the player. It has several methods and fields:

### Methods:

1. `main()`: This is the main method of the application. It initializes the game, creates the maze, and handles the game loop.

2. `createPassage(int x,int y,Array grid,int rows,int cols,int startRow,int startCol,PseudoRand rng,Stack stack)`: This method is responsible for creating a passage in the maze. It takes the current cell's coordinates, the grid, the number of rows and columns, the starting row and column, a random number generator, and a stack as parameters. It returns the next cell to visit.

3. `removeWall(Cell curr,Cell next)`: This method is responsible for removing the wall between the current cell and the next cell. It takes the current cell and the next cell as parameters.

4. `showGrid(int startRow,int startCol,Array Cells,int rows,int cols)`: This method is responsible for drawing the grid on the screen. It takes the starting row and column, the grid, and the number of rows and columns as parameters.

### Fields:

- `next`: This is a `Cell` object that represents the next cell to visit.
- `finishCell`: This is a `Cell` object that represents the finish cell.
- `i`, `j`, `w`: These are integers that represent the row, column, and width of the cells.
- `rows`, `cols`: These are integers that represent the number of rows and columns in the grid.
- `startRow`, `startCol`: These are integers that represent the starting row and column.
- `Cells`: This is an array of `Cell` objects that represents the grid.
- `tempArr`: This is a temporary array used for various purposes.
- `rng`: This is a `PseudoRand` object used for generating random numbers.
- `stack`: This is a `Stack` object used for storing the cells to visit.
- `player`: This is a `Player` object that represents the player.
- `dir`: This is an integer that represents the direction of the player's movement.
- `gameover`, `difficultySelected`: These are booleans that represent whether the game is over and whether the difficulty has been selected.
- `key`, `seed`: These are integers that represent the key pressed and the seed for the random number generator.

## PseudoRand.jack

This file contains the `PseudoRand` class which is used to generate pseudo-random numbers. It uses a linear congruential generator algorithm for generating the numbers. The formula used is `Xn+1 = 17Xn + 5 mod 31`.

### Methods:

1. `def(int x)`: This is the constructor of the `PseudoRand` class. It initializes the current number (`cur`) with the given number `x`.

2. `next(int mod)`: This method generates the next pseudo-random number. It first calculates the term `(cur * 17) + 5`, then takes the modulus of the term with 31 using the `modula` method, and assigns the result back to `cur`. If the term is greater than `mod`, it subtracts `mod` from the term until it is less than or equal to `mod`. It then returns the term.

3. `modula(int number, int mod)`: This method calculates the modulus of a number with respect to `mod`. If the number is greater than `mod`, it subtracts `mod` from the number until it is less than or equal to `mod`. If the number is equal to `mod`, it sets the number to 0. If the number is less than 0, it adds `mod` to the number until it is greater than or equal to 0. It then returns the number.

### Fields:

- `cur`: This is the current number used in the generation of the next pseudo-random number.

This class is used in the `Main` class for generating random numbers for various purposes, such as deciding the next cell to visit in the maze. The `next` method is used to get the next random number, and the `modula` method is used to ensure that the generated number is within the desired range.