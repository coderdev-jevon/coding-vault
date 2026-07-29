# Password Manager
Date: 2026-07-29
## Lessons
1. You can use `except` twice

## * Password Related Introduction
```
1. Hash: same input always gives exactly same string, one-way
2. Master password and master hash, to unlock whole password manager
3. Credential: one set of login info for one website/app
	website: "github" 
	username: "john123@gmail.com" 
	password: "GithubPass789!"
4. Salt: add extra string to password before hashing, every user get different salt
```
## * Create Password Hash
```python
def create_password_hash(pw):
    bytes_data = pw.encode('utf-8')
    hash_result = hashlib.sha256(bytes_data).hexdigest()
    return hash_result
```
## * Handle Errors
```python
PermissionError #Cannot write file/folder
OSError #Disk full, weird system issues, parent for PermissionError and FileNotFoundError, general
json.JSONDecodeError
RuntimeError #Program state or context is wrong, argument is okay
```

#project 