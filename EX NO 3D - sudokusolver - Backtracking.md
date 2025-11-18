# EX 3D Sudoku solver - Backtracking
## Date:
## Aim:
To write a Java program to solve a Sudoku puzzle by filling the empty cells.

For example:

<img width="357" height="322" alt="image" src="https://github.com/user-attachments/assets/334b8c39-d547-4743-aca0-de92e38bdd1c" />

## Algorithm
1. **Find next cell** — Traverse the board row-wise. If column reaches 9, move to next row. If current cell is non-zero, skip to the next cell.  
2. **Try numbers 1–9** — For an empty cell, attempt to place numbers 1 through 9.  
3. **Check safety** — Before placing a number, ensure it does not already appear in the same row, same column, or the corresponding 3×3 subgrid (`isSafe`).  
4. **Recurse** — If placing a number is safe, assign it and recursively attempt to solve the rest of the board. If recursion returns true, solution found.  
5. **Backtrack** — If no number leads to a solution, reset the cell to 0 and backtrack. If all cells are filled successfully, return true; otherwise return false.

## Program:
```
Program to implement sudoku solver

Developed by: Krithick Vivekananda
Register Number: 212223240075

import java.util.Scanner;

public class SudokuSolver {

    // Check if it's safe to place the number
    static boolean isSafe(int[][] board, int row, int col, int num) {
        // Check row and column
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == num || board[i][col] == num)
                return false;
        }

        // Check 3x3 subgrid
        int startRow = row - row % 3;
        int startCol = col - col % 3;

        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[startRow + i][startCol + j] == num)
                    return false;

        return true;
    }

    // Recursive backtracking solver
    static boolean solveSudoku(int[][] board, int row, int col) {
        if (row == 8 && col == 9)
            return true;

        if (col == 9) {
            row++;
            col = 0;
        }

        if (board[row][col] != 0)
            return solveSudoku(board, row, col + 1);

        for (int num = 1; num <= 9; num++) {
            if (isSafe(board, row, col, num)) {
                board[row][col] = num;
                if (solveSudoku(board, row, col + 1))
                    return true;
                board[row][col] = 0; // Backtrack
            }
        }

        return false;
    }

    // Utility to print the board
    static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] board = new int[9][9];

      //  System.out.println("Enter the Sudoku puzzle row by row (use 0 for empty cells):");

        for (int i = 0; i < 9; i++) {
            //System.out.print("Enter row " + (i + 1) + ": ");
            for (int j = 0; j < 9; j++) {
                board[i][j] = sc.nextInt();
            }
        }

      //  System.out.println("\nSolving...\n");

        if (solveSudoku(board, 0, 0)) {
            System.out.println("Solved Sudoku:");
            printBoard(board);
        } else {
            System.out.println("No solution exists.");
        }

        sc.close();
    }
}
```

## Output:
<img width="745" height="612" alt="image" src="https://github.com/user-attachments/assets/d01bd666-62e9-4c45-84a4-5bb704bec285" />

## Result:
The program was successfully implemented and the expected output is verified.
