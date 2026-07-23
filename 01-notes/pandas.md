# Pandas
Date: -

## Clone Git Hub Complete Tutorial
	1. copy url of the github tutorial
	2. go to CMD and change directory to your working folder
	3. type git clone url
	
## Set Virtual Environment (optional)
```bash
# Create virtual env in folder named venv
pyton -m venv venv
# Activate virtual env
venv\Scripts\Activate
# Install package
pip install -r requirements.txt
```

## Set up Visual Studio Code
	1. create ipynb (Interactive Python Notebook) to have the same utility as google colab
	2. try to run the code, select python environment of the venv you create
	3. there it is your ipynb notebook

## Features in IPYNB notebook
	1. use markdown cell to write type and Shift + Enter to run
	2. create new cell shortcut: press a to add cell above, press b to add cell below
	3. Shift + Enter -> run cell and go to below
	4. Ctrl + Enter -> run cell and stay
	5. Alt + Enter -> run cell and create new cell
	6. M -> change to markdown
	7. Y -> change to code
	8. DD -> delete cell
	9. Use md cell to hide cell by collapse (▾)

## Data Frames
#### Create Data Frames
```python
import pandas as pd

df = pd.DataFrame([[1,2,3], [4,5,6], [7,8,9]], columns=["A", "B", "C"], index=["X", "Y", "Z"]) #columns and index are optional
```

#### Print Out Data Frames
```python
df #look all of the rows
print(df) #look all of the rows
display(df) #look all of the rows

df.sample() #1 random row
df.sample(10) #10 random rows
df.sample(10, random_state=1) #to make it deterministic when run
df.head() #look first 5 rows
df.head(2) #to look at the top two rows
df.tail() #look last 5 rows
df.tail(2) #to look at the bottom two rows

df.columns #to look at the columns header
df.index df.index.tolist() #to look the index

## use real label
df.loc[rows, columns]
df.loc[:, ["Day", "Units Sold"]] #use specific label for column
df.loc[rows] #can be [0,1,2], 0:3, [0,1,5], 5:, etc

## use index
df.iloc[:, [0,2]] #use index instead of label

# grab specific item, basically use at for single item, use loc for slicing
df.at[row, column] #use label
df.iat[row, column] #use index

df.info() #to look at info, int64 == 64 bits == 8 bytes
df.describe() #to look at descriptive statistics

df.unique() #to look at unique values
df.nunique() #how many unique values in each volumn
df['A'].unique() #go to column A and find unique values
~ .isin(df['A'].unique()) #filters the one who is not in the list
	print(pd.Series(["Male", "Female", "Both"]).isin(df["Gender"].unique())) # it will return True/Fals

df.shape #return the same of the dataframe

# grab row and index
for index, row in coffee.iterrows():
    print(index)
    print(row["Units Sold"])
    print("\n\n\n\n")
```

#### Modify Data Frames
```python
#CHANGE DATA TYPE
bios_clean["born_year"].astype(int)
#CHANGE THE INDEX WILL CHANGE BEHAVIOR OF LOC AND ILOC
coffee.index = coffee["Day"] #to access column
coffee.index = coffee.Day #to access column if a single word

coffee.loc[1, "Units Sold"] = 10 # change the specific value read by loc and change the value to 10

#SORTING
coffee.sort_values("Units Sold") # ascending order
coffee.sort_values("Units Sold", ascending=True/False) # descending if false
coffee.sort_values(["Units Sold", "Coffee Type"], ascending=[0,1]) # sort by units sold first then if values are the same sort by coffee type, 0 means False, 1 means True
	#if your dataframe is quite complicated you can use this synthax
......sort_values(by=("height_cm", "mean"), ascending=False)

#FILTERING
	#single condition
bios.loc[bios["height_cm"] > 215, ["name", "height_cm"]]
bios[bios["height_cm"] > 215][["name", "height_cm"]]
	#multiple conditions
bios[(bios["height_cm"] > 215) & (bios["born_country"] == "USA")]
	#contains a certain substring
bios[bios["name"].str.contains("Shaq|patrick", case=False, na=False, regex=False)] # | is a regex used in pandas, case=False means case insensitive, na=False means null values will not be included, regex=False means to not use regex
bios[bios["born_country"].isin(["USA", "FRA"]) ] #to find matched values as in the list
bios.query("born_country == 'USA' and born_city =='Seattle'") #alternative so that not much duplicates of the data frame name

#FIND DUPLICATES
df["fruit"].duplicated(keep=["first", "last", False])
	#first keeps the first occurrence, last keeps the last occurence, False keeps None
bios_clean[bios_clean.duplicated(subset=["first_name", "born_year"], keep=False)][["first_name", "born_year"]]
```
#### Duplicate Data Frames
```python
coffee_new = coffee.copy() #duplicate a table
```

#### Renaming Columns
```python
coffee = coffee.rename(columns={"new_price": "price"}) #rename new_price to price
```
#### Adding/Removing Columns
```python
#ADDING COLUMNS
	##BY STRING METHODS
import numpy as np
coffee["new_price"] = np.where(coffee["Coffee Type"] == "Latte", 3, 2) #add new_price column and if Coffee Type is Latte, price is 3, else 2
bios_new["first_name"] = bios_new["name"].str.split(' ').str[0] #grab the first name of the full name
	##BY DATETIME
bios_new["born_datetime"] = pd.to_datetime(bios_new["born_date"], format="%Y-%m-%d") #change str to datetime to make it easier to modify, use format to make it more price
bios_new["born_year"] = bios_new["born_datetime"].dt.year #access to the year from the datetime
	##BY FUNCTION
bios["height_category"] = bios["height_cm"].apply(lambda x: "Short" if x < 165 else("Average" if x < 185 else "Tall")) #add a column by applying a function to the columns available
def categorize_weight(row):
    if row["weight_kg"] < 70:
        return "Lightweight"
    else:
        return "Heavyweight"
bios["weight_category"] = bios.apply(categorize_weight, axis=1)o every columns, axis=1 apply function to every rows

# axis=0 apply function t
#REMOVING COLUMNS
coffee.drop(columns=["price"], inplace=True) #remove specific column, inplace=True is used to delete it in reality, not on duplicates, main table columns is affected
coffee = coffee[["Day", "Coffee Type", "Units Sold", "new_price"]] #can be useful if you want to grab specific columns
```

#### String Functions
```python
bios_clean["born_region"] = bios_clean["born_region"].fillna("Unknown").str.capitalize()

bios_clean["born_region"] = bios_clean["born_region"].fillna("Unknown").str.title()
```
#### Merging & Concatenating Data
```python
#MERGE
bios_new = pd.merge(bios, nocs, left_on="born_country", right_on="NOC", how="left", suffixes=["1", "2"])
# merge(data1, data2, define whats on left, define whats on right, method based on picture, suffixes for similar labels)
combined_df = pd.merge(results, bios, on="athlete_id", how="left")

#CONCATENATE
new_df = pd.concat([usa, gbr])
```
![[Pasted image 20260427211020.png]]
#### Handling Null Values
```python
#CHANGE DATA TO NA
coffee.loc[[0,1], "Units Sold"] = np.nan

#FILL NA
coffee.fillna(10000)
coffee.fillna(coffee["Units Sold"].mean())
coffee.fillna(coffee["Units Sold"].interpolate())
bios_clean["born_country"] = bios_clean["born_country"].fillna(bios_clean["national_olympic_comittee"])
	# Looks at the symmetry and pattern on data

#DROP NA
coffee.dropna(subset=["Units Sold"], inplace=True)
	# don't use coffee =, it will return None

#CHECK NA or not NA
coffee[coffee["Units Sold"].notna()]
coffee[coffee["Units Sold"].isna()]
bios_clean["is_deceased"] = bios_clean["died_date"].notna()
```
#### Aggregating Data
```python
#COUNT VALUES
bios["born_city"].value_counts()
bios[bios["born_country"] == "USA"]["born_region"].value_counts()
	#the purpose of using this function is to calculate each items in the Series and return the count

#GROUP BY
coffee.groupby(["Coffee Type"])["Units Sold"].sum()
coffee.groupby(["Coffee Type", "Day"]).agg({"Units Sold": "sum", "price": "mean"})
	# .sum(), .average(), .mean()
bios.groupby([bios["year_born"], bios["month_born"]])["name"].count().reset_index().sort_values("name", ascending=False)

bios_clean.groupby("national_olympic_committee").agg({"height_cm": ["min", "max", "mean", "median"]})

bios_clean.groupby("national_olympic_committee")["height_cm"].agg(min_height="min", max_height="max", avg_height="mean", median_height="median").reset_index()

athlete_profile = bios_clean.groupby("born_country").agg(total_athletes=("athlete_id", "count"), pct_complete=("has_data", lambda x: x.mean() * 100), avg_height=("height_cm", "mean"), avg_weight=("weight_kg", "mean"), avg_bmi=("bmi", "mean"), pct_deceased=("is_deceased", lambda x: x.mean() * 100)).round(1).reset_index().sort_values("total_athletes", ascending=False)

#PIVOT
pivot = coffee.pivot(columns="Coffee Type", index="Day", values="revenue")
	pivot.loc["Monday", "Latte"]
	pivot.sum(axis=1)

#PIVOT TABLE
height_pivot = bios_clean.pivot_table(columns="height_category", index="born_country", values="athlete_id", aggfunc="count", fill_value=0)

#MELT
long_df = height_pivot.reset_index().melt(id_vars="born_country", value_vars=["Short", "Average", "Tall"], var_name="height_category", value_name="athlete_count")

**id_vars**: columns you **KEEP** (like country, decade)
- **value_vars**: columns you **UNPIVOT** (turn into rows)
- **var_name**: name for the new column
- **value_name**: name for the values column
```

#### Min, Max, Mean, Median
```python
## FOR FINDING MAX,MIN,MEAN,MEDIAN
min = bios_clean.min(numeric_only=True)
min_full = pd.Series(0, index=bios_clean.columns)
min_full.update(min)

max = bios_clean.max(numeric_only=True)
max_full = pd.Series(0, index=bios_clean.columns)
max_full.update(max)

median = bios_clean.median(numeric_only=True)
median_full = pd.Series(0, index=bios_clean.columns)
median_full.update(median)

mean = bios_clean.mean(numeric_only=True)
mean_full = pd.Series(0.0, index=bios_clean.columns)
for col in mean.index:

    mean_full[col] = mean[col]
```
#### Summary Table
```python
summary_table = pd.DataFrame({"category": ["Tallest Country", "Shortest Country", "Max-Min Difference"], "country": [country_height["born_country"].iloc[0], country_height["born_country"].iloc[-1], "---"], "height_cm": [country_height["height_cm"].iloc[0], country_height["height_cm"].iloc[-1], height_diff]})
```
#### Advanced Functionality
```python
#SHIFT
coffee["yesterday_revenue"] = coffee["revenue"].shift(2)
	# you can shift -2

#RANK
bios["height_rank"] = bios["height_cm"].rank(ascending=False)
bios.sort_values(["height_rank"]).sample(10)[["name", "height_rank"]]

#ROLLING
latte["3day"] = latte["Units Sold"].rolling(3).sum()

#ROLLING - CUMSUM
coffee["cumulative_revenue"] = coffee["revenue"].cumsum()
```

![[Pasted image 20260427211020.png]]
#### Save Modified Data Frame
```python
bios_new.to_csv("./data/bios_new.csv", index=False) #index=False to not include the index
```

> [!important]
> Learn to use Reg Ex to Filter Out Better

## Read CSV Files and Explore the Data
	Pros of CSV Files: Easy to use, read, and understand
	Cons of CSV Files: Takes up a lot of space, three times of feather files, 9 times of parquet files, one point 5 times of xlsx files
	
```python
#READ CSV FILE
coffee = pd.read_csv("./warmup-data/coffee.csv")
	#OR
## From github, copy the raw data link, and change the url of the file with the url in website, easy!

#EXPLORE DATA
coffee.head()
```

## Read Parquet Files
```python
#READ PARQUEST FILE
results = pd.read_parquest("./data/results.parquet")

#EXPLORE DATA
results.head()
```

## Read Excel Files

> [!important]
[Clean Data Tutorial](https://www.youtube.com/live/oad9tVEsfI0?si=QeIp8AGcGqrYgzBK)

```python
#READ PARQUEST FILE
olympics_data = pd.read_excel("./data/olympics-data.xlsx", sheet_name="results") #sheet name is optional

#EXPLORE DATA
olympics_data.head()
```

## Convert File Extensions
```python
olympics_data.to_excel
olympics_data.to_parquet
olympics_data.to_csv
```

## Additional Python Libraries

#### Gender Guesser
pip install gender-guesser
```python
## 2
import gender_guesser.detector as gender

d = gender.Detector()

bios_clean["gender"] = bios_clean["first_name"].fillna("unknown").apply(lambda x: d.get_gender(x))
```


#pandas
