# Snake: playtest notes

## How I played it

I opened `index.html` in Chrome (served from `localhost`, because the browser tool can't open `file://` pages) and played it in a real browser. The game is too fast to steer by hand through a screenshot-based tool, so I sent real keyboard events with tight timing. I also wrote a small steering script that read the canvas and pressed arrow keys to chase the food. I did not open the game code to decide what to test. I read it only afterwards, to explain the results below.

## What works

- The game opens straight from the file with no build step. It has a title, a Score / Best HUD, a 20x20 board and a controls hint.
- Arrow keys and WASD steer. Pressing the opposite direction (Left while moving Right) is ignored, so you can't kill yourself by reversing into your own neck.
- Eating food adds 10 points and grows the snake. My steering script ate 31 pieces in one run and reached a score of 310, and the snake grew as expected.
- Space pauses, and the snake stays frozen while paused. Space again resumes.
- Hitting a wall or your own body ends the game with "Game over — score N. Press Enter to restart."
- Enter restarts after a game over.
- Best score updates at game over and survives a page reload.

## What playing found (problems)

1. **The game starts instantly and you lose before you can react.** The snake starts moving the moment the page loads and reaches the right wall after about 1.3 seconds. Two of my first runs ended with score 0 and no input at all. It needs a "press a key to start" state, where the snake waits until the first arrow key.
2. **"Enter to restart" is only half true.** The hint always says Enter restarts, but Enter does nothing during a game. It only works after game over. I pressed it mid-game and nothing happened.
3. **Best doesn't update live.** Score was 310 while Best still said 0, and Best only caught up after I died. It's surprising to beat your record and not see it move.
4. **The game-over screen is easy to miss.** The only sign is a small green line under the board, and the board looks the same as during play. A dimmed board or a big overlay would make it obvious.
5. **Speed never changes.** The tick is a constant 110 ms, so the game is just as hard at score 300 as at score 0. It also feels too fast at the start (see 1).
6. **Small visual nits.** The head is only a slightly lighter green than the body and is hard to spot. The food fills its whole cell while the snake segments are inset by a pixel, so they look like different sizes. The canvas is 400x400 and looks small on a large monitor.

## What I would ask the agent to change

These are the requests. **None of them are applied yet.**

- [ ] Start paused with a "Press an arrow key to start" message, and begin moving on the first direction key.
- [ ] Make Enter restart at any time, or change the hint to "Enter to restart after game over".
- [ ] Update Best live as the score passes it.
- [ ] Make game over obvious: dim the board and show a large "Game over" message with the score.
- [ ] Slow the start down (about 150 ms per move) and speed up a little every few pieces of food.
- [ ] Make the head clearly different from the body, and draw food inset like the snake.
