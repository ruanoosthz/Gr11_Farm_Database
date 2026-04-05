# Database For Speculation Farming

## Table of Contents

## Problem Analysis
- [1A – Problem and Solution Description](#task-1a---problem-and-solution-description)
- [1B – User Story and Acceptance Test](#task-1b--user-story-and-acceptance-test)

## Data Dictionary
- [Variables and Components](#variables-and-components)
- [Text File](#text-file)
- [Arrays](#arrays)
- [User-defined Methods](#user-defined-methods)

## Database Design
- [Table 1 – Calf General Details](#1st-table)
- [Table 2 – Calf Health Conditions](#2nd-table)

## Screen Navigation (GUI Design)
- [Navigation Overview](#task-4---screen-navigation-gui-design)

## Input, Processing, Output (IPO)
- [Input – Screens 1 & 2](#input--screens-1--2)
- [Input – Screen 1](#input--screen-1)
- [Processing – Screens 1 & 2](#processing--screens-1--2)
- [Processing – Screen 1](#processing--screen-1)
- [Output – Screen 1 & 2](#output--screen-1--2)

## GUI Description
- [Database Sheet (Tab 2)](#database-sheet-tab-2)
- [Welcome Screen Sheet (Tab 1)](#welcome-screen-sheet-tab-1)
- [Display Sheet (Tab 3)](#display-sheet-tab-3)

---

# Problem and Solution Description

A cattle farm owner struggles to keep all his calf data centralised and wants to keep records of his calves' healthcare. He also wants to know what his approximate expenses will be after he has treated and vaccinated all the calves.

This program will enable him to store all the important cattle data in one place and will allow him to easily monitor the weight and health of the calves. The program allows the administrator to easily remove cattle from the database if they have been sold, and to add data for newly purchased cattle. The calves' weight can also be calculated at the current moment (date entered by user), and the feed costs will be added automatically.

The program will remove all excess/unnecessary data and only store the data essential for business purposes, such as the calf's code, its gender, weight, and the calf's health problems, if any.

---

# User Story and Acceptance Test

| | User 1 | User 2 |
|---|--------|--------|
| **User Role** | I am the owner of a cattle farm | I am a cattle farm administrator |
| **User Goal** | I want easy access to current calves' information | I want to keep all the calves' information centralised |
| **Why it is needed** | So that I can easily see what my expenses for the current period will be. | So that I can easily update and retrieve records to make administration simpler. |
| **Program Limitations** | The exact expenses to be incurred are not 100% accurate because unexpected price changes can occur. | The data must be read manually, and a scanner cannot be used to read the data. |

## Acceptance Test

- The GUI design allows for easy access to data.
- The GUI allows for simple navigation to different data.
- All the calves' data will be centralised in the relevant database table.
- Records can be easily updated or retrieved.
- A warning message will be displayed to ensure data is not deleted accidentally.
- Reading in the data will be convenient, easy, and fast.

---

# Data Dictionary

## Variables and Components

- Tables will be used to display all the information in the database.
- Buttons will be used to perform different actions (e.g., navigating between tabs).
- Variables will be correctly named with a short prefix referring to the data type (e.g., `sString` for String, `rReal` for Real).
- Global variables will allow values to be used throughout the program (e.g., an `iCount` variable to count data in an array and store the number).

## Text File

- Stores the different types of medicine and how many units are available.
- *More can be added.*

## Arrays

- An array will retrieve data from the text file containing stored vaccines and treatments.
- The data in the array can then be used to treat calves or to display the contents of the text file.

## User-defined Methods

- Code is used to restore the database to its original data.
- Example:  
  `conSpekulasie.Execute('DROP TABLE tblKalwers');`

---

# Database Design

## 1st Table – Calf General Details

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| Cattle ID | Text | Identifies different cattle |
| Date of Birth | DateTime | Used to determine age |
| Gender | Text | Calf's gender |
| Breed of cattle | Text | Calf's breed |
| Weight when purchased | Integer | Purchase weight to determine growth |
| Current weight of calf | Integer | Used to determine expenses |
| Location where cattle is present | Text | Used to locate cattle |

## 2nd Table – Calf Health Conditions

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| ID | Text | Identifies different cattle |
| Health Issues | Text | Health problems the calf has experienced |
| Is the problem treated? | Text | Whether the health issue has been handled |
| Date the problem was treated | DateTime | When the treatment took place |

### Record Management

- Records can be added by pressing a button and entering information into input boxes.
- Records can be deleted by selecting a record and pressing the correct button.
- When health problems are treated, the condition in the table will change automatically.
- Fields can be navigated using the correct arrow buttons.

---

# Screen Navigation (GUI Design)

<img width="695" height="341" alt="image" src="https://github.com/user-attachments/assets/33a513ad-0888-41c8-89c7-e52a8098ff4d" />


---

# Input, Processing, Output

## Input – Screens 1 & 2

| Input | Source | Data Type | Format | GUI Component | Validation |
|-------|--------|-----------|--------|----------------|-------------|
| iID | Keyboard | Integer | Long Integer | edtSearch | Scans database for specific record. If not found, an error message appears (mtError). |

## Input – Screen 1

| Input | Source | Data Type | Format | GUI Component | Validation |
|-------|--------|-----------|--------|----------------|-------------|
| iID | dbeID.text | Integer | Long Integer | dbeCattleID | Only health records of the entered ID appear. No error because selected record shows automatically. |
| sHealthProblem | Database | String | General Text | tblCondition | If no treatment is available for the health issue, an error message appears (mtError). |
| sQuantity | Keyboard | Integer | Short Integer | btnAdd | If entered 'Vaccine quantity available' is not an integer, an error message appears (mtError). |

## Processing – Screens 1 & 2

| Processing Task | Method |
|----------------|--------|
| Search database for specific calf and all its data | `while NOT Table1.EOF do`<br>`      If Table1['CattleID'] = sSearch then`<br>`         //Filter Health Table`<br>`         Break;`<br>`      Table1.Next;` |

## Processing – Screen 1

| Processing Task | Method |
|----------------|--------|
| Filter table to show only selected calf's health records | `iID := StrToInt(dbeID.Text);`<br>`tblHealth.Filter := 'CattleID = ' + IntToStr(iID);`<br>`tblHealth.Filtered := True;` |
| Create new record when calf is purchased | `Table1.Insert;`<br>`Table1.Edit;`<br>`Table1['DateOfBirth'] = InputBox('Date of Birth', 'Enter Cattle Date of Birth', '');`<br>`Table1.Post;` |
| Change 'False' to 'True' after health problem treated | `Table1.Edit`<br>`Table1['Treated'] := True;`<br>`Table1.Post` |

## Output – Screens 1 & 2

| Screen | Data | Format | GUI Component |
|--------|------|--------|----------------|
| Screen 1 | Calf's health records | Database record format | TDBGrid |
| Screen 2 | Available vaccine | Treatment Name – Quantity available | TRichEdit |

---

# GUI Description

## Database Sheet (Tab 2)
<img width="1014" height="629" alt="image" src="https://github.com/user-attachments/assets/437a6f37-c8cd-4247-a36b-349df893e593" />


## Welcome Screen Sheet (Tab 1)
<img width="882" height="492" alt="image" src="https://github.com/user-attachments/assets/ef5bd18d-2032-40e6-9db9-69998d29465e" />

## Display Screen (Tab 3)
<img width="879" height="520" alt="image" src="https://github.com/user-attachments/assets/c6de13f8-b383-4237-8b3d-27acb40bce3b" />
