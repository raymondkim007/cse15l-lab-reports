# Lab Report 5

This lab report will explore the process of debugging. More specifically, we will explore the pain TAs and course staff go through when trying to help students with debugging problems. 
<sub>god i hope i dont become a TA</sub> 

The process will be explored by simulating an EdStem post thread. The thread is entirely fictional, but was created to mimic what a real-life interaction would look like. 
The student's post and responses in particular were written to be especially painful for hyper-realism, and if you read carefully, you might notice the TA's slowly dwindling sanity and 
patience as the student stumbles through debugging. 

(If possible, please leave a comment on how accurate this simulation is.)

Each individual post/comment will be separated by a horizontal line. 

## Debugging Scenario
---
### Java Code Not Compiling
Author: Raymond Kim (_10 hours ago_)

> Hello. I'm currently working on the autograding script from lab 6/7, but I'm having trouble running it in the ieng6 server. 
> I pushed my local script in VS Code to a GitHub repository. 
> The script works fine on my computer, but when I clone the repo into ieng6 and try to run the bash script, the Java files don't compile. 
> 
> I've attached a screenshot below of what the problem looks like. 
> 
> I first thought it was a typo, or the file didn't properly get pushed, but as far as I can tell, the script is identical to my local copy. 
> Please help.

![Image](/Report5/lab5_image1.png)

---
Author: AwesomeTA1 (_6 hours ago_)
> Hi Raymond! I'm going to need some more details before I help you. Could you answer the following questions for me?
> - What operating system is your local computer running, and what version?
> - Could you link the GitHub repository where your original script is located, and the GitHub repo you used to test the autograder?
> - Could you type the specific commands you included that got you to the error shown in the screenshot?
> - Could you post the entire error code, either as text or as a screenshot?

---
Author: Raymond Kim (_4 hours ago_)
> My laptop is running Windows 11 Home 64-bit. The GitHub repo link is [here](https://github.com/raymondkim007/grader-review-raymondkim007).
> The student submission example is this one: https://github.com/ucsd-cse15l-f22/list-methods-lab3. 
> 
> The commands are listed in order below. 
> 
> `ssh cs15lsp23nw@ieng6.ucsd.edu`
> 
> `git clone https://github.com/raymondkim007/grader-review-raymondkim007`
> 
> `cd grader-review-raymondkim007`
> 
> `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3`

---
Author: AwesomeTA1 (_4 hours ago_)
> Please post the full error code as well. 

---
Author: Raymond Kim (_3 hours ago_)
> oh yeah sorry here it is

![Image](/Report5/lab5_image2.png)
![Image](/Report5/lab5_image3.png)
![Image](/Report5/lab5_image4.png)
![Image](/Report5/lab5_image5.png)

---
Author: AwesomeTA1 (_3 hours ago_)
> The first line of your error code states the following: `TestListExamples.java:1: error: package org.junit does not exist`. 
> This means that when compiling the relevant Java files, you didn't use the correct classpaths to link the JUnit dependencies. 
> 
> The ieng6 server uses Linux instead of Windows, whereas your code for the Java classpaths uses Windows syntax. 
> I'm guessing the ieng6 server couldn't read the classpaths correctly, which is why the JUnit package doesn't exist.
> Could you try switching to Linux syntax and see if it fixes the problem?
> 
> For a final suggestion, you could try using the `CPATH` variable defined in line 1 to make compiling and executing Java files easier.
> Here, `CPATH` is already defined in Mac/Linux syntax, so it should be much easier to encorporate. 

---
Author: Raymond KIm (_2 hours ago_)
> What are classpaths?

---
Author: TiredTA1 (_2 hours ago_)
> As the name suggests, classpaths are paths to classes that you want to use in your Java code. 
> In this case, since we want to test with JUnit, we need to link the JUnit dependencies when compiling. 
> This is what the `-cp` in `java -cp` does. 
> However, the syntax for `-cp` is different for Windows from Mac or Linux. You can refer to [Week 3](https://ucsd-cse15l-s23.github.io/week/week3/) of labs 
> for further details. Hope this helped!

--- 
Author: Raymond Kim (_2 hours ago_)
> I can't find it. Can you just tell me what I have to change?

--- 
Author: TA_killmenow (_1 hour ago_)
> In your `grade.sh`, try changing the following two lines:
> 
> `javac -cp ".;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar" *.java`
> 
> `javac -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar *.java`
> 
> to these two lines:
> 
> `java -cp ".;../lib/junit-4.13.2.jar;../lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > grade-results.txt`
> 
> `java -cp .:../lib/junit-4.13.2.jar:../lib/hamcrest-core-1.3.jar org.junit.runner.JUnitCore TestListExamples > grade-results.txt`.

---
Author: Raymond Kim (_43 minutes ago_)
> Do I have to edit the bash script with vim?

---
Author: TA_idontcarejustdoit (_27 minutes ago_)
> You can use vim and push to the GitHub repo, or edit the GitHub file directly. 
> Generally using vim is simpler, and you can practice GitHub pushing for review!

---
Author: Raymond Kim (_10 minutes ago_)
> The changes worked. Thank you!
---

### Further Information

Regarding the scenario above, the student was working on his autograder bash script `grade.sh` for labs week 6 and 7. 
The file structure for that lab is as follows:
- (dir) list-examples-grader
  - (dir) grading-area
  - (dir) lib
    - hamcrest-core-1.3.jar
    - junit-4.13.2.jar
  - (dir) student-submission
  - grade.sh
  - GradeServer.java
  - Server.java
  - TestListExample.java

The entire bash script for `grade.sh` before editing is shown below:

    CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

    rm -rf student-submission
    rm -rf grading-area

    mkdir grading-area

    git clone $1 student-submission 2> /dev/null
    echo 'Submission Cloned'

    # check submission for correct file

    student_file=`find student-submission -name ListExamples.java`
    if ! [[ -f $student_file ]]
    then 
        echo "Student submission not found"
        exit
    else 
        echo "Student submission found. Path: $student_file"
    fiRe

    # copy all relevant files to grading-area
    cp $student_file TestListExamples.java grading-area/

    # compile Java files
    cd grading-area
    javac -cp ".;../lib/hamcrest-core-1.3.jar;../lib/junit-4.13.2.jar" *.java
    if [[ $? -eq 1 ]]
    then 
        echo "ERROR: Java file cannot be compiled. Exit code 1"
        exit
    fi

    # run JUnit tests
    echo "Running JUnit tests..."
    java -cp ".;../lib/junit-4.13.2.jar;../lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > grade-results.txt
    grep "Tests run" grade-results.txt > fail-results.txt
    grep "OK" grade-results.txt > succ-results.txt

    failcheck=`wc fail-results.txt`

    echo "Tests completed. Results shown below:"
    if [[ $failcheck == "0 0 0 fail-results.txt" ]]
    then 
        echo "All tests passed!"
    else 
        failmsg=$(head -n 1 fail-results.txt)
        testcnt=${failmsg:11:1}
        failcnt=${failmsg:25:2}
        succcnt=$(($testcnt - $failcnt))
        echo "Score: $succcnt / $testcnt"
    fi

And the command lines used to trigger the bug, and which lines to edit to resolve the bug, are detailed in the EdStem thread shown above. 

## Reflection

I had used GitHub numerous times before for my personal coding projects, but as the majority of my projects were done in PyCharm which automatically links with GitHub (albeit not that well), I was always fascinated by navigating the computer and GitHub solely through the command line. I remember first watching someone pull from and push to GitHub (back then, I didn't even know what those terms meant) soley through the command line, and it was like watching magic. To be able to not only do it myself, but understand what each word means and how GitHub works in general is a huge lesson for me that I will continue using for the rest of my coding journey. The more I progressed throug the second half of this quarter, the more I felt like the command line was an immensely powerful tool that I was underutilizing until now. Overall, I feel like CSE15L is an extremely practically useful course that places emphasis on not just functionality, but readability and efficiency, skills I assume would be crucial in a collaborative workplace. 
