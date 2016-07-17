
# Library Caprentry - Counting with the Shell Lesson 2 - part 1

#### Objectives
* understand how to count lines, words, and characters with the shell
* understand how to mine files and extract matched lines with the shell
* understand how to combine mining with the shell and regular expressions

### Manipulating, counting and mining research data
* Now you can work with the unix shell you can move onto learning how to count and mine data. 
* These are rather simple and are unlikely to totally revolutionise your work. 
* They are, however, alongside the consistent file structure and naming, they are the foundation of a more powerful set of commands that can count and mine your data.



## Counting

For this section, you will begin by counting the contents of files using the Unix shell. 
* The Unix shell can be used to quickly generate counts from across files, something that is tricky to achieve using the graphical user interfaces of standard office suites.

To get started, use the **cd** command to navigate to the directory that contains our data. 
* Remember, if at any time you are not sure where you are in your directory structure, type **pwd** and hit enter.




```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data


Type **ls -F** and then hit enter. This prints, or displays, a list of files and directories in the current directory


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	everything-together.txt
    2014-01-31_JA-america.tsv*	firstdir/
    2014-01_JA.tsv			gallic.txt*
    2014-01_JA.tsv.zip		gulliver-backup.txt*
    2014-02-01_JA-art .tsv*		gulliver-twice.txt
    2014-02-02_JA-britain.tsv*	gulliver.txt*
    829-0.txt*


### Explain The .tsv data files

The files in this directory includes a zipeed and unzipped version of the dataset **2014-01_JA.tsv** that contains journal article metadata.  We unpacked this file at the beginning of the workshop.

Looking at the other data files, there are also four **.tsv** files derived from **2014-01_JA.tsv**. 
* Each of these four includes all data where a keyword such as africa or america appears in the ‘Title’ field of 2014-01_JA.tsv. 


### Note: 

**.TSV** files are those in which within each row the units of data (or cells) are **separated by tabs**. 
* They are similar to CSV (comma separated value) files were the values are separated by commas. 
* The latter are more common but can cause problems with the kind of data we have, where commas can be found within the cells (though with the right encoding this can be overcome). 
* Either way both can be read in simple text editors or in spreadsheet programs such as **Libre Office Calc or Microsoft Excel**.

Before we begin working with these files, lets double check we are in the right directory in which they are stored.


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data


Next we want to Count the contents of the files.
* The Unix command for counting is **wc**.
* Type **wc -w 2014-01-31_JA-africa.tsv** and hit enter. 


```bash
wc -w 2014-01-31_JA-africa.tsv
```

      511261 2014-01-31_JA-africa.tsv


The file contains 511261 words.
* The flag **-w** combined with wc instructs the computer to print a word count, and the name of the file that has been counted, into the shell.
* As was seen earlier today flags such as **-w** are an essential part of getting the most out of the Unix shell as they give you better control over commands.

If your reader request or piece of work is more concerned with number of entries (or lines) than the number of words, you can use the **line count flag**. 
* Type **wc -l 2014-01-31_JA-africa.tsv** and hit enter. 


```bash
wc -l 2014-01-31_JA-africa.tsv
```

       13712 2014-01-31_JA-africa.tsv


* Combined with wc the **flag -l** prints a line count and the name of the file that has been counted.

Finally, type **wc -c 2014-01-31_JA-africa.tsv** and hit enter. 

##### Note: OS X users should replace the -c flag with -m.


```bash
wc -m 2014-01-31_JA-africa.tsv
```

     3773660 2014-01-31_JA-africa.tsv


This wc command uses the **flag -c** in combination with the **command wc** to print a **character count** for 2014-01-31_JA-africa.tsv 

With these three flags, the most obvious thing we can use **wc** for is to **quickly compare the shape of sources** in digital format:
* for example word counts per page of a book, the distribution of characters per page across a collection of newspapers, the average line lengths used by poets. 
* You can also use **wc** with a combination of wildcards and flags to build more complex queries.

### Exercise - wc flags (2 mins)
Can you guess what the line **wc -l 2014-01-31_JA-a*.tsv** will do?  (try running the command)


```bash
wc -l 2014-01-31_JA-a*.tsv
```

       13712 2014-01-31_JA-africa.tsv
       27392 2014-01-31_JA-america.tsv
       41104 total


This wc command prints the line counts for 2014-01-31_JA-africa.tsv and 2014-01-31_JA-america.tsv, offering a simple means of comparing these two sets of research data.

It may be faster if you only have a handful of files to compare the line count for the two documents in Libre Office Calc, Microsoft Excel, or a similar spreadsheet program. 
* But when wishing to compare the line count for tens, hundreds, or thousands of documents, the Unix shell has a clear speed advantage.

As datasets increase in size you can use the Unix shell to do more than copy these line counts by hand, by the use of print screen, or by copy and paste methods.

### wc redirect operator

Using the **>** redirect operator we used earlier you can export query results to a new file for example:
* type **wc -l 2014-01-31_JA-a*.tsv > DATE_JA-a-wc.txt** (or something like that, the last bit after results/ could be anything!) and hit enter. 


```bash
wc -l 2014-01-31_JA-a*.tsv > DATE_JA-a-wc.txt
```

    

Check to make sure the file was created.


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	DATE_JA-a-wc.txt
    2014-01-31_JA-america.tsv*	everything-together.txt
    2014-01_JA.tsv			firstdir/
    2014-01_JA.tsv.zip		gallic.txt*
    2014-02-01_JA-art .tsv*		gulliver-backup.txt*
    2014-02-02_JA-britain.tsv*	gulliver-twice.txt
    829-0.txt*			gulliver.txt*


This runs the same query as before, but rather than print the results within the Unix shell it saves the results as **DATE_JA_a-wc.txt**.

To check the results in the file
* Type **head DATE_JA-a-wc.txt** to see the file contents in the shell (as it is 10 lines or fewer in length, all the file contents will be shown here).


```bash
head DATE_JA-a-wc.txt
```

       13712 2014-01-31_JA-africa.tsv
       27392 2014-01-31_JA-america.tsv
       41104 total


As you can see, the **redirect command** is useful to organize and group **wc** results in a single file.  

## End of counting section.


```bash

```
