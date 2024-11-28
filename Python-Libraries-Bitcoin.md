# **📜 The Mission of the Program**

This Python program is like a treasure calculator 🪙. It does the following:
1. **Takes a number** (how many Bitcoins you want to buy) from you as a command-line argument.
2. **Fetches the current Bitcoin price** using an online service (CoinDesk API).
3. **Calculates the total cost** of buying those Bitcoins in USD.
4. **Displays the cost beautifully formatted** to four decimal places with commas as thousands separators.

---

### **🚶 Walkthrough of the Program**

Let’s break it down step by step:

---

#### **1. Importing Libraries**
```python
import requests
import sys
```

- **`requests`**: This library lets you fetch data from the internet, like sending a bird 🦅 to an API and bringing back information.
- **`sys`**: This module helps with system-level tasks, like handling command-line arguments or exiting the program.

---

#### **2. Main Function**
```python
def main():
    if len(sys.argv) != 2:
        sys.exit("Usage: python bitcoin.py <number_of_bitcoins>")
```

- The program expects **one argument**: the number of Bitcoins you want to buy.  
  Example:  
  ```bash
  python bitcoin.py 2
  ```
- **What happens here**:
  - If you forget to pass an argument or pass too many, the program exits with an error message:  
    `"Usage: python bitcoin.py <number_of_bitcoins>"`

---

#### **3. Validating User Input**
```python
    try:
        bitcoins = float(sys.argv[1])
    except ValueError:
        sys.exit("Error: The number of Bitcoins must be a numeric value.")
```

- **Why this step**:
  - The program tries to convert your input (e.g., "2") into a `float`.  
    Bitcoins can be fractional, like `0.25 Bitcoins`.
  - If you pass something invalid, like `"pirate"`, Python will raise a `ValueError`, and the program will exit with:  
    `"Error: The number of Bitcoins must be a numeric value."`

---

#### **4. Fetching Bitcoin Price**
```python
    try:
        response = requests.get("https://api.coindesk.com/v1/bpi/currentprice.json")
        response.raise_for_status()  # Checks for HTTP request errors
        price = response.json()["bpi"]["USD"]["rate_float"]
    except requests.RequestException:
        sys.exit("Error: Unable to fetch Bitcoin price.")
    except (KeyError, ValueError):
        sys.exit("Error: Unexpected data format from the API.")
```

- **What’s happening here**:
  1. **Send a request** to the CoinDesk API to get the latest Bitcoin price.
  2. **Handle potential issues**:
     - If the request fails (e.g., no internet), Python raises an exception, and the program exits with:
       `"Error: Unable to fetch Bitcoin price."`
     - If the API response is malformed or doesn’t contain the expected keys, the program exits with:
       `"Error: Unexpected data format from the API."`

- **API Response Example**:
  ```json
  {
    "bpi": {
      "USD": {
        "rate_float": 38761.0833
      }
    }
  }
  ```

- The price is extracted from the JSON response:  
  `price = 38761.0833`

---

#### **5. Calculating Total Cost**
```python
    cost = bitcoins * price
    print(f"${cost:,.4f}")
```

- **What’s happening here**:
  - Multiply the number of Bitcoins (`bitcoins`) by the current price (`price`).
  - Format the result to look pretty:
    - **`,`:** Adds commas for thousands separators.
    - **`.4f`:** Displays exactly four decimal places.
  - Example:
    ```plaintext
    $77,522.1666
    ```

---

### **🧪 Example Run**

**Command**:
```bash
python bitcoin.py 2
```

**Steps**:
1. Input validation:
   - `sys.argv[1]` is `"2"` → Converted to `float`: `2.0`.
2. Fetch Bitcoin price:
   - API response gives `price = 38761.0833`.
3. Calculate cost:
   - `cost = 2.0 * 38761.0833 = 77522.1666`.
4. Print result:
   ```plaintext
   $77,522.1666
   ```

---

### **💡 Key Concepts Explained**

1. **Command-Line Arguments**:
   - Use `sys.argv` to get inputs directly from the command line.
   - Validate input to ensure it's numeric and meaningful.

2. **Making HTTP Requests**:
   - Use `requests.get()` to fetch data from the internet.
   - Handle exceptions like connection errors gracefully.

3. **JSON Parsing**:
   - Use `response.json()` to decode API responses.
   - Extract values from nested JSON objects.

4. **String Formatting**:
   - Use `f"{value:,.4f}"` to format numbers elegantly for display.

---

### **🚩 The Fun Takeaway**

Imagine this program as your **personal Bitcoin broker**:
- You tell it how many Bitcoins you want.
- It talks to a global price oracle to get real-time data.
- It calculates the cost and gives you a crystal-clear price tag.


#### **You can copy this Code**
```python
   import sys
import requests


def main():
    # Validate and retrieve the number of Bitcoins from the command-line argument
    bitcoins = get_bitcoins()

    # Fetch the current price of Bitcoin in USD
    price = fetch_bitcoin_price()

    # Calculate the total cost
    cost = bitcoins * price

    # Output the cost formatted to four decimal places with thousands separators
    print(f"${cost:,.4f}")


def get_bitcoins():
    """
    Retrieves the number of Bitcoins from the command-line argument.

    Returns:
        float: The number of Bitcoins to buy.

    Exits:
        If the argument cannot be converted to a float or is missing.
    """
    if len(sys.argv) != 2:
        sys.exit("Usage: python bitcoin.py <number_of_bitcoins>")

    try:
        return float(sys.argv[1])
    except ValueError:
        sys.exit("Error: The number of Bitcoins must be a numeric value.")


def fetch_bitcoin_price():
    """
    Fetches the current price of Bitcoin in USD from the CoinDesk API.

    Returns:
        float: The current price of Bitcoin in USD.

    Raises:
        Exits the program with an error message if the API request fails.
    """
    try:
        response = requests.get("https://api.coindesk.com/v1/bpi/currentprice.json")
        response.raise_for_status()  # Raise an exception for HTTP errors
        data = response.json()
        return data["bpi"]["USD"]["rate_float"]
    except requests.RequestException:
        sys.exit("Error: Unable to fetch Bitcoin price.")
    except KeyError:
        sys.exit("Error: Unexpected data format from the API.")


if __name__ == "__main__":
    main()

```


