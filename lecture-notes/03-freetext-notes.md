## Working with free text

* we've explored using the shell to manipulate, count, and mine tabulated data
* but most library data is not so nicely structured and is much messier than journal article metadata
* but many of these same techniques can be applied to non-tabbed data
* we just need to think about what we want out of the data

* we are going to leap forward a bit in this lesson in terms of difficulty
* we won't learn everything about what commands we are running in detail 
* we are going to prepare and pull apart text to show the potential of Unix shell in research

* work together on this exercise 

* we want to be in our `data/` folder again

```bash
pwd
```

* Yesterday we created the `gulliver.txt` file that was downloaed from *Project Gutenberg*
* Let's look at it using the command `less`

```bash
less -N gulliver.txt
```

* i've used -N to make `less` show me the line numbers
* let's look at the end of the document using `G`
* i want to remove all the `terms of usage` statements at the end of the document
* to do that we will use a command call `sed` (stream editor)

```bash
sed '9352,9714d' gulliver.txt > gulliver-nofoot.txt
```
* this sed command in conjunction with `d` will look at gulliver.txt and delet all values between the lines specified
* we save the results to a new file 

* let's do the same thing for the preface to the book

```bash
sed '1,37d' gulliver-nofood.txt > gulliver-noheadfoot.txt
```

* this slices off the header of the book, so we have the text of the book
* we still need to clean the text further
* we'll use the `tr` command, used for translating or deleting characters

```bash
tr -d [:punct:] < gulliver-noheadfoot.txt > gulliver-noheadfootpunct.txt
```

* we use the `d` flag of tr to delete all the punctuation
* note: this requires both forms of redirection
  * output redirection `>` 
  * input redirection `<`
  * read how it works

* lastly, regularize teh text by removing all the uppercase lettering

```bash
tr [:upper:] [:lower:] < gulliver-noheadfootpunct.txt > gulliver-clean.txt > gulliver-clean.txt
```

## Named Entity Recognition 

* Named entities are definite noun phrases that refer to specific types of individuals, such as organizations, persons, dates, and so on. 
	* ORGANIZATION - Georgia-Pacific Corp., WHO
	* PERSON - Eddy Bonte, President Obama
	* LOCATION -Murray River, Mount Everest
	* DATE June, 2008-06-29
	* TIME two fifty a m, 1:30 p.m.
	* MONEY 175 million Canadian Dollars, GBP 10.40
	* PERCENT - twenty pct, 18.75 %
	* FACILITY Washington Monument, Stonehenge
	* GPE South East Asia, Midlothian
* We are using the Stanford NER <http://nlp.stanford.edu/software/CRF-NER.shtml> tool 

```bash
stanford-ner/ner.sh gulliver-noheadfootpunct.txt > gulliver_ner.txt
```

### break above down

* calls ner.sh inside `stanford-ner/` on `gulliver-noheadfootpunct.txt` and redirects to `gulliver_ner.txt`
* let's look at file - it annotates the file with /0 or some entity description
* it will append a /PERSON, /ORGANIZATION or /LOCATION tag respectively. 

```bash
sed 's/\/O / /g' < gulliver_ner.txt > gulliver_ner-clean.txt`
```

* the sed command ‘s/before/after/g’ changes all instances of the before pattern to the after pattern
* let's remove the /0 so we can better see and further analyze the file
* The pattern that we are trying to match has a forward slash in it, so we have to precede that with a backslash to escape it.

```bash
egrep -o -f locpattr gulliver_ner-clean.txt | sed 's/\/LOCATION//g' | sort | uniq -c | sort -nr > gulliver_ner-loc-freq.txt
```
* egrep is a variant of grep for patterns ( extra regex) = same as running grep -E
* we use the `-o` flag to print only the matches
* `-f` reads the file `locpattr`
*  we pull out the locations (can be multiple words adjacency sequence), send to sed to delete LOCATION, sort, do a uniq count, and sort in reverse by number order (not alpha)

* challenge

* recreate this pipe but use the personpattr file instead, examine the pattern, notice how it differs
* what is the top occuring personal name?


