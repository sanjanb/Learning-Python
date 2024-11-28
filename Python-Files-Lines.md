### **Project: Lines of Code Counter**

This project involves creating a Python program that counts the **lines of code (LOC)** in a given Python file while excluding:

1. **Comments**: Lines that start with a `#`, optionally preceded by whitespace.
2. **Blank Lines**: Lines containing only whitespace.

---

### **Objective**
The goal is to provide an accurate count of the actual "code lines" in a Python file, which can give an indication of program complexity. However, this measure is simplified and does not necessarily correlate directly to the true complexity of a program.

---

### **Core Features**
1. **Input Validation**:
   - The program takes exactly one command-line argument: the name (or path) of a `.py` file.
   - If the argument is missing, invalid, or the file doesn't exist, the program exits with an appropriate error message.

2. **Line Filtering**:
   - Excludes:
     - Lines that are empty or contain only whitespace.
     - Lines that start with `#` (considered comments).
   - Counts:
     - Lines with actual Python code.
     - Lines containing docstrings (`""" or '''`), as they are part of the program.

3. **Error Handling**:
   - Detects and gracefully handles:
     - Missing or incorrect arguments.
     - Non-Python files.
     - Non-existent files.

4. **Ease of Use**:
   - Outputs a clean result: the total number of lines of code.

---

### **Program Flow**

1. **Command-Line Argument Handling**:
   - The program begins by checking if the user provided exactly one argument. If not, it displays the usage syntax and exits.

2. **File Validation**:
   - Ensures the file has a `.py` extension.
   - Checks if the file exists on the system.

3. **Counting LOC**:
   - Opens the file and processes it line by line.
   - For each line:
     - Removes leading whitespace using `lstrip()` to simplify analysis.
     - Skips:
       - Lines that are completely blank (`""` after stripping).
       - Lines that start with `#`.

4. **Output**:
   - Displays the total LOC after filtering.

---

### **Key Concepts Explained**

#### **1. What Counts as a Line of Code (LOC)?**
A **line of code** is any line in a Python file that contributes to the program's logic, functionality, or output. This includes:
- Variable declarations and assignments.
- Function and class definitions.
- Expressions (e.g., `print()` or calculations).
- Control flow statements (`if`, `for`, etc.).

#### **2. Exclusions**
- **Blank Lines**: These improve readability but do not contain logic.
- **Comments**: These are useful for documentation but are not executable.

#### **3. Why Exclude Blank Lines and Comments?**
Blank lines and comments:
- Do not contribute to the functionality or complexity of the code.
- Counting them would give an inflated LOC count, misrepresenting the program's size and complexity.

#### **4. Command-Line Arguments**
Command-line arguments allow users to interact with programs dynamically. In Python, `sys.argv` is a list where:
- `sys.argv[0]` is the script name.
- `sys.argv[1:]` are the arguments provided by the user.

#### **5. File Handling**
Python's `open()` function is used to read the file. It’s enclosed in a `try` block to handle cases where the file doesn’t exist.

#### **6. String Processing**
- `lstrip()`: Removes leading whitespace, simplifying checks for blank lines and comments.
- `startswith("#")`: Detects if a line is a comment.

---

### **Example**

#### **Input File: `example.py`**
```python
# This is a sample Python file

def greet(name):
    """Returns a greeting message."""
    return f"Hello, {name}"  # Return the greeting

# End of file
```

#### **Steps**

1. **Initial Lines**:
   - Line 1: Comment → Ignored.
   - Line 2: Blank → Ignored.
   - Line 3: Function definition → Counted.
   - Line 4: Docstring → Counted.
   - Line 5: Return statement → Counted.
   - Line 6: Comment → Ignored.

2. **LOC Count**: 3.

---

### **Edge Cases**

1. **Empty File**:
   - Contains no lines or only blank lines.
   - LOC = 0.

2. **Only Comments**:
   ```python
   # Comment 1
   # Comment 2
   ```
   - LOC = 0.

3. **Docstrings**:
   ```python
   """
   This is a docstring.
   It explains something.
   """
   print("Code after docstring")
   ```
   - Docstrings are part of code and counted.
   - LOC = 2.

4. **Mixed Blank and Non-Blank Lines**:
   ```python
   x = 5

   y = 10  # Variable declaration
   ```
   - LOC = 2.

---

### **Error Scenarios**

1. **No Command-Line Argument**:
   ```bash
   $ python lines.py
   Usage: python lines.py <filename>
   ```

2. **Non-Python File**:
   ```bash
   $ python lines.py file.txt
   Error: File must be a Python file with a .py extension.
   ```

3. **File Does Not Exist**:
   ```bash
   $ python lines.py nonexistent.py
   Error: File 'nonexistent.py' does not exist.
   ```

---

### **Benefits**

1. **Code Quality**: Focuses on functional LOC, helping developers assess code size without distractions from comments or blank lines.
2. **Error Handling**: Prevents crashes and guides users with clear error messages.
3. **Practical Application**: Useful for quickly estimating program complexity or reviewing a team's contributions.

---

### **Conclusion**

This project teaches:
- Handling command-line arguments.
- File operations (opening, reading, and handling missing files).
- Filtering lines using string methods.
- Error handling and graceful exits.

By implementing this program, you’ll gain practical skills in **file processing**, **error handling**, and **basic code metrics**, essential for many real-world applications.

**You can copy the code**:
   ```python
   import sys
import os

def count_lines_of_code(file_path):
    """
    Counts the number of lines of code in a Python file, excluding blank lines and comments.

    Args:
        file_path (str): Path to the Python file.

    Returns:
        int: Number of lines of code.
    """
    loc = 0
    try:
        with open(file_path, "r") as file:
            for line in file:
                stripped_line = line.lstrip()
                # Skip blank lines or lines starting with '#'
                if stripped_line == "" or stripped_line.startswith("#"):
                    continue
                loc += 1
    except FileNotFoundError:
        sys.exit(f"Error: File '{file_path}' not found.")
    return loc


def main():
    # Ensure exactly one command-line argument is provided
    if len(sys.argv) != 2:
        sys.exit("Usage: python lines.py <filename>")

    file_path = sys.argv[1]

    # Ensure the file has a .py extension
    if not file_path.endswith(".py"):
        sys.exit("Error: File must be a Python file with a .py extension.")

    # Ensure the file exists
    if not os.path.isfile(file_path):
        sys.exit(f"Error: File '{file_path}' does not exist.")

    # Count lines of code and print the result
    loc = count_lines_of_code(file_path)
    print(f"Number of lines of code: {loc}")


if __name__ == "__main__":
    main()

   ```

---
