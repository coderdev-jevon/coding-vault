# Notes Project
Date: 2026-07-30
## Lessons
1. Define `constants` at the top, repetitions are not clean
2. Always consider when to use GET and POST, use POST if you perform edit or delete, because it is more safe this way
3. Multiple layers of protection are better
## * Scan Folders
3 Methods
```python
#1
import os
folder = 'notes'
items = os.listdir(folder)
folders_list = []
files_list = []
# Cons: you don't know which is folder, which is file

for item in items:
	full_path = os.path.join(folder, name)
	if os.path.isdir(full_path):
		folders_list.append(item)
	elif os.path.isfile(full_path):
		files_list.append(item)
		
#2
with os.scandir(folder) as entries:
	for entry in entries:
		if entry.is_dir():
			folders_list.append(entry.name)
		elif entry.is_file() and entry.name.endswith(".md"):
			files_list.append(entry.name)
```

## OS Functionality
```python
# JOINING PATH
os.path.join(folder, name) #do the task but zero security
os.path.abspath(os.path.join()) # returns full absolute path from the root of the disk, resolve ., ..

__file__ #is special python variable, holds path to current .py script

os.sep #is OS directory separator character

os.path.commonpath([A, B]) # Find the common URL path betweent those two, use this to prevent transverse attack
```

## * Errors Regarding Files and Folders
```python
FileNotFoundError # file/folder doesn't exist
PermissionError # No permission
IsADirectoryError # Open a directory as a file
UnicodeDecodeError # Trying to read non-UTF8 file
OSError # Generic OS error
FilExistsError # File already exists
```
## * Prevent Attacks
#### ** HTML and md attack
```python
import bleach
import markdown

raw_html = markdown.markdown(md_text, extensions=["extra"]) 
# extension extra is used for tables, pictures
safe_html = bleach.clean(raw_html) # prevent any html tags
```

## * Additional
```python
return Response(body, status_code) # HTTP response body is sent to browser
```
#project #errors