English Draughts (Checkers) — Rules and Test Specification
1. Starting Position
Board & Orientation: The game is played on an 8×8 board, using only the dark squares. Each player must have a dark square on their left side (the “double corner”).
Initial Placement: Each player has 12 men, placed on the first three rows of dark squares closest to them.
First Move: Dark pieces move first.
2. Movement and Capturing Rules
2.1 Moves of a Man
A man may move only diagonally forward, one square at a time.
2.2 Moves of a King
A king may move diagonally forward or backward, also one square at a time.
2.3 Capturing
Mandatory Capture: If a capture is available, the player must capture. If multiple captures exist, the player may choose any (no “maximum capture” rule).
Direction:
A man may capture both forward and backward, provided a free landing square exists.
A king may capture diagonally in any direction.
Multiple Captures: If further captures are available after a jump, the capturing sequence must continue. The same piece may not be captured twice in a single turn.
3. Key Test Scenarios
Initialization: Validate correct board orientation and initial piece placement (12 per side, dark squares, double corner).
Non-Capturing Move: Ensure a non-capturing move is allowed only when no capture is available.
Mandatory Capture: Verify the engine rejects a simple move if a capture is possible.
Backward Capture by a Man: Confirm that a man can capture backward, even though it cannot move backward without capture.
Multiple Captures: Confirm that after the first capture, the sequence must continue if another capture is available.
King Movement and Capture: Verify a king moves only one diagonal square in any direction, and performs captures correctly.
No Double Capture of the Same Piece: Ensure the same opposing piece cannot be captured twice in one turn.
Promotion: Confirm promotion to king occurs when a man reaches the farthest rank.
Turn Order: Ensure dark moves first and players alternate turns.
Move Legality Boundaries: Disallow moves to light squares, off-board coordinates, or occupied squares without capture.
Draw/Stalemate (if implemented): Verify or document rules for draws (e.g., move repetition, no captures within N moves).
4. High-Priority Bugs
Allowing a non-capturing move when capture is available.
A man not being able to capture backward.
A king moving incorrectly (e.g., multiple squares like in Russian draughts).
Lack of enforcement for mandatory continuation of multiple captures.
Allowing the same piece to be captured twice in a single move.
Incorrect identification of promotion rows.
5. Test Data and Fixtures
Standard initial position for baseline validation.
Custom test positions to target: mandatory capture, backward capture by man, multi-captures, promotion scenarios, blocked moves, and illegal moves.
Turn-based fixtures to ensure correct alternation and dark’s first move.
6. UI/UX Recommendations for Testability
Stable selectors: Add attributes such as data-square="d6", data-piece="man-dark", data-turn="dark" for automated tests.
Move highlights: Indicate legal moves when a piece is selected for easier user understanding and test validation.
Interaction model: Support both drag-and-drop and click-to-move for accessibility and test automation.
Engine separation: Keep rules logic separate from rendering; expose the game state for unit testing.
7. Engine Architecture and Testing
Rules Engine Module: Should handle legal move generation, mandatory captures, multi-capture sequences, promotion, and turn switching independently of UI.
Unit Tests: Cover each rule and edge case in isolation.
Property-Based Testing: Use randomized board states to check invariants, such as:
Non-capturing moves are disallowed when captures exist.
Multi-capture continuation is mandatory.
Moves cannot land on light squares or off the board.
No piece can be captured more than once in a turn.
8. Acceptance Criteria
Correct initial setup and orientation.
Move generation strictly follows rules.
Mandatory capture and multi-captures are enforced
Men can capture backward but not move backward.
Kings move one diagonal square in any direction and capture per rules.
Promotion is reliable and correct.
Illegal moves are rejected with appropriate handling.
Turn order is strictly enforced.
UI accurately represents the engine’s state.
9. Suggested Enhancements
Scoring: Award points for captures or combos.
Undo/Redo: Maintain a move history for corrections and learning.
Replay/Export: Allow saving and reviewing move logs.
Diagnostics Panel: Display current turn, available captures, and pending multi-capture obligations.