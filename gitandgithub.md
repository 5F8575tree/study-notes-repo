# Git and Github

## Introduction to Git

### What is Git?

    - A version control system (i.e. tracks and manages changes to files)
    - Think of it like making 'save points' on a video game, that you can go back to if you mess up
    - You can also branch off and then later create hybrids of the parts of the branches that you like best
    - Created by Linus Torvalds in 1991, passed over to Hamano Jun in 2005

### Git is NOT Github

    - Git runs on your local machine, it doesn't even require internet. After you download it, you can use it
    - GitHub is a website that hosts Git repositories and stores them in the Cloud for collaborations

## Installations & Basics

    - Git is a command line tool (although there are GUI versions)
    - The command-line is often faster, but the user interface is awful and the learning curve is steep
    - You MUST know the command-line method, but GUI is nice for many projects

# Shortcut Keys!

    - git --version
    - git config user.name (not setting a user name, but checking)
    - If you do want to subsequently change your email (or name) with: git config --global user.email "new@email.address"
    - You can use the up/down arrows to cycle through previous commands
    - ls (lists contents of current directory)
    - start . (opens up the current directory in the GUI)
    - ls FolderName (lists contents of a specific FolderName) (FolderName/innerFolder)
    - clear (clears the terminal)
    - pwd (prints the current working directory)
    - cd FolderName (changes the current working directory to FolderName)
    - cd .. (changes the current working directory to the parent directory)
    - touch FileName.[ext] (creates a new file called FileName.[ext] in your current directory(unless you write the path from the current directory)) *You can make multiple files are once
    - rm FileName (deletes the file called FileName) *WARNING: This will delete the file permanently
    - mkdir FolderName (creates a new directory called FolderName in your current directory)
    - rmdir FolderName (deletes the directory called FolderName)
    - rm -rf FolderName (deletes the directory called FolderName and all of its contents)
    - mv FileName FolderName (moves the file called FileName to the directory called FolderName)
    - *As you can see, folders and filenames are best with just one word*
    - ls -a (lists all files and folders in the current directory (including hidden/.git files))
    - ls -l (lists all files and folders in the current directory with their sizes)
    - ls -al (lists all files and folders in the current directory with their sizes and their permissions (including hidden/.git files))
    -

# Git Basics: Adding & Commiting

## Git Repo

    - Every git repo is its own little history, they are not connect to other repos
    - You can create a new repo with: git init (without doing so, you are not really working with git, merely making files with git commands)
    - git status gives information on the current state of your repo
    - git init creates a new repo in your current directory

### What is in a git repo?

    - Once you have initiated a repo, git will track the directory and EVERYTHING inside it (including children, grandchildren, and so on...) If you imagine a GUI folder, the git repo would include that folder, as well as everything nested within it - folders, files, and all of their contents
    - Do NOT init a repo inside of another repo!!!!
    - That's why it is important to run git status before git init

## git Commit

    - Returning to the idea of 'saving' a video game before playing on, a commit is a saving checkpoint
    - The first commit should occur after initiating the repo
    - git commit -m "message" (this is the message that will be displayed when you commit)

### Commit Workflow

    1. WORK ON STUFF: Make new files, edit, delete, changes to your code, etc.
    2. STAGE: git add <fileName1> <fileName2> etc. (this adds all of the files in your current directory to the staging area) - it is a way of *grouping* specific changes together in preparation for a commit **IMPORTANT: It is good practise to group changes together in your commit rather than just commiting a mass update as a checkpoint**
    3. COMMIT: commits the changes you've made to the repo (with a message, for example, 'Converting all css to scss', 'Added branded navbar', or 'completed a URL-checking function')

    - Before you commit, you can run git status to see what's in your staging area
    - git commit (on it's own will open a commit 'file' that you can fill out in VSCode)
    - git commit -m "Enter your message here"
    - Using git add . will add all changes to the staging area (so make sure they are all related to the same thing as best practise). Likewise with git add -a

### git log

    - Prints to terminal the history of commits including author, date/time, email, and message
    - q will exit the git log

### Commits In Detail

    - git-scm.com has the git documentation (it can be tricky to read, but there are SO many options for each git command and you will probably never use most and certainly will not remember them). The reference manual is really useful for this!

### Atomic Commits

    - Ideally, you want a commit to encompass a single change, feature, or fix. It should be focused on a single thing, else your project will be more difficult to maintain.
    - Also far easier for code reviewing!

### Writing Commit Messages

    - The message should be written in *present-tense imperative style*
    - It seems unnatural, but you want to write something like "Make new navbar" instead of "Made a new navbar", or "Create new file" instead of "Created a new file"
    - You should be concise and consistent, and as specific as possible
    - If it is just for your own project, feel free to use whatever you want ;-)

### Escape VIM

    - :wq
    - If you are wanting to add a message, first press i then type your message, then esc, then :wq

### Configuring VS Code as the Default Editor

    - git config --global core.editor "code --wait"
    - This will make git use VS Code as the default editor for commits

### Git Log Shorten Logs

    - git log --oneline
    - This makes the log view much shorter so that you can more easily reference the logs

### Committing with GitKracken

    - Open (new) repository > make changes to your project > on the right-hand side you can see the changes > click the stage button next to the changes > click the commit button > enter a message > click the commit button > gitkraken will open up and show you the changes you've made
    - GitKracken is like a cool-looking version of the VSCode extension for git, my preference is probably with VSCode as it is a balance between the terminal and GitKracken GUI

### Amend Commits

    - If you realise that, for example, you put a typo in your commit message, or grouped the wrong file into the commit, etc., you can use amend **But it only works on the last commit made**
    - git add <forgotten-file-name-if-applicable>
    - git commit --amend
    - Amend will then open up the git commit 'file' in VSCode and you can then edit the commit message

### .gitignore File

    - There are various things that you will want to add to your gitignore file, for example node_modules/ or .env files
    - You can even ignore anything that ends in a certain way by using an asterisk, e.g. *.[ext]
    - You can also ignore a specific file by using a full path, e.g. /path/to/file/to/ignore

## Branches

### What are Branches?

    - Each commit has a hash reference, and also references at least one parent hash reference (with the exception of the initial commit)
    - In real-life, you may be working with other developers doing other things to the code, and you may be trying separate things in your code (a new color scheme, plus fixing a bug somewhere). If all commits were lineal, you would keep breaking your code and making work impossible
    - Think of branches as creating separate versions of your code, and you can then merge them back together
    - Branches exist in isolation, so you can only break that specific branch
    - So, with the example above, you would create one branch for the new color scheme, and another branch for the bug fix task. Later on, you may then try a completely new branch for a design overhall as an experiment, which may be branched from your bug fix branch [in total, we now have 4 contexts: main/original, color scheme, bug fix > experimental design]

### The Master Branch

    - Simply the original branch. Nothing special beyond that, but you can use it as the 'official' definitely working, definitely keeping, branch
    - HEAD is a reference to a branch that is currently open
    - git branch (without any arguments) will list all branches (the branch with the asterisk is the current branch)

### Create a Branch

    - git branch <branchName>
    - A branch name shouldn't include any spaces and should be very concise, yet informative (e.g. 'new-color-scheme')
    - Creating a branch does NOT automatically switch you to that branch
    - git switch <branchName>
    - git switch -c <branchName> (this will create a branch AND switch you to it)
    - If you attempt to switch to a different branch without committing or stashing your changes, you will be forced to do so (unless the changes you have made do not conflict with any other branch, in which case the changes will come with you to the new branch! This is mainly the case with adding a new file or new code, since this won't 'conflict' with any other branch)

### git checkout for Switching Branches?

    - git checkout <branchName>
    - It switches branch, but it does a LOT more than git switch

### Deleting & Renaming Branches

    - git branch -d <branchName> (this will delete the branch)
    - git branch -m <branchName> <newBranchName> (this will rename the branch)
    -
