# TicTacToe
A old game where a user can play with machine
import random

# initialize the board
board = ["-", "-", "-",
         "-", "-", "-",
         "-", "-", "-"]

human = "X"
computer = "O"

currentPlayer = None

gameRunning = True
winner = None

def printBoard(board):
    print(board[0] + " | " + board[1] + " | " + board[2])
    print("---------")
    print(board[3] + " | " + board[4] + " | " + board[5])
    print("---------")
    print(board[6] + " | " + board[7] + " | " + board[8])


def playerInput(board):
    global currentPlayer
    inp = int(input("Select a spot 1-9: "))
    if board[inp-1] == "-":
        board[inp-1] = currentPlayer
    else:
        print("Oops player is already at that spot.")


def checkHorizontle(board):
    global winner
    if board[0] == board[1] == board[2] and board[0] != "-":
        winner = board[0]
        return True
    elif board[3] == board[4] == board[5] and board[3] != "-":
        winner = board[3]
        return True
    elif board[6] == board[7] == board[8] and board[6] != "-":
        winner = board[6]
        return True

def checkRow(board):
    global winner
    if board[0] == board[3] == board[6] and board[0] != "-":
        winner = board[0]
        return True
    elif board[1] == board[4] == board[7] and board[1] != "-":
        winner = board[1]
        return True
    elif board[2] == board[5] == board[8] and board[2] != "-":
        winner = board[3]
        return True

def checkDiag(board):
    global winner
    if board[0] == board[4] == board[8] and board[0] != "-":
        winner = board[0]
        return True
    elif board[2] == board[4] == board[6] and board[4] != "-":
        winner = board[2]
        return True

def checkIfWin(board):
    global gameRunning
    if checkHorizontle(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False
    elif checkRow(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False
    elif checkDiag(board):
        printBoard(board)
        print(f"The winner is {winner}!")
        gameRunning = False

def checkIfTie(board):
    global gameRunning
    if "-" not in board:
        printBoard(board)
        print("It is a tie!")
        gameRunning = False


currentPlayer = random.choice([human, computer])
print(f"The {currentPlayer} will go first.")

# start the game
while gameRunning:
    if currentPlayer == human:
        # player's turn
        printBoard(board)
        playerInput(board)
        checkIfWin(board)
        if(gameRunning == True):
            checkIfTie(board)
        currentPlayer = computer
    else:
        # computer's turn
        print("Computer's turn")
        spot = random.randint(0, 8)
        if board[spot] == "-":
            board[spot] = computer
        else:
            continue
        checkIfWin(board)
        if(gameRunning == True):
            checkIfTie(board)
        currentPlayer = human

