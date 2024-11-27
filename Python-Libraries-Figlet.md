# Explanation of the `figlet.py` Code with Documentation Using What, How, and Why

---

### **What Does This Program Do?**
The program uses the `pyfiglet` library to render ASCII art from text input provided by the user. It supports:
1. **Random Font Selection**: If no font is specified in the command-line arguments.
2. **Specific Font Rendering**: If a valid font name is provided with the `-f` or `--font` argument.
3. **Error Handling**: Exits with an appropriate error message if invalid arguments or font names are given.

---

### **Code Walkthrough**

#### 1. **Imports**
```python
import sys
import random
from pyfiglet import Figlet
```

**What?**
- `sys`: Used to handle command-line arguments and exit the program in case of errors.
- `random`: Enables random selection of fonts when no specific font is provided.
- `pyfiglet`: The library for generating ASCII art.

**Why?**
These modules provide the necessary functionalities:
- `sys` helps manage user input through command-line arguments.
- `random` allows choosing a random font dynamically.
- `pyfiglet` is the core library for rendering ASCII text.

---

#### 2. **Main Function**
```python
def main():
    # Create a Figlet instance
    figlet = Figlet()
    available_fonts = figlet.getFonts()
```

**What?**
- Initializes a `Figlet` object to interact with the library.
- Retrieves the list of all available fonts using `getFonts()`.

**How?**
- `Figlet()` creates the object, and `getFonts()` fetches the fonts supported by the library.

**Why?**
The program needs access to the font list to validate user input or randomly select a font.

---

#### 3. **Command-Line Argument Handling**
```python
    # Check for command-line arguments
    if len(sys.argv) == 1:  # No arguments; use a random font
        font = random.choice(available_fonts)
    elif len(sys.argv) == 3 and (sys.argv[1] == "-f" or sys.argv[1] == "--font"):
        if sys.argv[2] not in available_fonts:  # Invalid font
            sys.exit("Invalid usage")
        font = sys.argv[2]  # Valid font provided
    else:
        sys.exit("Invalid usage")  # Invalid arguments
```

**What?**
- Handles different cases of user input through command-line arguments:
  - No arguments: Selects a random font.
  - Two arguments (`-f` or `--font` with a valid font): Uses the specified font.
  - Any invalid input: Exits with an error message.

**How?**
- Checks the length of `sys.argv` to determine the number of arguments.
- Verifies the validity of the font provided in the second argument.
- Exits the program with `sys.exit("Invalid usage")` for invalid cases.

**Why?**
- To ensure the program behaves predictably and gracefully handles errors.
- Allows flexibility for the user to either select a specific font or let the program choose randomly.

---

#### 4. **Set the Font**
```python
    # Set the selected font
    figlet.setFont(font=font)
```

**What?**
- Applies the chosen font to the `Figlet` object.

**How?**
- Uses the `setFont` method with the selected `font` as an argument.

**Why?**
This step ensures that the text is rendered using the correct font, whether it is user-specified or randomly chosen.

---

#### 5. **Prompt the User for Input**
```python
    # Prompt user for input text
    text = input("Enter text: ")
```

**What?**
- Asks the user to input a string to be converted into ASCII art.

**How?**
- The `input()` function captures the user's input.

**Why?**
The program needs text to process and render in the selected font.

---

#### 6. **Render and Output the Text**
```python
    # Print the text in the chosen font
    print(figlet.renderText(text))
```

**What?**
- Converts the input text into ASCII art using the selected font and prints it.

**How?**
- The `renderText()` method generates ASCII art for the input string.

**Why?**
This is the program's core functionality—transforming user input into ASCII art using the FIGlet library.

---

#### 7. **Run the Main Function**
```python
if __name__ == "__main__":
    main()
```

**What?**
- Ensures that the `main()` function runs only when the file is executed directly.

**How?**
- Python’s special variable `__name__` equals `"__main__"` only when the script is run directly, not when imported.

**Why?**
Prevents unintended execution when the file is imported as a module elsewhere.

---

### **Why Are These Features Useful?**
1. **Random Font Selection**:
   - Adds creativity and surprise for the user.
   - Ensures that the program works even without specific input.
   
2. **Custom Fonts**:
   - Gives users control over the output appearance.
   - Supports personalization for various use cases.

3. **Error Handling**:
   - Enhances robustness by guiding users to provide valid input.
   - Prevents crashes or undefined behavior.

4. **Dynamic Rendering**:
   - Makes the program flexible for different types of text input.

---

### **Output Examples**

#### Example 1: Random Font
```bash
$ python figlet.py
Enter text: Hello!
<Hello! rendered in a random font>
```

#### Example 2: Valid Font
```bash
$ python figlet.py -f slant
Enter text: CS50
   ___________ __________ 
  / ____/ ___// ____/ __ \
 / /    \__ \/___ \/ / / /
/ /___ ___/ /___/ / /_/ / 
\____//____/_____/\____/  
```

#### Example 3: Invalid Font
```bash
$ python figlet.py -f invalid_font
Invalid usage
```

---

### **How to Save and Use on GitHub**
1. Save the file as `figlet.py`.
2. Commit the file to a repository:
   ```bash
   git init
   git add figlet.py
   git commit -m "Add figlet ASCII art generator"
   git push origin main
   ```
