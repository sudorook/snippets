# date

## Output time in nanoseconds

Combine the `%s` and `%N` output codes to display output in nanoseconds:
```
date -d <datestring> '+%s%N'
```

## Convert HH:MM:SS to number of seconds

Set the date to the start of the Unix epoch to output number of seconds:
```
date -d '1970-01-01 <HH:MM:SS> UTC' '+%s'
```

If the time stamp also includes nanoseconds, adjust as follows:
```
date -d '1970-01-01 <HH:MM:SS.NS> UTC' '+%s%N'
```
