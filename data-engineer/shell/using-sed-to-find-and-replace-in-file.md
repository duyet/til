---
description: sed = Stream EDitor
---

# Using \`sed\` to find and replace in file

## sed find and replace text

```text
sed 's/word1/word2/g' input.file
```

Find and replace text and save to new file

```text
sed 's/word1/word2/g' input.file > output.file
```

Note: 

* `s/` means substitute
* `/g` means global replace

## Can change delimiter `/` to something else:

```text
sed 's~word1~word2~g' input.file > output.file
```

## Find and replace in the line contains something

```text
sed -i -e '/FOO/s/love/sick/' input.txt
```

In this example only find the word `love` and replace it with the `sick` if line content a specific string such as `FOO`

## Find and replace multiple files in sub-folder

```text
find ./ -type f -exec sed -i -e 's/apple/orange/g' {} \;
```

`-i`  to save the temporary file

Source: [https://stackoverflow.com/a/6759339](https://stackoverflow.com/a/6759339)

