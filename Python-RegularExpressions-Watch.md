# **Overview of the Problem**

Websites often embed YouTube videos using `iframe` HTML elements, where the `src` attribute contains the video's URL in formats like:

- `https://www.youtube.com/embed/VIDEO_ID`
- `http://youtube.com/embed/VIDEO_ID`

These URLs allow videos to be played directly on the website. However, if someone wants to share the video directly on YouTube, they would need the shorter, shareable format:

- `https://youtu.be/VIDEO_ID`

The task is to write a Python program that:
1. Detects these embedded YouTube URLs in an HTML string.
2. Extracts the video ID (e.g., `VIDEO_ID`).
3. Converts the URL into its shorter `youtu.be` equivalent.
4. Returns `None` if the HTML string contains no valid YouTube video embed.

---

### **How the Program Works**
The program:
1. Prompts the user to input an HTML string.
2. Searches for an embedded YouTube video URL in the string using a **regular expression**.
3. Extracts the `VIDEO_ID` from the URL if a match is found.
4. Constructs and outputs the shorter `youtu.be` URL or `None` if no match is found.

---

### **Step-by-Step Breakdown of the Code**

#### **Code Implementation**

```python
import re
import sys

def main():
    print(parse(input("HTML: ")))

def parse(s):
    # Regular expression to match YouTube iframe src
    pattern = r'src="https?://(?:www\.)?youtube\.com/embed/([^"]+)"'
    
    # Search for the pattern in the input string
    match = re.search(pattern, s)
    
    if match:
        # Extract the video ID (the first captured group)
        video_id = match.group(1)
        # Return the shorter YouTube URL
        return f"https://youtu.be/{video_id}"
    return None

if __name__ == "__main__":
    main()
```

---

### **1. Modules Used**
- **`import re`:** The `re` module allows us to use **regular expressions** to search for specific patterns in the input HTML string.
- **`import sys`:** Enables interaction with the system, such as handling input and output. While not extensively used in this project, it's often included in command-line utilities.

---

### **2. Main Functionality**

#### **`main()`**
1. **Prompts the user for input:**
   ```python
   input("HTML: ")
   ```
   The user provides an HTML string containing (or not containing) an `iframe`.

2. **Calls the `parse()` function:**
   Passes the HTML string to `parse()` to extract and process the embedded YouTube URL.

3. **Prints the output:**
   If a YouTube URL is found, the shorter URL is displayed. Otherwise, `None` is printed.

---

#### **`parse(s)`**

This function performs the core task of the project: detecting and processing YouTube URLs in the HTML.

1. **Regular Expression Pattern**
   ```python
   pattern = r'src="https?://(?:www\.)?youtube\.com/embed/([^"]+)"'
   ```
   - **`src="`:** Matches the opening of the `src` attribute in an `iframe`.
   - **`https?://`:** Matches URLs starting with `http://` or `https://`.
   - **`(?:www\.)?`:** Matches `www.` optionally. The `?:` indicates a **non-capturing group**.
   - **`youtube\.com/embed/`:** Matches the domain `youtube.com` and the `/embed/` path where video IDs are present.
   - **`([^"]+)`:** Captures everything after `/embed/` up to the next double quote (`"`). This is the **video ID**.

   Example:
   Input: `<iframe src="https://www.youtube.com/embed/xvFZjo5PgG0"></iframe>`
   Match: `src="https://www.youtube.com/embed/xvFZjo5PgG0"`
   Captured Group: `xvFZjo5PgG0`

2. **Search for Matches**
   ```python
   match = re.search(pattern, s)
   ```
   - `re.search()` scans the input string for the first occurrence of the pattern.
   - Returns a **match object** if the pattern is found, otherwise `None`.

3. **Extract Video ID**
   ```python
   if match:
       video_id = match.group(1)
   ```
   - `match.group(1)` retrieves the first captured group in the regular expression, which is the `VIDEO_ID`.

4. **Construct Shorter URL**
   ```python
   return f"https://youtu.be/{video_id}"
   ```
   - Formats the shorter, shareable URL using the extracted `VIDEO_ID`.

5. **Return `None` if No Match**
   ```python
   return None
   ```
   - If no valid YouTube URL is found, the function returns `None`.

---

### **3. Testing the Program**

#### **Sample Inputs and Outputs**

1. **Valid YouTube Embed**
   - Input: `<iframe src="https://www.youtube.com/embed/xvFZjo5PgG0"></iframe>`
   - Output: `https://youtu.be/xvFZjo5PgG0`

2. **Valid Embed with Extra Attributes**
   - Input:
     ```html
     <iframe width="560" height="315" src="https://www.youtube.com/embed/xvFZjo5PgG0" title="YouTube video player"></iframe>
     ```
   - Output: `https://youtu.be/xvFZjo5PgG0`

3. **Non-YouTube URL**
   - Input: `<iframe src="https://cs50.harvard.edu/python"></iframe>`
   - Output: `None`

4. **No `iframe` Tag**
   - Input: `<p>No iframe here!</p>`
   - Output: `None`

---

### **How the Program Works**
1. **User Input:**
   - The program asks the user to enter an HTML string containing an `iframe`.

2. **Pattern Matching:**
   - The program searches for a `src` attribute in the format of YouTube embed URLs.

3. **URL Extraction:**
   - If a YouTube embed URL is found, the video ID is extracted from it.

4. **URL Conversion:**
   - The extracted video ID is used to construct a shorter `youtu.be` URL.

5. **Output:**
   - The shorter URL or `None` is displayed.

---

### **Future Enhancements**
- **Support Multiple URLs:** Modify the program to find and process multiple YouTube URLs in one HTML string.
- **Error Handling:** Provide user-friendly messages for invalid inputs.
- **HTML Parsing:** Use an HTML parser (e.g., `BeautifulSoup`) for more complex HTML structures.
