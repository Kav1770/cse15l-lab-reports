# Lab Report 1
## Installing VScode
First, go to the VScode website. Here is the link: [VScode](https://code.visualstudio.com/). Hit the blue "Download" button in the top right corner of the website. Now click the downloads button that corresponds to your device. For example, if you have a Mac then click the bright blue button that says "Mac" on it. Once the .zip file is downloaded, click on it and open VScode.
You should see a screen similar to this except you may not see anything in recents:

![Image](https://user-images.githubusercontent.com/126924884/230634340-0774a3b0-15fb-408a-8f10-50925ae13eb9.png)

At this point you have succesfully installed VScode.

## Remotely Connecting
**Accessing Your CSE 15L login**

First you will need to know your account for CSE 15L at the following: [Link](https://sdacs.ucsd.edu/~icc/index.php). Now, you should see a screen that says "Account Lookup" at the top. ![Image](https://user-images.githubusercontent.com/126924884/230638434-9ad063dd-b6f7-4e87-b827-693171a78478.png)

1. For the box titled **"Username"**, put your student Username for TritonLink. For the box titled **"Student ID"**, put your PID. Then hit submit. 
2. You should see a screen titled **"Account Lookup Results"** and under **"Additional Accounts"**, you should see a button called **"cs15lsp23zz"** (where zz is different for each student). Now copy **"cs15lsp23zz"** and click the button. 
3. There should be a yellow box with a blue link called **"Global Password Change Tool"** and click the link. 
4. Now you should see a page title **"Global Password Reset."** Under "Student, AX, or Course-Specific Student Accounts", click the **"Proceed to the Password Change Tool" link**. 
5. Now in the gray box, in the box under "Enter your username:" **type in the username that you copied(AKA "cs15lsp23zz")** and push continue. 
6. Then push **"I want to reset my course-specific account password" link** and authenticate with Duo. When it asks to confirm your email address click the "yes" button. Then you should see a screen titled "Thank you. We sent you an email." 
7. In your email, there should be an email about the password reset. Click the link that says **"UC San Diego Password reset page."** Then enter your new password and click change your password.

**Connecting**

If your are on windows install git for Windows and git bash for VScode at the following links:
* [Git for Windows](https://gitforwindows.org/)
* [Git Bash for VScode](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994)

Next open a terminal in VScode using either Ctrl/Command + ` or using the toolbar on the top left click Terminal then New Terminal menu options. 
Then use "ssh" in the terminal with the following line:
```
$ ssh cs15lsp23zz@ieng6.ucsd.edu
```
**Note: Do not include the $ in the terminal command and the zz are different for each student, thus you will have to use your own CSE 15L username**

you should get the following code in response:
```
$ ssh cs15lsp23zz@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 

```
This is a normal. Types "yes" and press the return or enter key on your keyboard.
Next it will ask for your password. Type in your password.
**Note: The password will not show as your are typing it so do not be alarmed**

If this program worked succesfully your should see something like the following:
![Image](https://user-images.githubusercontent.com/126924884/230695410-0cc36c98-12d6-4b9c-b310-69d8fe90599d.png)

Now we can start trying some commands on the remote server!

## Trying Some Commands
Here are some commands that you can try:
```
* pwd - will print the current working directory
* cd <path> - will change the current working directory
* cat <path> - will print the contents of the file of the path
* ls <path> - will list the folders on the current path
* mkdir "Name" - will create a new directory using "Name" at the current working directory
```
  
Some more commands which you can try are:
```
ls -lat
ls -a
cd ~
ls <directory>
```
  
For example:
![Image](https://user-images.githubusercontent.com/126924884/230696202-c817975a-624a-4e26-a9ab-74d6a069ba53.png)
**Note: I will be using $ to denote a terminal command so anything that does not have a '$' at the beginnning is printed by the computer. Also do not include $ in the terminal code.**

1. In this example, I checked the path using **pwd** and it returned the pathway on the remote computer:
```
$ pwd
/home/linux/ieng6/cs15lsp23/cs15lsp23hk
```

2. Then I checked what was in this folder using **ls**:
```
$ ls
perl5 
```

3. Then I used **ls – lat** and **ls –a** to look at the all files (including any hidden files) in the following way:
```
$ ls – lat
$ ls –a 
```
The functionality of these commands is displayed by the picture above but more specifically, ls –a prints all of the files (including any hidden files) and ls – lat prints all of these files as well along with some information about those files. 


4. Next I went into *perl5* with **cd** and checked the ls of the outer folder that I was just in and the pathway using **ls..** and **pwd**:
```
$ cd perl5
$ ls ..
perl15
$ pwd
/home/linux/ieng6/cs15lsp23/cs15lsp23hk/perl15
```
5. Then I tried accessing a directory called "Documents" by using cd in the following way: 
```
$ cd Documents
``` 
but that directory did not exist at the time so I kept getting **no such file or directory**.

6. I then tried using mkdir to make the Documents folder, but at first, I missused mkdir and used it by itself which resulted in an error. Then I used **mkdir Documents** and created a documents directory in perl15 and went into documents using **cd** and checked the path.
```
$ mkdir 
 mikdir missing operand
 Try 'mkdir --help' for more information
$ mkdir Documents
$ ls 
Documents
$ cd Documents
$ pwd Documents
/home/linux/ieng6/cs15lsp23/cs15lsp23hk/perl15/Documents
```

**To exit out of the server you can use the command "exit" or just Ctrl-D or you can open a new terminal using the instructions above.** 


