# 13.2: `sed` and `awk`
Date: 2026-10-06

## * Introduction to `sed` and `awk`
They are ==much lighter (fewer system resources) than python==, so it is more a reasonable choice during booting the system situation.

## * `sed`
Abbreviation for stream editor

`Input Stream -> Working Stream -> Output Stream`

## ==* `sed` Command Syntax==
```bash
sed -e command <filename> # e stands for editing
	sed -e s/cat/dog/ pets.txt # substitute cat with dog
	sed -e s/cat/dog/g pets.txt # g stands for global, so substitute every match
sed -f scriptfile <filename> # read commands from script file and operate it on the file
echo "I hate you" | sed s/hate/love/ # I love you
```

## ==* `sed` Basic Operations==
You can use `:, |, or anything else` instead of `/`
```bash
sed 1,3s/pattern/replace_string/g file # substitute pattern in 1,3 range of lines

sed -i s/pattern/replace_string/g file # in-place
```


## ==* `awk`==
```bash
awk 'pattern { action }' file
```

#### ==** `awk` Basic Operations==
```bash
awk '{ print $0 }' /etc/passwd # print entire file
awk -F: '{ print $1 }' /etc/passwd # print first field of every line
awk -F: '{ print $1 $7}' /etc/passwd # print first and seventh field of every line
```

#### ** Field Separator
`-F{separator}` allows you to choose different separator
