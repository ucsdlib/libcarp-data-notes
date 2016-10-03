# Git and Github Lecture Notes

Before Class

* setup slides. make sure i can have speaker notes for slides in separate window (print just in case
* setup shell (plain Terminal)

PreReqs
* Git: everyone type ‘git’ in command line. Make sure you get a response that isn’t a variant of ‘unrecognized command'
* Github: register for Github account if haven’t already. do it at the break, or if you need a mental break

_Switch to slides for Intro to Version Control_

## Intro to Version Control
Use Slides https://docs.google.com/presentation/d/1_8zDM_eZMF-Nkjvz35_gBAifJaoB_of54Q9CsbulPSc/edit?usp=sharing

## Setting Up Git
*Objectives: get system set up for proper attribution of your work*

* open shell (git bash, terminal) to your home folder `cd ~`
* verify `pwd`
* specify your name, this will be recorded in your commit history. So we know who did what
* `git config --global user.name “<username>"`
* specify email, also recorded in commits
* `git config --global user.email “<email address>"`
* email address tagged in commits. If concerned
  https://help.github.com/articles/keeping-your-email-address-private/
* Text Editor, used when committing if a message is not supplied on the command line. we’ll discuss more
* `git config --global core.editor "nano -w"`
* `git config --global core.editor “vim"`
* line endings. remember that conversation we had about how the wc command knows there’s a line ending? Well, different operating systems do this different, and it matters in git too. https://help.github.com/articles/dealing-with-line-endings/#global-settings-for-line-endings
    - mac/linux: `git config --global core.autocrlf input`
    - windows: `git config --global core.autocrlf true`
* `--global` means will apply for every command entered afterward. The majority of the time, you’ll use this. You’ll want the same text editor, and generally the same other config settings. Different user accounts example (work vs home)
* let’s check our settings (please do the same) `git config –-list`
* **CHECK IN** Who has everything set?
* Reminder: All the commands will be logged on the class **etherpad** as well.
* While I will try and go slow, if you get lost, `git help` and `git help <command>` is your friend.
* Discuss usage (`git status` every time something changes) it’s a very good habit to get into.
* _QUESTIONS?_

## Creating a Repository
Objectives: start tracking versions in a particular folder/directory (repository)

* start in home directory `cd ~`
* create directory and change directories
* `mkdir learning-git`
* `cd learning-git`
* tell git where to store old records and versions of file
* `git init`
* list contents: `ls`
* doesn’t look like anything changed. right? wrong.
* list everything (including hidden files) `ls -a`
* result is a subdirectory with information about project. you could think of it as a database for tracking all the repository changes. note: if this is removed, we don't have access to versioning anymore. be careful!
* ask status of project `git status`
* You can always run `git status` to check in and see what state your content is is
* the output also adds very helpful comments
* **CHECK IN** Who has a `learning-git` directory with that is now tracked by git?
* _QUESTIONS?_

## Tracking Changes
*Objectives: practice workflow (modify-add-commit), explain where information is stored*

* create new file: `nano basics.md` (.md is markdown file)
* you do not necessarily have to use the same editor as your `core.editor` setting. but in our case, they are probably the same
* add text
```
# Git Basics
* `git init` - creates a new git repository in the current folder
```
* In nano: `CTRL-X` will exit and prompt to save. Hit `Y` to save.
* `ls`
* `cat basics.md`
* show status of project: `git status`
* draw attention to "untracked files": there's something not being tracked
* add file: `git add basics.md`
* `git status` draw attention to "Changes to be committed": it's tracking, but the changes aren't recorded
* commit file: `git commit -m “document git repository initialize command"`
* commits record to history in .git, called a revision, with short identifier
* discuss good commits: brief (<50 characters), for more info, add empty line (adds in separate field)
    - think of log like narrative. NO ‘fixed typo’, ‘added new content’, ‘deleted old code'
* `git status`
* check history: `git log`
* lists all revisions in reverse chronological order: full identifier (relate to short identifier, same initial characters),
    - walk through commit content
* make another change (this is just one way): `nano basics.md`
* new bullet: ```* `git status` - I can use this anytime to see the current status of the repository"```
* Confirm changes: `cat basics.md`
* check status: `git status`
    - note ‘modified’ because this is a file git knows about that has changed, not an ‘untracked file’ this time
* look at differences with `git diff`. talk through the output of the diff
* do a `git commit` (intentionally forgetting to `add` first)
* _Question:_ why didn’t this work?
* add file: `git add basics.md`
* commit: `git commit -m "document git status command`
* look at `git log`
* _SLIDE: Committing Changes to Git challenge_
* _SLIDE: Git Staging Area_
* _SLIDE: Git Staging Area (multiple files)_
* Let’s watch the staging area a bit more closely and make another change `nano basics.md`
* new bullet: ```* `git add <file>` - places the file in the git staging area"```
* `git diff` (talk about what this shows)
* `git add`, `git status`, `git diff` (`git diff`, by default, doesn’t see a difference between what’s in the current directory and what is committed)
* To see the difference with the staging area (what's in our shopping cart) we type `git diff —staged`
* commit: `git commit -m “document git add command"`
* `git status`
* `git log` (look at history of commits)
* _SLIDE: Challenge: Tracking Changes_

## Exploring History
*Objectives: last thing before we dive into wonderful world of Github. identify and use Git commit numbers, compare versions, restore old versions*
* `git diff HEAD~1 basics.md` (remember head from commands yesterday? same thing here, head is the top of the repo)
    - note: we’re diffing against HEAD. when not specified, that’s what it runs against
* `git diff HEAD~2 basics.md`
* what if we want to see the differences between the previous two commits?
* `git diff HEAD~1..HEAD~2`
* we can also use the unique IDs for the commits to do the same thing. but honestly, unless you’re going back beyond a few versions, better of with `HEAD`
* If using a unique ID, you can just use the first 7 characters of the ID
* let’s see how we can restore an old version, you know in case we accidentally run a script that wipes out our source file 😃
* `> basics.md`
* `cat basics.md`
* `git status`
* we now have an “oh sh*t” moment. how can we get out file back the way it was?
* `git diff` (yep, there’s all the stuff we deleted)
* `git checkout HEAD basics.md`
* `cat basics.md`
* YAY! We have our previously committed file back
* we can go back farther as well for a file. HEAD~1, or we can use the commit ID. Had we committed that change accidentally, we could have used HEAD~1 to get us back to the previous version.
* note: easy accident is to forget to specify a file when checking out a commit
  * git will tell you that you are in a `detached HEAD` state. awesome huh.
  * DO NOT make any changes in this state. If it happens, do `git checkout master` to get back.
* _Questions?_
- _SLIDE: Recovering older versions of a file_
- _SLIDE: Exploring History_

## Remotes In Github
*Objectives: explain why remote repos, clone remote repos, push/pull*

* Ok, we’ve worked in isolation for a while, but it’s time to bring Github into the picture!
* You might hear Git and Github used interchangeably but they are different things. Git is the version control system itself. As we’ve already seen, we can do a lot on our own computer without having ever brought Github into the converstation. So, what’s Github?
* Github is the largest place on the internet that you can go to collaborate with collegues using the Git version control system. Is has most of the world's open source software available on it.
* Basically, it’s where your collegues are, or will be once you convince them to use git 😃
* Right now we’ve been working entirely locally on our repository.
* That’s OK, because it’s a DVCS. We have our local complete copy.
* But we want to share with our friends and collaborate, so let’s learn how to do that
* **Go to Github** - create `git-basics` repo_
* talk through all the options, including README, public vs private, .gitignore, license
* NO README, LICENSE, ANYTHING. No new files
* copy URL to clipboard use https
* `git remote add origin https://github.com/<username>/git-basics.git`
    - `origin` is an alias. it could technically be anything. but it is a convention widely used for referring to remote repos. Stick to it!
* let’s make sure that worked by looking at our remote
* Review remotes: `git remote -v` (v stands for verbose output. but we can always look that up in git help remote)
* let’s look at visual of what our setup is as it stands now
* _SLIDE: New Github Repository - Existing Project_
* `git push origin master` You will need to authenticate now with your GH username + password
    - this is a mouthful. explain.
    - look at a visual of what changed
* **CHECK IN** - Can everyone see their repository in Github?
* _SLIDE: Github Remote Repository Populated_
* The opposite action of pushing content to a remote repository is pulling updates from it. we do that with
* `git pull origin master` - Run it.
    - in this case, pulling has no effect since we’re already at the latest change
    - but, if a change had been made by a friend since our last pull, we would get those changes
* _SLIDE: Challenge Github GUI_
* _SLIDE: Push vs Commit_

## Collaborating (with Pull Requests and branches)
*Objectives: collaborate pushing to common repo*
* ok, we’re going to work on a shared repo now.
* pair up with your tablemate to collaborate with
- Each person lead the other to their git-basics repo on Github
    - demo this with class TA
- Fork the owner's repository into your own account (explain)
- `cd ~`
- Make a safe directiory to work in `mkdir collaborating-test`
- `cd collaborating-test`
- clone your forked repo into a new directory
- `git clone <repo>`
- `cd git-basics`
- do a `git status`.
- see how it says “On branch master”. By default all the changes we’ve been making are on the master branch. You can see this in Github too (show it)
- `git status`
- now we’ll add entries for push, pull, and fork
    - `nano git-basics.md`
    - add a bullet: ```* `git push <remote> <branch>` send changes in local
      repository to remote repository branch```
    - add a bullet: ```* `git pull <remote> <branch>` get changes from remote
      repository branch into local repository```
    - add a bullet: ```* Forking a repository - Create a complete copy of an
      existing Github repository to enable collaboration.```
    - `git add git-basics.md`
    - `git commit -m "documenting forking a repository and push/pull commands."`
    - `git push origin master` - Now look on Github
    - See how git asks us about a PR? Let’s do that and add proper information about our changes, and ask if we can merge our changes in master
* **CHECK IN** Do all collaborators have PRs?
* Owner - review the changes. You can make comments if you’d like to see anything different, @mention, you can add emojis and request changes.
* Merge the PR and delete the remote branch. (Why can we delete the remote branch?)
* Owner - do a `git pull origin master`
* **CHECK IN** Do you all owners have the collaboraits changes?
* SWITCH (IF THERE’S TIME) OR Do via a fork + PR
* **Questions?**
* _SLIDE_: Github at SIO
* _SLIDE_: Using Git: Alternatives to the command line
