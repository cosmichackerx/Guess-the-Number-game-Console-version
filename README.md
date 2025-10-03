# Guess-the-Number-game-Console-version
---
```java
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Random rnd = new Random();

        System.out.println("🔥 Welcome to Guess The Number! 🔥");
        boolean playAgain = true;

        while (playAgain) {
            // Choose difficulty
            System.out.println("\nChoose difficulty: (1) Easy (1-20), (2) Medium (1-100), (3) Hard (1-1000)");
            int choice = readInt(sc, "Enter 1, 2 or 3: ");
            int max = switch (choice) {
                case 1 -> 20;
                case 3 -> 1000;
                default -> 100; // medium or any invalid choice
            };

            int secret = rnd.nextInt(max) + 1;
            int attempts = 0;
            int maxGuesses = Math.max(5, (int) Math.ceil(Math.log(max) / Math.log(2)) + 1); // suggested limit

            System.out.printf("I picked a number between 1 and %d. Try to guess it! You have %d attempts.\n", max, maxGuesses);

            boolean guessed = false;
            while (attempts < maxGuesses && !guessed) {
                int guess = readInt(sc, "Your guess: ");
                attempts++;

                if (guess <= 0 || guess > max) {
                    System.out.printf("Please guess a number within 1 and %d. Attempt wasted!\n", max);
                    continue;
                }

                if (guess == secret) {
                    System.out.printf("✨ You nailed it! The number was %d. Attempts: %d\n", secret, attempts);
                    guessed = true;
                } else if (guess < secret) {
                    System.out.println("Too low. Aim higher! ↑");
                } else {
                    System.out.println("Too high. Aim lower! ↓");
                }

                // Optional hint: tell how close they are
                if (!guessed) {
                    int diff = Math.abs(secret - guess);
                    if (diff <= Math.max(1, max / 20)) {
                        System.out.println("You're burning hot! 🔥");
                    } else if (diff <= Math.max(2, max / 10)) {
                        System.out.println("Warm. ♨️");
                    } else {
                        System.out.println("Cold. 🥶");
                    }
                    System.out.printf("Attempts left: %d\n", maxGuesses - attempts);
                }
            }

            if (!guessed) {
                System.out.printf("💥 Out of attempts! The number was %d. Better luck next time.\n", secret);
            }

            System.out.print("Play again? (y/n): ");
            playAgain = sc.next().trim().equalsIgnoreCase("y");
            sc.nextLine(); // clear rest of line
        }

        System.out.println("Thanks for playing! Come back when you're ready to be roasted again 😏");
        sc.close();
    }

    // Safe integer reader: keeps prompting until a valid integer is entered
    private static int readInt(Scanner sc, String prompt) {
        while (true) {
            System.out.print(prompt);
            String line = sc.nextLine().trim();
            try {
                return Integer.parseInt(line);
            } catch (NumberFormatException e) {
                System.out.println("That's not a number. Try again, genius. 💀");
            }
        }
    }
}
```
---
Here’s a polished **`README.md`** you can drop alongside your `GuessTheNumber.java` file. It explains the game, how to run it, and what features it has — in a clean, professional style but still keeping the fun tone of your code.  

---

```markdown
# 🎲 Guess The Number (Java Console Game)

A fun little **number guessing game** written in Java.  
The program picks a random number, and you try to guess it within a limited number of attempts.  
Difficulty levels, hints, and playful feedback are included to keep things interesting. 🔥

---

## 🚀 Features
- **Difficulty Levels**:
  - Easy → range **1–20**
  - Medium → range **1–100**
  - Hard → range **1–1000**
- **Smart attempt limit** → based on the range size (logarithmic formula).
- **Hints**:
  - Too high / Too low
  - Hot 🔥 / Warm ♨️ / Cold 🥶 proximity feedback
- **Replay option** → play as many rounds as you like.
- **Input validation** → wrong inputs don’t crash the game.

---

## 🖥️ How to Run

1. Make sure you have **Java 17+** installed (Java 21 recommended).
   ```bash
   java -version
   ```
2. Save the code as `GuessTheNumber.java`.
3. Compile the program:
   ```bash
   javac GuessTheNumber.java
   ```
4. Run the game:
   ```bash
   java GuessTheNumber
   ```

---

## 🎮 Gameplay Example

```
🔥 Welcome to Guess The Number! 🔥

Choose difficulty: (1) Easy (1-20), (2) Medium (1-100), (3) Hard (1-1000)
Enter 1, 2 or 3: 2
I picked a number between 1 and 100. Try to guess it! You have 8 attempts.

Your guess: 50
Too low. Aim higher! ↑
Cold. 🥶
Attempts left: 7

Your guess: 75
Too high. Aim lower! ↓
Warm. ♨️
Attempts left: 6

Your guess: 68
✨ You nailed it! The number was 68. Attempts: 3
Play again? (y/n): n
Thanks for playing! Come back when you're ready to be roasted again 😏
```

---

## 📂 Project Structure
```
GuessTheNumber.java   # Main game source file
README.md             # Documentation
```

---

## 🧠 Notes
- The attempt limit is calculated as:
  ```
  maxGuesses = max(5, log2(maxRange) + 1)
  ```
  This ensures fairness across difficulty levels.
- Input is validated with a helper method `readInt()` that keeps prompting until a valid integer is entered.

---

## ✨ Future Enhancements
- Add a **scoreboard** to track wins/losses.
- Add a **multiplayer mode** (player vs player).
- Add **colorful console output** for better UX.

---

## 📜 License
This project is free to use, modify, and share for learning purposes.
```

