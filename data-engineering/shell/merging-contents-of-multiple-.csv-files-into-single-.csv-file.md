# Merging contents of multiple .csv files into single .csv file

```
awk '(NR == 1) || (FNR > 1)' *.csv > out.csv
```

Both NR and FNR represent the number of the line being processed (1 based index). FNR is the current line within each File while NR is the current total Number of Records across all files. 

* (NR == 1) is including the first line of the first file (header), 
* (FNR > 1) skips the first line of each subsequent file.
