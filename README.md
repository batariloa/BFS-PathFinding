# PathFinding - BFS Search in a 2D Grid - Catching up 

Solution for the problem: "[Catching Up](https://www.codingame.com/ide/puzzle/catching-up)".
The provided code can also be tested on the mentioned link.

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

My goal was to solve the given problem using the Breadth First Search (BFS) algorithm. We are given 10 strings that represent the map, each containting 10 characters. 
We first take the provided strings, and transform them into a 2D array, which will serve as an internal representation of the map. We will use another 2D array to keep track of visited fields.
We can mark the areas which represent walls as visited, therefore the algorithm will not walk us into these areas.

The algorithm will find it's neighbours (fields it can go to next) using the explore method. The explore method will reverse the order of directions in which it explores. This way, we can avoid following the AI around in circles (Test 06 - Free Chase fails without reversal.).
The explore method:
```
public void explore(int row, int col, List < Character > currentPath) {


    // U, D, L, R
    //We are adding the 4 possible movement directions into an array, so we can reverse their order in the next iteration

    List < Location > movements = Arrays.asList(new Location(row - 1, col), new Location(row + 1, col), new Location(row, col - 1), new Location(row, col + 1));
    List < Character > komande = Arrays.asList('U', 'D', 'L', 'R'); 


    if (reverse) {                        //reversing the order of exploration every 2 iterations 
        Collections.reverse(movements);
        Collections.reverse(komande);
    }
    for (int i = 0; i < movements.size(); i++) {



        int rowPomeren = movements.get(i).row;
        int colPomeren = movements.get(i).col;
        char slovo = komande.get(i);

        if (isValid(rowPomeren, colPomeren, grid, visited)) {


            List < Character > temp = new ArrayList < Character > (currentPath);
            temp.add(slovo);
            queue.add(new Location(rowPomeren, colPomeren,
                temp));
            visited[rowPomeren][colPomeren] = true;
        }



    }
    reverse = !reverse;


}

```

Each time the location of the enemy (marked 'E), the BFS would recalculate the shortest path.
During each iteration of the main Thread's while loop, our character takes one move, and recalculates the shortest path if needed. 
 
