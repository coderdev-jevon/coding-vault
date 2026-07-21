# Github Workflow Update
Date: 2026-07-21
## Part 1: Daily routine for your Obsidian Notes Repo (`coding-learning-notes`)

This is your documentation vault, only markdown notes.

### Step 1: Terminal steps (3 lines only)

1. Open terminal, enter vault folder

```
cd C:/.../coding-vault
```

2. Stage all new/edited notes

```
git add .
```

3. Save change with clear message (write what you learned today)

```
git commit -m "2026-07-21: Added PyMongo client/db variable notes + bug log 404 flask"
```

4. Upload to GitHub cloud

```
git push
```

### How to make this fast daily habit

After every coding session (5 mins):

1. Write your markdown learning note
2. Run those 4 git commands above to sync GitHub immediately

- Commit message rule: `date: short summary of new content`

## Part 2: For your code projects (flask/mongodb/pandas inside coding-projects)

Each project is its own separate GitHub repository.

### When to push project code

- **Every time you add a working new feature** (not every tiny line)
    
    Example triggers to push:
- Added MongoDB save function to your Flask app
- Fixed 404 URL bug
- Wrote full pymongo connection script

Project git command example (enter project folder first):
```
cd C:/.../coding-projects/text-analyzer-flask
git add .
git commit -m "Add mongodb insert one logic to save text analysis"
git push
```

## Part 3: Two modes to keep GitHub always updated

### Mode A: Light daily push (recommended for you, low effort)

Every day after coding:

1. Push Obsidian vault notes (short commit of today’s learning doc)
2. If you finished a working feature in your Flask project → push project repo too
    
    If you only read notes without writing new content: skip project push, just push vault.

### Mode B: Auto-sync trick (optional, no manual git typing)

1. Install Git GUI app like GitKraken / SourceTree
2. Link your vault and all project repos
3. The app shows all changed files visually, one click commit + push
    
    Great if you hate typing terminal commands every day.

## Part 4: Common mistakes to avoid

1. Do NOT push `coding-projects` folder inside your notes vault repo
    
    Notes repo only contains markdown learning docs, raw code lives separate repos.
2. Write clear commit messages, don’t just write `update files`
    
    Good: `2026-07-21: Explained client/db pymongo variable`
    
    Bad: `update note`
3. If you delete a note in Obsidian trash, git add . will remove it from GitHub too (auto sync delete)
4. Never push sensitive data inside code (MongoDB connection string with raw password)
    
    Hide secrets with environment variables before pushing project code.

## Part 5: Minimal daily checklist you can follow

- [ ]  Finish coding practice session
- [ ]  Write markdown note of what you learned today
- [ ]  Open terminal, push coding-vault to GitHub notes repo
- [ ]  If new working feature added to Flask/Pandas project → push project repo
- [ ]  End day