# PDF

## Extract metadata

Extract PDF metadata, such as chapters and bookmarks, into a text file:
```
pdftk input.pdf dump_data output metadata.txt
```


## Add metadata in file to PDF

Embed PDF metadata as text into a PDF:
```
pdftk input.pdf update_info metadata.txt output output.pdf
```

## Remove the first page from a PDF

To remove pages and page ranges from a PDF, use `pdftk` to:
```
pdftk input.pdf cat 2-end output output.pdf
```

The above command will not preserve metadata, though.
