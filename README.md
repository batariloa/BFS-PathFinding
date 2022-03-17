# PathFinding

Solution for the problem found on:
https://www.codingame.com/ide/puzzle/catching-up

# Rules

The map is a 10x10 board, where each grid block is either a wall block or a floor block. Each character, you and the sus man, can only move in 4 directions—straight UP, DOWN, LEFT, RIGHT. In each turn, a legal move is to move in those 4 directions for 1 block length without end up going inside a wall block or going out of the map border.

Initialization Input

Before you take the first turn, you are given an input of 11 lines. The first line is an integer K representing after how many turns the sus man will make another move. The next 10 lines are a 10x10 two-dimensional char array. '*' represents a wall block and '-' represents a floor block. The uppercase characters 'P' represent your spawning location, and 'E' represent the sus man’s spawning location.

Input For a Game Turn

At the start of each turn, you will receive an input containing 2 integers in the same line, eneY and eneX, representing, respectively, the sus man’s vertical and horizontal coordinates. If the sus man is at the upper-left corner of the map, both eneY and eneX should have the value 0. If sus man goes DOWN for a block length, eneY will increase for 1. If sus man goes RIGHT for a block length, eneX will increase for 1.

The sus man will make a move in response to your move, but with a cold down. K turns after the sus man’s last move sus man will make another move. In the first turn, sus man always makes a move. When sus man makes a move, he stays STILL or goes UP, DOWN, LEFT, or RIGHT for a distance of 1 block. Among these 5 choices, sus man will always make the one which will result in the greatest distance to the player in this turn.

Output

To end a turn, you should output an uppercase character from 'U', 'D', 'L', 'R' to indicate your move of respectively going UP, DOWN, LEFT, or RIGHT for a distance of 1 block length.

# My Solution

My task was to demonstrate the use of the Breadth First Search (BFS) algorithm. We are presented 10 strings that represent the map, each containting 10 characters. 
We first take these strings, and transform them into a 2D matrix, which will be an internal representation of the map. We will use another 2D array to keep track of visited fields.
We can mark the areas which represent walls as visited, therefore the algorithm will not walk us into these areas.

The algorithm will find it's neighbours (fields it can go to next) using 4 methods: for moving up, down, left and right. 

The method for moving up:
```
  //moving up
  
   if (isValid(p.row - 1, p.col, grid, visited)) {       //checking if this field is a wall, or out of bounds
   
        List<Character> temp = new ArrayList<Character>(p.putanja); 
        temp.add('U');                                    // letter representing the required movement to get to this area
        queue.add(new Predmet(p.row - 1, p.col, temp));  //adding new Node to the queue, which containts the shortest path to reach it, and it's coordinates
        visited[p.row - 1][p.col] = true;                //setting this Node as visited
       
      }

```

Each time the location of the enemy (marked 'E), the BFS would recalculate the shortest path.
During each iteration of the main Thread's while loop, our character takes one move, and recalculates the shortest path if needed. 
