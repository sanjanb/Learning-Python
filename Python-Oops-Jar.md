# **jar.py**: Implementation of the `Jar` class

#### **Class Design**
1. **Attributes**:
   - `capacity`: Maximum number of cookies the jar can hold.
   - `_size`: Number of cookies currently in the jar (private attribute).

2. **Methods**:
   - `__init__`: Initializes the jar with a default capacity of 12 unless specified.
   - `__str__`: Converts the current state of the jar into a string of 🍪 emojis.
   - `deposit`: Adds a specified number of cookies, ensuring the total doesn’t exceed the capacity.
   - `withdraw`: Removes a specified number of cookies, ensuring the jar has enough cookies for withdrawal.
   - `capacity` (property): Returns the jar’s maximum capacity.
   - `size` (property): Returns the current number of cookies in the jar.

```python
class Jar:
    def __init__(self, capacity=12):
        if not isinstance(capacity, int) or capacity < 0:
            raise ValueError("Capacity must be a non-negative integer")
        self._capacity = capacity
        self._size = 0

    def __str__(self):
        return "🍪" * self._size

    def deposit(self, n):
        if n < 0 or self._size + n > self._capacity:
            raise ValueError("Cannot deposit beyond capacity")
        self._size += n

    def withdraw(self, n):
        if n < 0 or self._size < n:
            raise ValueError("Cannot withdraw more than current size")
        self._size -= n

    @property
    def capacity(self):
        return self._capacity

    @property
    def size(self):
        return self._size
```

---

### **test_jar.py**: Testing the `Jar` class

#### **Test Cases**
1. **Initialization (`test_init`)**:
   - Ensure `Jar` initializes correctly with valid capacities.
   - Ensure `Jar` raises a `ValueError` for invalid capacities.

2. **String Representation (`test_str`)**:
   - Ensure the string representation matches the number of cookies deposited.

3. **Deposit (`test_deposit`)**:
   - Ensure valid deposits update the jar correctly.
   - Ensure deposits beyond capacity raise a `ValueError`.

4. **Withdraw (`test_withdraw`)**:
   - Ensure valid withdrawals update the jar correctly.
   - Ensure withdrawals exceeding the number of cookies raise a `ValueError`.

```python
import pytest
from jar import Jar

def test_init():
    jar = Jar()
    assert jar.capacity == 12
    assert jar.size == 0
    with pytest.raises(ValueError):
        Jar(-1)
    with pytest.raises(ValueError):
        Jar("abc")

def test_str():
    jar = Jar()
    assert str(jar) == ""
    jar.deposit(3)
    assert str(jar) == "🍪🍪🍪"
    jar.deposit(2)
    assert str(jar) == "🍪🍪🍪🍪🍪"

def test_deposit():
    jar = Jar()
    jar.deposit(5)
    assert jar.size == 5
    with pytest.raises(ValueError):
        jar.deposit(10)  # Exceeds capacity
    with pytest.raises(ValueError):
        jar.deposit(-3)  # Negative deposit

def test_withdraw():
    jar = Jar()
    jar.deposit(7)
    jar.withdraw(3)
    assert jar.size == 4
    with pytest.raises(ValueError):
        jar.withdraw(5)  # More than current size
    with pytest.raises(ValueError):
        jar.withdraw(-1)  # Negative withdrawal
```

---

### **Explanation of the Code**
1. **Validation in `__init__`**:
   - Ensures the capacity is a non-negative integer.
   - Raises a `ValueError` for invalid inputs.

2. **String Representation**:
   - Repeats the emoji 🍪 based on the number of cookies in the jar (`_size`).

3. **Deposit Logic**:
   - Checks if the addition exceeds capacity.
   - Raises an error for negative deposits or if the total exceeds `_capacity`.

4. **Withdraw Logic**:
   - Checks if the withdrawal exceeds the current size.
   - Raises an error for negative withdrawals or if the amount to withdraw is greater than `_size`.

5. **Testing**:
   - Validates expected behavior for normal operations.
   - Ensures edge cases (e.g., exceeding capacity or invalid input) are handled gracefully.

---

### **Running Tests**
1. Save `jar.py` and `test_jar.py` in the same folder.
2. Run tests using `pytest`:
   ```bash
   pytest test_jar.py
   ```
3. Confirm all tests pass with green checks.

---

This project demonstrates object-oriented programming concepts like encapsulation, properties, and error handling in Python while reinforcing the importance of thorough testing. Let me know if you have any questions! 😊
