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

## Generate a date-based label

To generate a unique-enough ID using the current timestamp, try:
```
date +%Y%m%d-%H%M%S
```

Should more specificity be needed, for example, if more than one ID needs to be
generated per second, add the `%N` option for nanoseconds:
```
date +%Y%m%d-%H%M%S-%N
```
