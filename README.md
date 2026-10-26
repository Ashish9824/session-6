# session-6

### Task 1: Countdown Timer (10 Down to 1)

```c
#include <stdio.h>

int main() {
    printf("Countdown starting...\n");

    // For loop: starts at 10, decrements by 1 each iteration until 1
    for (int i = 10; i >= 1; i--) {
        printf("%d\n", i);
    }

    printf("Blast off! 🚀\n");
    return 0;
}

```

---

### Task 2: Menu-Driven Console App (`while` Loop)

```c
#include <stdio.h>
#include <string.h>

int main() {
    // Array storing up to 10 team names
    char teams[10][50] = {
        "Mumbai Indians",
        "Chennai Super Kings",
        "Royal Challengers Bengaluru"
    };
    int teamCount = 3;
    int choice = 0;

    // While loop keeps running until the user selects option 3 (Exit)
    while (choice != 3) {
        printf("\n=== IPL Team Manager ===\n");
        printf("1. View Favorite Teams\n");
        printf("2. Add a New Team\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        // Clear input buffer newline
        while (getchar() != '\n');

        if (choice == 1) {
            printf("\n--- Favorite IPL Teams ---\n");
            for (int i = 0; i < teamCount; i++) {
                printf("%d. %s\n", i + 1, teams[i]);
            }
        } else if (choice == 2) {
            if (teamCount < 10) {
                printf("Enter new team name: ");
                fgets(teams[teamCount], sizeof(teams[teamCount]), stdin);
                teams[teamCount][strcspn(teams[teamCount], "\n")] = '\0'; // Remove newline
                teamCount++;
                printf("Team added successfully!\n");
            } else {
                printf("Team list is full!\n");
            }
        } else if (choice == 3) {
            printf("Exiting application. Goodbye!\n");
        } else {
            printf("Invalid choice! Please select 1, 2, or 3.\n");
        }
    }

    return 0;
}

```

---

### Task 3: 'Guess the Song' Game (`do-while` Loop)

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

int main() {
    // List of songs
    const char *songs[] = {
        "Starboy",
        "Believer",
        "Mockingbird",
        "Shape of You"
    };
    int totalSongs = 4;

    // Seed random number generator and pick a random song
    srand(time(NULL));
    int randomIndex = rand() % totalSongs;
    const char *targetSong = songs[randomIndex];

    char guess[100];
    int attempts = 0;

    printf("=== Spotify Guess the Song Game ===\n");
    printf("Hint: Choose among 'Starboy', 'Believer', 'Mockingbird', 'Shape of You'\n\n");

    // Do-while loop guarantees the user gets at least one guess prompt
    do {
        attempts++;
        printf("Attempt %d - Enter your guess: ", attempts);
        fgets(guess, sizeof(guess), stdin);
        guess[strcspn(guess, "\n")] = '\0'; // Strip trailing newline

        if (strcasecmp(guess, targetSong) != 0) {
            printf("Incorrect guess, try again!\n\n");
        }
    } while (strcasecmp(guess, targetSong) != 0);

    printf("\nBingo! You guessed it right: \"%s\" in %d attempts! 🎵\n", targetSong, attempts);
    return 0;
}

```

---

### Task 4: Entry-Controlled vs. Exit-Controlled Loops

#### Core Distinction

* **Entry-Controlled Loop (`for`, `while`):** The condition is evaluated **before** entering the loop body. If the condition is false at the very beginning, the body will execute **0 times** (it is skipped entirely).
* **Exit-Controlled Loop (`do-while`):** The condition is evaluated **after** the loop body runs. Even if the condition is false at the start, the loop body executes **at least once**.

---

#### Code Snippets Demonstrating False Condition at Start

##### 1. Entry-Controlled (`while` loop)

```c
#include <stdio.h>

int main() {
    int balance = 0; // Less than 100

    // Condition is evaluated FIRST
    while (balance >= 100) {
        printf("Withdrawal approved!\n");
        balance -= 100;
    }

    printf("Transaction completed (while loop never executed).\n");
    return 0;
}

```

* **Behavior:** Because `balance >= 100` is `0 >= 100` (`false`), the body is skipped completely. Output is only the outer print statement.

##### 2. Exit-Controlled (`do-while` loop)

```c
#include <stdio.h>

int main() {
    int balance = 0; // Less than 100

    // Body runs FIRST before condition is evaluated
    do {
        printf("Withdrawal attempted!\n");
        balance -= 100;
    } while (balance >= 100);

    printf("Transaction completed (do-while executed exactly 1 time).\n");
    return 0;
}

```

* **Behavior:** The statement `"Withdrawal attempted!"` prints once, even though `balance >= 100` is `false` from the start.
