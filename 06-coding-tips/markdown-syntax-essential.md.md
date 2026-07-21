# Markdown Syntax Essential
Date: 2026-07-21
## ==Headings==
```
# Main Topic (File Title) 
## Subheading 1 
### Subheading 2 
#### Subheading 3
```
## ==Code Blocks==

### Single line inline code (variable/function names)

`` `MongoClient` ``

Result: `MongoClient`

### Multi-line code block (full scripts, wrap with triple backticks + language name)

```python
from pymongo import MongoClient

MONGODB_URL = "your-link-here"
client = MongoClient(MONGODB_URL)
db = client.thirty_days_of_python
```

Supported languages: `python`, `html`, `bash`, `sql`

## ==Bold / Italic for emphasis==

```
**Critical step: save your database password!**
*SRV connection string requires dnspython installed*
```

**Critical step: save your database password!**

_SRV connection string requires dnspython installed_

## ==Lists (bullet / number for steps)==

### Unordered bullet list

```
- Install pymongo[srv]
- Copy SRV connection URL
- Replace <password> placeholder
```

### Numbered step list

```
1. Open MongoDB Atlas Connect page
2. Copy auto-generated password
3. Click Create Database User
```

## ==Task checklist (great for review plans / to-learn list)==

markdown

```
- [x] Understand client variable
- [ ] Practice inserting multiple records
- [ ] Build /history route to fetch DB data
```

- [x]  = completed
- [ ]  = pending

## ==Blockquote (important warnings, key takeaways)==

markdown

```
> Do NOT set debug=True on public deployed websites (security risk)
```

> Do NOT set debug=True on public deployed websites (security risk)

## ==Internal Links (Obsidian only, jump between notes)==

Link another note file `mongodb-db-variable.md`:

markdown

```
[[mongodb-db-variable]]
```

Perfect for connecting related concepts (Flask routes ↔ PyMongo save logic)

## ==Tags (Obsidian filter system, organize topics)==

Put at bottom of every note for easy search:

```
#python #mongodb #pymongo #database
```

## ==Table (compare concepts, bug logs)==


```
| Term | Simple Meaning |
|------|----------------|
| Client | Python’s connection to MongoDB server |
| DB | Single database inside your cluster |
| Collection | "Table" to store your analysis data |
```

## ==Divider line (split big sections)==

```
---
```

#markdown 