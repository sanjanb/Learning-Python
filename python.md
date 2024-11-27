markdown
# 🎨 FIGlet Learning Journey

This repository documents my progress in learning how to implement and use the `figlet.py` program for rendering ASCII art. Inspired by the FIGlet tool, this project uses the `pyfiglet` Python module to convert text into ASCII art with customizable fonts.

---

## 📚 Learning Goals
1. Understand the purpose of FIGlet and ASCII art rendering.
2. Learn how to use the `pyfiglet` module in Python.
3. Handle command-line arguments effectively with `sys.argv`.
4. Implement error handling for invalid input.
5. Use dynamic font rendering based on user input or random selection.

---

## 🚀 Features of `figlet.py`
- **Random Font Selection**: No arguments? A random font is selected for your text.
- **Custom Font Rendering**: Specify a font with `-f` or `--font` and see your text in style.
- **Error Handling**: Friendly error messages for invalid usage or non-existent fonts.

---

## 🛠️ Tools & Libraries Used
- **Python**: Core programming language.
- **pyfiglet**: Python module for FIGlet ASCII art rendering.
- **sys**: Command-line argument handling.
- **random**: Random font selection for added creativity.

---

## 📝 Progress & Learnings

| Date       | Milestone                                      | Key Takeaways                                                                                                                                 |
|------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| 2024-11-27 | Initialized the project                        | Set up the repository and explored the basics of the `pyfiglet` module. Learned to create a `Figlet` object and retrieve available fonts.   |
| 2024-11-28 | Implemented random font selection              | Used the `random.choice()` function to pick a font dynamically. Ensured compatibility with multiple fonts.                                  |
| 2024-11-29 | Added command-line argument handling           | Learned to use `sys.argv` to parse and validate user inputs for custom font rendering.                                                      |
| 2024-11-30 | Enhanced error handling                        | Added `sys.exit()` for invalid arguments or font names, improving the program's robustness.                                                 |
| 2024-12-01 | Completed user input prompt and ASCII rendering | Integrated `input()` to capture text and `renderText()` for ASCII art generation. Validated the program with multiple test cases.           |

---

## 🎯 Example Outputs

### **Random Font Output**
```bash
$ python figlet.py
Enter text: Hello!
<Random Font ASCII Art>
```

### **Custom Font Output**
```bash
$ python figlet.py -f slant
Enter text: GitHub Rocks!
   ________.__.__  __           ___.                 
  /  _____/|__|__|/  |_  ____   \_ |__   ____  ____  
 /   \  ___|  |  \   __\/ __ \   | __ \_/ __ \/ ___\ 
 \    \_\  \  |  ||  | \  ___/   | \_\ \  ___/\  \___
  \______  /__|__||__|  \___  >  |___  /\___  >\___  >
         \/                \/       \/     \/     \/ 
```

### **Error Message**
```bash
$ python figlet.py -f invalid_font
Invalid usage
```


4. **Explore Fonts**:
   Use the `pyfiglet.getFonts()` method in Python to see all available fonts.

---

## 🔗 Resources
- [FIGlet Official Website](http://www.figlet.org/)
- [pyfiglet Documentation](https://pypi.org/project/pyfiglet/)
- [ASCII Art Examples](http://www.figlet.org/examples.html)

---

## 🖼️ Future Enhancements
- Add a GUI interface for font selection.
- Support more text customization options (e.g., color rendering).
- Save ASCII art to a file.

---

## 📜 License
This project is licensed under the [MIT License](LICENSE).

---

## ❤️ Acknowledgments
- Thanks to [FIGlet](http://www.figlet.org/) for the inspiration!
- Kudos to the creators of `pyfiglet` for making ASCII art fun and accessible.
```

---

### **How to Use This `README.md`**
1. Replace placeholders like `your-username` with your actual GitHub username.
2. Add a `LICENSE` file if necessary (e.g., MIT License).
3. Update the "Progress & Learnings" table as you continue your journey.
4. Push the `README.md` to your repository.

This structure not only documents your learning process but also makes your repository attractive and informative for visitors.
