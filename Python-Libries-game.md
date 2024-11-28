# **Documentation for `game.py`**

## **Overview**
This program is an interactive guessing game where:
1. The user selects an upper limit (`level`) for a randomly generated number.
2. The program generates a random number between 1 and the chosen level (inclusive).
3. The user is prompted to guess the number. After each guess, the program provides feedback:
   - **"Too small!"** if the guess is lower than the secret number.
   - **"Too large!"** if the guess is higher than the secret number.
   - **"Just right!"** if the guess matches the secret number, at which point the game ends.

---

## **Code Breakdown**

### **1. Importing the Random Library**
```python
import random
```

- **What?**
  - The `random` module is used to generate random numbers.
- **Why?**
  - To make the guessing game dynamic, the program needs a randomly chosen number as the secret number.
- **How?**
  - The `random.randint(a, b)` function generates a random integer between `a` and `b` (inclusive).

---

### **2. Main Function**
```python
def main():
    level = get_positive_integer("Level: ")
    secret_number = random.randint(1, level)
    play_game(secret_number)
```

#### **Purpose**:
The `main()` function serves as the entry point of the program. It:
1. Prompts the user to set an upper limit (`level`) for the guessing range.
2. Generates a secret random number within the range [1, level].
3. Starts the guessing game by calling the `play_game` function.

---

### **3. Getting a Positive Integer**
```python
def get_positive_integer(prompt):
    """
    Prompt the user for a positive integer.

    Args:
        prompt (str): The prompt to display to the user.

    Returns:
        int: A positive integer entered by the user.
    """
    while True:
        try:
            value = int(input(prompt))
            if value > 0:
                return value
        except ValueError:
            pass
        print("Invalid input. Please enter a positive integer.")
```

#### **What?**
This function repeatedly prompts the user for a positive integer until valid input is provided.

#### **Why?**
To ensure robust input handling, the program must:
1. Validate that the input is a number.
2. Check that the number is greater than zero.

#### **How?**
1. The function uses an infinite loop (`while True`) to repeatedly ask for input.
2. Inside the loop:
   - **Try Block**: Converts the user input to an integer.
     - If successful and the number is positive, it returns the value.
   - **Except Block**: Handles cases where the input is not a valid integer (e.g., letters or special characters).
3. If the input is invalid or non-positive, the user is reprompted with an error message.

#### **Example**:
- Input: `"10"` → Valid → Returns `10`
- Input: `"cat"` → Invalid → Displays error message → Reprompts
- Input: `"-5"` → Invalid → Displays error message → Reprompts

---

### **4. Playing the Game**
```python
def play_game(secret_number):
    """
    Play the guessing game with the user.

    Args:
        secret_number (int): The randomly generated number the user must guess.
    """
    while True:
        guess = get_positive_integer("Guess: ")

        if guess < secret_number:
            print("Too small!")
        elif guess > secret_number:
            print("Too large!")
        else:
            print("Just right!")
            break
```

#### **What?**
This function runs the core gameplay loop, where the user repeatedly guesses the secret number.

#### **Why?**
The program needs to:
1. Validate guesses.
2. Provide feedback on whether the guess is too low, too high, or correct.

#### **How?**
1. The function uses a loop (`while True`) to continuously prompt for guesses.
2. Each guess is compared with the `secret_number`:
   - **`guess < secret_number`**: Displays "Too small!" if the guess is smaller than the secret number.
   - **`guess > secret_number`**: Displays "Too large!" if the guess is larger.
   - **`guess == secret_number`**: Displays "Just right!" and exits the loop using `break`.
3. The `get_positive_integer` function ensures all guesses are valid positive integers.

---

### **5. Program Entry Point**
```python
if __name__ == "__main__":
    main()
```

#### **What?**
This ensures the `main()` function is executed only when the script is run directly.

#### **Why?**
- When importing this script into another Python file as a module, the `main()` function should not run automatically.
- This is standard Python practice for modularity and reusability.

---

## **Program Flow**

1. **Level Selection**:
   - The user sets the upper limit for the guessing range.
   - Example: If the user enters `10`, the secret number will be randomly chosen between 1 and 10.

2. **Game Start**:
   - The user repeatedly guesses the number until they are correct.
   - Feedback is provided after each guess.

3. **Game End**:
   - When the user guesses the number correctly, the program outputs `"Just right!"` and ends.

---

## **Example Usage**

### **Scenario 1: Simple Playthrough**
#### Input:
```plaintext
Level: 10
Guess: 5
Too small!
Guess: 8
Too large!
Guess: 7
Just right!
```

#### Explanation:
- The secret number is `7`.
- The user guesses `5` (too low), then `8` (too high), and finally `7` (correct).

---

### **Scenario 2: Handling Invalid Input**
#### Input:
```plaintext
Level: cat
Invalid input. Please enter a positive integer.
Level: -1
Invalid input. Please enter a positive integer.
Level: 20
Guess: dog
Invalid input. Please enter a positive integer.
Guess: 15
Too large!
Guess: 10
Too small!
Guess: 13
Just right!
```

#### Explanation:
- The program gracefully handles invalid inputs (`cat`, `-1`, and `dog`), reprompting the user each time.

---

## **Key Points**
1. **Robust Input Validation**: Ensures all inputs are positive integers.
2. **Dynamic Gameplay**: Randomized secret number makes each game unique.
3. **User Feedback**: Guides the user with precise hints after each guess.
4. **Code Modularity**: Separate functions (`get_positive_integer` and `play_game`) improve readability and reusability.

---

## **Potential Enhancements**
1. **Guess Counter**:
   - Track the number of guesses and display it when the game ends.
   - Example: `"Just right! You guessed it in 5 tries."`
2. **Difficulty Levels**:
   - Allow the user to choose difficulty levels (e.g., Easy, Medium, Hard) with preset ranges.
3. **Replay Option**:
   - Ask the user if they want to play another round after finishing.
