# Lab Report 5
## Debugging Post
*1. What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?*

**I am working on MacBook Pro(13-inch, M2, 2022) and have a macOS version 12.5. I am programming in Java using Visual Studio Code.**


*2. Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.*

**In the server that I am running I see the following error. It prints a series of errors pointing at parts of the JUnit tests saying that it cannot find the symbol.**
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/905f082b-21c6-4786-8192-a7558a2ebaaa)
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/a9cee1b7-2d07-4b8b-bdf1-932c2b718a9b)
**I expected to see some JUnit output and not a score of 2/4 and I did not expected to see any of the errors.**
**This output is an exampled of the desired output and works when using bash in the terminal**
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/4c0e581a-ad08-49f7-a647-9f480a7a8245)

*3. Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.*

**I initially ran the following code to start the server. (The last line was returned by the terminal).**
```
$ javac Server.java GradeServer.java
$ java GradeServer 4006
Server Started! Visit http://localhost:4006 to visit.
``` 
**When I click on the server and type into the following url in, the server produces the error**
```
http://localhost:4006/grade?repo=https://github.com/ucsd-cse15l-w23/lab3
``` 
**This is the full result that I see in the server.**
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/8b0884db-ac95-480b-8d2d-11933681bbb7)
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/8aaac6dd-6b6a-4b75-9248-69c8d76dd8ed)

## Bug Fix
**TA Response:**
There might be something wrong when you import JUnit. Can you show more of your grade.sh and TestListExamples.java. 

**Student Response:** 
Sure! Here is my grade.sh for context:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/37be173a-1df5-4947-bbfd-3e5119e62395)
Here is my TestListExamples.java for context:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/85205d1b-0eb0-4464-aa83-d7c44e9f70c7)

**TA Response:**
It doesn't have to do with your direct import of JUnit but it is related. The bug is on line 1 of grade.sh. Your code left out the .jar in .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar. Your code at that line should look like this:
```
$ CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2'
``` 

**Student Response:** 
That fixed it thank you!

## Set Up
The repository that was used was the [list-examples-grader](https://github.com/ucsd-cse15l-f22/list-examples-grader/blob/main/grade.sh) from Scenario 2. I specifically accessed the grade.sh, Server.java, GradeServer.java and TestListExamples.java. I only edited grade.sh. 
Before running the program, the directory structure looked like:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/f2956264-13f6-4701-969f-0ac97b0417a0)

After running the program, this is what my directory structure looked like:
![Image](https://github.com/Kav1770/cse15l-lab-reports/assets/126924884/1402093f-446d-4b16-980e-694a77644229)

**The contents of grade.sh before bug fix:**
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2'

rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

if [[ -f student-submission/ListExamples.java ]]
then
  echo 'ListExamples.java found'
else
  echo 'ListExamples.java not found'
  echo 'Score: 0/4'
fi

cp student-submission/ListExamples.java ./

javac -cp $CPATH *.java

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt

FAILURES=`grep -c FAILURES!!! junit-output.txt`

if [[ $FAILURES -eq 0 ]]
then
  echo 'All tests passed'
  echo '4/4'
else

  RESULT_LINE=`grep "Tests run:" junit-output.txt`
  COUNT=${RESULT_LINE:25:1}

  echo "JUnit output was:"
  cat junit-output.txt
  echo ""
  echo "--------------"
  echo "| Score: $COUNT/4 |"
  echo "--------------"
  echo ""
fi
``` 
**The contents of Server.java before bug fix**
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url) throws IOException;
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}

``` 
**The contents of GradeServer.java before the bug fix**
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
      System.out.println(System.currentTimeMillis() + "; just read: " + (char)c);
    }
    return result;
  }
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream out = p.getInputStream();
    return String.format("%s\n", streamToString(out));
  }
}
class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               return ExecHelpers.exec(new String[]{"bash", "grade.sh", parameters[1]});
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
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
**The contents of TestListExamples**
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;
class IsMoon implements StringChecker {
  public boolean checkString(String s) {return s.equalsIgnoreCase("moon");}
}
public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "z");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "d", "z");
    assertEquals(expected, merged);
  }
  @Test(timeout = 500)
  public void testFilterSingle() {
    List<String> input = Arrays.asList("Moon", "MOO", "moo");
    List<String> expect = Arrays.asList("Moon");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);
  }

  @Test(timeout = 500)
  public void testFilterMulti() {
    List<String> input = Arrays.asList("Moon", "MOO", "moon", "MOON");
    List<String> expect = Arrays.asList("Moon", "moon", "MOON");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);}
}

``` 
**The full command lines to trigger the bug is:**
```
$ javac Server.java GradeServer.java
$ java GradeServer 4001             
``` 
**The url I used in the browser was:**
```
http://localhost:4006/grade?repo=https://github.com/ucsd-cse15l-w23/lab3           
``` 
**The bug fix was to change line 1 in grade.sh to the following code**
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'           
``` 
## Reflection
Something cool I learned in the second half of the course was vim. I actually thought vim was rather interesting because I could do everything from the terminal without having to open VS code or the browser or another terminal. I thought it was interesting how you could put a number before a command and it would repeat that command that number of times. For example, the following code would go down 7 times. 
```
7j<enter>           
``` 
I also think its interesting that you can do commit your code to your git account and push it to your Github account(after some reconfiguration).
