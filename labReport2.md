# Lab Report 2
## Part 1 - String Server 
The following is the code in my StringServer.java file.
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler{
  String strs = "";

  public String handleRequest(URI url){
    if(url.getPath().equals("/")){
        return strs;
      }
      else{
        return strs;
      }
      }
      
    
    if (url.getPath().contains("/add-message")) {
      String[] query = url.getQuery().split("=");
      if(query[0].equals("s")){
        strs += query[1] +"\n";
        return strs ;
      }
      else{
         return ("Error 404: Not Found!");
       }
    }
    else{
      return("Error 404: Not Found!");
    }
  }
}
class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
 }
```
This code when started will say "Server Started! Visit http://localhost:4000 to visit."
When you initially visit this link you will see a blank screen like the following image:
![Image](https://user-images.githubusercontent.com/126924884/233493870-8b4cf738-3b35-405f-83d6-6908a2499260.png)
Your code ran the main method which takes input from the terminal. The method turned terminal input into a port and ran: **Server.start(port, new Handler());**
This starts the server and creates a new Handler which runs handleRequest every time you enter a url. HandleRequest takes the url that you entered as a URI and it checks the path. 

**Reminder: The Path part of the URL is after the domain(after the .com, .org, .gov, .edu, and etc). and a ?.**

Currently, the **url** is *http://localhost:4000/* and the **path** is just "/". This means that the url is currently at the root and will print strs. However since nothing has been add to the **string strs** and strs was only initialized as an empty string when a new Handler was created, when strs is returned by handleRequest, nothing is appears. 

![Image](https://user-images.githubusercontent.com/126924884/233496634-3d989536-1b98-4706-bb7c-4ed62c250e94.png)
Now we have input the following URL into handleRequest: *localhost:4000/add-message?s=hello* and the path is "add-message". The server continue and handleRequest will be rerun with the new URL as the parameter. Since the path contains "/add-message", the program splits the query into an array with "=" being the delimiter.

**Reminder: The Query part of the URL is anything after the ? but before a #.**

In this case, Since we do not have a "#" in the url, the query is "s=hello" which is split into "s", "hello" and saved into the **query variable**. Since the first element is "s" then the second element("hello") is added to the string variable **strs** along with a "\n" to start a new line. Then when strs is returned by handler, **hello appears on the server!"

![Image](https://user-images.githubusercontent.com/126924884/233498282-c7c46a81-76cf-4d84-9e73-f286c08d22c7.png)
Now we have input the following URL into handleRequest *localhost:4000/add-message?s=how%20are%20you*.

**Note: The %20 are substituting for spaces so even though localhost:4000/add-message?s=how are you' was input, it turned into localhost:4000/add-message?s=how%20are%20you, so I will use %20 and spaces interchangeably.***

The path still contains "add-message", so the program will split the query("s = how%20are%20you") into "s", "how are you" and save it into **the variable query**. Since the first element is "s", the second element is added along with a "\n" to strs. 
However, the **server has not been reset** so strs still contains "hello\n" from the last URL, so strs becomes "hello\nhow are you\n" which when returned results hello and how are you appearing on the server on different lines.  

## Part 2 - Debugging 
The following code is part of ArrayExamples and is meant to take an input array denoted by **arr** and return a new array with all of the elements from the input array but in reverse order.

```
oilknjhjvgcf
```

