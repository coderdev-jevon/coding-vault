# Python Standard Library
Date: 2026-07-27
## Lessons
1. How to use `timedelta` in like `timedelta(days=7)`
2. Coder often you this combo
	```python
	if not file.is_file():
		continue
		
	# instead of
	if file.is_file():
		...
		
	#why? This is to make the indention to not be too far, keep the indent minimum
	```
3. `IOError` means Input/Output Error, it merged into `OSError`, so it means failed to read/write/access a file or path.
4. To use `itertools.groupby` in the most optimal way, first, sort it out first
5. Use `list(dict.fromkeys(list))` to get unique values, which order kept
6. Why implement `if file.is_file()` because there's a possibility `.log` named is a folder
7. Always consider variable names, don't make it the same as function name
8. `range(0,13)` this range start from 0 to 12
9. You can prevent `KeyError` by dictionary using this syntax
	```python
	value = dict_name.get(key_name, default)
	```
10. If a function returns `None`, probably you forgot to return in a certain condition
11. `If line:` checks if the line is empty or not

## * `datetime`
```python
datetime.now()
datetime.strptime() #string → datetime
strftime() #datetime → string
.year / .month / .day #attributes
timedelta #(add/subtract days, calculate date difference #Comparing datetime objects (`dt1 < dt2`)
```

## * `pathlib`
```python
Path() #create paths
.exists(), `.is_file()`
.open() #read/write
.parent`, `.name`, `.suffix`
#Path joining (no messy manual `/` or `\`)

folder = Path('transactions_logs')
all_log_files = folder('*.log')

folder.glob("record_*.txt") #starting with record_
folder.glob("**/*.log") #search for sub folders

```

## * `collections`
```python
Counter #count occurrences (your category count in summary)
defaultdict #avoid key error when accumulating sums
deque #fast append/pop from both ends (better than list for queues)
namedtuple #(lightweight data holder, precursor to classes)
```
#### ** `deque`
It is works as a list, and it is optimized to add/remove from both ends
```python
dq = deque()

dq.append("newest")
dq.appendleft("oldest")

dq.pop()
dq.popleft()

dq = deque(list, maxlen=5) #limit data to 5 items, no need manual append
```

#### ** `namedtuple`
basically it is a lightweight dictionary, but it is immutable, cannot append or modify, it can spot typos instantly
```python
# Define blueprint once 
ExpenseRecord = namedtuple("ExpenseRecord", ["date", "category", "description", "total"]) 

# Build instance 
record = ExpenseRecord( 
	date="2026-07-27", 
	category="Food", 
	description="Lunch", 
	total=15000 
) 

print(record.date) 
print(record.category)
```
#### ** `Counter`
```python
counter = Counter(record.category for record in records) #saves memory, because it does not need the data to be stored in full memory list
# or
counter = Counter((record.category for record in records))
```

## * `os`
```python
os.environ #read environment variables (your Flask PORT)
os.getcwd() #current working directory
os.mkdir() #create folder
os.listdir() #list files inside folder
```

## * `random`
```python
random.randint(a,b)
random.choice(list)
random.shuffle()
```

## * `statistics`
```python
statistics.mean() #average spending
statistics.median() #median expense
statistics.mode() #most frequent category
```

## * `itertools`
all functions produce `iterables` (lazy), they don't create full lists
```python
import itertools
#1
itertools.chain #combine multiple iterators
	list_a = [1,2,3]
	list_b = [10, 20, 30]
	combined = itertools.chain(list_a, list_b)
	print(list(combined)) # [1,2,3,10,20,30]

#2
itertools.islice #take first N items from generator
	itertools.islice(logs, 3)

#3
itertools.groupby #group data (group expenses by month!), first sort it out

	import itertools
	
	students = [
	    {"name": "Jevon", "gender": "Male", "age": 18},
	    {"name": "Alvaro", "gender": "Female", "age": 19},
	    {"name": "Devin", "gender": "Male", "age": 18}
	]
	
	groupby_gender = itertools.groupby(students, key=lambda x: x["gender"])
	
	for group_key, items in groupby_gender:
	    print(f"Group: {group_key}")
	    for item in items:
	        print(item)

#4
itertools.count #infinite counter generator

	counter = itertools.count(start=10, step=2)
	print(next(counter)) #10
	print(next(counter)) #12

#5 
itertools.product # nested loops without nested for

	categories = ["Food", "Transport"] 
	payments = ["Cash", "E-Wallet"] 
		for cat, pay in itertools.product(categories, payments): print(cat, pay)
	
#6
itertools.accumulate # for cumulative sum
	amounts = [1000, 2500, 3000]
	running_total = itertools.accumulate(amounts)
	print(list(running_total)) # [1000, 3500, 6500]

```

#project 