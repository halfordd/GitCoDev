# LESSON 1: Fundamental Operations with Git

Lecture notes on the fundamental local operations with Git. A hands-on lesson for introducing version control, tracking changes, and the tracking history. 
These notes contains the following pointers for the instructor:

* Numbers between `[]` are indicative of how much time should be spend in each topic or exercise to keep in track with the lesson [schedule.](schedule.md)
* The text in  **Instructor note** contain explanations or reminders for the instructor. For example:
    `````{admonition} Instructor's Note

    Ensure that all users have git and bash available at the start of the course.
    ````` 

````{card} 
Presentation 
^^^    

This contains general information about the lesson and illustrations for supporing the explanations of some of the concepts, and 

*[Collaborative software development](https://docs.google.com/presentation/d/1BucILQ9Osz_2tKYF3kF-c3uZFND8xfJ4/edit?usp=sharing)*
````

The key topic covered on this day are:

* What are Version Control and Git
* Git Command syntax and getting help
* Creating an Empty Repository
* Tracking Changes in Working Documents
  * With the Index
  * Tracking Directories
  * Ignoring and untracking files
  * Ignoring untracked directories
* Undoing changes
  * Undoing changes with the Index
  * Deleting and renaming tracked files and directories
* Sequencing changes into a history
  * Committing changes
  * Inspecting changes using the history
  * Undoing changes with the history
  * Marking the history with tags



## Episode 1: Git repositories for version control
**[ca 50 min total]** 

### 1.1.0 Welcome slides
**[10 min]**

### 1.1.1 Introduction to Git
**[10 min]**

* Create a directory for the course

```shell
    cd ~/Desktop/
    ls
    mkdir -p 2410-gitcodev/git
    ls
    ls 2410-gitcodev/
```
```shell
    cd 2410-gitcodev/git/
    ls
    pwd
```
* Check which shell is available 

```shell
    echo $SHELL
    echo
```

* Check installed version of Git

``` shell
    git
    git --version
    git version
```

### 1.1.2 Git Command Syntax and Getting Help
**[10 min]**

```shell
    git help
    git help help
    git config
    git config --list
```
```shell
    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    git config --global core.editor nano
    git config --global core.autocrlf input # false for Win
    git config --global init.defaultBranch main
    git config --list
    git help config
```
```shell
    git help glossary
    git help -g
```

### 1.1.3. Creating an Empty Reposiory
**[10 min]**

````{admonition} Instructor's Note

    Here and throughout, it is possible to edit the file with an editor rather than appending
    lines with *echo*, however this will make the nature of the changes invisible in any
    gitautopush record.
````

``` shell
    pwd
    ls
    echo 'first line'
    echo 'first line' >lines.txt
    ls
```
```shell
    cat lines.txt
    echo 'second line' >>lines.txt
    cat lines.txt 
    git status
    git init
```
```shell
    ls
    ls -a
    ls -aF
    ls -aF .git
    ls
```

### 1.1.4. Q&A
**[10 min]**

### Short Break
**[10 min]**

## Episode 2: Tracking Changes in Working Documents
**[ca 75 min instruction + 20 min break]**

### 1.2.1 Tracking Changes with the Index
**[10 min]**

```shell
    git status 
    git add lines.txt
    git status 
    ls -a .git
    git diff lines.txt
```
```shell
    echo 'third line' >>lines.txt
    cat lines.txt
    git diff lines.txt
    git status 
    git add lines.txt
```
```shell
    git status 
    git add lines.txt
    git status 
    git diff lines.txt
```


````{card} 
Exercise 1 --- Tracking changes with the Index
**[5 min]**
^^^    

```{include} exercises/L1-ex01.md
```

```{dropdown} Answers

    [No answers yet]

```
````

#### Tracking Directories
**[10 min]**

```shell
    mkdir directory
    ls
    ls -F
    git status 
    touch directory/emptyfile.txt
```
```shell
    ls -R
    ls -RF
    git status 
    git status -u
    git help status
```
```shell
    git add directory
    git status
```

### 1.2.2 Not Tracking and Stop Tracking
**[10 min]**

```shell
    history
    history 20
    history 20 >history.log
    cat history.log 
    git status
```
```shell
    echo '*.log'
    echo '*.log' >.gitignore
    git status
    ls -a
    ls -aF
```
```shell
    git add .gitignore
    git status 
    echo 'lines.txt' >>.gitignore
    cat .gitignore
```
```shell 
    git status 
    git add .gitignore 
    git status 
```
#### Ignore Untracked Directories
**[10 min]**

```shell
    touch directory/trackme.txt
    touch directory/donttrackme.txt
    ls directory/
    git status 
    echo 'directory' >> .gitignore
```
```shell
    cat .gitignore 
    git status
    echo '!directory' >> .gitignore
    cat .gitignore 
    git status
```
```shell 
    cat .gitignore 
    echo 'directory' >>.gitignore
    cat .gitignore 
    git status 
    git help gitignore
```
```shell
    git status 
    git add .gitignore 
    git status 
```
```shell
    git rm --staged directory/emptyfile.txt
    git rm --cached directory/emptyfile.txt 
    git status 
    ls -FR
```


````{card} 
Exercise 2 --- Stop tracking Changes in a File
**[5 min]**
^^^    

```{include} exercises/L1-ex02.md
```

```{dropdown} Answers

    [No answers yet]

```
````

### Longer Break
**[20 min]**

### 1.2.3 Undoing Changes with the Index
**[10 min]**
```shell
    cat lines.txt 
    echo 'fifth line' >>lines.txt 
    cat lines.txt 
    git status 
    git diff lines.txt
```
```shell
    git restore lines.txt
    cat lines.txt 
    git status 
    git diff lines.txt
    git restore lines.txt
```
```shell
    cat lines.txt 
    git status 
    echo '!directory' >>.gitignore
    ls
    git status 
```
```shell
    git status -u
    git add directory/trackme.txt 
    git status -u
    git add directory/donttrackme.txt 
    git add directory/emptyfile.txt
```
```shell 
    git status 
    git add .gitignore 
    git status 
```

### 1.2.4  Deleting and renaming tracked files and directories
**[10 min]**

```shell
    git rm --cached directory/donttrackme.txt 
    git status 
    rm directory/
    rm -r directory/
    ls -FR
```
```shell
    git status 
    git restore directory
    git status 
    ls -FR directory/
    touch directory/donttrackme.txt
```
```shell
    git status 
    git rm directory
    git rm -r directory
    git status 
    git rm -rf directory
```
```shell
    git status 
    ls -FR directory/
    git restore directory
    git status 
    git status -u
```
```shell
    mv directory/donttrackme.txt directory/trackne.txt
    git status -u
    # use the command `git mv <oldname> <newname>`
    # lines.txt Lines.txt
    git status -u
    git mv lines.txt Lines.txt
    git status -u
```

````{card} 
Exercise 3 --- Renaming Tracked Files
**[5 min]**
^^^    

```{include} exercises/L1-ex03.md
```

```{dropdown} Answers

    [No answers yet]

```
````

## Episode 3: Organizing Tracked Changes in a History
**[ca 75 min + 10 min break]**

### 1.3.1 Commiting Changes with a Configured Identify and a Message
**[10 min]**

```shell
    cat Lines.txt 
    git diff
    git status 
    git commit -m 'Add first four lines' Lines.txt
```
```shell
    git status 
    git log
```


`````{card} 
Exercise 4 --- Commit Changes in a Tracked File
**[5 min]**
^^^    

````{include} exercises/L1-ex04.md
````

````{dropdown} Answers    
```shell
    git status 
    git commit -m 'Add .gitignore' .gitignore 
    git status 
```
```shell
    rm -r directory  # to keep things clean
    git status 
    ls
    git log
```
````
`````


`````{card} 
Exercise 5 --- Follow the state of the repository in the commit routine
**[5 min]**
^^^    

````{include} exercises/L1-ex05.md
````

````{dropdown} Answers    
```shell
    # Procedure for exercise 5
    echo 'fifth line' >>Lines.txt 
    cat Lines.txt 
    git status 
    git add Lines.txt 
    git status
```
```shell 
    git commit -m 'Add fifth lines' Lines.txt 
    git status 
    history
    git log
```
````
`````

### 1.3.2 Inspecting Changes Using the History


`````{card} 
Exercise 6 --- Follow the state of the index in the commit routines
**[5 min]**
^^^    

````{include} exercises/L1-ex06.md
````

````{dropdown} Answers    

```shell
    # procedure for exercise 6
    git status 
    git diff
    echo 'sixth line' >>Lines.txt 
    git diff
    git add Lines.txt
```
```shell 
    git diff
    git diff Lines.txt
    git commit -m 'Add sixth line' Lines.txt 
    git diff
    git log
```
```shell
    git log --oneline
    git status 
    echo 'seventh line' >>Lines.txt 
    git diff Lines.txt
    git add Lines.txt
```
```shell 
    git diff Lines.txt
    git status 
    git log --oneline
    git diff HEAD Lines.txt
    git diff e278702 Lines.txt
```
```shell
    git diff HEAD~1 Lines.txt
    git log --oneline
    git diff 7f2ca Lines.txt
    git diff HEAD~2 Lines.txt
    git diff HEAD~3 Lines.txt
```
```shell
    git diff HEAD~7 Lines.txt
    git diff Lines.txt
    git diff HEAD~3 Lines.txt
    git diff HEAD HEAD~1 Lines.txt
    git diff HEAD~1 HEAD Lines.txt
```
```shell
    git diff HEAD~4 HEAD~2 Lines.txt
    git diff HEAD~3 HEAD~2 Lines.txt
    git log
    # 
    pwd
```
```shell
    git status 
    git log --oneline
    git diff Lines.txt
    git diff HEAD Lines.txt
    git diff HEAD~1 Lines.txt
```
```shell
    git diff HEAD HEAD~1 Lines.txt
    git diff HEAD~1 HEAD Lines.txt
    diff HEAD HEAD Lines.txt 
    git diff HEAD HEAD Lines.txt 
    git diff HEAD~2 HEAD~2 Lines.txt
```
````
`````

###Short break
**[10 min]**

`````{card} 
Exercise 7 --- Explore the changes recorded in the history
**[5 min]**
^^^    

````{include} exercises/L1-ex07.md
````

````{dropdown} Answers    
```shell
    # No answers yet
```
````
`````

> Exercise 8 is an optional exercise about [comparing differences in the history.](./exercises/L1-ex08.md)


### 1.3.3 Undoing Changes with the History
**[10 min]**

````{note}
This topic involves using `git restore`. Actual commands are missing.

**TODO**:  Fill out detail in this section
````

### 1.3.4 Marking the History Using Tags
**[10 min]**

* Lightweight tags

```shell
    git log --oneline
    git tag 'hey'
    git log --oneline
    git log
```
```shell
    git tag 'hey' HEAD~1
    git tag 'hey2' HEAD~1
    git log --oneline
    git tag 'hey3' HEAD~5
    git tag 'hey4' 87ab7b6
```
```shell 
    git log --oneline
    git diff HEAD HEAD~1 Line.txt
    git diff HEAD HEAD~1 Lines.txt
    git diff hey hey2 Lines.txt
    git log --oneline
```
```shell
    git diff hey hey2 Lines.txt
    echo 'eighth line' >>Lines.txt
    cat Lines.txt 
    git status 
    git add Lines.txt
```
```shell 
    git status 
    git commit -m 'Add eighth line' Lines.txt
    git log --oneline
    git tag -d hey1
    git tag -d hey4
```
```shell
    git log --oneline
    git diff hey hey4 Lines.txt
    git log --oneline
    git tag -d hey2
    git tag -d hey
```
```shell
    git tag HEAD~4 v1
    git tag v1 HEAD~4
    git log --oneline
    git tag v2 HEAD~3
    git tag v3 HEAD~2
```
```shell
    git log --onelein
    git log --oneline
    git tag v4 HEAD~1
    git tag v5 HEAD
    git log --oneline
```


`````{card} 
Exercise 9 --- Add lightweight tags to the history
**[5 min]**
^^^    

````{include} exercises/L1-ex09.md
````

````{dropdown} Answers    
```shell
    # no answers yet
```

````
`````

* Annotated Tags

```shell
    git tag -a
    git tag -a -m 'First annotated tag' 
    git tag -a -m 'First annotated tag' TAG1
    git log --oneline
```
```shell
    git tag
    git show
    git show HEAD~1
    true
```

## Wrap Up
**[10 min]**

```{note}
Give a short wrap up about what has been learned.
```
