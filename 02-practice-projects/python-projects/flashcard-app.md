# Flashcard App
Date: 2026-08-02




## Lessons
1. Shorter key name is better for a lightweight database.
2. `indent=2` is enough to save space
3. The purpose of using id to uniquely identify each items, id need not to be continuous.
4. JSON does not support `datetime` objects
5. All data transferred via HTML form is transferred as plain string
6. List reference types does not create new data, but it links to the main data, `data[deck_name]` as an example.


## Open and Read File at the Same Time
```python

with open("file_path", "r+", encoding="utf-8") as f:
	data = json.load(f)
	data["new_data"] = []
	
	# Used to reset file pointer after reading to the very end
	f.seek(0)
	
	json.dump(data, f, ensure_ascii=False, indent=2)
	
	# Used to remove file leftovers after writing
	f.truncate()
```

## * How to use `<textarea>`
```html
<textarea name="" rows="" cols="">Text</textarea>

# Rows is how many lines
# Cols is how many characters each line
```

## * Error Codes
```python
404 #Not Found
400 #Bad Request, invalid input
500 # Write Failed
```

## * `repr`
```python
print(repr(text)) #repr stands for representation, it returns developer friendly string representation like \n \r
```

## * `| safe and .replace`
```html
# If your html does not recognize \n new line character you can
<p>{{ card.back.replace("\n", "<br>") | safe }}</p>
# safe is used here to tell the html that it is a safe tag, valid one
```

## * Why not use `set()` to shuffle
1. Set randomness is deterministic, all is based of hash values
2. Some data types like dictionary can't be hashed
3. Order is not controllable, probability is a mess

## * CSS Tags
```
width: 100vw; #viewport width
height: 100vh; #viewport height
```

#project #html #errors 