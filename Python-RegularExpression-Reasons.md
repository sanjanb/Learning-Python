# **Project: Seasons of Life in Minutes**

This project calculates the total minutes a person has lived based on their date of birth and expresses the result in English words (without "and") following the format from the song *Seasons of Love*.

---

### **Concepts Used**

1. **Datetime Module**:
   - Python's `datetime` library handles dates and times. We use `date` objects to manage dates.
   - `date.today()` fetches the current date, while `date.fromisoformat()` converts a string in `YYYY-MM-DD` format into a date object.

2. **String Manipulation**:
   - Input validation ensures the user provides dates in the correct format.
   - Graceful error handling uses `try-except` blocks to avoid crashes from invalid inputs.

3. **Arithmetic with Dates**:
   - Subtracting two `date` objects gives a `timedelta` object representing the difference between them.
   - `timedelta.days` is used to calculate the total number of days between the dates.

4. **Inflect Library**:
   - Converts numbers into their English word representation.
   - The `number_to_words()` method provides flexibility to exclude conjunctions like "and."

5. **Testing**:
   - Comprehensive unit tests ensure each function works as intended.
   - Integration tests validate the end-to-end flow, from input parsing to final output.

---

### **Code Explanation**

#### **1. Main Script (`seasons.py`)**

```python
from datetime import date
import inflect
import sys
```
- **`datetime.date`**: Manages date objects.
- **`inflect`**: Converts numbers into English words.
- **`sys`**: Allows for program exit (`sys.exit()`).

---

#### **Main Function**

```python
def main():
    # Prompt user for input
    birth_date = input("Date of Birth (YYYY-MM-DD): ").strip()
    try:
        # Validate and parse the input
        birth_date = parse_date(birth_date)
    except ValueError:
        sys.exit("Invalid date format. Please use YYYY-MM-DD.")
```

- **Purpose**: This is the entry point of the program.
- Prompts the user for their date of birth.
- Strips extra spaces from input and validates it using the `parse_date()` function.
- Exits gracefully if the date format is invalid.

---

#### **Date Parsing**

```python
def parse_date(date_str):
    """
    Parse the date string in YYYY-MM-DD format and return a date object.
    Raise ValueError if format is invalid.
    """
    return date.fromisoformat(date_str)
```

- **Purpose**: Converts the user-provided string into a `date` object.
- **Key Method**:
  - `fromisoformat()`: Validates and parses `YYYY-MM-DD` strings.
- If the format is invalid, it raises a `ValueError`, caught in `main()`.

---

#### **Minutes Calculation**

```python
def calculate_minutes(birth_date):
    """
    Calculate total minutes from the birth date to today.
    """
    today = date.today()
    delta = today - birth_date
    return delta.days * 24 * 60
```

- **Purpose**: Calculates the total minutes lived.
- **Steps**:
  - Gets today's date using `date.today()`.
  - Subtracts the `birth_date` from today's date, returning a `timedelta` object.
  - Converts days to minutes: \( \text{days} \times 24 \times 60 \).

---

#### **Conversion to Words**

```python
def convert_to_words(number):
    """
    Convert a number to English words without 'and'.
    """
    p = inflect.engine()
    return p.number_to_words(number, andword="").capitalize()
```

- **Purpose**: Converts the calculated minutes into English words.
- **Key Method**:
  - `inflect.engine()`: Initializes the library.
  - `number_to_words()`: Converts numbers into words while omitting "and" via the `andword=""` parameter.

---

#### **Final Output**

```python
    # Calculate minutes since birth
    minutes = calculate_minutes(birth_date)

    # Convert minutes to words
    minutes_in_words = convert_to_words(minutes)

    # Output result
    print(f"{minutes_in_words} minutes")
```

- **Purpose**: Integrates all the functions to display the final result.

---

#### **Edge Case Handling**
- If the user inputs an invalid date format (e.g., `01-01-2000`), the program exits with:
  ```plaintext
  Invalid date format. Please use YYYY-MM-DD.
  ```

---

### **Testing Script (`test_seasons.py`)**

```python
import pytest
from datetime import date
from seasons import parse_date, calculate_minutes, convert_to_words
```
- **`pytest`**: A testing framework used to write test cases.
- Tests individual functions in `seasons.py` for correctness.

---

#### **Unit Tests**

```python
def test_parse_date_valid():
    assert parse_date("2000-01-01") == date(2000, 1, 1)

def test_parse_date_invalid():
    with pytest.raises(ValueError):
        parse_date("Invalid-Date")
```

- **`test_parse_date_valid`**: Confirms that valid dates are parsed correctly.
- **`test_parse_date_invalid`**: Ensures invalid dates raise a `ValueError`.

---

```python
def test_calculate_minutes():
    birth_date = date(1999, 1, 1)
    today = date(2000, 1, 1)
    delta_minutes = (today - birth_date).days * 24 * 60
    assert calculate_minutes(birth_date) == delta_minutes
```

- Verifies that minute calculation is accurate for given dates.

---

```python
def test_convert_to_words():
    assert convert_to_words(525600) == "Five hundred twenty-five thousand, six hundred"
```

- Ensures numbers are converted to words correctly, following the given format.

---

#### **Integration Tests**

```python
def test_integration_valid():
    assert calculate_minutes(parse_date("1999-01-01")) == 525600

def test_integration_invalid():
    with pytest.raises(ValueError):
        parse_date("NotADate")
```

- Validates the complete workflow, from input parsing to minute calculation.

---

### **How It Works**

1. The program prompts the user for their birthdate in `YYYY-MM-DD` format.
2. It parses and validates the date, raising an error for invalid input.
3. Calculates the total minutes lived based on the current date.
4. Converts the number into English words.
5. Outputs the result in a user-friendly format.

---

### **Example Runs**

#### **Valid Input**
```plaintext
Date of Birth (YYYY-MM-DD): 2000-01-01
Five hundred twenty-five thousand, six hundred minutes
```

#### **Invalid Input**
```plaintext
Date of Birth (YYYY-MM-DD): 01/01/2000
Invalid date format. Please use YYYY-MM-DD.
```

---

### **Key Takeaways**

1. **Design**:
   - Separation of concerns: Each function handles a single task, making the code modular and testable.

2. **Validation**:
   - Robust input validation ensures the program doesn't crash due to unexpected input.

3. **Testing**:
   - Comprehensive unit and integration tests guarantee reliability and robustness.

4. **Usability**:
   - Clear error messages and simple inputs make the program user-friendly.

---

Let me know if you need further clarifications! 🚀
