# **Project Explanation: Time Conversion Tool**

This project implements a Python program that converts time ranges from a 12-hour clock format to a 24-hour (military) clock format. The tool ensures strict validation of input formats and raises errors for invalid inputs.

---

### **Detailed Code Breakdown**

#### **1. Overview of Components**
- **Main Functionality**:
  - Accepts a time range in 12-hour format.
  - Converts it to 24-hour format.
  - Ensures inputs are in the correct format and valid.

- **Validation**:
  - Uses a regular expression (regex) to enforce input format rules.
  - Ensures logical time values (e.g., no "13:00 AM" or "8:60 AM").

- **Error Handling**:
  - Raises a `ValueError` for invalid formats or out-of-range time values.

---

#### **2. Code Breakdown**

##### **Imports**

```python
import re
```

- The `re` module is imported for **regular expression matching**, which allows precise format validation.

---

##### **Main Function**

```python
def main():
    print(convert(input("Hours: ")))
```

- **Purpose**: Acts as the entry point of the program.
- **Logic**:
  1. Prompts the user for a time range (e.g., `9:00 AM to 5:00 PM`).
  2. Passes the input to the `convert()` function.
  3. Prints the returned 24-hour formatted time.

---

##### **Convert Function**

```python
def convert(s):
    pattern = r"^(\d{1,2}(?::\d{2})?) (AM|PM) to (\d{1,2}(?::\d{2})?) (AM|PM)$"
    match = re.match(pattern, s)

    if not match:
        raise ValueError

    start_time, start_period, end_time, end_period = match.groups()
    start_24 = to_24_hour(start_time, start_period)
    end_24 = to_24_hour(end_time, end_period)

    return f"{start_24} to {end_24}"
```

- **Purpose**: Validates and converts the input time range to 24-hour format.

- **Steps**:
  1. **Regex Matching**:
     - The regex pattern ensures inputs follow the format: `HH:MM AM to HH:MM PM`.
     - Examples of valid formats:
       - `9:00 AM to 5:00 PM`
       - `12 PM to 12 AM`
     - Examples of invalid formats:
       - `9AM to 5PM` (missing space).
       - `8:60 AM to 4:60 PM` (invalid minute values).

     **Regex Explanation**:
     - `\d{1,2}`: Matches 1-2 digits (hour).
     - `(?::\d{2})?`: Matches optional `:MM` (minute part).
     - `(AM|PM)`: Matches either "AM" or "PM".
     - `to`: Matches the literal "to".
     - `^` and `$`: Ensure the pattern matches the entire input string.

  2. **Error Handling**:
     - If `re.match()` fails, it raises a `ValueError`, indicating invalid format.

  3. **Time Extraction**:
     - `match.groups()` extracts four components:
       - `start_time`, `start_period` (e.g., `9:00`, `AM`).
       - `end_time`, `end_period` (e.g., `5:00`, `PM`).

  4. **Conversion**:
     - Calls `to_24_hour()` to convert both start and end times to 24-hour format.

  5. **Output**:
     - Combines the converted start and end times into a single string (e.g., `09:00 to 17:00`).

---

##### **to_24_hour Function**

```python
def to_24_hour(time, period):
    parts = time.split(":")
    hour = int(parts[0])
    minute = int(parts[1]) if len(parts) > 1 else 0

    if hour < 1 or hour > 12 or minute < 0 or minute > 59:
        raise ValueError

    if period == "AM":
        hour = 0 if hour == 12 else hour
    elif period == "PM":
        hour = 12 if hour == 12 else hour + 12

    return f"{hour:02}:{minute:02}"
```

- **Purpose**: Converts a single 12-hour time string to a 24-hour format.

- **Steps**:
  1. **Splitting and Parsing**:
     - Splits the input time into `hour` and `minute` (e.g., `9:00` → `9`, `00`).
     - Defaults `minute` to `0` if it’s absent (e.g., `9 AM`).

  2. **Validation**:
     - Ensures:
       - `hour` is between 1 and 12.
       - `minute` is between 0 and 59.

  3. **Conversion Logic**:
     - **AM**:
       - Converts `12` to `00` (midnight).
       - Leaves other hours unchanged.
     - **PM**:
       - Converts `12` to `12` (noon).
       - Adds 12 to all other hours (e.g., `3 PM` → `15`).

  4. **Formatting**:
     - Returns the time as a zero-padded string in `HH:MM` format.

---

#### **3. Test Cases**

The `test_working.py` file uses `pytest` to ensure the program behaves as expected.

##### **Valid Input Tests**

```python
def test_valid_inputs():
    assert convert("9:00 AM to 5:00 PM") == "09:00 to 17:00"
    assert convert("10:30 PM to 8:00 AM") == "22:30 to 08:00"
    assert convert("12:00 AM to 12:00 PM") == "00:00 to 12:00"
    assert convert("12 PM to 12 AM") == "12:00 to 00:00"
```

- Verifies that valid inputs produce correct 24-hour conversions.

---

##### **Invalid Input Tests**

```python
def test_invalid_inputs():
    with pytest.raises(ValueError):
        convert("8:60 AM to 4:60 PM")
    with pytest.raises(ValueError):
        convert("9AM to 5PM")
    with pytest.raises(ValueError):
        convert("09:00 to 17:00")
    with pytest.raises(ValueError):
        convert("9 AM - 5 PM")
    with pytest.raises(ValueError):
        convert("10:7 AM - 5:1 PM")
    with pytest.raises(ValueError):
        convert("13:00 AM to 5:00 PM")
```

- Tests edge cases to ensure:
  - Invalid formats or values raise `ValueError`.

---

### **Concepts Used**

1. **Regular Expressions (Regex)**:
   - Validates input format rigorously.

2. **String Manipulation**:
   - Splits and parses time components efficiently.

3. **24-hour Time Conversion**:
   - Handles AM/PM distinctions and edge cases like midnight (`12 AM`) and noon (`12 PM`).

4. **Error Handling**:
   - Uses `ValueError` for input validation failures.

5. **Unit Testing**:
   - Employs `pytest` to automate the testing process.

---

### **How to Run**

1. Run the program:
   ```bash
   python working.py
   ```
   Example input: `9:00 AM to 5:00 PM`

2. Run the tests:
   ```bash
   pytest test_working.py
   ```

---

### **Learning Outcomes**

- Mastered regex for validating user input.
- Built robust time conversion logic.
- Practiced test-driven development (TDD) with `pytest`.
- Gained insights into error handling and defensive programming.
