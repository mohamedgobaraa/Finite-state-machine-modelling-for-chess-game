# Chess Game Finite State Machine (FSM)
This README provides an overview of the Chess Game FSM implemented in Python. The project is a simple command-line chess game using the python-chess library, where a player competes as White against a bot playing Black. The game tracks states and events, transitioning based on moves made and special conditions like check, checkmate, and draw scenarios.

## Requirements
### Python 3.x
### python-chess library for handling chess logic. Install it via:
```
pip install chess
```
### Code Overview
### Classes and Enums

GameState Enum
Defines the various states of the game:

INITIALIZING: Game is setting up.
IN_PROGRESS: Game is active.
CHECK: White is in check.
CHECKMATE: Game ends in checkmate.
STALEMATE: Game ends in a stalemate.
DRAW: Game ends in a draw.
END: Game has ended.

### GameEvent Enum
Defines possible game events, which trigger state transitions:

START_GAME: Starts the game.
MOVE_MADE: A move has been made.
CHECK_OCCURS: A check occurs.
CHECKMATE_OCCURS: Checkmate happens.
STALEMATE_OCCURS: Stalemate happens.
DRAW_DECLARED: Draw is declared.
END_GAME: Ends the game.

ChessGameFSM Class
A finite state machine for managing the game state based on player and bot moves. Main components:

__init__: Initializes the game in the INITIALIZING state with a fresh chess board.
on_event(self, event): Processes events to transition between states.
player_move_white(self, move_uci): Allows the player to make a move in UCI format (e.g., "e2e4"). Checks for game-ending conditions like checkmate or stalemate.
bot_move_black(self): Randomly selects a legal move for the bot playing as Black, checking for special conditions post-move.

### How the FSM Works
#### Game Initialization:

The game starts in the INITIALIZING state.
On the START_GAME event, it transitions to the IN_PROGRESS state, and the board is displayed.

#### Player Move (White):

When a valid move is made, the board is updated.
The FSM checks for special conditions:
If checkmate, stalemate, or insufficient material occurs, corresponding events are triggered.
If the game continues, it calls bot_move_black() for the bot's turn.

#### Bot Move (Black):

A random legal move is chosen for Black.
Similar to the player's move, it checks for check, checkmate, stalemate, or draw conditions, and triggers the appropriate events.

#### Game End:

The game reaches the END state when an END_GAME event is received, or if a game-ending condition occurs.


Example Usage
```python
game = ChessGameFSM()
game.on_event(GameEvent.START_GAME)  # Start the game

# Player move as White (in UCI format, e.g., "e2e4")
game.player_move_white("e2e4")
```
## Key Methods
on_event(event): Transitions the FSM based on the input event and prints the state change.
player_move_white(move_uci): Executes a move for the White player and checks for state changes.
bot_move_black(): Executes a move for the Black bot and checks for state changes.

## Example Game Flow
The player initializes the game with START_GAME.
The player inputs moves for White via player_move_white(move_uci).
After each move, the bot makes a move for Black.
The game continues until a checkmate, stalemate, or draw condition ends the game.

## Future Improvements
Add move validation feedback for players.
Implement more intelligent bot logic for improved gameplay.
Support for more chess rules, such as en passant and castling feedback.

## License
This code is for educational purposes. Feel free to modify and expand it for personal or project use.






