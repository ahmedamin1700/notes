---
id: a5c348ac-5917-4e29-98fa-2136b8237dbe
aliases:
  - python-core-file-io-cli-tools
tags: []
---

# python-core-file-io-cli-tools

## 1. Virtual Environments (The Foundation)
Before writing code, always create an isolated environment. This prevents library conflicts between projects.

### How to use:
```bash
# Linux
python3 -m venv venv
source venv/bin/activate
```

## 2. Modern File Paths: pathlib
Old Python tutorials use `os.path.join`. Modern Python (3.6+) uses `pathlib`. It treats paths as objects, not strings.

Why it's better:
It is cross-platform (handles Windows \ vs Linux / automatically) and more readable.

Examples:
```Python
from pathlib import Path

# Get current directory
current_dir = Path.cwd()

# Create a path to a file (doesn't create the file yet)
target_file = current_dir / "data" / "report.txt" 

# Check if exists
if target_file.exists():
    print("File is there!")

# Get file parts
print(target_file.suffix)  # .txt
print(target_file.stem)    # report
print(target_file.parent)  # .../data

# Iterate over a folder
folder = Path("downloads")
for item in folder.iterdir():
    if item.is_file():
        print(f"Found file: {item.name}")
```

## 3. Moving Files: shutil
`pathlib` finds files, `shutil` moves or copies them.

```Python
import shutil
from pathlib import Path

source = Path("downloads/image.jpg")
destination_folder = Path("pictures")

# Create folder if it doesn't exist
destination_folder.mkdir(exist_ok=True) 

# Move the file
shutil.move(str(source), str(destination_folder / source.name))
```

## 4. Command Line Arguments: argparse
To make your script professional, you shouldn't hardcode paths. Pass them when running the script (e.g., `python main.py /users/me/downloads`).

```Python
import argparse

def main():
    parser = argparse.ArgumentParser(description="Organize files in a folder.")
    
    # Positional argument (required)
    parser.add_argument("path", type=str, help="The path to organize")
    
    # Flag argument (optional, True/False)
    parser.add_argument("--dry-run", action="store_true", help="Simulate without moving files")

    args = parser.parse_args()

    print(f"Organizing: {args.path}")
    if args.dry_run:
        print("DRY RUN MODE: No files will be moved.")

if __name__ == "__main__":
    main()
```

## 5. Logging (Better than print)
`print()` is for the user. logging is for the developer (you) to see what happened later.

```Python
import logging

# Basic setup
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

logging.info("Script started.")
try:
    result = 10 / 0
except ZeroDivisionError:
    logging.error("Failed to calculate math.")
```

### 6. Project Structure
For this week, organize your files like this:

```Text
folder_organizer/
│
├── main.py            # The entry point (argparse logic)
├── utils.py           # Functions (scanning, moving files)
├── tests/
│   └── test_utils.py  # Basic tests
├── README.md          # How to use it
└── .gitignore         # Ignore venv/ and __pycache__/
```