# **Project Overview**:

In this project, we are tasked with creating a personalized PDF certificate (referred to as a "Shirtificate") using an image (`shirtificate.png`) as the background and overlaying the user's name onto the image. The output will be a `shirtificate.pdf` file that contains the user's name placed at a specific position over the background image.

### **Key Requirements**:
1. **Prompt the user for input**: The user will input their name.
2. **Overlay the name on a background image**: The background image (`shirtificate.png`) will be used as the base of the certificate, and the user’s name will be placed on top.
3. **Output a PDF file**: The result will be saved as a PDF (`shirtificate.pdf`).
4. **Use the `fpdf2` library**: This is the library we’ll use to handle PDF creation.

### **Concepts Involved**:
1. **PDF Generation**: Creating PDFs programmatically involves using libraries that allow you to set text, images, fonts, and their positions on a page. In this project, we'll use the `fpdf2` library.
   
2. **Class Inheritance**: We extend the `FPDF` class from `fpdf2` to create a custom class (`PDF`) that allows us to modify the header and footer for every page of the PDF.

3. **Handling Images in PDFs**: The image (in this case, `shirtificate.png`) is placed as a background, and we overlay text on top of it.

4. **User Input**: We take the user’s name as input and customize the certificate by placing the name at a specific position on the PDF.

### **Code Breakdown**:

Here is the code implementation for the project, followed by a detailed explanation:

```python
from fpdf import FPDF

# Custom class to add header and footer to every page of the PDF
class PDF(FPDF):
    def header(self):
        # Add a header (optional, you can skip this)
        self.set_font('Arial', 'B', 12)
        self.cell(0, 10, 'Shirtificate Certificate', 0, 1, 'C')

    def footer(self):
        # Add a footer with the page number
        self.set_y(-15)
        self.set_font('Arial', 'I', 8)
        self.cell(0, 10, f'Page {self.page_no()}', 0, 0, 'C')

# Create PDF instance
pdf = PDF()

# Add a page
pdf.add_page()

# Set the image as the background
pdf.image('shirtificate.png', x = 0, y = 0, w = 210, h = 297)  # A4 size

# Prompt for the user's name
name = input("Enter your name: ")

# Set the font for the text (overlay)
pdf.set_font('Arial', 'B', 36)

# Set text color
pdf.set_text_color(255, 255, 255)  # White color

# Position the text on the page
pdf.set_xy(50, 150)  # Adjust the (x, y) values to place text over the image
pdf.cell(0, 40, name, 0, 1, 'C')

# Output the PDF to a file
pdf.output('shirtificate.pdf')

print("Your Shirtificate has been created as shirtificate.pdf!")
```

### **Detailed Explanation of the Code**:

1. **Importing the `FPDF` Class**:
   ```python
   from fpdf import FPDF
   ```
   - The `FPDF` class from the `fpdf2` library is used to generate PDFs. This class provides methods to add pages, set fonts, position text, and more.

2. **Custom `PDF` Class**:
   ```python
   class PDF(FPDF):
       def header(self):
           self.set_font('Arial', 'B', 12)
           self.cell(0, 10, 'Shirtificate Certificate', 0, 1, 'C')

       def footer(self):
           self.set_y(-15)
           self.set_font('Arial', 'I', 8)
           self.cell(0, 10, f'Page {self.page_no()}', 0, 0, 'C')
   ```
   - We extend the `FPDF` class to create a custom `PDF` class. This allows us to customize the header and footer of every page.
   - **`header` method**: This method adds a title at the top of each page. In this case, we use the text "Shirtificate Certificate".
   - **`footer` method**: This method adds a page number at the bottom of each page. We use `self.page_no()` to get the current page number.

3. **Creating the PDF Instance**:
   ```python
   pdf = PDF()
   pdf.add_page()
   ```
   - We instantiate an object of the `PDF` class and call `add_page()` to add a new page to the PDF. Each PDF file starts with one or more pages, and the `add_page()` method ensures we have a blank page on which to place the image and text.

4. **Adding the Image as Background**:
   ```python
   pdf.image('shirtificate.png', x = 0, y = 0, w = 210, h = 297)
   ```
   - The `image()` method is used to add the `shirtificate.png` image as the background of the certificate. We set the image’s `x` and `y` coordinates to `(0, 0)` to position it at the top-left corner of the page, and set the width (`w`) and height (`h`) to the A4 size (210mm by 297mm).

5. **Prompting for User Input**:
   ```python
   name = input("Enter your name: ")
   ```
   - We use the `input()` function to prompt the user to enter their name. This input will be used to personalize the certificate.

6. **Setting the Font for the Name**:
   ```python
   pdf.set_font('Arial', 'B', 36)
   pdf.set_text_color(255, 255, 255)  # White color
   ```
   - We set the font to **Arial**, **bold** (`'B'`), and a size of `36` to make the name prominent.
   - We also set the text color to white using `set_text_color(255, 255, 255)` to ensure the name stands out against the image background.

7. **Positioning the Text**:
   ```python
   pdf.set_xy(50, 150)
   pdf.cell(0, 40, name, 0, 1, 'C')
   ```
   - `set_xy(50, 150)` positions the text at coordinates (50mm, 150mm) on the page.
   - `cell(0, 40, name, 0, 1, 'C')` creates a cell (box) of width `0` (which means auto-width), height `40mm`, with the user’s name centered (`'C'`).

8. **Outputting the PDF**:
   ```python
   pdf.output('shirtificate.pdf')
   print("Your Shirtificate has been created as shirtificate.pdf!")
   ```
   - The `output()` method generates the PDF and saves it as `shirtificate.pdf`.
   - The message "Your Shirtificate has been created..." is printed to the console to confirm the process.

### **How to Run the Program**:

1. **Setup**:
   - First, ensure you have the `shirtificate.png` image in the same directory as the script.
   - Run the program using:
     ```bash
     python shirtificate.py
     ```

2. **Test**:
   - Enter your name when prompted. The program will generate a PDF (`shirtificate.pdf`) containing the name overlaid on the background image.

3. **Output**:
   - Open the generated `shirtificate.pdf` to check if the name appears as expected over the background.

### **Concepts Used**:
1. **Inheritance**: By extending the `FPDF` class, we created a customized version of the `FPDF` that allowed us to add custom headers and footers to every page.
2. **PDF Text and Image Handling**: We utilized the `image()` and `cell()` methods to handle positioning and rendering of images and text in the PDF.
3. **User Input**: We used Python’s built-in `input()` function to take user input, which is then inserted into the PDF.

### **Testing**:
- Test with different names to ensure the text overlays correctly.
- Try with different images to see how the certificate handles various backgrounds.
