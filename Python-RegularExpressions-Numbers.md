# Explanation of the Project

This project implements a program that validates whether a given string is a valid IPv4 address. An IPv4 address is a 32-bit identifier for devices on a network, represented in dot-decimal notation (e.g., `192.168.0.1`). Each component, called an *octet*, must be an integer between `0` and `255`. The project includes:

1. **Validation Functionality:** A function to determine if a string is a valid IPv4 address.
2. **Unit Testing:** A separate file with tests to verify that the function works as expected.

---

### Deep Dive into the Code

#### File: `numb3rs.py`

This file contains the implementation of the validation functionality.

##### **1. Main Function**

```python
def main():
    print(validate(input("IPv4 Address: ")))
```

- **Purpose:** The `main()` function serves as the entry point of the program.
- **What it Does:**
  - Prompts the user to input an IPv4 address.
  - Calls the `validate()` function with the input and prints the result (`True` or `False`).
- **Example:**
  If the user inputs `192.168.0.1`, it will print `True`. If they input `999.999.999.999`, it will print `False`.

##### **2. Validate Function**

```python
def validate(ip):
    # Regular expression to match a valid IPv4 address format
    pattern = r"^(\d+)\.(\d+)\.(\d+)\.(\d+)$"
    match = re.match(pattern, ip)
    if match:
        # Convert the matched groups to integers and check their range
        octets = [int(group) for group in match.groups()]
        if all(0 <= octet <= 255 for octet in octets):
            return True
    return False
```

- **Purpose:** This function checks if a given string `ip` is a valid IPv4 address.

##### Step-by-Step Explanation:
1. **Regex Pattern:**
   - `r"^(\d+)\.(\d+)\.(\d+)\.(\d+)$"`
     - **`^` and `$`:** Ensure the string starts and ends with the pattern (no extra characters).
     - **`\d+`:** Matches one or more digits.
     - **`\.`:** Matches a literal dot (`.`).
     - **Four Groups:** Captures four sets of digits separated by dots.

   Example Match:
   - Input: `"192.168.0.1"`
   - Captured Groups: `["192", "168", "0", "1"]`

2. **Matching with `re.match`:**
   - If the input string matches the pattern, the groups (digits) are captured.
   - If the input doesn't match, `match` will be `None`.

3. **Converting to Integers:**
   - `octets = [int(group) for group in match.groups()]`
   - Converts the captured groups into integers for range validation.

4. **Range Validation:**
   - `if all(0 <= octet <= 255 for octet in octets):`
   - Ensures that each octet is between `0` and `255`.

5. **Return Value:**
   - Returns `True` if all conditions are satisfied.
   - Returns `False` otherwise.

##### Example:
- Input: `"192.168.0.1"`
  - Matches the pattern.
  - Octets: `[192, 168, 0, 1]`.
  - All octets are within range, so it returns `True`.
- Input: `"275.3.6.28"`
  - Matches the pattern.
  - Octets: `[275, 3, 6, 28]`.
  - The first octet (`275`) is out of range, so it returns `False`.

---

#### File: `test_numb3rs.py`

This file contains unit tests for the `validate()` function.

##### **1. Test for Valid Addresses**

```python
def test_valid_addresses():
    assert validate("127.0.0.1") == True
    assert validate("192.168.0.1") == True
    assert validate("255.255.255.255") == True
    assert validate("0.0.0.0") == True
```

- **Purpose:** Ensure that `validate()` correctly identifies valid IPv4 addresses.
- **Test Cases:**
  - `"127.0.0.1"` is valid.
  - `"192.168.0.1"` is valid.
  - `"255.255.255.255"` (all maximum values) is valid.
  - `"0.0.0.0"` (all minimum values) is valid.

##### **2. Test for Invalid Addresses**

```python
def test_invalid_addresses():
    assert validate("275.3.6.28") == False  # First octet invalid
    assert validate("255.255.255.256") == False  # Last octet invalid
    assert validate("192.168.1.1000") == False  # Octet too large
    assert validate("1.2.3.-1") == False  # Negative number
    assert validate("192.168.1.abc") == False  # Non-numeric
    assert validate("1.2.3.4.5") == False  # Too many octets
    assert validate("192.168") == False  # Too few octets
    assert validate("192.168..1") == False  # Missing octet
    assert validate("cat") == False  # Completely invalid
    assert validate("255") == False  # Only one octet
```

- **Purpose:** Ensure that `validate()` correctly identifies invalid IPv4 addresses.
- **Test Cases:**
  - Addresses with invalid numbers (`275.3.6.28`, `255.255.255.256`).
  - Addresses with too many or too few octets (`1.2.3.4.5`, `192.168`).
  - Addresses with non-numeric or negative values (`192.168.1.abc`, `1.2.3.-1`).
  - Completely invalid strings like `"cat"` or `"255"`.

---

### Testing Process

1. **Manual Testing:**
   - Run `python numb3rs.py` and test inputs like:
     - Valid: `"192.168.0.1"`, `"255.255.255.255"`.
     - Invalid: `"275.3.6.28"`, `"cat"`.

2. **Automated Testing with `pytest`:**
   - Run `pytest test_numb3rs.py` in the terminal.
   - All tests should pass if the function works correctly.

---

### Summary

- **numb3rs.py:** Implements the validation logic using regular expressions and range checks.
- **test_numb3rs.py:** Provides comprehensive tests for valid and invalid inputs to ensure the function's correctness.
- **Purpose of Tests:** Validate edge cases and ensure the function handles all inputs robustly.
