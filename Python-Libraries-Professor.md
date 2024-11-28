## **Code Implementation**
```python
import random


def main():
    # Get the user's level
    level = get_level()

    # Initialize score
    score = 0

    # Generate 10 math problems
    for _ in range(10):
        x = generate_integer(level)
        y = generate_integer(level)
        correct_answer = x + y

        # Ask the user to solve the problem
        if ask_question(x, y, correct_answer):
            score += 1

    # Output the final score
    print(f"Score: {score}")


def get_level():
    """
    Prompts the user for a difficulty level (1, 2, or 3).
    Returns:
        int: The selected level.
    """
    while True:
        try:
            level = int(input("Level: "))
            if level in [1, 2, 3]:
                return level
        except ValueError:
            pass


def generate_integer(level):
    """
    Generates a random non-negative integer with the specified number of digits.
    
    Args:
        level (int): The difficulty level (1, 2, or 3).
    
    Returns:
        int: A random integer with the specified number of digits.
    
    Raises:
        ValueError: If the level is not 1, 2, or 3.
    """
    if level == 1:
        return random.randint(0, 9)
    elif level == 2:
        return random.randint(10, 99)
    elif level == 3:
        return random.randint(100, 999)
    else:
        raise ValueError("Invalid level")


def ask_question(x, y, correct_answer):
    """
    Prompts the user to solve a math problem and provides feedback.
    The user gets up to three attempts for each problem.
    
    Args:
        x (int): The first number in the problem.
        y (int): The second number in the problem.
        correct_answer (int): The correct answer to the problem.
    
    Returns:
        bool: True if the user answers correctly, False otherwise.
    """
    attempts = 0
    while attempts < 3:
        try:
            # Prompt the user for an answer
            answer = int(input(f"{x} + {y} = "))
            if answer == correct_answer:
                return True
            else:
                print("EEE")
        except ValueError:
            print("EEE")
        attempts += 1

    # After three incorrect attempts, display the correct answer
    print(f"{x} + {y} = {correct_answer}")
    return False


if __name__ == "__main__":
    main()
```

---

### **Explanation**

#### **1. Main Function**
- Controls the program flow:
  - Prompts the user to select a difficulty level.
  - Initializes the score to `0`.
  - Loops through 10 math problems, generating random numbers based on the selected level.
  - Tracks the score by counting the number of correct answers.
  - Outputs the final score.

#### **2. `get_level` Function**
- Repeatedly prompts the user for a difficulty level until they enter `1`, `2`, or `3`.
- Ensures input validation by catching invalid entries.

#### **3. `generate_integer` Function**
- Generates random numbers based on the number of digits:
  - **Level 1**: Single-digit numbers (`0–9`).
  - **Level 2**: Two-digit numbers (`10–99`).
  - **Level 3**: Three-digit numbers (`100–999`).
- Raises a `ValueError` if the level is not valid.

#### **4. `ask_question` Function**
- Displays the math problem (`x + y = ?`) and validates the user's input.
- Allows the user up to three attempts to answer correctly.
  - If the answer is incorrect or invalid, the program displays `"EEE"`.
  - After three failed attempts, it reveals the correct answer.
- Returns `True` if the user answers correctly, `False` otherwise.

---

### **Example Usage**

#### Input/Output 1:
```plaintext
Level: 2
37 + 42 = 79
37 + 42 = 50
EEE
37 + 42 = 100
EEE
37 + 42 = 79
Correct Answer: 79
Score: 1
```

#### Input/Output 2 (Invalid Inputs):
```plaintext
Level: cat
Level: -1
Level: 2
37 + 42 = 79
```

---

### **Key Features**
1. **Input Validation**:
   - Ensures correct level selection and numerical answers.
2. **Dynamic Problem Generation**:
   - Problems are randomly generated based on the selected level.
3. **User Feedback**:
   - Provides hints like `"EEE"` for incorrect answers and displays the correct answer after three attempts.
4. **Score Tracking**:
   - Tracks and outputs the user's performance.
