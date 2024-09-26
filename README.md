# README for Lab10 - Fishing Game

## Project Description
This project is a simple fishing game implemented in C. The game uses signals to simulate actions such as putting the fishing rod into the water, waiting for a fish to bite, pulling the rod, and catching fish. The game will run until the user stops it manually.

### Files
- `lab10.c`: The main source code for the fishing game.
- `Makefile`: Used to compile and build the executable for the project.

### Compilation Instructions
To compile the project and generate the executable, use the `Makefile`. Simply run the following command:

```bash
make
```

This will compile `lab10.c` and create an executable called `lab10`.

### How to Run the Game
Once the executable is built, you can run the game by typing:

```bash
./fishing_game
```

### Gameplay Instructions
1. **Start the game**: Run the executable, and the game will initialize with the message "Fishing rod is ready!"
2. **Put the fishing rod**: Press `Ctrl + C` (`SIGINT`) to simulate putting the fishing rod into the water. A random timer will start, simulating the time it takes for a fish to bite.
3. **Pull the fishing rod**: After the timer goes off, press `Ctrl + C` again to pull the rod and check if a fish has been caught.
4. **Exit the game**: Press `Ctrl + Z` (`SIGTSTP`) to exit the game. The total number of caught fish will be displayed.

### Signals Used
- **SIGINT** (`Ctrl + C`): Used for putting and pulling the fishing rod.
- **SIGTSTP** (`Ctrl + Z`): Used to exit the game.
- **SIGALRM**: Generated internally after a random time to simulate the fish biting.

### Functions Description

1. **`put_pull_rod(int signum)`**:
   - Handles the fishing rod actions.
   - If the rod is in the water, it simulates pulling it out. If a fish was caught, the total number of fish caught is updated.
   - If the rod is not in the water, it simulates putting the rod into the water and starts waiting for a fish.

2. **`fish_eating(int signum)`**:
   - Handles the event of a fish biting.
   - If the rod is in the water, it indicates that a fish is biting, and the player should pull the rod.

3. **`exit_game(int signum)`**:
   - Exits the game gracefully, displaying the total number of fish caught before termination.

### Variables Description

- **`int fishNum`**: Counts the total number of fish caught during the game.
- **`int boolean`**: Acts as a state to track whether the rod is in the water or not.
- **`int fish_eaten`**: Indicates whether a fish is biting and ready to be caught.
- **`int bait`**: Tracks whether the bait is in the water.
- **`double total_time`**: Tracks the total time spent in the game (used for future extensions).

### Additional Notes
- The game simulates a simple fishing experience with random timers.
- Make sure you have `make` and a C compiler installed on your system before running the game.
