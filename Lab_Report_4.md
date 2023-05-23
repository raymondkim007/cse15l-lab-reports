# Lab Report 4 - Command Line Tasks

This lab report will explore using the command line to edit files within, and commit and push to, repositories on GitHub. 
We will be following the numbered tasks outlined in [Week 7 of Labs](https://ucsd-cse15l-s23.github.io/week/week7/#week7-lab-report), and will be using a forked repository of [CSE15L Lab 7](https://github.com/ucsd-cse15l-s23/lab7), which itself is essentially a copy of ListExamples and its related files from Lab 4. 

The numbered tasks are displayed below. 

1. **(Setup)** Delete any existing forks of the repository you have on your account
2. **(Setup)** Fork the repository
3. **(The real deal)** Start the timer!
4. Log into ieng6
5. Clone your fork of the repository from your Github account
6. Run the tests, demonstrating that they fail
7. Edit the code file to fix the failing test
8. Run the tests, demonstrating that they now succeed
9. Commit and push the resulting change to your Github account (you can pick any commit message!)

This lab report will be walking through steps 4~9 in detail. As a side note, a few prerequisites had to be completed in order to start step 4, including but not limited to the following:

- Creating an SSH Key in the local computer for logging into ieng6 from the local terminal
- Copying the SSH Key from the local computer to the ieng6 account (specifically `~/.ssh/authorized_keys`)
- Creating an SSH Key in the ieng6 account for authentication usage with GitHub
- Adding the SSH Key from the ieng6 account to the GitHub account

## Following the Steps

For all the key press descriptions below, all phrases inputted will be enclosed in square brackets \[ \], and all special characters (or individually typed characters) will be enclosed in angle brackets < >. 

### Step 4. Log into ieng6

![Image](/Report4/lab4_image1.png)

Keys Pressed: `[ssh cs15lsp23nw@ieng6.ucsd.edu]<Enter>`

The command run was the SSH login command for my account-specific ieng6 machine, using my CSE15L specific username `cs15lsp23nw`. Normally I would have to input my password afterwards once prompted, but because I had set up my SSH Key from my local host and added it to `~/.ssh/authorized_keys` beforehand, this is no longer necessary. This command connects me to the ieng6 remote server, where I will be cloning, editing files within, and pushing to the aforementioned GitHub repository. 

### Step 5. Cloning the GitHub fork

![Image](/Report4/lab4_image2.png)

Keys Pressed: `[git clone git@github.com:raymondkim007/lab7.git]<Enter>`

The command run was the `git clone` command that clones a given repository into a certain directory. As no specific directory was specified, the repository was cloned into the current working directory, with all files contained within a folder called `lab7`. The actual repository was inputted using the generated SSH Key from GitHub, which allows direct access and writing of repository data (cloning & pushing) from the command line and SSH. 

### Step 6. Running JUnit Tests - Fail

![Image](/Report4/lab4_image3.png)

Keys Pressed: 
- `[cd lab7]<Enter>`
- `<Ctrl + R>[javac]<Enter>`
- `<Ctrl + R>[java ]<Enter>`

The commands run included changing directories to `lab7`, compiling all Java files using the JUnit library dependencies stored in `lab7/lib`, then executing the class tester file `ListExamplesTests`. The terminal outpput shows one of the two JUnit tests in `ListExamplesTests.java` to fail. 

The commands for the last two steps of compiling and executing - `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` and `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` respectively - had already been used before from a previous test run, but was buried within the history. Using `<Ctrl + R>` allows direct access to the bash history to search previous commands. Using the queries `[javac]` and `[java ]` (with a space) allowed me to access the correct commands easily and efficiently without typing entire commands or classpaths. 

### Step 7. Editing the Java File

![Image](/Report4/lab4_image4.png)

Keys Pressed:
- `[vim ListExamples.java]<Enter>`
- `<r><2>`
- `<:>[wq]<Enter>`

The commands run included opening the Java file `ListExamples.java` using `vim` on the bash terminal, editing `index1` to `index 2`, then saving and exiting the `vim` editor. 

For the second step, the default cursor placement after entering the `vim` editor was already placed at the correct location - Line #44 Character #12 - so all I had to input was `<r>`, which replaces the currently selected character to whichever character is inputted next. The last step uses the colon command `:wq`, a combination of `:w` which writes to the file (saves it) and `:q` which quits the `vim` editor.

### Step 8. Running JUnit Tests - Pass

![Image](/Report4/lab4_image5.png)

Keys Pressed: 
- `<up><up><up><Enter>`
- `<up><up><up><Enter>`

The commands run is nearly identical to Step 6 - compiling all Java files using the JUnit library dependencies stored in `lab7/lib`, then executing the class tester file `ListExamplesTests`. The terminal output now shows that both JUnit tests passed. However, this time instead of querying the bash history with `<Ctrl + R>`, I used the `<up>` arrow to chronologically search the bash history. I had used the same commands only 3 command line inputs before, and so using the `<up>` arrow was faster. 

### Step 9. Commit and Pushing CHanges

![Image](/Report4/lab4_image6.png)

Keys Pressed:
- `[git add ListExamples.java]<Enter>`
- `[git commit -m "Fixed ListExamples.java"]<Enter>`
- `[git push origin main]<Enter>`

The commands run included adding the Java file `ListExamples.java` as one of the modified files to be tracked, committing the local changes with the commit message `"Fixed ListExamples.java"`, then pushing the local commit to the online GitHub repository. 

For the last step, `origin` refers to the remote repository. We can set this manually using `git remote add origin <URL>`, but in this case it is unnecessary as the origin is already set when cloning the GitHub repository with `git clone`. 
