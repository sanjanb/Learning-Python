# **Project Overview: Fun Math Quiz**

The **Fun Math Quiz** is an interactive program designed to test and improve your math skills in an engaging way. Players solve 10 addition problems with numbers based on their selected difficulty level. It’s designed to feel like a game, making math both fun and challenging.

---

### **How It Works**

1. **Choose Difficulty Level**:
   - The player selects a level to determine the difficulty of the math problems:
     - **Level 1 (Easy):** Single-digit numbers (0–9).
     - **Level 2 (Medium):** Two-digit numbers (10–99).
     - **Level 3 (Hard):** Three-digit numbers (100–999).

2. **Solve 10 Problems**:
   - The program generates 10 random addition problems based on the chosen level.
   - For example:
     - Level 1: `5 + 3 = ?`
     - Level 2: `45 + 67 = ?`
     - Level 3: `354 + 768 = ?`

3. **Attempt to Solve**:
   - The player has **3 attempts** to answer each problem.
   - Feedback is provided after each incorrect attempt with a playful message like `"Oops! Try again."`
   - If the player cannot answer correctly in 3 tries, the program displays the correct answer.

4. **Score Calculation**:
   - For every correct answer, the player earns 1 point.
   - After completing all 10 questions, the program displays the player’s final score out of 10.

5. **Replayability**:
   - Each game generates **new random problems**, making it different every time.

---

### **Key Features**

1. **Levels of Difficulty**:
   - Tailors the questions to the player’s skill level, making it suitable for beginners and pros.

2. **Encouraging Feedback**:
   - Friendly messages after incorrect answers keep the game light-hearted and fun.

3. **Limited Attempts**:
   - Adds a sense of challenge by restricting the player to 3 tries per question.

4. **Dynamic Question Generation**:
   - Random numbers ensure every quiz is unique.

5. **Score Tracking**:
   - Keeps players motivated by displaying their final score.

---

### **Technical Breakdown**

#### **1. Functions**

| Function         | Purpose                                                                                                                                       |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `main()`         | Manages the overall flow of the program: difficulty selection, problem generation, score tracking, and displaying the final score.            |
| `get_level()`    | Prompts the user to choose a difficulty level (1, 2, or 3) and ensures valid input.                                                           |
| `generate_integer(level)` | Generates a random number based on the difficulty level. For example, single-digit numbers for Level 1 and three-digit numbers for Level 3. |
| `ask_question(x, y, correct_answer)` | Prompts the player with a math problem, checks the answer, provides feedback, and allows up to 3 attempts.                          |

#### **2. Concepts Used**
- **Random Number Generation**: Creates math problems dynamically using `random.randint`.
- **Input Validation**: Ensures that user input is appropriate (e.g., valid level, numeric answers).
- **Loops and Conditionals**: Controls question attempts and tracks correct/incorrect answers.
- **Scorekeeping**: Tracks the player’s score using a counter variable.

---

### **Example Gameplay**

#### **Input/Output Example**

**Scenario: Player chooses Level 2 and plays the game.**

```plaintext
🎯 Welcome to Math Mayhem! 🎯
Choose your level (1 = Easy, 2 = Medium, 3 = Hard): 2
🤓 You've chosen Level 2. Let the games begin!

🔥 Question 1: 🔥
🤔 What's 45 + 67? 100
❌ Oops! Try again. (Hint: Think carefully!)
🤔 What's 45 + 67? 112
🎉 Correct! You're on fire! 🔥

🔥 Question 2: 🔥
🤔 What's 23 + 89? 120
❌ Oops! Try again. (Hint: Think carefully!)
🤔 What's 23 + 89? 112
❌ Oops! Try again. (Hint: Think carefully!)
🤔 What's 23 + 89? 112
📢 The correct answer was: 112

🏆 Game Over! Your final score is: 1/10 🏆
```

---

### **Why This Project Matters**

1. **Fun Way to Learn Math**:
   - Makes practicing addition enjoyable for students and anyone looking to sharpen their math skills.

2. **Replayable & Challenging**:
   - The dynamic generation of problems means players never see the same question twice.

3. **Engages Users**:
   - Encourages users with friendly messages and score tracking, keeping them motivated to improve.

4. **Practical Programming Concepts**:
   - Demonstrates input validation, conditionals, loops, and randomization—all essential for beginner programmers.

---

### **Future Enhancements**

1. **Add Subtraction, Multiplication, or Division**:
   - Include different operations for a more diverse quiz.

2. **Timed Mode**:
   - Introduce a timer for each question to add pressure and excitement.

3. **Leaderboard System**:
   - Record high scores for competitive play among friends or classmates.

4. **Visual Interface**:
   - Build a graphical user interface (GUI) for a more polished look.


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
