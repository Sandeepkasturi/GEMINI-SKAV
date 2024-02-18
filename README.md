Sure! Below is a detailed line-by-line documentation for your Streamlit application code:

```python
import streamlit as st
import requests
import webbrowser
import pyautogui
from google.generativeai import configure, GenerativeModel
from IPython.display import Markdown
import textwrap
import os
```

1. `import streamlit as st`: Imports the Streamlit library, which is used to create interactive web applications with Python.
2. `import requests`: Imports the Requests library, which is used to make HTTP requests to web servers.
3. `import webbrowser`: Imports the Webbrowser module, which allows opening URLs in the default web browser.
4. `import pyautogui`: Imports the PyAutoGUI library, which provides cross-platform support for automating GUI interactions.
5. `from google.generativeai import configure, GenerativeModel`: Imports the necessary modules from the Google Generative AI library.
6. `from IPython.display import Markdown`: Imports the Markdown class from IPython.display module, used for rendering Markdown text.
7. `import textwrap`: Imports the Textwrap module, which is used to format and wrap plain text.
8. `import os`: Imports the OS module, which provides functions for interacting with the operating system.

```python
# Set up the Generative AI configuration with the API key
configure(api_key='Your_Generative_AI_API_Key')

# Create a Generative Model instance (assuming 'gemini-pro' is a valid model)
model = GenerativeModel('gemini-pro')
```

1. Configures the Generative AI with the API key required for authentication.
2. Creates an instance of the GenerativeModel using the specified model ('gemini-pro').

```python
# Function to convert plain text to Markdown format
def to_markdown(text):
    text = text.replace('•', '  *')
    return Markdown(textwrap.indent(text, '> ', predicate=lambda _: True))
```

Defines a function `to_markdown` that takes plain text as input, replaces bullet points with Markdown format, and returns the Markdown-formatted text.

```python
# Function to download and save HTML code
def download_html_code(html_content):
    try:
        file_name = "extracted_html.html"
        downloads_path = os.path.join(os.path.expanduser("~"), "Downloads")
        file_path = os.path.join(downloads_path, file_name)
        with open(file_path, "w", encoding="utf-8") as f:
            f.write(html_content)
        st.success(f"HTML content saved to {file_path}")
    except Exception as e:
        st.error(f"An error occurred while saving HTML content: {str(e)}")
```

Defines a function `download_html_code` to download and save HTML code to a file named "extracted_html.html" in the user's Downloads directory. It also displays a success message if the operation is successful, otherwise, it shows an error message.

```python
# Function to automatically write content to Notepad
def write_to_notepad(content):
    try:
        file_name = "generated_code.txt"
        downloads_path = os.path.join(os.path.expanduser("~"), "Downloads")
        file_path = os.path.join(downloads_path, file_name)
        with open(file_path, "w", encoding="utf-8") as f:
            f.write(content)
        st.success(f"Content written to Notepad and saved to {file_path}")
    except Exception as e:
        st.error(f"An error occurred while writing to Notepad: {str(e)}")
```

Defines a function `write_to_notepad` to automatically write content to a file named "generated_code.txt" in the user's Downloads directory. It also displays a success message if the operation is successful, otherwise, it shows an error message.

```python
# Function to open URLs in the default web browser
def open_url(url):
    webbrowser.open(url)
```

Defines a function `open_url` to open URLs in the default web browser when called with a valid URL as the argument.

```python
# Main Streamlit application
def main():
    st.title("SKAV TECH")
    st.markdown("Streamlit-powered SKAV TECH AI: Extract HTML, AI Chatbot, Notepad Integration, and More for Enhanced Web Interaction.")
```

Defines the main function `main()` for the Streamlit application. Sets the title of the application to "SKAV TECH" and displays a markdown text describing the application.

Stay tuned for the next part of the documentation!

```python
    # HTML Extraction section
    st.header("Extract HTML Code")
    url = st.text_input("Enter URL:")
    if st.button("Extract HTML Code"):
        try:
            response = requests.get(url)
            if response.status_code == 200:
                download_html_code(response.text)
            else:
                st.error(f"Failed to retrieve HTML content. Status code: {response.status_code}")
        except Exception as e:
            st.error(f"An error occurred: {str(e)}")
```

Creates a header titled "Extract HTML Code" in the Streamlit application. Provides a text input field for the user to enter a URL. If the user clicks the "Extract HTML Code" button, it sends an HTTP GET request to the entered URL. If the request is successful (status code 200), it downloads and saves the HTML content to a file named "extracted_html.html" in the user's Downloads directory. If the request fails, it displays an error message.

```python
    # AI Chatbot section
    st.header("SKAV AI Chatbot")
    question = st.text_input("Ask the model a question:")
    if st.button("Ask SKAV AI"):
        # Call your AI model and get the response
        response = model.generate_content(question)
        st.text("SKAV AI Response:")
        st.write(response.text)

        # Check if the response is related to code writing
        if "write code" in question.lower() or "develop code" in question.lower() or "can you write" in question.lower() or "code" in question.lower():
            write_to_notepad(response.text)

        # Check if the response contains a URL
        if "http" in response.text:
            st.write("The response contains a URL. Do you want to open it?")
            if st.button("Open URL"):
                open_url(response.text)
```

Creates a header titled "SKAV AI Chatbot" in the Streamlit application. Provides a text input field for the user to ask the AI model a question. If the user clicks the "Ask SKAV AI" button, it generates a response using the AI model and displays it in the application. If the response contains keywords related to writing code, it automatically writes the response to a file named "generated_code.txt" in the user's Downloads directory. If the response contains a URL, it prompts the user to open the URL in their default web browser.

```python
        # Additional buttons
        st.markdown('---')
        st.markdown("&copy; 2024 - All rights reserved SKAV TECH.")
        st.subheader('Our recent projects using online templates')
        button_col3, button_col4 = st.columns(2)

        if button_col3.button('DataVerse AI'):
            open_url("https://dataverse-ai.vercel.app/")

        if button_col4.button('Ulink'):
            open_url("https://ulink-io.vercel.app")

if __name__ == "__main__":
    main()
```

Adds additional buttons below the AI Chatbot section. Displays a horizontal line using markdown. Shows a copyright symbol along with the year and the company name. Displays a subheader titled "Our recent projects using online templates". Provides two buttons that, when clicked, open URLs of recent projects in the user's default web browser.

This comprehensive documentation explains each part of the Streamlit application code and its functionalities for enhanced web interaction. Users can easily understand and navigate through the application's features when deployed on GitHub.
