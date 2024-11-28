# **Project Overview:**

The goal of the project is to **clean** a CSV file that contains student names in a combined format (First Name, Last Name) into two separate columns: **first name** and **last name**. The program reads from an existing CSV file (`before.csv`), processes the data, and writes a cleaned version to a new CSV file (`after.csv`). The program performs several tasks like error handling, file reading, string manipulation, and file writing.

### **Detailed Explanation:**

1. **Problem Breakdown:**
   - **Input File (`before.csv`)**: Contains a column `name` which holds both the first name and last name in a combined format like `"Abbott, Hannah"`.
   - **Output File (`after.csv`)**: Requires the columns `first`, `last`, and `house` where:
     - `first` is the first name (e.g., `Hannah`)
     - `last` is the last name (e.g., `Abbott`)
     - `house` is the Hogwarts house (e.g., `Hufflepuff`).

   Example Input:
   ```
   name,house
   "Abbott, Hannah",Hufflepuff
   "Bell, Katie",Gryffindor
   ```

   Example Output:
   ```
   first,last,house
   Hannah,Abbott,Hufflepuff
   Katie,Bell,Gryffindor
   ```

2. **Steps of the Program:**
   The main task is to:
   - **Read the input CSV file** and process its rows.
   - **Split the `name` column** into first and last names.
   - **Write the processed data** to an output CSV file in the correct format.

3. **Required Libraries:**
   - We will use Python's built-in `csv` module to handle reading and writing CSV files.
   - `sys` is used for command-line argument parsing.

### **Code Walkthrough:**

```python
import csv
import sys

def main():
    # Step 1: Check if exactly two command-line arguments are provided
    if len(sys.argv) != 3:
        sys.exit("Usage: python scourgify.py input_file output_file")

    # Get input and output file names from the command-line arguments
    input_file = sys.argv[1]
    output_file = sys.argv[2]

    try:
        # Step 2: Open the input CSV file in read mode
        with open(input_file, newline='') as infile:
            reader = csv.DictReader(infile)  # Read the CSV file as dictionaries

            # Step 3: Open the output CSV file in write mode
            with open(output_file, mode='w', newline='') as outfile:
                fieldnames = ['first', 'last', 'house']  # Specify the columns for output file
                writer = csv.DictWriter(outfile, fieldnames=fieldnames)

                writer.writeheader()  # Write the header (column names)

                # Step 4: Process each row in the input file
                for row in reader:
                    # Split the full name (last, first) into first and last names
                    full_name = row['name'].split(', ')  # This splits by ", "
                    last_name = full_name[0]
                    first_name = full_name[1]

                    # Step 5: Write the cleaned data to the output file
                    writer.writerow({'first': first_name, 'last': last_name, 'house': row['house']})

    except FileNotFoundError:
        # Step 6: Handle file not found errors
        sys.exit(f"Error: The file {input_file} does not exist.")
    except Exception as e:
        # Catch any other unexpected errors
        sys.exit(f"An error occurred: {e}")

# This line ensures the program runs when executed directly
if __name__ == "__main__":
    main()
```

### **Explanation of the Code:**

#### **1. Command-Line Arguments Parsing:**
```python
if len(sys.argv) != 3:
    sys.exit("Usage: python scourgify.py input_file output_file")
```
- **`sys.argv`** captures command-line arguments.
- We check if exactly two arguments are provided: one for the input file (`before.csv`) and one for the output file (`after.csv`).
- If the number of arguments is incorrect, the program exits with a helpful error message using `sys.exit()`.

#### **2. Opening and Reading the Input CSV File:**
```python
with open(input_file, newline='') as infile:
    reader = csv.DictReader(infile)
```
- We use `open(input_file, newline='')` to open the input file. `newline=''` ensures correct handling of newlines in the CSV file.
- `csv.DictReader(infile)` reads the CSV file as a dictionary where each row is represented as a dictionary with column names as keys.
  - For example, a row like `"Abbott, Hannah",Hufflepuff` will be represented as:
    ```python
    {"name": "Abbott, Hannah", "house": "Hufflepuff"}
    ```

#### **3. Writing to the Output CSV File:**
```python
with open(output_file, mode='w', newline='') as outfile:
    fieldnames = ['first', 'last', 'house']
    writer = csv.DictWriter(outfile, fieldnames=fieldnames)
    writer.writeheader()
```
- We open the output file (`after.csv`) for writing using `open(output_file, mode='w', newline='')`.
- We specify the column names (`fieldnames`) as `['first', 'last', 'house']` since that's the desired structure for the output file.
- `csv.DictWriter(outfile, fieldnames=fieldnames)` creates a `DictWriter` object that will write dictionaries to the output file.
- `writer.writeheader()` writes the header (`first`, `last`, `house`) to the output file.

#### **4. Processing Each Row:**
```python
for row in reader:
    full_name = row['name'].split(', ')  # Split the 'name' column by ", "
    last_name = full_name[0]
    first_name = full_name[1]
    writer.writerow({'first': first_name, 'last': last_name, 'house': row['house']})
```
- The program processes each row in the `reader` object (which is a dictionary).
- It splits the `name` field (e.g., `"Abbott, Hannah"`) using `split(', ')` to separate the last and first names. The result is a list with two items: `["Abbott", "Hannah"]`.
  - `last_name = full_name[0]` and `first_name = full_name[1]` assign the respective parts to `last_name` and `first_name`.
- `writer.writerow()` writes the cleaned data (`first_name`, `last_name`, and `house`) to the output CSV.

#### **5. Error Handling:**
```python
except FileNotFoundError:
    sys.exit(f"Error: The file {input_file} does not exist.")
except Exception as e:
    sys.exit(f"An error occurred: {e}")
```
- **FileNotFoundError**: If the input file does not exist, the program exits with a message indicating that the file was not found.
- **Generic Exception Handling**: Any other unexpected errors are caught and displayed with a relevant message.

#### **6. Running the Program:**
```python
if __name__ == "__main__":
    main()
```
- This line ensures that the `main()` function is executed only when the script is run directly (not imported as a module).

### **How to Run the Program:**

1. Create a folder called `scourgify`.
2. Place your `before.csv` file (provided in the instructions) inside this folder.
3. Create a Python file `scourgify.py` and paste the code above.
4. Open the terminal and navigate to the `scourgify` folder.
5. Run the program with:
   ```bash
   python scourgify.py before.csv after.csv
   ```

   This will read the data from `before.csv`, process it, and save the output to `after.csv`.

### **Expected Output (after.csv):**
```
first,last,house
Hannah,Abbott,Hufflepuff
Katie,Bell,Gryffindor
Susan,Bones,Hufflepuff
Terry,Boot,Ravenclaw
...
```

### **Conclusion:**
The **Scourgify** project demonstrates how to process CSV files in Python using the `csv` module. The program performs tasks such as:
- Reading and writing CSV data.
- Manipulating strings (splitting full names).
- Handling command-line arguments and errors.

By following this approach, you can clean and transform data for better usability in tasks like creating personalized letters, mail merges, or data analysis.


#### **You can copy the code:**
```python
import csv
import sys

def main():
    # Ensure correct number of arguments
    if len(sys.argv) != 3:
        sys.exit("Usage: python scourgify.py input_file output_file")

    input_file = sys.argv[1]
    output_file = sys.argv[2]

    try:
        # Open the input file for reading
        with open(input_file, newline='') as infile:
            reader = csv.DictReader(infile)

            # Prepare to write to the output file
            with open(output_file, mode='w', newline='') as outfile:
                fieldnames = ['first', 'last', 'house']
                writer = csv.DictWriter(outfile, fieldnames=fieldnames)

                # Write header to the output file
                writer.writeheader()

                # Process each row in the input file
                for row in reader:
                    # Split the name into first and last names
                    full_name = row['name'].split(', ')
                    last_name = full_name[0]
                    first_name = full_name[1]

                    # Write the processed row to the output file
                    writer.writerow({'first': first_name, 'last': last_name, 'house': row['house']})

    except FileNotFoundError:
        sys.exit(f"Error: The file {input_file} does not exist.")
    except Exception as e:
        sys.exit(f"An error occurred: {e}")

if __name__ == "__main__":
    main()
```
