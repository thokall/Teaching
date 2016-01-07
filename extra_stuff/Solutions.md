## Final commments

Many tools that are available on most unix systems can be used to count featueres (like sequences etc) in text files.

```bash
$ grep '>' file.fasta | wc 
```

Will identify all fasta header rows in a fasta file and parse the output to the command wc which count the number of rows and characters and can hence be used to count the number of sequences in a file

```bash
$ module load Fastx/0.0.14
$ fasta-formatter -i file.fasta > filenew.fasta
$ grep '>' filenew.fasta | tr -d "len=" | awk '{sum+=$2} END {print sum}'
```

Will use the program fasta-formatter ot create a fasta file that instead of being 80 characters wide will have the header on 1 row and then the full sequence on the second row.
Header rows are then parse to the tr command, where the characters len= are deleted and the second column that now contains the length reported by trinity are summed up using awk.

```bash
$ module load ucsc-utlities/v287
$ faFilter -minSize=1000 file.fasta filenew.fasta
```

Filter the fasta file to only contain reads longer or equal to 1000bp long.

```bash
$  grep -E '.{1000}' filenew.fasta -B1 | grep '>' -c
```

NB! This needs a fasta file that have each single sequence on one line (eg. the output from fasta-formatter).
It identifies all rows which have 1000 or more characters and grabs the row before that (-B1) pipes this to grep and count the number of header rows that are followed by a 1000bp or longer sequence.

On top of this one can of course write code in your favorite scripting language, the carry-home message is that there are many suitable tools available and many issues can be solved without writing much code.