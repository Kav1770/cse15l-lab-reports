# Installing VScode
First, go to the VScode website. Here is the link: [Link](https://code.visualstudio.com/). Hit the blue "Download" button in the top right corner of the website. Now click the downloads button that corresponds to your device. For example, if you have a Mac then click the bright blue button that says "Mac" on it. Once the .zip file is downloaded, click on it and open VScode.
You should see a screen similar to this except you may not see anything in recents:

![Image](https://user-images.githubusercontent.com/126924884/230634340-0774a3b0-15fb-408a-8f10-50925ae13eb9.png)

At this point you have succesfully installed VScode.

# Remotely Connecting
## Accessing Your CSE 15L login
First you will need to know your account for CSE 15L at the following link: [Link](https://sdacs.ucsd.edu/~icc/index.php). Now, you should see a screen that says "Account Lookup" at the top. ![Image](https://user-images.githubusercontent.com/126924884/230638434-9ad063dd-b6f7-4e87-b827-693171a78478.png)

For the box titled "Username", put your student Username for TritonLink. For the box titled "Student ID", put your PID. Then hit submit. You should see a screen titled "Account Lookup Results" and under "Additional Accounts", you should see a button called "cs15lsp23zz" (where zz is different for each student). Now copy "cs15lsp23zz" and click the button. There should be a yellow box with a blue link called "Global Password Change Tool" and click the link. Now you should see a page title "Global Password Reset." Under "Student, AX, or Course-Specific Student Accounts", click the "Proceed to the Password Change Tool" link. Now in the gray box, in the box under "Enter your username:" type in the username that you copied(AKA "cs15lsp23zz") and push continue. Then push "I want to reset my course-specific account password" link and authenticate with Duo. WHen it asks to confirm your email address click the "yes" button. Then you should see a screen titled "Thank you. We sent you an email." In your email, there should be an email about the password reset. Click the link that says "UC San Diego Password reset page." Then enter your new password and click change your password.

## Connecting
if your are on windows install git for Windows and git bash for VScode at the following links:
link: [Git for Windows](https://gitforwindows.org/)
link: [Git Bash for VScode](https://stackoverflow.com/questions/42606837/how-do-i-use-bash-on-windows-from-the-visual-studio-code-integrated-terminal/50527994#50527994)

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

# Trying Some Commands

