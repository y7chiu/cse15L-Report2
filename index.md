# Lab Report 2 - Servers and Bugs
----------------------------------
Hi!

This is my CSE15 Lab Report 2! My name is Yi-Chan(Frankie) Chiu.

Today, I am going to talk about the `Servers and Bugs`!

# Part 1 : StringServer

Write a web server called `StringServer` that supports the path and behavior described below. It should keep track of a single string that gets added to by incoming requests.

> **This is my code**

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("%s", str);
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    str += parameters[1] + "\n";
                    return String.format("%s", str);
                }
            }
            return "404 Not Found!";
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

> **After fininshing coding, using below code to type into the terminal:**

```
javac Server.java StringServer.java
java StringServer [anynumber]
```

> **We will get the weblink, as below. We will see that there are blank inside the website. We have to add some words into the weblink.**

<img width="1095" alt="截圖 2023-04-22 16 27 01" src="https://user-images.githubusercontent.com/130111605/233811767-fd22cef2-7715-4c88-aa3c-59252942a9ff.png">


> **Add `/add-message?s=[any string]` and we will see that the website present the string we type!**

<img width="1210" alt="截圖 2023-04-22 16 27 44" src="https://user-images.githubusercontent.com/130111605/233811828-dd8ab57b-beb6-4fb9-be27-681b023178ff.png">

> **Add `/add-message?s=[any string]` again and we will see that the String we type again goes into the next line**

<img width="1120" alt="截圖 2023-04-22 16 28 13" src="https://user-images.githubusercontent.com/130111605/233811945-bdfdba50-f3a4-4a25-b28c-4f24a3316d72.png">

> * Which methods in your code are called?

I used Contains method, String format mehtod, eqauls method.

> * What are the relevant arguments to those methods, and the values of any relevant fields of the class?

As we can see, I set the initial string into "", and after the code finding the key word `/add-message` it will goes into the if-else loop, so this is why the string can print out as the string format I prefer. (The String in the string format is `%s`.

> * How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

```
if (url.getPath().contains("/add-message")) {
String[] parameters = url.getQuery().split("=");
```

These two codes are the key point that could change the url words into what the assignment asked. The handler is going to catch the `args`. When we get the url fix to whatever we want, the url will go into the if-else statement just like filter, once the conditional code get what they want for specific string, for this example is `"/add-message"`. THe code will go into the next step. This is the time we get add whatever we want after adding **=** to make the assinment complete.





----------------------------------------------------------------------------------------
# Part 2

I choose the ArrayExamples and ArrayTest from lab 3 to find out the symptoms and bugs:

**PROVIDE:**

> A failure-inducing input for the buggy program, as a JUnit test and any associated code

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
----------------------------------------------------------------------------------------
> An input that **doesn’t induce a failure**, as a JUnit test and any associated code

```
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
}
```

----------------------------------------------------------------------------------------
> The `symptom`, as the output of running the tests 

<img width="1028" alt="截圖 2023-04-20 23 04 31" src="https://user-images.githubusercontent.com/130111605/233553295-a58b231c-4e54-44a6-97e1-c6b4b211d314.png">

----------------------------------------------------------------------------------------
> The `bug`, as the before-and-after code change required to fix it

**Before:**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

**After:**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[0];
      arr[i] = arr[arr.length-i-1];
      arr[arr.length-i-1] = temp;
    }
  }
```

As we can see, for the reverse, we need **temp** to be the temporary place to store the data, which cannot directly use the array index to change the value as the original code did. While reaching the middle length of the array, it is like the mirror that we know the first half part, the second part will automatically know it by setting the arr[arr.length-i-1] to arr[i].

----------------------------------------------------------------------------------------
# Part 3
In these two weeks, I learned lots of things related to the website acees or using remote access the website by using `scp`. For the `scp` git command, orignially, I did not know that we should first log out from our **course specific account** so that we can access it. Also, I truely learned that how to identify the weblink in the real operating lab. In the course, it is easy to identify it because there are some hints to follow. However, the lab can make me understand the problem what I do not understand in the practical lab. For example, in the lab, me and my partner did not know what is the order of looking the String after `?` sign in the weblink. The lab makes me understand lot of things I did not know before.

----------------------------------------------------------------------------------------
-LAB REPORT 2 END-


