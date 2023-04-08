# Lab Report 1 - Remote Access and FileSystem

This tutorial documents my (rak007@ucsd.edu) process of logging into my course-specific account on `ieng6` on Windows. 

## Installing VS Code

As we use the terminal in VS Code for Remote Access, we were required to download VS Code. 
If the user is using Windows, the user also had to download Git Bash, in order to use Git Bash in terminal. 
However, as I already had VS COde from CSE 11 with Professor Cao, and Git Bash from personal projects, I did not have to separately download either installer.

Below is a picture of VS Code running on my Windows computer. 
![Image](image1.png)

## Remotely Connecting

### Creating a Git Bash Terminal

We then had to create a Git Bash terminal in VS Code. 

I first started by opening a terminal, then opening the command pallete with `Ctrl + Shift + P`. I typed in and clicked on 'Select Default Profile', then selected 'Git Bash' in the options displayed. 

![Image](image2.png)

![Image](image3.png)

By then clicking on the `+` button and clicking on the 'bash' option, I was able to add a Git Bash terminal in VS Code. 

![Image](image4.png)

Using the side panel on the right, I was able to toggle between the two terminal types as needed. This tutorial will only use the Git Bash terminal for the Remote Access. 

![Image](image5.png)

### Using SSH to Connect Remotely

In the Git Bash Terminal, we connect to the server by inputting the following command below:

        $ ssh cs15lsp23nw@ieng6.ucsd.edu

where the username `cs15lsp23nw` is my CSE15L specific username. Sometimes, one may receive a prompt that looks as follows:

<pre><code>The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?</pre></code>

In this case, the user can just input `yes` into the terminal, then proceed to input their CSE15L password into the prompt.

![Image](image6.png)

BY doing that, I was able to successfully login to the server and proceed to the login terminal, which looks like below.y
![Image](image7.png)

## Trying Some Commands

Below are the server terminal results after runing a few different directory commands. 

        [cs15lsp23nw@ieng6-202]:~:$ ls

![Image](image8.png)

- `ls`, short for 'list directory', shows the content files and directories contained in the current or specified directory. As no path name is given after `ls`, all contents of the current directory is shown, with the only thing shown being a directory labeled `perl5`.

        [cs15lsp23nw@ieng6-202]:~:$ ls -a

![Image](image9.png)

- In `ls -a`, the `-a` indicates a specific option - in this case, the option to show hidden files and directories within the current or specified directory. As no path is specified, all contents, both public and hidden, is shown for the current directory, including but not limited to `perl5`. 

        [cs15lsp23nw@ieng6-202]:~:$ ls -lat

![Image](image10.png)

- Here, `-lat` indicates three different options, with `-l` for displaying detailed information about the listed files/directories, `-t` for displaying the files in the order of last modified, and `-a` the same as before.

        [cs15lsp23nw@ieng6-202]:~:$ cd perl5
        [cs15lsp23nw@ieng6-202]:perl5:$ ls
        [cs15lsp23nw@ieng6-202]:perl5:$ ls -a

![Image](image11.png)

- The `cd` command, short for 'change directory', indicates for the terminal to move directories to the one specified. In this case, as we specified the relative path of perl5 within the current directory, the terminal moves to perl5 as current directory. The `perl5` directory is currently empty, as listing public and hidden contents yield no result. 

        [cs15lsp23nw@ieng6-202]:~:$ ls /home/linux/ieng6/cs15lsp23/cs15lsp23zz

![Image](image12.png)

- Here, we attempt to change directories to another user's directory. This fails, as we do not have permission to access the directories. 

        [cs15lsp23nw@ieng6-202]:~:$ cd /home/linux/ieng6/cs15lsp23/public 
        [cs15lsp23nw@ieng6-202]:public:$ ls

![Image](image13.png)

- We change directories to the `public` directory, located within the parent directory of our home directory. Listing all contents of `public` gives us various files and directories. We can use `cat` to print the contents as follows. 

        [cs15lsp23nw@ieng6-202]:public:$ cat hello.txt

![Image](iamge14.png)



If no path is specified, the terminal automatically goes to the home directory 




