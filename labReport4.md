# Lab Report 4
## Logging into ieng6
First, I remotely connected to the ieng6 server by typing the following code:
```
$ ssh cs15lsp23hk@ieng6.ucsd.edu
```
(I performed this command from muscle memory). This displayed the following output:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/8dfbd762-8349-4ccd-86d4-d763a7e80e5e)
**Note: I was not prompted for my password because I was able to configure it so I would not need to.**

## Cloning your Fork
Next, I had forked the [lab7 repository](https://github.com/ucsd-cse15l-s23/lab7). Then, in order to clone the fork of lab 7, I went to the fork on my GitHub account and clicked on the green button labelled "<> Code". After clicking on it, I saw I drop down menu that looks like the screen shot below:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/58fb90a1-5ed0-4659-8df8-77ee1246147e)
I then clicked on the tab labelled "SSH" and copied the link.
Then I navigated back to the terminal and typed in the following code:
```
$ git clone git@github.com:Kav1770/lab7.git
```
This produced the following output:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/f70a302d-eda5-45fe-a9bc-6283ba573f15)
**Note: If this fork had been previously cloned on the same account make sure to delete it using rm -r lab7.**

## Running the Tests
Now, in order to determine if the ListExamples.java file passes all of the tests in the ListExamplesTests.java, we will use JUnit. I first navigated to the correct file by typing ls. This produced the following in the terminal: 
*"bash-for-quiz  docsearch  lab7  path-examples  perl5  stringsearch  tutor  wavelet"*

In order to go into lab7 and have access to the ListExamples.java and ListExamplesTests.java files, I then typed 
```
$ cd lab7
```
Then I pressed ls to check if I was in the right folder and it printed "ListExamples.java  ListExamplesTests.java  lib  test.sh".

Here is a screenshot of the above sequence:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/b4f7b1b2-59f5-473f-8d50-f2fd7dcb58a9)

Now that I know thet I am in the right folder, I typed in the following code which I got from the Monday Week 3 lecture notes. 
```
$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar ListExamples.java ListExamplesTests.java
$ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
```
This produces the following output:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/6957fb52-d19c-45be-95eb-7942156eac20)
This produces an error because there is a bug in ListExamples.java.
## Fixing the Code
I opened ListExamples.java in the terminal by typing the following code:
```
$ vim ListExamples.java
```
This takes me to the following screen. 
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/21189e84-8742-46af-82c9-de576590ca35)
It appears that there is a comment at the bottom of the code to change index1 to index2 that was never fixed. 
I pressed the following keys to fix the mistake:
```
$ 7j<enter>
$ xi2<esc>
$ :wq
```
**Note: I did not push the key '$'. I just put it there for ease of reading**
* I pushed **'7j'** together because 'j' by itself will go down one line but '7j' will go down 7 lines and looking at my cursor I saw that I needed to go down 7 lines from where I was.
* I pressed **'enter'** the terminal would know I only wanted to type '7j' and wouldn't wait for any other input. 
* I was directly on the number I wanted to delete. I pressed the **'x'** key to delete it.
* I pressed **'i'** to enter insert mode so I could edit the file and I pressed '2' to enter that number into the file.
* I pressed **'esc'** to exit out of insert mode.
* The I pressed **':wq'** to save the code and quit. 

This returned me to the normal terminal.

## Running the Tests(again)
To check if I had fixed the error. I pushed the arrow key 3 times and hit enter to access the search history for Junit. I pressed 3 times for the both lines:
```
$ javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar ListExamples.java ListExamplesTests.java
$ java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
```
I ended up with the following code. 
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/65526f25-14ef-4a63-b85f-21c3ec5881f4)
Clearly the bug is fixed since the tests ran succesfully.

## Committing and Pushing to your Account
Now we want to commit these changes and push them to our Gthub account so these errors won't happen again.
I typed the following in order to add the changes made in ListExamples.java to the staging area so it can be committed. Then I committed it using git commit. 
```
$ git add ListExamples.java
$ git commit -m "Bug Fixed"
```
**Note: -m is not necessary. Normally, it would take you into vim to type your commit message but I wanted to stay in the terminal since my message was short. (My commit message was "Bug Fixed"). **

This should output the following result:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/27fb817e-64ca-4d4a-a21e-597a00783006)

I have now successfully fixed an error in my code and committed the fix to my repository on my personal GitHub account, all without leaving my terminal!
