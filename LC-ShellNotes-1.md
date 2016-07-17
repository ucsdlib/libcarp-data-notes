
# Library Carpentry Controlling data with the Shell

Pass out handout

Tools Installation:
* GitBash Installation Windows
* MacOS use of Terminal

Introduction to lesson resources:

* Show Workshops site - Available schedule and lessons
* Etherpad - shared note taking (show on screen)
* Stickies - Red and Green (need help and I’m good) explanation
* Helpers Available

Downloading data files for lesson:
http://github.com/ucsdlib/libcarp-data-notes/


# Introduction

#### Answering the Questions:
* What is the shell?
* What is the command line?
* Why should I use it?
#### Objectives for this session:
* understand the basics of the Unix shell
* understand why and how to use the command line
* use shell commands to work with directories and files
* use shell commands to find and manipulate data


#### Introducing the Shell:
The data:
* Run git clone https://github.com/ucsdlib/libcarp-data-notes/
* Open and show data files that will be used in lesson
* **Unzip 2014-01_JA.tsv.zip** in libcarp-data-notes folder


Get the data at:


```bash
git clone https://github.com/ucsdlib/libcarp-data-notes/
```

    Cloning into 'libcarp-data-notes'...
    remote: Counting objects: 55, done.[K
    remote: Compressing objects: 100% (42/42), done.[K
    remote: Total 55 (delta 19), reused 33 (delta 8), pack-reused 0[K
    Unpacking objects: 100% (55/55), done.
    Checking connectivity... done.


## Begin with brief shell explanation.

In this session we will introduce programming by looking at how data can be manipulated, counted, and mined using the Unix shell, a **command line interface or CLI** to your computer and the files to which it has access.

The shell is one of the most productive programming environments ever created. 
* Its syntax may be cryptic, but people who have mastered it can experiment with different commands interactively, then use what they have learned to automate their work.
* Graphical user interfaces may be better at the first, but the shell is still unbeaten at the second.

A Unix shell is a **command-line interpreter** that provides a user interface for:
* the Linux operating system and for Unix-like systems (such as iOS)
* Soon to be integrated in new versions of Windows

For Windows users, the shell program such as **Git Bash** provide a Unix-like interface. 
* This session will cover a small number of basic commands, which constitute building blocks upon which more complex commands can be constructed to fit your data or project.

The motivations for wanting to learn shell commands are many and various. 
* What you can quickly learn from this workshop are the basics to quickly query lots of data for the information you want in a fast and efficient way.



#### Examples:
To give you some idea of what the shell can do, I will demonstrate how to find the number of articles published in 2009 in academic history journals whose title contains the word ‘International’.

First, let’s use a shell command to see how big this file is.
* Type **wc -l ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv**


```bash
wc -l ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv
```

      507732 /Users/rotsuji/desktop/libcarp-data-notes/data/2014-01_JA.tsv


The shell command **wc** with the argument **-l** (for lines) tells us this is a **500,000 line data file**. 
* Excel will struggle to manipulate that, but the shell won’t. 

To introduce the shell, let’s look at a complete string of shell commands to:
* find the number of articles published in 2009 in academic history journals whose title contains the word ‘International’ from the 500000 line data file.


```bash
grep 2009 ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv | grep INTERNATIONAL | awk -F'\t' '{print $5}' | sort | uniq -c
```

      40 AFRICA -LONDON- INTERNATIONAL AFRICAN INSTITUTE-
       1 ARCHAEOLOGY ETHNOLOGY AND ANTHROPOLOGY OF EURASIA
      34 AUSTRALIAN JOURNAL OF INTERNATIONAL AFFAIRS
     947 BAR INTERNATIONAL SERIES
     105 CHINA REVIEW INTERNATIONAL
      70 FOREIGN POLICY -WASHINGTON-
      13 GESTA
      38 INDONESIAN QUARTERLY
       2 INTERNATIONAL AFRICAN LIBRARY
     274 INTERNATIONAL HISTORY REVIEW
      80 INTERNATIONAL JOURNAL OF AFRICAN HISTORICAL STUDIES
      17 INTERNATIONAL JOURNAL OF AFRICAN RENAISSANCE STUDIES
      23 INTERNATIONAL JOURNAL OF CONTEMPORARY IRAQI STUDIES
      16 INTERNATIONAL JOURNAL OF HISTORICAL ARCHAEOLOGY
      13 INTERNATIONAL JOURNAL OF IBERIAN STUDIES
     217 INTERNATIONAL JOURNAL OF MARITIME HISTORY
     169 INTERNATIONAL JOURNAL OF MIDDLE EAST STUDIES
      95 INTERNATIONAL JOURNAL OF NAUTICAL ARCHAEOLOGY
      70 INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
      25 INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
      55 INTERNATIONAL JOURNAL OF THE CLASSICAL TRADITION
      46 INTERNATIONAL REVIEW OF SOCIAL HISTORY
      42 INTERNATIONALES ASIENFORUM
      28 JEUNE AFRIQUE
       1 JOURNAL OF AFRICAN AMERICAN HISTORY
      31 JOURNAL OF CONTEMPORARY AFRICAN STUDIES
       1 JOURNAL OF MODERN AFRICAN STUDIES
       2 RESEARCH IN INTERNATIONAL STUDIES SOUTHEAST ASIA SERIES
       1 REVOLUTIONARY RUSSIA


#### Break down and briefly explain each command:

* The string of commands is simple, powerful, and does what we want. 
* It may seem intimidating but it is logical and eminently within your reach and something you can do.
* Review each part in turn:

#### First part:
* #### grep 2009 2014-01_JA.tsv
* grep is the command here. 
* It tells the computer to search the spreadsheet 2014-01_JA.tsv for all the lines that contain the string 2009 and to store those in memory. 
* The pipe then tells the machine to hold those in memory for the minute as we have something else we want to do.


```bash
grep 2009 ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv | head -10 
```

    History_1a-rdf.tsv	Harnish, D.	2	26	ASIAN MUSIC	0044-9202	(Uk)RN000200906	ASIAN MUSIC 26(2), 157-159. (1995)	Cilokaq Music of Lombok	xxu	eng	SOCIETY FOR ASIAN MUSIC, INC.	1995
    History_1a-rdf.tsv	Arana, M.	2	26	ASIAN MUSIC	0044-9202	(Uk)RN000200918	ASIAN MUSIC 26(2), 160-162. (1995)	Eternal Voices: Traditional Vietnamese Music in the United States	xxu	eng	SOCIETY FOR ASIAN MUSIC, INC.	1995
    History_1a-rdf.tsv	Ming-mei, Y.	2	26	ASIAN MUSIC	0044-9202	(Uk)RN000200920	ASIAN MUSIC 26(2), 163-165. (1995)	Soul of China - Guqin Recital by Professor LI Xiang Ting	xxu	eng	SOCIETY FOR ASIAN MUSIC, INC.	1995
    History_1a-rdf.tsv	Manuel, P.	2	26	ASIAN MUSIC	0044-9202	(Uk)RN000200931	ASIAN MUSIC 26(2), 166-167. (1995)	Retooling a Tradition: A Rajasthani Puppet Takes Umbrage at His Stringholders	xxu	eng	SOCIETY FOR ASIAN MUSIC, INC.	1995
    History_1a-rdf.tsv	Rawnlsey, G. D.	3	9	CONTEMPORARY RECORD	0950-9224	(Uk)RN002372009	CONTEMPORARY RECORD 9(3), 586-601. (1995)	How Special is Special? The Anglo-American Alliance During the Cuban Missile Crisis	xxk	eng	FRANK CASS LONDON	1995
    History_1a-rdf.tsv	Kraus, H.-C.	1	262	HISTORISCHE ZEITSCHRIFT	0018-2613	(Uk)RN003512009	HISTORISCHE ZEITSCHRIFT 262(1), 162-163. (1996)	J. J. Sack, From Jacobite to Conservative. Reaction and Orthodoxy in Britain, c. 1760-1832	gw	eng	BOEHLAU VERLAG HISTORISCHE ANTHROPOLOGIE	1996
    History_1a-rdf.tsv	Frantz, J. B.	1	53	WILLIAM AND MARY QUARTERLY	0043-5597	(Uk)RN003732009	WILLIAM AND MARY QUARTERLY 53(1), 216-218. (1996)	Griffin, Revolution and Religion: American Revolutionary War and the Reformed Clergy	xxu	eng	INSTITUTE OF EARLY AMERICAN HISTORY AND CULTURE	1996
    History_1a-rdf.tsv	Markoff, I.	2	29	MIDDLE EAST STUDIES ASSOCIATION BULLETIN		(Uk)RN005420090	MIDDLE EAST STUDIES ASSOCIATION BULLETIN 29(2), 157-160. (1995)	Introduction to Sufi Music and Ritual in Turkey	xxk	eng	THE MIDDLE EAST STUDIES ASSOCIATION OF NORTH AMERICA, INC.	1995
    History_1a-rdf.tsv	Keefe, S. E.	1	80	GEORGIA HISTORICAL QUARTERLY	0016-8297	(Uk)RN008662009	GEORGIA HISTORICAL QUARTERLY 80(1), 206-207. (1996)	Loftin, Healing Hands	xxu	eng	UNIVERSITY OF GEORGIA	1996
    History_1a-rdf.tsv	Downes, P.	4	29	EIGHTEENTH CENTURY STUDIES	0013-2586	(Uk)RN011720092	EIGHTEENTH CENTURY STUDIES 29(4), 413-432. (1996)	Sleep-Walking Out of the Revolution: Brown's Edgar Huntly	xxu	eng	THE JOHNS HOPKINS UNIVERSITY PRESS	1996


#### Second part:
* #### grep INTERNATIONAL 
* The shell is case sensitive by default. 
* This tells the computer to look for the capitalised string international on those lines that have 2009 in them.
* Again it holds this subset in memory.


```bash
grep 2009 ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv | grep INTERNATIONAL | head -10
```

    History_1b-rdf.tsv	Cherry, S.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200927951	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 7-30. (2006)	Medicine and rural health care in nineteenth and early twentieth century Europe	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Barona, J. L.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200927966	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 31-51. (2006)	Rural health, medicine and cultural interaction in late nineteenth and early twentieth century Spain	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Andresen, A.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200927976	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 52-72. (2006)	Towards equality? Rural health and health legislation in Norway, 1860-1912	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Cherry, S.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200927987	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 73-91. (2006)	Zemstvo health care in rural Russia c. 1864-1917	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Farr, I.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200927990	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 92-108. (2006)	Medical topographies in nineteenth century Bavaria	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Williamson, T.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200928000	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 109-122. (2006)	The disappearance of malaria from the East Anglian Fens	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Moll, I.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200928016	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 123-137. (2006)	Health networks in nineteenth century rural Majorca	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Andresen, A.	2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200928026	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 138-157. (2006)	Perspectives on the interaction of medicine and rural cultures: Spain, Norway and European Russia, 1860 - 1910	xxk	eng	lincoln	2006
    History_1b-rdf.tsv		2	2	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES	1750-0478	(Uk)RN200928037	INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES 2(2), 158-160. (2006)	I.Borowy and W.D. Gruner (eds) Facing illness in troubled times: health in Europe in the interwar years 1918-1939	xxk	eng	lincoln	2006
    History_1b-rdf.tsv	Piliang, I.J.	3	35	INDONESIAN QUARTERLY	0304-2170	(Uk)RN224067136	INDONESIAN QUARTERLY 35(3), 206-220. (2007)	Seeking for Victory, Not Biting The Dust: Political Parties' Situation Prior to 2009 General Elections	io	eng	CENTRE FOR STRATEGIC AND INTERNATIONAL STUDIES	2007


#### Third part:
* ##### awk -F'\t' '{print $5}'
* This command not be covered in detail for this class. 
* Brief explanation, it identifies 2014-01_JA.tsv is a tab-separated spreadsheet and instructs the computer to print to the shell the 5th column which contains journal titles of all the lines we’ve queried down to (those with 2009 in them, and then those with INTERNATIONAL in them) and to hold that in memory.


```bash
grep 2009 ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv | grep INTERNATIONAL | awk -F'\t' '{print $5}' | head -20
```

    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
    INDONESIAN QUARTERLY
    INDONESIAN QUARTERLY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
    INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY


#### Fourth part:
* ##### sort
* This command will sort that column.


```bash
grep 2009 ~/desktop/lc-data/libcarp-data-notes/shell-data/2014-02-01_JA-art.tsv | grep INTERNATIONAL | awk -F'\t' '{print $5}' | sort
```

    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    BAR INTERNATIONAL SERIES
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    CHINA REVIEW INTERNATIONAL
    FOREIGN POLICY -WASHINGTON-
    INTERNATIONAL JOURNAL OF AFRICAN HISTORICAL STUDIES
    INTERNATIONAL JOURNAL OF AFRICAN HISTORICAL STUDIES
    INTERNATIONAL JOURNAL OF CONTEMPORARY IRAQI STUDIES
    INTERNATIONAL JOURNAL OF MARITIME HISTORY
    INTERNATIONAL JOURNAL OF MARITIME HISTORY
    INTERNATIONAL JOURNAL OF MARITIME HISTORY
    INTERNATIONAL JOURNAL OF MARITIME HISTORY
    INTERNATIONAL JOURNAL OF MIDDLE EAST STUDIES
    INTERNATIONAL JOURNAL OF NAUTICAL ARCHAEOLOGY
    INTERNATIONAL JOURNAL OF THE CLASSICAL TRADITION
    INTERNATIONAL JOURNAL OF THE CLASSICAL TRADITION
    INTERNATIONAL JOURNAL OF THE CLASSICAL TRADITION


#### The fifth final command:
* ##### uniq -c
* final command will tell the comouter to remove duplicates but, as it is doing so, to count those duplicates and hold that data in memory.
* As this is the last bit, the shell then - by default - prints the results to the shell, i.e. the number of articles published in 2009 in academic journals whose title contains the word ‘International’, with counts separated by journal.


* There are a few false positives, but this is still a good start: from 500,000 lines of journal article metadata to a few numbers and names just by typing one line of code.


```bash
grep 2009 ~/desktop/libcarp-data-notes/data/2014-01_JA.tsv | grep INTERNATIONAL | awk -F'\t' '{print $5}' | sort | uniq -c

```

      40 AFRICA -LONDON- INTERNATIONAL AFRICAN INSTITUTE-
       1 ARCHAEOLOGY ETHNOLOGY AND ANTHROPOLOGY OF EURASIA
      34 AUSTRALIAN JOURNAL OF INTERNATIONAL AFFAIRS
     947 BAR INTERNATIONAL SERIES
     105 CHINA REVIEW INTERNATIONAL
      70 FOREIGN POLICY -WASHINGTON-
      13 GESTA
      38 INDONESIAN QUARTERLY
       2 INTERNATIONAL AFRICAN LIBRARY
     274 INTERNATIONAL HISTORY REVIEW
      80 INTERNATIONAL JOURNAL OF AFRICAN HISTORICAL STUDIES
      17 INTERNATIONAL JOURNAL OF AFRICAN RENAISSANCE STUDIES
      23 INTERNATIONAL JOURNAL OF CONTEMPORARY IRAQI STUDIES
      16 INTERNATIONAL JOURNAL OF HISTORICAL ARCHAEOLOGY
      13 INTERNATIONAL JOURNAL OF IBERIAN STUDIES
     217 INTERNATIONAL JOURNAL OF MARITIME HISTORY
     169 INTERNATIONAL JOURNAL OF MIDDLE EAST STUDIES
      95 INTERNATIONAL JOURNAL OF NAUTICAL ARCHAEOLOGY
      70 INTERNATIONAL JOURNAL OF OSTEOARCHAEOLOGY
      25 INTERNATIONAL JOURNAL OF REGIONAL AND LOCAL STUDIES
      55 INTERNATIONAL JOURNAL OF THE CLASSICAL TRADITION
      46 INTERNATIONAL REVIEW OF SOCIAL HISTORY
      42 INTERNATIONALES ASIENFORUM
      28 JEUNE AFRIQUE
       1 JOURNAL OF AFRICAN AMERICAN HISTORY
      31 JOURNAL OF CONTEMPORARY AFRICAN STUDIES
       1 JOURNAL OF MODERN AFRICAN STUDIES
       2 RESEARCH IN INTERNATIONAL STUDIES SOUTHEAST ASIA SERIES
       1 REVOLUTIONARY RUSSIA


Point out this string of shell commands is an example of how powerful the shell can be to quickly find inforamtion in a large data set. 

# Basics - navigating the shell

* We will begin with the basics of navigating the Unix shell.



* ##### Start by opening your shell.
* MacOS open Terminal
* Windows start Gitbash

* When you open the Terminal, you will likely see a black window with a cursor flashing next to a dollar sign. 
* This is our command line, and the 
##### $ 
is the **'command prompt'** to show the system is ready for your input.

* when working command window or at any other time today, you are unsure of where you are in a computer’s file system, you can find out what directory you are in using:
##### pwd 
which stands for **“print working directory”**, and hitting enter - which executes commands in the shell. 
* Try typing pwd and hitting enter.


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes


* The standard output displays your current location in the OS file system.

* Next, to orient ourselves, let’s get a listing of what files are in this directory. 
* Type **'ls'** 
* you see a list of every file and directory within your current location.


```bash
ls
```

    03-foundations-slides.html	LC-ShellNotes-2.ipynb
    03-foundations-slides.md	README.md
    04-regex1-slides.html		data
    LC-ShellNotes-1.ipynb


* Looking at the directory, You may want more information than just a list of files.
* You can do this by specifying various **'flags'** to go with our basic commands. 
*  Flags are additions to a command that provide the computer with a bit more guidance of what sort of output or manipulation you want.

* If you type **'ls -l'** and hit enter the computer: 


```bash
ls -l
```

    total 432
    -rw-r--r--   1 rotsuji  staff   11408 Jul 16 23:08 03-foundations-slides.html
    -rw-r--r--   1 rotsuji  staff   11366 Jul 16 23:08 03-foundations-slides.md
    -rw-r--r--   1 rotsuji  staff    6537 Jul 16 23:08 04-regex1-slides.html
    -rw-r--r--@  1 rotsuji  staff  178893 Jul 16 23:18 LC-ShellNotes-1.ipynb
    -rw-r--r--   1 rotsuji  staff    3759 Jul 16 23:03 LC-ShellNotes-2.ipynb
    -rw-r--r--   1 rotsuji  staff     107 Jul 16 23:08 README.md
    drwxr-xr-x  11 rotsuji  staff     374 Jul 16 23:13 data


* The standard output shows a long list of files that contains information similar to what you’d find in your finder or explorer.
*  E.g. the size of the files in bytes, the date it was created or last modified, and the file name.

*  In everyday usage you will be more used to units of measurement like kilobytes, megabytes, and gigabytes. 
* There is another flag **'-h'** 
* when used with the **'-l'** flag, this adds the unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte in order to reduce the number of digits to three or less using base 2 for sizes.

* Now ls -h won’t work on its own. When you want to use two flags, you can just run them together. 
* By typing **'ls -lh'** and hitting enter you receive an output in a human-readable format (note: that the order here doesn’t matter).


```bash
ls -lh
```

    total 432
    -rw-r--r--   1 rotsuji  staff    11K Jul 16 23:08 03-foundations-slides.html
    -rw-r--r--   1 rotsuji  staff    11K Jul 16 23:08 03-foundations-slides.md
    -rw-r--r--   1 rotsuji  staff   6.4K Jul 16 23:08 04-regex1-slides.html
    -rw-r--r--@  1 rotsuji  staff   175K Jul 16 23:18 LC-ShellNotes-1.ipynb
    -rw-r--r--   1 rotsuji  staff   3.7K Jul 16 23:03 LC-ShellNotes-2.ipynb
    -rw-r--r--   1 rotsuji  staff   107B Jul 16 23:08 README.md
    drwxr-xr-x  11 rotsuji  staff   374B Jul 16 23:13 data


### Tip - Manual pages
Use the **man** command to invoke the manual page (documentation) for a Shell command. 

* For example, **man ls** displays all the flags/options available to you - which saves you remembering them all! Try this for each command you’ve learned so far. 
* Use the **spacebar** to navigate the manual pages, and **q** to quit. Note: this command is for Mac and Linux users only. It may not work for Windows users.

## Change directories

Now that You’ve now spent some time in your home directory
Let’s go somewhere else. 
You can do browse through your directories by typing the **'cd'** or **'Change Directory command'** with the directory name.
before you do that...

Start from our home directory


```bash
cd ~
```

    

* Type **'pwd'** to show your current location


```bash
pwd
```

    /Users/rotsuji


* then type **'cd desktop'** to go to your desktop folder.


```bash
cd desktop
```

    

* type **'pwd'** again to show your current location.
* the path should be your desktop folder.


```bash
pwd
```

    /Users/rotsuji/desktop


* You’ll note that this only takes you ‘down’ through your directory structure (as in into more nested directories). 
* If you want to go back, you can type **'cd ..'**. This moves ‘up’ one directory, putting you back where you started. 
* If you ever get completely lost, the command **'cd -- (or cd ~ or even just cd)'** will bring you right back to the home directory, right where you started.


```bash
cd ~
```

    

* Type **'pwd'** again to make sure you were moved back to your home directory.


```bash
pwd
```

    /Users/rotsuji


### Tip: 
* To switch back and forth between two directories use **'cd -'**.


```bash
cd -
```

    /Users/rotsuji/desktop



```bash
cd -
```

    /Users/rotsuji


### Exercise: (2 mins)
Try exploring: move around the computer, get used to moving in and out of directories, see how different file types appear in the Unix shell.

Being able to navigate your file system using the bash shell is very important for using the Unix shell effectively. 

As you become more comfortable, you’ll soon find yourself skipping directly to the directory that you want.



## Summary
After this basic introduction, within the Unix shell, you can now:

* use the command **pwd** to find out where you are in on your computer
* use the command **ls** to list directory contents
* use the **man** command to check the manual page
* use **flags -l and -lh** to guide the output of the **ls** command
* use the command **cd** to move around your computer


# Basics

As well as navigating directories, you can interact with files on the command line: you can read them, open them, run them, and even edit them, often without ever having to leave the interface. 

Sometimes it is easier to do this using a Graphical User Interface, such as Word or your normal explorer, but the more you work here, the more it is useful, and the more you write scripts, the more you’ll need this basic knowledge.

Here are a few basic ways to interact with files.

Go to your data folder

type **pwd** to show your current location


```bash
pwd
```

    /Users/rotsuji


Browse to your data folder using the commands we just learned


```bash
cd desktop/libcarp-data-notes/data/
```

    


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data


* List the contents of the folder using **ls** with the flag **-F** to identify folders.


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	2014-02-01_JA-art .tsv*
    2014-01-31_JA-america.tsv*	2014-02-02_JA-britain.tsv*
    2014-01_JA.tsv			829-0.txt*
    2014-01_JA.tsv.zip		gallic.txt*


* Now you can create a new directory. 
* For convenience’s sake, we will create it in the directory you extracted the data provided in advance. 
* type **mkdir firstdir** and hit enter. 


```bash
mkdir firstdir
```

    

* use **ls -F** again to check the folder was created by the mkdir command.


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	2014-02-02_JA-britain.tsv*
    2014-01-31_JA-america.tsv*	829-0.txt*
    2014-01_JA.tsv			firstdir/
    2014-01_JA.tsv.zip		gallic.txt*
    2014-02-01_JA-art .tsv*


* The folder has been created.
* you can tell by the **forward slash** after the folder name.
* We used the **mkdir** command (meaning ‘Make Directorys’) to create a directory named **‘firstdir’**. Now, move into that directory using the **cd** command.


```bash
cd firstdir
```

    

* Check your folder path to make sure you are in the new 'firstdir'
* type **pwd**


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data/firstdir


### Tip - Tab completion
There’s a trick to make things a bit quicker. Go up one directory (cd ..). To navigate to the firstdir directory you could type cd firstdir. Alternatively, you could type cd f and then hit tab You will notice that the interface completes the line to cd firstdir. Hitting tab at any time within the shell will prompt it to attempt to auto-complete the line based on the files or sub-directories in the current directory. Where two or more files have the same characters, the auto-complete will only fill up to the first point of difference, after which you can add more characters, and try using tab again. We would encourage using this method throughout today to see how it behaves (as it saves loads of time and effort!).

### Manipulating files

The thing we are going to do is manipulate files using the shell.

* Navigate to the text directory in the pre-circulated data directory. 
* In here there is a copy of Jonathan Swift’s Gulliver’s Travels downloaded from Project Gutenberg. 


```bash
cd /Users/rotsuji/desktop/libcarp-data-notes/data/
```

    


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data


* type **ls -lh** and hit enter to see details of this file.


```bash
ls -lh
```

    total 346224
    -rwxr-xr-x  1 rotsuji  staff   3.6M Jul 16 23:08 2014-01-31_JA-africa.tsv
    -rwxr-xr-x  1 rotsuji  staff   7.4M Jul 16 23:08 2014-01-31_JA-america.tsv
    -rw-rw-r--  1 rotsuji  staff   125M Jun 10  2015 2014-01_JA.tsv
    -rw-r--r--  1 rotsuji  staff    29M Jul 16 23:08 2014-01_JA.tsv.zip
    -rwxr-xr-x  1 rotsuji  staff   1.8M Jul 16 23:08 2014-02-01_JA-art .tsv
    -rwxr-xr-x  1 rotsuji  staff   1.4M Jul 16 23:08 2014-02-02_JA-britain.tsv
    -rwxr-xr-x  1 rotsuji  staff   598K Jul 16 23:08 829-0.txt
    drwxr-xr-x  2 rotsuji  staff    68B Jul 16 23:22 firstdir
    -rwxr-xr-x  1 rotsuji  staff    13B Jul 16 23:08 gallic.txt


#### Next step, Using the Cat Command

There is a command utility build into the shell that lets you read files.
* The command is the **cat** or concatinate command.
* The basic command reads files sequentially, writing them to standard output.



#### To try this
* type **cat 829-0.txt**. 
* The terminal window erupts and Gulliver’s Travels cascades by: this is what is known as printing to the shell or standard output. 
* It's a great command, in theory, but you can’t really make any sense of that amount of text. 
* Instead, you may want to just look at the first or the last bit of the file.


```bash
cat 829-0.txt | head -50
```

    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    


## Tip - cancelling the output if it is long
* type **ctrl-c**

The output is quite long. 
* To view the first several lines only we'll use the **head** command.


```bash
head 829-0.txt
```

    
    
    
    
    
    
    
    
    
    


* The **head** command provides a view of the first ten lines, whereas **tail 829-0.txt** provides a perspective on the last ten lines. 


```bash
tail 829-0.txt
```

    
    
    
    
    
    
    
    
    
    


Using **head** and **tail** is a good way to quickly determine the contents of the file.

#### Less command
Another way to navigate files is to view the contents one screen at a time. 

Type **less 829-0.txt** to see the first screen, **spacebar** to see the next screen and so on, then **q** to quit (return to the command prompt).

**less 829-0.txt** (does not work in jupyter - check terminal on screen for output)

#### mv Command

Now we want to change the file name to something more descriptive. 
* You can **‘move’** it to a new name by using the **mv** or move command. 
* To do this type **mv 829-0.txt gulliver.txt** and hit enter. 
* This is equivalent to the ‘rename file’ function.


```bash
mv 829-0.txt gulliver.txt
```

    

check file has been created by typing the command **ls -F**


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	2014-02-02_JA-britain.tsv*
    2014-01-31_JA-america.tsv*	firstdir/
    2014-01_JA.tsv			gallic.txt*
    2014-01_JA.tsv.zip		gulliver.txt*
    2014-02-01_JA-art .tsv*


* You will see the file has been renamed to is now **gulliver.txt**

Now, if you wanted to duplicate the file instead of renaming the file, you could use:
* the **cp** or **copy command** 
* type **cp gulliver.txt 829-0.txt** 



```bash
cp gulliver.txt 829-0.txt
```

    

* running the **cp** command has now created a renamed copy of gulliver.txt
* type **ls -F** to see the 829-0.txt file was created. 


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	2014-02-02_JA-britain.tsv*
    2014-01-31_JA-america.tsv*	829-0.txt*
    2014-01_JA.tsv			firstdir/
    2014-01_JA.tsv.zip		gallic.txt*
    2014-02-01_JA-art .tsv*		gulliver.txt*


For demo purposes to compare the .txt files
* run **cat command** for both files.

### Tip - Up/Down arrow command cycling
* Now that you have seen and used several new commands, it’s time for another trick. 
* Pressing the **up arrow** twice on your keyboard. Notice that mv 829-0.txt gulliver.txt appears before your cursor. You can continue pressing the up arrow to cycle through your previous commands. 
* The **down arrow** cycles back toward your most recent command. 
* This is another important labour-saving function and something we’ll use a lot.


```bash
cat 829-0.txt | head -10
```

    
    
    
    
    
    
    
    
    
    



```bash
cat gulliver.txt | head -10
```

    
    
    
    
    
    
    
    
    
    


* As you can see a new renamed file was created leaving the original file intact. 

### Tip - History command
* use the **history** command to see a list of all the commands you’ve entered during the current session. 
* You can also use **Ctrl + r** to do a reverse lookup. 
* Hit **Ctrl + r**, then start typing any part of the command you’re looking for. 
* The past command will autocomplete. 
* Hit enter to run the command again, or press the arrow keys to start editing the command. 
* If you can’t find what you’re looking for in the reverse lookup, use **Ctrl + c** to return to the prompt.

#### demo in terminal

## Exercise - use cp to duplicate a file (2 min)
Use **cp** to duplicate the **gulliver.txt** file and give it the filename **gulliver-backup.txt**: any ideas how you do that?

##### **ANSWER:** 
$**cp gulliver.txt gulliver-backup.txt**


```bash
cp gulliver.txt gulliver-backup.txt
```

    


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	829-0.txt*
    2014-01-31_JA-america.tsv*	firstdir/
    2014-01_JA.tsv			gallic.txt*
    2014-01_JA.tsv.zip		gulliver-backup.txt*
    2014-02-01_JA-art .tsv*		gulliver.txt*
    2014-02-02_JA-britain.tsv*


#### Combining with Cat

now that you have two copies of Gulliver’s Travels, we are going to put them together to make an even longer book.



To combine, or concatenate, two or more files use the **cat** command again. 
* Type **cat gulliver.txt gulliver-backup.txt** and press enter. 



```bash
cat gulliver.txt gulliver-backup.txt | head -50
```

    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    


* This prints, or displays, the combined files within the shell. 
* 
As you can see, it is too long to read on this window! 
* Luckily, by using the **>** redirector, you can send the output to a new file, rather than the terminal window.

Use the **up arrow** to get to the last command
* ammend the line to
* **cat gulliver.txt gulliver-backup.txt > gulliver-twice.txt** and press enter (check terminal for output)


```bash
cat gulliver.txt gulliver-backup.txt > gulliver-twice.txt
```

    

Now, when you type **ls -F** you’ll see **gulliver-twice.txt** appear in your directory.


```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	829-0.txt*
    2014-01-31_JA-america.tsv*	firstdir/
    2014-01_JA.tsv			gallic.txt*
    2014-01_JA.tsv.zip		gulliver-backup.txt*
    2014-02-01_JA-art .tsv*		gulliver-twice.txt
    2014-02-02_JA-britain.tsv*	gulliver.txt*


#### Wildcards - Combining more than 2 files

When combining more than two files, using a **wildcard** can help avoid having to write out each filename individually. 
* A useful wildcard is ***** which is a place holder for zero or more characters or numbers (note: this is slightly different from regex…). 
* **make sure next cat command is run in the shell-data folder!**
* **pwd**, **ls -F**
* doulbe check to make sure working folder is **shell-data**


```bash
pwd
```

    /Users/rotsuji/desktop/libcarp-data-notes/data



```bash
ls -F
```

    2014-01-31_JA-africa.tsv*	829-0.txt*
    2014-01-31_JA-america.tsv*	firstdir/
    2014-01_JA.tsv			gallic.txt*
    2014-01_JA.tsv.zip		gulliver-backup.txt*
    2014-02-01_JA-art .tsv*		gulliver-twice.txt
    2014-02-02_JA-britain.tsv*	gulliver.txt*


now, if you type **cat *.txt > everything-together.txt** and hit enter, a combination of all the .txt files in the current directory are combined in alphabetical order as **everything-together.txt**. 




```bash
cat *.txt > everything-together.txt
```

    


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



```bash
cat everything-together.txt | head -50
```

    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    


* This can be very useful if you need to combine a large number of smaller files within a directory so that you can work with them in a text analysis program.

Another wildcard worth remembering is **?** which is a place holder for a single character or number. 
* **Will not cover this wildcard now**
* We shall return to shell wildcards later - for now, note again that they are similar to but not excatly the same as the Regex we saw in the previous module.

### Deleting files - rm Command

Finally, onto deleting. 
* We won’t use it now, but if you do want to delete a file, for whatever reason, the command is **rm**, or remove.

Be careful with the **rm command**, as you don’t want to delete files that you do not mean to. 
* Unlike deleting from within your Graphical User Interface, there is no recycling bin or undo options. 
* For that reason, if you are in doubt, you may want to exercise caution or maintain a regular backup of your data.


The syntax for **rm** is the same as **cp and mv**: for example **rm gulliver.txt**

## Summary

Within the Unix shell you can now:

* use the command **mv** to rename and move files.
* use the command **cp** to create a file from an existing file.
* use the command **cat** to combine more than one file of the same file type.
* use the wildcards ***** and **?** as place holders that delimit which files are to be manipulated by a given an action.
* use the **rm** command to delete unwanted files.

#### Key points to remember:
* the shell is powerful
* the shell can be used to copy, move, and combine multiple files



```bash

```
