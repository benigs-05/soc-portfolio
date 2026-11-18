SCANNING 

```
cat log-session-x.csv | cut -d "," -f3 | uniq -c
```

```
read file -> extract one column -> count repeated lines
```


```
cat log-session-x.csv
```

prints the whole CSV file to the terminal.

```
time,src_ip,dst_ip,action
10:00,192.168.1.5,8.8.8.8,allow
10:01,192.168.1.5,1.1.1.1,allow
```

`cat` just displays it.


```
cut -d "," -f3
```

means:

```
split each line using comma as the delimiter
show field/column 3
```

```
uniq -c
```

counts unique values that are next to each other, so we can actually use sort first 

```
sort | uniq -c 
```
Without -c it will just show values and not count it 






```
awk -F',' '$5=="\"192.168.230.1\"" {print $6}' log-session-2.csv | sort -n | uniq
```


```
From log-session-2.csv,
find rows where destination IP is 192.168.230.1,
print the destination port,
sort the ports numerically,
and show each unique port once.
```


```
Use awk to process the file line by line.
```

Awk is good for saying:

```
if this column matches something, print another column
```

