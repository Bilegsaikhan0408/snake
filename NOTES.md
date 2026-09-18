# Snake notes

## First playthrough

I opened the game in Chrome and tried to play. It was more or less unplayable at first, because the snake starts moving the moment the page loads. It reaches the right wall in about a second and a half, so my first two games ended at 0 points before I'd pressed anything. The game is fast, so I also used a small script to press keys for me and steer toward the food while I watched the results.

The basics were fine. The arrow keys and WASD work, and pressing the opposite direction does nothing, so you can't turn back into your own neck. Eating food gives 10 points and makes the snake longer, and Space pauses. Running into a wall or yourself ends the game. My script got up to 310 points in one run without any problems.

## What was wrong

The biggest problem was the instant start, as above. You need time to look at the board first.

The hint says "Enter to restart", but Enter did nothing in the middle of a game. It only worked after dying, so the hint wasn't really true.

Best score only changed when the game ended. I had 310 points and Best still said 0, and it caught up only after I crashed. That felt broken.

Game over was easy to miss. The board looked exactly the same and the only sign was a small line of text underneath it. I'd already crashed and kept staring at the board.

The speed never changed. It was too fast at the start and just as fast after 30 pieces of food, so it never got more exciting.

There were also a couple of small looks things. The head was almost the same green as the body, so I couldn't tell which end was which. The food was drawn slightly bigger than the snake's squares, which looked off.

## What I asked the agent to change

I told the agent, in words, to fix each of these:

1. Wait for the first arrow key before the snake starts, with a message saying so.
2. Make Enter restart at any time.
3. Update Best right when the score passes it.
4. Dim the board and show a big GAME OVER with the score.
5. Start slower, and speed up a little every few pieces of food.
6. Make the head a clearly different color, and draw the food the same size as the snake's squares.

## After the changes

I played it again and each fix works:

- The snake now waits, and the game says "Press an arrow key to start". If your first key would turn the snake straight back on itself, it still waits.
- Enter restarts in the middle of a game.
- Best moves along with the score as soon as you pass it, and it is still remembered after a reload.
- The game over screen is impossible to miss now.
- The game starts at 150 ms per move and gets faster every 3 pieces of food, down to 70 ms, which it reached at 300 points.
- The head is yellow, so it's easy to see, and the food matches the snake's squares.
