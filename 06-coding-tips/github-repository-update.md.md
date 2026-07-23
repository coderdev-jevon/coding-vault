# GitHub Repository
Date: 21-07-26

## * Step by Step for First Upload
1. Create repository on GitHub (Uncheck Add README and .gititgnore)
2. Open your folder by VS Code
3. Open terminal and type
```
git init #1

git remote add origin https://github.com/YOUR_USERNAME/coding-projects.git #2

git add . #3

git commit -m "Initial upload: 30days-python-flask-api project" #4

git branch -M main #5

git push -u origin main #6
```

#### ** If Remote Origin Already Exists
```
# 1

git remote remove origin

git remote add origin https://github.com/YOUR_USERNAME/coding-vault.git

git remote -v #checking

# 2
Remove-Item -Recurse -Force .git

ls -Hidden #checking

git init git remote add origin 
https://github.com/YOUR_USERNAME/coding-vault.git

```

#### ** Using Master as Initial Branch Warning
```
# 1
git branch -M main

# 2
git config --global init.defaultBranch main

```

## * Step by Step for Updating