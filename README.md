## **README.md**

---

# Bulk File Rename Tool

This repository contains methods for bulk renaming files in a folder using Excel and Batch Files . These tools are designed to help you efficiently manage and organize your files by appending numeric sequences to filenames.

## **Table of Contents**

- [Features](#features)
- [Usage](#usage)
  - [Method 1: Using Excel and Batch Files](#method-1-using-excel-and-batch-files)
  - [Method 2: Using PowerShell](#method-2-using-powershell)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## **Features**

- **Excel Integration**: Utilize Excel formulas to generate new filenames and rename commands.
- **Batch File Support**: Execute batch scripts to automate the renaming process.
- **PowerShell Scripts**: Use PowerShell for a more flexible and powerful renaming solution.
- **User-Friendly**: Step-by-step instructions suitable for users with varying levels of technical expertise.

## **Usage**

### **Method 1: Using Excel and Batch Files**

This method involves using Excel to generate a list of rename commands and executing them via a batch file.

#### **Step 1: Retrieve File Names**

1. **Open the Target Folder**:
   - Navigate to the folder containing the files you wish to rename using File Explorer.

2. **Copy File Names**:
   - Press `Ctrl + A` to select all files.
   - Hold the `Shift` key, right-click, and select "**Copy as path**".
     - *Note: If "Copy as path" is not available, refer to [Alternative Method](#alternative-method) below.*

#### **Step 2: Edit File Names in Excel**

1. **Open Excel**:
   - Create a new Excel workbook.

2. **Paste File Names**:
   - Paste the copied file paths into Column A.

3. **Add Sequential Numbers**:
   - In Column B, enter sequential numbers starting from `1`.
   - Format the numbers to three digits using the `TEXT` function (e.g., `001`, `002`).

4. **Generate New File Names**:
   - In Column C, use the following formula to append the number to the original filename:
     ```excel
     =LEFT(A2, FIND(".", A2) - 1) & TEXT(B2, "000") & MID(A2, FIND(".", A2), LEN(A2))
     ```
   - This formula extracts the base filename, appends a three-digit number, and retains the original file extension.

5. **Create Rename Commands**:
   - In Column D, generate the rename commands using the following formula:
     ```excel
     ="rename """ & A2 & """ """ & C2 & """"
     ```
   - This creates commands in the format:
     ```
     rename "original_filename.ext" "new_filename001.ext"
     ```

#### **Step 3: Execute the Batch File**

1. **Copy Rename Commands**:
   - Select all the commands in Column D and copy them.

2. **Create a Batch File**:
   - Open Notepad or any text editor.
   - Paste the copied commands.
   - Save the file with a `.bat` extension (e.g., `rename_files.bat`) in the target folder.

3. **Run the Batch File**:
   - Double-click the batch file to execute the rename commands.
   - A Command Prompt window will appear, processing each rename command.

*For detailed steps, refer to the [Reddit Answer](https://www.reddit.com/r/Windows11/comments/1g81hk9/rename_files_in_folder_as_filenamenumeric/).*

*Ensure you have backed up your files before runni