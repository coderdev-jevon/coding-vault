# Expense Tracker
Date: 2026-08-01

## Lessons
1. Flask set default folder structure to always put html files inside templates.
2. Always look which one is the direct parent tag to apply CSS style
3. `request` and `requests`, one is for read form data and URL argument and the other one is for web scraping
4. A function should always return something
5. `drop` for data frame doesn't affect the original data so need to assign it `df = df.drop(index=index)`
## * How to Read and Write CSV
```python
import pandas as pd

df = pd.read_csv("file_path")
df.to_csv(FILE_PATH, index=False) #Do not save index column

rows = df.itertuples(index=False)
```

## * Meta Tags HTML
Meta means beyond baseline concept, like higher level view of something
Meta tags in HTML is used as hidden instructions to browsers and search engines.
```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Simple expense tracker">
<meta name="keywords" content="expense tracker, budget, record spending">
<meta name="author" content="Your Name">
<meta https-equiv="refresh" content="5; url=https://example.com">
```

## * HTML Tags
```html
<select name="">
	<option value="" selected></option>
	<option value=""></option>
</select>
```
## *  Connect HTML with CSS
```html
<link rel="stylesheet" href="style.css">
```

## * CSS Methods
```css
display: flex; /* flexible */
flex-direction: row | column /* arrange  */
justify-content: center; /* horizontally center if row, it only works on container space*/
align-items: center; /* vertically center if row*/
height: 100vh; /* vh is viewport height / screen percentage*/
border: 1px solid black;
padding: 5px /* space inside box wall */
margin: 5px /* space outside box wall */
gap: 5px /* create space between child elements */
```

## * Errors
```python
TypeError #Correct data type but type mismatch
ValueError #Type is correct, value is bad
UnicodeDecodeError #Encoding mismatch
pd.errors.ParserError #File format corrupted, messy text
```

## * Rename Key in Dictionary
```python
old_name = "a"
new_name = "b"

dict[new_name] = dict.pop(old_name)
```
#project #css #html #errors