# 15_puzzle_problem
UVa 10181
/*
 * Howard Szeto
 * backtracking: given an input of arrangement of num 1-15 on 4x4 board,
 * output a sequence of move such that the numbers are arranged in the order
 */
import java.util.*;
import java.io.*;
class Main
{
    final static int GOINGUP = 1, GOINGDOWN = 2, GOINGLEFT = 3, GOINGRIGHT = 4, MAXMOVE = 50;
    int moves[], board[][], empty_rowLoc, empty_columnLoc, numMoves, minimumMovesNeeded;
    public Main(int newBoard[][], int rowLoc, int columnLoc)
    { /* init constructor */
        moves = new int[MAXMOVE];
        board = new int [4][4];
        minimumMovesNeeded = 0;
        for(int j=0;j<newBoard.length;j++) //copy the board over
            for(int k=0;k<newBoard[j].length;k++)
            {
                board[j][k] = newBoard[j][k];
                if(board[j][k]!=0)
                    minimumMovesNeeded += ((int)Math.abs(j-(board[j][k]-1)/4)+(int)Math.abs(k-(board[j][k]-1)%4));
            }
        empty_rowLoc = rowLoc; empty_columnLoc = columnLoc; /* empty location */
        numMoves = 0;
    }
    public Main(int movesSoFar[], int currentBoard[][], int newMove, int rowLoc, int columnLoc)
    { /* constructor */
        int i;
        moves = new int[MAXMOVE];
        board = new int[4][4];
        for(i=0;movesSoFar[i]!=0&&i<moves.length;i++)
            moves[i]=movesSoFar[i];
        moves[i] = newMove;
        numMoves = i+1;
        for(int j=0;j<board.length;j++)
            for(int k=0;k<board[j].length;k++)
                board[j][k] = currentBoard[j][k];
        minimumMovesNeeded = 0;
        if(newMove==GOINGUP)
        {
            board[rowLoc][columnLoc] = board[rowLoc-1][columnLoc];
            board[rowLoc-1][columnLoc] = 0;
            empty_rowLoc = rowLoc-1; empty_columnLoc = columnLoc;
        }
        else if(newMove==GOINGDOWN)
        {
            board[rowLoc][columnLoc] = board[rowLoc+1][columnLoc];
            board[rowLoc+1][columnLoc] = 0;
            empty_rowLoc = rowLoc+1; empty_columnLoc = columnLoc;
        }
        else if(newMove==GOINGLEFT)
        {
            board[rowLoc][columnLoc] = board[rowLoc][columnLoc-1];
            board[rowLoc][columnLoc-1] = 0;
            empty_rowLoc = rowLoc; empty_columnLoc = columnLoc-1;
        }
        else
        {
            board[rowLoc][columnLoc] = board[rowLoc][columnLoc+1];
            board[rowLoc][columnLoc+1] = 0;
            empty_rowLoc = rowLoc; empty_columnLoc = columnLoc+1;
        }
        for(int j=0;j<board.length;j++) //copy the board over
            for(int k=0;k<board[j].length;k++)
            {
                if(board[j][k]!=0)
                    minimumMovesNeeded += ((int)Math.abs(j-(board[j][k]-1)/4)+(int)Math.abs(k-(board[j][k]-1)%4));
            }
    }
    public static void main(String arg[])
    {
        Scanner sc = new Scanner (System.in);
        int initBoard[][]=new int [4][4];
        int n = sc.nextInt(); /*num of case*/
        for(int i=1;i<=n;i++)
        {
            for(int j=0;j<16;j++)
                initBoard[j/4][j%4] = sc.nextInt();
            findSoln(initBoard);
        }
    }
    public static void findSoln(int startingBoard[][])
    {
        int rowLoc=0, columnLoc=0;
        int initMoves[] = new int [MAXMOVE];
        boolean foundSoln = false;
        Deque<Main> possibleMoves = new ArrayDeque<Main>();
        for(int j=0;j<startingBoard.length;j++) /*search for the empty spot */
            for(int k=0;k<startingBoard.length;k++)
                if(startingBoard[j][k] == 0)
                {
                    rowLoc=j;  columnLoc=k;
                    j=4;  k=4; /* break the search loop) */
                }
        possibleMoves.add(new Main(startingBoard, rowLoc, columnLoc)); /* start the stack */
        int minimumRequirement = possibleMoves.peek().minimumMovesNeeded;
        while(!possibleMoves.isEmpty())
        {
            int matchedPieces;
            Main currentAssignment = possibleMoves.remove();
            if(currentAssignment.numMoves + currentAssignment.minimumMovesNeeded > MAXMOVE || currentAssignment.minimumMovesNeeded > minimumRequirement+4)
                continue;
            if(currentAssignment.minimumMovesNeeded < minimumRequirement)
                minimumRequirement = currentAssignment.minimumMovesNeeded;
            for(matchedPieces=0;matchedPieces<15;matchedPieces++)
            /* check if the board matches the desired arrangement */
                if(currentAssignment.board[matchedPieces/4][matchedPieces%4]!=matchedPieces+1)
                    break;
            if(matchedPieces==15)
            {
                for(int i=0;i<currentAssignment.moves.length;i++)
                    if(currentAssignment.moves[i]==GOINGUP)
                        System.out.print("U");
                    else if(currentAssignment.moves[i]==GOINGDOWN)
                        System.out.print("D");
                    else if(currentAssignment.moves[i]==GOINGLEFT)
                        System.out.print("L");
                    else if(currentAssignment.moves[i]==GOINGRIGHT)
                        System.out.print("R");
                    else
                        break;
                foundSoln = true;
                System.out.println();
                break;
            }
            if(currentAssignment.numMoves < MAXMOVE)
            {
                if(currentAssignment.empty_rowLoc!=0)
                if(currentAssignment.numMoves==0 || currentAssignment.moves[currentAssignment.numMoves-1]!=GOINGDOWN)
                    possibleMoves.add(new Main(currentAssignment.moves,currentAssignment.board, GOINGUP, currentAssignment.empty_rowLoc, currentAssignment.empty_columnLoc));
                if(currentAssignment.empty_rowLoc!=3)
                if(currentAssignment.numMoves==0 || currentAssignment.moves[currentAssignment.numMoves-1]!=GOINGUP)
                    possibleMoves.add(new Main(currentAssignment.moves,currentAssignment.board, GOINGDOWN, currentAssignment.empty_rowLoc, currentAssignment.empty_columnLoc));
                if(currentAssignment.empty_columnLoc!=0)
                if(currentAssignment.numMoves==0 || currentAssignment.moves[currentAssignment.numMoves-1]!=GOINGRIGHT)
                    possibleMoves.add(new Main(currentAssignment.moves,currentAssignment.board, GOINGLEFT, currentAssignment.empty_rowLoc, currentAssignment.empty_columnLoc));
                if(currentAssignment.empty_columnLoc!=3)
                if(currentAssignment.numMoves==0 || currentAssignment.moves[currentAssignment.numMoves-1]!=GOINGLEFT)
                    possibleMoves.add(new Main(currentAssignment.moves,currentAssignment.board, GOINGRIGHT, currentAssignment.empty_rowLoc, currentAssignment.empty_columnLoc));
            }
        }
        if(!foundSoln)
            System.out.println("This puzzle is not solvable.");
    }
}
