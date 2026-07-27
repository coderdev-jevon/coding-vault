# Log File Reader
Date: 2026-07-27

```python
from pathlib import Path

def log_reader(file_path: str | Path):
    FILE_PATH = Path(file_path)
    try:
        with FILE_PATH.open('r', encoding='utf-8') as f:
            for line in f:
                stripped_line = line.strip()
                yield(stripped_line)
    except FileNotFoundError:
        print("File is not found")

if __name__ == '__main__':
    logs = log_reader('app.log')
    for entry in logs:
        print(entry)
```
## Lessons
1. No need parentheses on `yield`
2. `ALL_CAPS` is for global constants, inside function use lower case
3. How to apply generators to read logs not but `readlines()`
4. Learn about hint annotations
5. Learn about the use of `if __name__ == '__main__'`
## * Generators (Yield)
```python
def read_log_lines(file_path):
	with open(file_path, 'r', enconding='utf-8') as log_file:
		for line in log_file:
			stripped_line = line.strip()
			yield stripped_line
			# yield sends value out like return then pauses the function
x = read_log_lines(..)
print(next(x)) # resumes the next iteration
print(next(x))
```

## * Hint Annotation
```python
def log_reader(file_path: str | Path):
	..
# : as type hints tell anyone who reads the code that this parameter accept a string or Path object
```

## * Local Use Only
```python
def log_reader():
	....
if __name__ == `__main__`:
	logs = log_reader()

# use this syntax if you want this file only used for testing, personal use only, importing will not trigger the function

from log_reader import log_reader

# if you import it to another file, the __name__ will become the module name "log_reader"

```
#project #generators #hintannotation

