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

