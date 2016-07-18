## Mining 

* Shell can do much more than count! 
* The `grep` (global regluar expression print) searches across multiple files for specific character strings
  * Faster than a GUI search 
  * Combined with redirection `>` operator is a powerful data mining tool searching for patters across multiple files, subsetting into new derived files
* Esp. benefitial for working with large numbers of files

**Start in the `data/` directory**

* Remember how to see where we are in the file structure: 

```bash
pwd
```

* Should be something like `/Users/riley/Desktop/data`

* Let's look across all the .tsv files for instances of 1999  (character cluster)

```bash
grep 1999 *.tsv
```

* use up arrow to recall the last command and amend the command: 

```bash
grep -c 1999 *.tsv
```

* The shell outputs the number of times the string `1999` appeared in each *.tsv
* the Year corresponds to the date field for each journal article in the file ( look at the file )

* Srings need not be numbers

```bash
grep -c revolution *.tsv
```

* counts the instances of the string `revolution` with the defined files and prints those counts to the shell

* now let's add a `-i` flag to our previous command

```bash
grep -ci revolution *.tsv
```

* this repeats the query but prints the case insensitive count (incl. instances of both `revolution` and `Revolution`)
* note how the count has increased 30 fold for journal article titles that contain the key word america
* we could use our up arrow here and redirect this output into `results/` to save the work

```bash
grep -ci revolution *.tsv > results/2016-07-19_JA-revolution.txt
```

* So far we have counted strings in files and printed to the shell or files those counts
* The real power of `grep` comes in that you can use it to create subsets of tabulated data (or any data) from one or **multiple files**

```bash
grep -i revolution *.tsv
```

* this looks in the defined files and prints any lines containing `revolution` without regard for case

```bash
grep -i revolution *.tsv > results/2016-07-19_JAi-revolution.txt
```

* this saves the subsetted data to the file
* however if we look at this file (look), it contains every instance of 'revolution' including as a single word or as part of other words such as 'revolutionary'
* dependin on your objectives this is useful or not
* `grep` provides the `w` flag so we can look for whole words - greater precision in our search

```bash
grep -iw revolution *.tsv > results/2016-07-19_JAiw-revolution.tsv
```
* this now looks in the files and exports any lines containing the whole world `revolution`

* we can now show the differences between the files we created

```bash
wc -l results/*.tsv
```

**We can use the regular expression syntax covered earlier to search for similar words**

* look at teh file `gallic.txt`

```bash
cat gallic.txt
```
* it contains `fr[ae]nc[eh]`
* the brackets here express the pattern of a character range
* now we can use with `grep`

```bash
grep -iw --file=gallic.text *.tsv
```

* the shell will print out each line containing the following:

```
- france
- french
- frence
- franch
```

* If we include the `-o` flag, we will print only the matching part of the lines, e.g. (this is handy for isolating/checking results)

```bash
grep -iwo revolution *.tsv
```

OR:

```bash
grep -iwo --file=gallic.txt *.tsv
```

* we could pipe those to a file for a list of cases to evaluate or further analyze

## Challenges 

* Break up into pairs and work on the challenges in the ether pad
* put up the yellow flag when you are done
* put up the red flag if you get stuck

1. Search for all case sensitive instances of a word you choose in the ‘America’ and ‘Africa’ tsv files in this directory. Print your results to the shell.

2. Count all case sensitive instances of a word you choose in the ‘America’ and ‘Africa’ tsv files in this directory. Print your results to the shell.

3. Count all case insensitive instances of that word in the ‘America’ and ‘Africa’ tsv files in this directory. Print your results to the shell.


4. Search for all case insensitive instances of that word in the ‘America’ and ‘Africa’ tsv files in this directory. Print your results to a new >.tsv file.

5. Search for all case insensitive instances of that whole word in the ‘America’ and ‘Africa’ tsv files in this directory. Print your results to a new .tsv >file. 

> ## Solution >~~~ >grep -iw hero 2014-01-31* > new2.tsv >~~~ >{: .bash}

## finally: compare the line counts of the last two files you created and open the files in a text editor and search using the editor
