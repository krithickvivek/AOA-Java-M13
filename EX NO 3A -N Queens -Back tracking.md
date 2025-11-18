
# EX 3A N Queens Problem - Backtracking
## Date:
## Aim:
To Write a Java program for N queens using backtracking approach. You are given an integer N. For a given N x N chessboard, find a way to place 'N' queens such that no queen can attack any other queen on the chessboard. A queen can be attacked when it lies in the same row, column, or the same diagonal as any of the other queens. You have to print one such configuration.

<img width="241" height="209" alt="image" src="https://github.com/user-attachments/assets/96aacb61-4f34-423f-b324-5e34454e42b8" />

**Note:**
- Get the input from the user for N . The value of N must be from 1 to 4
- If solution exists Print a binary matrix as output that has 1s for the cells where queens are placed
- If there is no solution to the problem  print  "Solution does not exist"

## Algorithm
1. **Start** the program and read the board size `N` from the user.
2. **Initialize** an `N x N` board with all zeros to represent empty squares.
3. **Place queens column by column** using a recursive backtracking procedure: for each column, try every row and use the `isSafe()` check to decide if a queen can be placed.
4. **Backtrack** when a placement leads to no solution for the next columns (remove the queen and try the next row); continue until all columns are filled or all possibilities are exhausted.
5. **Print** the board if a solution is found or print "Solution does not exist" if not, then **stop** the program.  

## Program:
```
Program to implement N queens

Developed by: Krithick Vivekananda
Register Number: 212223240075  

import java.util.Scanner;

public class NQueens {
    static int N;

    // Function to print the solution
    static void printSolution(int[][] board) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Function to check if a queen can be placed on board[row][col]
    static boolean isSafe(int[][] board, int row, int col) {
        // Check left side of current row
        for (int i = 0; i < col; i++)
            if (board[row][i] == 1)
                return false;

        // Check upper diagonal on left side
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
            if (board[i][j] == 1)
                return false;

        // Check lower diagonal on left side
        for (int i = row, j = col; i < N && j >= 0; i++, j--)
            if (board[i][j] == 1)
                return false;

        return true;
    }

    // Recursive utility function to solve N-Queens
    static boolean solveNQUtil(int[][] board, int col) {
        if (col >= N)
            return true;

        for (int i = 0; i < N; i++) {
            if (isSafe(board, i, col)) {
                board[i][col] = 1;

                if (solveNQUtil(board, col + 1))
                    return true;

                board[i][col] = 0; // Backtrack
            }
        }

        return false;
    }

    // Main solver function
    static boolean solveNQ() {
        int[][] board = new int[N][N];

        if (!solveNQUtil(board, 0)) {
            System.out.println("Solution does not exist");
            return false;
        }

        printSolution(board);
        return true;
    }

    // Driver method
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt(); // Accept board size
        solveNQ();
    }
}
```

## Output:
<img width="682" height="268" alt="image" src="https://github.com/user-attachments/assets/9a585056-30c5-4ec0-a3ea-2a0d8f663574" />

## Result:
The program was successfully implemented and the output is verified. 
