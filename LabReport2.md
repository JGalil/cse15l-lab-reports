# Lab Report 3

# Part 1
Code for StringServer:

```Java
import java.io.IOException;
import java.net.URI;


class Handler implements URLHandler {
    String inputted = "";

    public String handleRequest(URI url) {

        if (url.getPath().equals("/")) {
            return inputted;
        }
        else{ 
            if(url.getPath().contains("/add-message")){
                String[] parameters = url.getQuery().split("=");
                String added = parameters[1];
                inputted += (added + "\n");
                return inputted;
            }
            else{
                return "404 Not Found!";
            }
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
![image](https://user-images.githubusercontent.com/122497361/215415467-eb95ba99-5edc-4e7d-acfc-0d93f8389a03.png)
For this message the following methods are called:
- handleRequest(http:localhost:4120/add-message?s=hello)
- this method then checks if there is a / in the path
- If there is, then it checks whether or not "add-message" is in the path
- In this case it is, so it returns the String following the "=" in the path and appends a "\n" character
- this makes sure that the next inputs are put in new lines
- In this case the String is "Hello"
- The String I made for inputs that appends the user input followed by a new line command changes values to "Hello\n"

![image](https://user-images.githubusercontent.com/122497361/215415926-e77e7768-2b89-46af-be3c-0c427e300c4a.png)
For this message the following methods are called:
- handleRequest(http:localhost:4120/add-message?s=hello)
- this method then checks if there is a / in the path
- If there is, then it checks whether or not "add-message" is in the path
- In this case it is, so it returns the String following the "=" in the path
- In this case the String is "World"
- Since there has already been an input, "World" is displayed on a new line
- The String I made for inputs that appends the user input followed by a new line command changes values to "Hello\nWorld\n"

# Part 2

Failure inducing input as JUnit test:
```Java
 @Test
 public void testReversed() {
   int[] input1 = {}; 
   assertArrayEquals(new int[] {}, ArrayExamples.reversed(input1));


   int[] input2 = { 1, 2, 3, 4 };


   assertArrayEquals(new int[] { 4, 3, 2, 1 }, ArrayExamples.reversed(input2));
 }
```

Non-Failure inducing input as JUnit test:
```Java
@Test 
	public void testReverseInPlace1() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace1(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```

Outputs:
![image](https://user-images.githubusercontent.com/122497361/215422182-50b97ba4-1ed6-4be8-87ae-52486d9415c3.png)

Code before fix:
```Java
static void reverseInPlace1(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

Code after fix:
```Java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i++) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i-1];
      arr[arr.length-i-1]= temp;
    }
  }
```

Reason:
The method needed a temporary value to avoid overwriting already swapped elements and needed to have the 
number of loop iterations divided in half, as swapping the first half with the second already fulfills the goal
of reversing the array

# Part 3
I didn't know how one would set up a server with Java and how one would parse the path of the URL for certain inputs.
Additionally, it was very interesting to see the code behind making a simple Java server and how the port numbers worked



