# Robot Framework Beginner Practical

## Introduction

This practical will guide you through setting up and writing your first automated test using Robot Framework in Visual Studio Code. Robot Framework is a keyword-driven test automation framework that makes it easy to write tests in a human-readable format.

**What You'll Learn:**
- How to install Robot Framework and required tools
- How to set up Visual Studio Code for Robot Framework
- How to write your first basic test
- How to run tests and view results

**Prerequisites:**
- Windows operating system
- No prior programming or testing experience required

---

## Part 1: Installation and Setup

### Step 1: Install Python

Robot Framework requires Python to run.

1. Open your web browser and go to: https://www.python.org/downloads/
2. Click the **Download Python** button (should be version 3.10 or above)
3. Run the installer
4. **IMPORTANT:** Check the box that says **"Add Python to PATH"** before clicking Install
5. Click **Install Now**
6. Wait for installation to complete

**Verify Installation:**
1. Press `Windows Key + R`
2. Type `cmd` and press Enter
3. In the command prompt, type:
   ```
   python --version
   ```
4. You should see something like `Python 3.12.x`

### Step 2: Install Robot Framework

1. Open Command Prompt (if not already open)
2. Type the following command and press Enter:
   ```
   pip install robotframework
   ```
3. Wait for installation to complete

**Verify Installation:**
```
robot --version
```
You should see the Robot Framework version displayed.

### Step 3: Install SeleniumLibrary

SeleniumLibrary allows Robot Framework to automate web browsers.

In Command Prompt, type:
```
pip install robotframework-seleniumlibrary
```

### Step 4: Install Visual Studio Code

1. Go to: https://code.visualstudio.com/
2. Click **Download for Windows**
3. Run the installer with default settings
4. Launch Visual Studio Code

### Step 5: Install RobotCode Extension

1. In Visual Studio Code, click the **Extensions** icon on the left sidebar (or press `Ctrl + Shift + X`)
2. In the search bar, type: **RobotCode**
3. Click on **RobotCode - Robot Framework Support** by d-biehl
4. Click **Install**
5. Wait for installation to complete (this may also install Python extensions automatically)

---

## Part 2: Create Your First Project

### Step 1: Create a Project Folder

1. Create a new folder on your computer called `robot_practice`
   - You can create it on your Desktop or in Documents
2. In Visual Studio Code:
   - Click **File** → **Open Folder**
   - Navigate to and select the `robot_practice` folder
   - Click **Select Folder**

### Step 2: Create a Tests Folder

1. In VS Code, right-click in the Explorer pane (left side)
2. Select **New Folder**
3. Name it: `tests`

### Step 3: Create Your First Test File

1. Right-click on the `tests` folder
2. Select **New File**
3. Name it: `first_test.robot`
   - **Important:** The file must end with `.robot`

---

## Part 3: Write Your First Test

### Test 1: Simple Log Test

Let's start with a very basic test that just logs a message. Copy this code into your `first_test.robot` file:

```robotframework
*** Settings ***
Documentation    My first Robot Framework test

*** Test Cases ***
My First Test
    Log    Hello, Robot Framework!
    Log    This is my first automated test
```

**Understanding the Code:**
- `*** Settings ***` - Section for configuration and documentation
- `*** Test Cases ***` - Section where we write our tests
- `My First Test` - The name of our test case
- `Log` - A keyword that prints messages
- The text after `Log` is what will be printed

**Save the file** (Ctrl + S)

---

## Part 4: Run Your First Test

### Running from VS Code

1. Right-click anywhere in the `first_test.robot` file
2. Select **Robot Framework: Run Test**
3. Watch the output in the Terminal at the bottom

**Alternative Method:**
1. Open Terminal in VS Code (`Ctrl + ~` or Terminal → New Terminal)
2. Type:
   ```
   robot tests/first_test.robot
   ```

### View the Results

After the test runs, you'll see:
- Console output showing the test passed
- Three new files created in your project folder:
  - `log.html` - Detailed execution log
  - `report.html` - Summary report
  - `output.xml` - Raw data file

**To view the report:**
1. Right-click on `report.html` in VS Code
2. Select **Reveal in File Explorer**
3. Double-click the file to open in your browser

---

## Part 5: Working with Variables

Let's create a test that uses variables.

Create a new file: `tests/variables_test.robot`

```robotframework
*** Settings ***
Documentation    Learning to use variables

*** Variables ***
${NAME}          John Doe
${AGE}           25
${CITY}          Singapore

*** Test Cases ***
Display User Information
    Log    Name: ${NAME}
    Log    Age: ${AGE}
    Log    City: ${CITY}
    
Calculate Next Year Age
    ${next_year_age}=    Evaluate    ${AGE} + 1
    Log    Next year you will be ${next_year_age} years old
```

**Understanding the Code:**
- `*** Variables ***` - Section for defining reusable values
- `${NAME}` - A variable (must be in `${...}` format)
- `${next_year_age}=` - Creating a new variable during test execution
- `Evaluate` - Keyword that performs calculations

**Run this test** using the same methods as before.

---

## Part 6: Create Custom Keywords

Custom keywords let you reuse steps across multiple tests.

Create a new file: `tests/keywords_test.robot`

```robotframework
*** Settings ***
Documentation    Learning to create custom keywords

*** Keywords ***
Greet User
    [Arguments]    ${username}
    Log    Hello, ${username}!
    Log    Welcome to Robot Framework

Calculate Sum
    [Arguments]    ${num1}    ${num2}
    ${result}=    Evaluate    ${num1} + ${num2}
    Log    ${num1} + ${num2} = ${result}
    [Return]    ${result}

*** Test Cases ***
Test Greeting
    Greet User    Alice
    Greet User    Bob

Test Calculator
    ${total}=    Calculate Sum    10    20
    Log    The total is ${total}
    Should Be Equal As Numbers    ${total}    30
```

**Understanding the Code:**
- `*** Keywords ***` - Section for custom reusable keywords
- `[Arguments]` - Defines inputs the keyword accepts
- `[Return]` - Sends a value back to the caller
- `Should Be Equal As Numbers` - Validates that values match

---

## Part 7: Web Testing Example

Now let's create a simple web test. This will open a browser and navigate to a website.

Create a new file: `tests/web_test.robot`

```robotframework
*** Settings ***
Documentation    Basic web testing example
Library          SeleniumLibrary

*** Variables ***
${URL}           https://www.google.com
${BROWSER}       Chrome

*** Test Cases ***
Open Google Homepage
    Open Browser    ${URL}    ${BROWSER}
    Maximize Browser Window
    ${title}=    Get Title
    Log    Page title is: ${title}
    Sleep    2s
    Close Browser

Search Test (Basic)
    Open Browser    ${URL}    ${BROWSER}
    Maximize Browser Window
    Sleep    1s
    Close Browser
```

**Understanding the Code:**
- `Library    SeleniumLibrary` - Imports web testing capabilities
- `Open Browser` - Opens a web browser
- `Get Title` - Gets the page title
- `Sleep` - Waits for specified time
- `Close Browser` - Closes the browser

**Run this test** - You'll see Chrome browser open automatically!

---

## Part 8: Understanding Test Results

After running tests, examine the generated files:

### report.html
- Shows overall test statistics
- Lists all tests with Pass/Fail status
- Shows execution time

### log.html
- Detailed step-by-step execution
- Shows all Log messages
- Click on test names to expand details
- Shows screenshots (for web tests)

### Reading the Console Output
```
==============================================================================
Tests.First Test                                                              
==============================================================================
My First Test                                                         | PASS |
------------------------------------------------------------------------------
Tests.First Test                                                      | PASS |
1 test, 1 passed, 0 failed
```

---

## Part 9: Common Issues and Solutions

### Issue 1: "robot is not recognized"
**Solution:** Python is not in PATH. Reinstall Python with "Add Python to PATH" checked.

### Issue 2: "No module named 'SeleniumLibrary'"
**Solution:** Run: `pip install robotframework-seleniumlibrary`

### Issue 3: Browser doesn't open
**Solution:** SeleniumLibrary 4+ manages browser drivers automatically. If issues persist, update:
```
pip install --upgrade robotframework-seleniumlibrary
```

### Issue 4: Red underlines in VS Code
**Solution:** 
1. Press `Ctrl + Shift + P`
2. Type: `Python: Select Interpreter`
3. Choose your Python installation

---

## Quick Reference

### Robot Framework Structure
```robotframework
*** Settings ***
# Imports and configuration

*** Variables ***
# Define reusable values

*** Test Cases ***
# Your actual tests

*** Keywords ***
# Custom reusable actions
```

### Common Keywords
- `Log` - Display messages
- `Should Be Equal` - Compare values
- `Should Contain` - Check if text contains substring
- `Sleep` - Wait for specified time
- `Set Variable` - Create a variable
- `Evaluate` - Perform calculations

### SeleniumLibrary Keywords
- `Open Browser` - Open web browser
- `Close Browser` - Close browser
- `Click Element` - Click on web element
- `Input Text` - Type into text field
- `Get Title` - Get page title
- `Maximize Browser Window` - Maximize window

---

## Next Steps

Congratulations! You've completed the Robot Framework beginner practical. Here's what you can explore next:

1. **Learn more keywords**: Check the Robot Framework documentation
2. **Web element locators**: Learn to find elements by ID, Name, XPath
3. **Data-driven testing**: Run same test with different data
4. **Test libraries**: Explore DatabaseLibrary, RequestsLibrary, etc.

### Useful Resources
- Official Documentation: https://robotframework.org/
- SeleniumLibrary Docs: https://robotframework.org/SeleniumLibrary/
- Robot Framework User Guide: https://robotframework.org/robotframework/

---

## Summary

In this practical, you learned:
- ✅ How to install Python, Robot Framework, and VS Code
- ✅ How to set up the RobotCode extension
- ✅ How to create and structure Robot Framework test files
- ✅ How to use variables in tests
- ✅ How to create custom keywords
- ✅ How to write basic web tests with SeleniumLibrary
- ✅ How to run tests and interpret results

Keep practicing and experimenting with different keywords and test scenarios!
