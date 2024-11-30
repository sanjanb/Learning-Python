# **Project Overview**

The project involves implementing a Python program to count the occurrences of the word "um" in a given text. The count should:
1. Be **case-insensitive** (e.g., "Um", "UM", and "um" are all considered the same).
2. Only count "um" as a **standalone word** (not part of another word, e.g., "yummy" or "umbrella").

The project includes:
1. **Implementation** of the `count` function in `um.py`.
2. **Testing** the function with various cases in `test_um.py` using `pytest`.

---

### **File Structure**

- **`um.py`**: The main program that includes the `count` function to perform the counting logic and allows user interaction.
- **`test_um.py`**: A test file that validates the correctness of the `count` function using different test cases.

---

### **Detailed Explanation of the Implementation**

#### **1. `um.py` Implementation**

```python
import re

def main():
    print(count(input("Text: ")))

def count(s):
    # Regular expression to match "um" as a standalone word, case-insensitively
    pattern = r"\bum\b"
    matches = re.findall(pattern, s, re.IGNORECASE)
    return len(matches)

if __name__ == "__main__":
    main()
```

**Explanation of Each Component:**

1. **Regular Expressions (`re`)**:
   - **Purpose**: Used to match patterns in text.
   - The `re` module provides powerful tools for working with regular expressions in Python.
   - In this project:
     - We use `re.findall()` to find all occurrences of "um" in the input string.

2. **`count` Function**:
   - **Input**: A string `s` (text provided by the user).
   - **Output**: An integer (the number of times "um" appears as a standalone word).
   - **Logic**:
     - `\b`: Matches a **word boundary** (ensures "um" is not part of another word).
     - `um`: Matches the literal word "um".
     - `\b`: Ensures the match ends with a word boundary.
     - `re.IGNORECASE`: Makes the match **case-insensitive**.

3. **`main` Function**:
   - Prompts the user for input (`input("Text: ")`).
   - Calls the `count` function with the provided input.
   - Prints the result.

4. **`if __name__ == "__main__":`**:
   - Ensures the `main` function runs only when `um.py` is executed directly.

---

#### **2. `test_um.py` Implementation**

```python
from um import count

def test_single_um():
    assert count("um") == 1
    assert count("Um.") == 1
    assert count("um?") == 1

def test_multiple_ums():
    assert count("um, um, um.") == 3
    assert count("Um, thanks, um...") == 2
    assert count("um um um") == 3

def test_no_um():
    assert count("yummy") == 0
    assert count("umbrella") == 0
    assert count("aluminum") == 0

def test_mixed_cases():
    assert count("Um, UM, uM.") == 3
    assert count("um... UM.") == 2

def test_with_punctuation():
    assert count("um. um! um?") == 3
    assert count("Um? Thanks, um.") == 2
```

**Explanation of Each Test:**

1. **Test Framework**:
   - Uses `pytest`, a Python library for testing.
   - Functions starting with `test_` are automatically identified and executed by `pytest`.

2. **Test Cases**:
   - **`test_single_um`**:
     - Tests the simplest cases where "um" appears once in various forms.
   - **`test_multiple_ums`**:
     - Ensures multiple occurrences of "um" are counted correctly.
   - **`test_no_um`**:
     - Validates that "um" within other words (e.g., "umbrella") is not counted.
   - **`test_mixed_cases`**:
     - Confirms that the function handles case-insensitivity.
   - **`test_with_punctuation`**:
     - Tests that punctuation marks do not interfere with counting.

3. **Assertions**:
   - The `assert` statement checks whether the function's output matches the expected value.
   - If the condition is `True`, the test passes; otherwise, it fails.

---

### **Concepts Used**

1. **Regular Expressions (`re` module)**:
   - **Purpose**: Identify patterns in text.
   - Key functions:
     - `re.findall(pattern, string, flags)`: Finds all matches of `pattern` in `string`. Returns a list of matches.
   - **Pattern Explanation**:
     - `r"\bum\b"`:
       - `\b`: Matches a word boundary (start or end of a word).
       - `um`: Matches the literal string "um".
       - `\b`: Ensures no extra characters after "um".

2. **String Matching**:
   - Handles case-insensitivity using `re.IGNORECASE`.
   - Differentiates standalone words from substrings using word boundaries (`\b`).

3. **Unit Testing with `pytest`**:
   - Modular test functions for different scenarios.
   - Ensures the robustness of the `count` function against edge cases.

4. **Error Handling**:
   - Regular expressions inherently filter incorrect matches (e.g., substrings like "umbrella").

---

### **Examples**

1. **Interactive Testing** (`um.py`):
   ```
   $ python um.py
   Text: um, thanks, um...
   2
   ```

2. **Automated Testing** (`test_um.py`):
   ```
   $ pytest test_um.py
   ============================= test session starts ==============================
   ...
   collected 5 items                                                              

   test_um.py .....                                                          [100%]

   ============================== 5 passed in 0.03s ===============================
   ```

---

### **Why This Approach is Effective**

1. **Efficiency**:
   - The `re.findall` method directly identifies matches in one pass over the text.
   - The use of `\b` avoids unnecessary computation.

2. **Robustness**:
   - Comprehensive test coverage ensures edge cases are handled (e.g., punctuation, case-insensitivity).

3. **Scalability**:
   - Regular expressions can easily be modified to match other patterns if needed.

4. **Readability**:
   - The logic is modular, making it easy to understand and maintain.

---

This project demonstrates the power of **regular expressions** and emphasizes the importance of **testing** in software development. It provides a practical example of solving a real-world problem using Python's built-in capabilities.
