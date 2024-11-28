# **Project Overview**
The goal of this project is to create a Python program that reads data from a CSV file of pizza prices, processes that data, and displays it in a well-formatted table using ASCII art. The table will be created using the `tabulate` library, which is a Python package that allows you to print tables in various formats, such as plain text, grid format, and more.

The CSV file will contain data about Sicilian pizza prices, with columns for different pizza types and sizes (small, large). Our program should:
1. Accept a CSV file as input.
2. Validate that the file exists and is a CSV file.
3. Read the contents of the CSV file.
4. Format the data into a table.
5. Display the table in a grid format using ASCII art.

If any issues arise (e.g., incorrect file type or missing arguments), the program should exit with an error.

---

### **Steps to Solve the Problem**

1. **Accept a command-line argument**: The program will accept a CSV file path via a command-line argument. We will use the `sys.argv` list to get the file path from the command line.

2. **Validate the file**: The program should check:
   - If exactly one argument is provided (besides the script name).
   - If the file path ends with `.csv`.
   - If the file exists.

3. **Read the CSV file**: We will use the `csv` module to read the CSV file. The `csv.reader` or `csv.DictReader` method can be used to load the file data into a structure.

4. **Format the table**: Using the `tabulate` library, we'll format the CSV data into a readable table in grid format.

5. **Error Handling**: If any validation checks fail (e.g., file not found, wrong file extension), the program should exit using `sys.exit()`.

---

### **Code Implementation**
Here's the code implementation for this project.

```python
import sys
import csv
from tabulate import tabulate

def main():
    # Ensure exactly one command-line argument is passed
    if len(sys.argv) != 2:
        print("Usage: python pizza.py <CSV file>")
        sys.exit(1)

    # Get the file path from the argument
    filename = sys.argv[1]

    # Validate if the file has a .csv extension
    if not filename.endswith(".csv"):
        print("File must be a CSV file.")
        sys.exit(1)

    # Try to open the file and read it
    try:
        with open(filename, newline='') as file:
            reader = csv.reader(file)
            
            # Read the CSV file into a list of rows
            data = list(reader)

            # Check if the CSV file is empty
            if len(data) == 0:
                print("CSV file is empty.")
                sys.exit(1)
            
            # Format the data into a table using tabulate library
            table = tabulate(data, headers='firstrow', tablefmt='grid')
            print(table)

    except FileNotFoundError:
        print(f"File '{filename}' not found.")
        sys.exit(1)
    except Exception as e:
        print(f"An error occurred: {e}")
        sys.exit(1)

if __name__ == "__main__":
    main()
```

---

### **Detailed Explanation of the Code**

#### 1. **Importing Modules**

```python
import sys
import csv
from tabulate import tabulate
```
- **`sys`**: This module is used to access command-line arguments (`sys.argv`), and to exit the program with `sys.exit()` in case of errors.
- **`csv`**: The CSV module provides functionality to read from and write to CSV files. Here, we use it to read the data from the provided CSV file.
- **`tabulate`**: This package is used to format and print the data as a table in a user-friendly manner.

#### 2. **Main Function Logic**

```python
def main():
    if len(sys.argv) != 2:
        print("Usage: python pizza.py <CSV file>")
        sys.exit(1)
```
- The program expects exactly one argument (besides the script name). If the number of arguments is not correct, it will display a usage message and exit.

#### 3. **File Validation**

```python
filename = sys.argv[1]
if not filename.endswith(".csv"):
    print("File must be a CSV file.")
    sys.exit(1)
```
- **Get the filename**: The filename is retrieved from the command-line arguments (`sys.argv[1]`).
- **Check for `.csv` extension**: It validates that the file has a `.csv` extension. If it doesn't, the program prints an error message and exits.

#### 4. **Opening the File and Reading the CSV Data**

```python
try:
    with open(filename, newline='') as file:
        reader = csv.reader(file)
        data = list(reader)
```
- **Open the file**: The program tries to open the CSV file with the `open()` function. If the file is not found, it will raise a `FileNotFoundError`.
- **Read the data**: The `csv.reader()` function is used to read the CSV file line by line. It returns an iterable object that we convert into a list (`data`), which contains the rows of the CSV file.

#### 5. **Error Handling**

```python
except FileNotFoundError:
    print(f"File '{filename}' not found.")
    sys.exit(1)
except Exception as e:
    print(f"An error occurred: {e}")
    sys.exit(1)
```
- **FileNotFoundError**: If the file is not found, a custom error message is printed, and the program exits.
- **General Exception Handling**: Any other errors (e.g., invalid CSV format) will be caught by a general exception handler, which prints the error message and exits.

#### 6. **Formatting the Table**

```python
table = tabulate(data, headers='firstrow', tablefmt='grid')
print(table)
```
- **Using `tabulate`**: The `tabulate()` function is used to format the `data` into a table. The `headers='firstrow'` option tells `tabulate` to treat the first row as headers for the table.
- **`tablefmt='grid'`**: This specifies the format in which the table should be printed (in this case, a grid-style ASCII table).

#### 7. **Exit on Success**

If everything runs successfully, the formatted table is printed to the console.

---

### **Example Execution**

#### 1. **Valid Input**

Let’s assume you have the following `sicilian.csv` file:

```csv
Sicilian Pizza,Small,Large
Cheese,$25.50,$39.95
1 item,$27.50,$41.95
2 items,$29.50,$43.95
3 items,$31.50,$45.95
Special,$33.50,$47.95
```

Running the program with the command:

```bash
python pizza.py sicilian.csv
```

Output:

```plaintext
+------------------+---------+---------+
| Sicilian Pizza   | Small   | Large   |
+==================+=========+=========+
| Cheese           | $25.50  | $39.95  |
+------------------+---------+---------+
| 1 item           | $27.50  | $41.95  |
+------------------+---------+---------+
| 2 items          | $29.50  | $43.95  |
+------------------+---------+---------+
| 3 items          | $31.50  | $45.95  |
+------------------+---------+---------+
| Special          | $33.50  | $47.95  |
+------------------+---------+---------+
```

#### 2. **Invalid Input (No CSV File)**

```bash
python pizza.py
```

Output:

```plaintext
Usage: python pizza.py <CSV file>
```

#### 3. **Invalid Input (File Not Found)**

```bash
python pizza.py non_existent_file.csv
```

Output:

```plaintext
File 'non_existent_file.csv' not found.
```

---

### **Conclusion**

This program allows you to easily convert pizza menu data from a CSV file into a well-formatted ASCII art table. It uses the `csv` module to read CSV files, handles errors gracefully, and formats the data into a grid-style table using the `tabulate` library. The program is designed to be user-friendly, with clear error messages and input validation.

By following this approach, you learn about file handling, reading CSV files, and formatting data in Python, along with error handling and using third-party libraries like `tabulate`.

You can copy this code:

```python
import sys
import csv
from tabulate import tabulate

def main():
    # Check if exactly one command-line argument is provided
    if len(sys.argv) != 2:
        sys.exit("Usage: python pizza.py <filename>")

    # Get the filename from the command-line argument
    file_name = sys.argv[1]

    # Check if the file ends with '.csv'
    if not file_name.endswith('.csv'):
        sys.exit("Usage: The file must have a '.csv' extension")

    # Try to open and read the CSV file
    try:
        with open(file_name, mode='r', newline='', encoding='utf-8') as file:
            reader = csv.DictReader(file)  # Read the CSV file as a dictionary
            data = list(reader)  # Convert to list of dictionaries
    except FileNotFoundError:
        sys.exit(f"Error: The file '{file_name}' does not exist.")
    except Exception as e:
        sys.exit(f"Error: {e}")

    # Format the table using the tabulate library
    print(tabulate(data, headers="keys", tablefmt="grid"))

if __name__ == "__main__":
    main()

```
