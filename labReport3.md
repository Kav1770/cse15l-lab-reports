# Lab Report 3
## Downloading /technical files
Remotely connect and login into your ieng6 account. Then open this [link](https://github.com/ucsd-cse15l-s23/docsearch). Click the Fork button in the top left. Now click on the green button labelled "<> Code". Then under the HTTPS tab, you should see a url ending in ".git". Copy this code. Now time the following code into the terminal:
```
$ git clone https://github.com/exampleGithubUsername/docsearch.git
```
**Note: The link above is an example. Make sure to copy your own!**
Finally, make sure to go into docsearch then go into technical using cd twice. Now you are in the technical folder. If you ls, you should see 911report, biomed, government, and plos. 


## Researching Grep Commands
For reference, grep by itself searches a file or files for the given string, print matching lines. The following is the syntax for grep:
```
$ grep <string> <file>
```
We will now explore different command-line options for grep:

**Case Insensitivity**

grep -i makes the search case insensitive. 
For example, You could use grep normally to find the string "company" in the 911reports text files:
```
$ grep "company" 911report/*.txt
```
This returns the following:
![Image](https://user-images.githubusercontent.com/126924884/236640361-f84e4654-3be5-494a-9272-2c516021722c.png)
This is only looking for lowercase "company" and is clearly case sensitive.

However, if you were to use grep-i in the following way, it would return the image below:
```
$ grep -i "company" 911report/*.txt
```
![Image](https://user-images.githubusercontent.com/126924884/236640506-a5cb6eff-0b73-492c-969e-b9becf07ed2a.png)
As you can see, it now shows both "company" and "Company" in your search so it is not case sensitive.

Here is another example of grep -i vs grep normally in the plos directory. 
Using grep normally to find "humani" in plos returns the following:
![Image](https://user-images.githubusercontent.com/126924884/236640752-22a7de0f-62c1-4656-a1c9-6551e9eb10e2.png)
The above output only shows lowercase "humani".

However, using grep-i shows both lowercase and uppercase versions of the string.
![Image](https://user-images.githubusercontent.com/126924884/236640867-5b95f3ec-0e5c-46c9-be23-6f626356cb7e.png)

**Usecases:**
This command could be used in cases where the programmer is uncertain if the string that they are looking for has uppercase characters and just wants to search for all cases in which a string occurs in a file. Another case maybe that the programmer is certain that there are uppercase and lowercase versions of the string that is being searched for, and wants to find all cases of the string regardless of the case. This command is useful in decreasing the amount of commands that the programmer has to use by making the search case insensitive. 

Source for grep-i commands were the following links:
* [Wikibooks](https://en.wikibooks.org/wiki/Grep)
* [GeeksforGeeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

**Count Of Lines**

grep -c only prints the count of lines that match a "string". For example, in a file with "apple" "banana" "ripe" on different lines. Calling grep -c on the string "a" would print 2. 

**Usecases:**
This could be used if the programmer wants to know how many lines contain a certain string for each file in a directory without seeing all of the instances, so the programmer can specificially look in those files later on. Furthermore, the programmer may just want a count and not every single line that the string appears on as it can fill up the terminal very quickly. Ultimately this command allows the programmer to simplify the output of grep into a number rather than entire bodies of text.

When called directly on a directory it will print the count of the string for each .txt file.
```
$ grep -c "society" plos/*.txt
```
![Image](https://user-images.githubusercontent.com/126924884/236641283-fc55737f-d80a-42a0-90b7-1aae8d8034d5.png)
It continues to all of the files in the plos directory.  

This is really long. Why dont we use grep -c on plos/journal.pbio.0020156.txt specifically. 
```
$ grep -c "society" plos/journal.pbio.0020156.txt
```
This produces a much shorter output. 
![Image](https://user-images.githubusercontent.com/126924884/236641459-e1f34bba-f364-4f8c-b743-31a9a3701713.png)
This shows that in plos/journal.pbio.0020156.txt there are 10 instances of "society".

Source:
* [GeeksforGeeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)



**Does Not Match**

grep -v will print out the lines that do not contain a "string."

**Usecases:**
This can be useful if the programmer is looking for lines in a file that do not include a certain string. This can also be useful if the programmer is looking to see which file in a directory may not include a specific string and what line does not include that. Ultimately, this command is very useful to find parts of files that do not include a certain string.

Looking specifically in plos/journal.pbio.0020156.txt, we can see which lines do not contain the string "a". 
```
$ grep -v "a" plos/journal.pbio.0020156.txt
```
This produces the following results:
![Image](https://user-images.githubusercontent.com/126924884/236641630-84113734-d256-41fa-9729-dfe62e7bfe71.png)
These are the only lines in this file that do not contain the string "a". 

If we try the below code on the entire directory plos, we get the following results:
```
$ grep -v " " plos/*.txt
```
![Image](https://user-images.githubusercontent.com/126924884/236641730-f744a726-593f-4a3c-a05e-b6bb334e6f3d.png)

This continues for the rest of the files in plos. 
It shows that for every single file in plos, there is no line that does not contain " ". 

Source:
* [GeeksforGeeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

**List Of Filenames**

grep -l will print out the filenames of the files which matches but not the actual line.

For example, if we write the following command it should only print the filenames in plos which have a match to the string "society".
```
$ grep -l "society" plos/*.txt
```
This returns the following.
![Image](https://user-images.githubusercontent.com/126924884/236641956-f3859f7c-68b4-40a0-b127-fd8be0637388.png)
The above output is all of the filenames in plos that match the string but not what actually matched. 

Another example of this is if we write the following command it should only print the filenames in plos which have a match to the string "sanity".
```
$ grep -l "sanity" plos/*.txt
```

This returns the following:
![Image](https://user-images.githubusercontent.com/126924884/236642171-e4947017-4501-491b-a7f4-4b6b4f634678.png)
This shows that in plos there is only one file with the string "sanity". 

Source:
* [GeeksforGeeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)


