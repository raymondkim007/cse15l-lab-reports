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

<pre><code>$ ssh cs15lsp23nw@ieng6.ucsd.edu</code></pre>

where the username `cs15lsp23nw` is my CSE15L specific username. Sometimes, one may receive a prompt that looks as follows:

<pre><code>The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?</pre></code>

In this case, the user can just input `yes` into the terminal, then proceed to input their CSE15L password into the prompt.

![Image](image6.png)

BY doing that, I was able to successfully login to the server and proceed to the login terminal, which looks like below.

![Image](image7.png)

## Trying Some Commands

Below are the server terminal results after runing a few different directory commands. 

<pre><code>[cs15lsp23nw@ieng6-202]:~:$ ls</pre></code>

![Image](image8.png)



