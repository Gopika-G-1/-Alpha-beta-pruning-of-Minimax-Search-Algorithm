<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: G.GOPIKA       </h3>
<h3>Register Number/Staff Id:212225230081           </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)


## program:

```
import math

# Initialize the Tic-Tac-Toe board
board = [" " for _ in range(9)]

# Display the board
def print_board():
    for i in range(0, 9, 3):
        print("|".join(board[i:i+3]))
        if i < 6:
            print("---------")

# Check winner
def check_winner():
    win_positions = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),
        (0, 3, 6), (1, 4, 7), (2, 5, 8),
        (0, 4, 8), (2, 4, 6)
    ]

    for a, b, c in win_positions:
        if board[a] == board[b] == board[c] != " ":
            return board[a]

    if " " not in board:
        return "Draw"

    return None

# Minimax with Alpha-Beta Pruning
def minimax(is_maximizing, alpha, beta):
    result = check_winner()

    if result == "X":
        return 1
    elif result == "O":
        return -1
    elif result == "Draw":
        return 0

    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "X"
                score = minimax(False, alpha, beta)
                board[i] = " "

                best_score = max(best_score, score)
                alpha = max(alpha, best_score)

                if beta <= alpha:
                    break

        return best_score

    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "O"
                score = minimax(True, alpha, beta)
                board[i] = " "

                best_score = min(best_score, score)
                beta = min(beta, best_score)

                if beta <= alpha:
                    break

        return best_score

# Find the computer's best move
def best_move():
    best_score = -math.inf
    move = None

    for i in range(9):
        if board[i] == " ":
            board[i] = "X"
            score = minimax(False, -math.inf, math.inf)
            board[i] = " "

            if score > best_score:
                best_score = score
                move = i

    return move

# Main game
def play_game():
    print("TIC-TAC-TOE GAME")
    print("You are O, Computer is X")
    print("Enter positions from 1 to 9")
    print("1 | 2 | 3")
    print("---------")
    print("4 | 5 | 6")
    print("---------")
    print("7 | 8 | 9")

    while True:
        print("\nCurrent Board:")
        print_board()

        # Player move
        try:
            pos = int(input("\nEnter your position (1-9): ")) - 1
        except ValueError:
            print("Invalid input! Enter a number.")
            continue

        if pos < 0 or pos >= 9 or board[pos] != " ":
            print("Invalid move! Try again.")
            continue

        board[pos] = "O"

        result = check_winner()
        if result:
            break

        # Computer move
        print("\nComputer's turn...")
        move = best_move()
        board[move] = "X"

        result = check_winner()
        if result:
            break

    print("\nFinal Board:")
    print_board()

    if result == "Draw":
        print("\nGame Draw!")
    else:
        print("\nWinner:", "Computer (X)" if result == "X" else "Player (O)")


# Start the game
play_game()
```

# output:
![alt text](<WhatsApp Image 2026-11-19 at 4.25.18 PM.jpeg>)

![alt text](<WhatsApp Image 2026-11-19 at 4.25.41 PM.jpeg>)

# result:
We have successfully implemented Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game.