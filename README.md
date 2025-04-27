# cs472-homework-3---building-an-http-client-solved
**TO GET THIS SOLUTION VISIT:** [CS472 Homework 3 – Building an HTTP Client Solved](https://www.ankitcodinghub.com/product/cs472-hw3-building-an-http-client-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;121130&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS472  Homework 3 - Building an HTTP Client Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
Directions

NOTE there is a lot to read here, but dont freak out, there is not a lot to do

For this assignment you will be building 2 versions of an operational HTTP client. The client should work with a real HTTP server. Testing for the purposes of grading will be using httpbin.org, although you can use whatever server you want for development, so long as it supports nonencrypted HTTP vs encrypted HTTPs.

Note that the make file includes test suites for the 2 versions of the program you will be implementing. More on this in a bit.

To make the programming assignment realistic, I am limiting the amount you can receive in any one call from the server to 1024 bytes. Thus, you need to loop around and keep receiving data until you get the entire payload from the server (except of course, if the response is less than 1024 bytes).

Part1: Simple HTTP Client

The first program is client-cc, which sends a message to an HTTP server with a header Connection: Close. This simplifies things a good bit, making HTTP/1.1 work like HTTP/1.0. The implementation for this client is in client-cc.c. I provided a lot of the scaffolding, you just need to implement the parts of the code that I commented with // TODO: what_you_need_to_do.

When processing data returned from the server you can just keep looping recv(…) calls. When the server is done sending data it will close the socket. When this happens, recv(…) will return a negative number instead of the number of bytes read to indicate an error. In this case it is not really an error, but more of an indicator that the server closed the socket. All you need to do is to close the socket on the client end when this happens.

Part2: A robust and practical HTTP Client

The second scaffold I provided is for the client-ka executable. The source code is in client-ka.c. This version must implement the Connection: Keep-Alive protocol properly. I discussed this in class, but as a refresher, this header basically requires the client to open a socket once, and then it can continue to issue multiple requests over the same socket. When the program terminates the socket should close. However, the client must also take care of being sensitive to the serve’s behavior, as it can close the socket at any time. Thus care must be taken to properly handle the condition when the program is trying to send to the server and the server closed the socket. This situation requires the client to open a new socket when it detects this situation.

The other key challenge with implementing the Keep-Alive protocol is properly managing the recv(…) calls. You need to inspect the Content-Length header that the server sends back and make sure you properly terminate looping recv(…) calls when you get all of the data from the server. In other words, you need to track the amount of data you received, and ensure you don’t loop and make an extra recv(…) call as this will block the client.

For this program, I wrote most of the code for you, again you need to flush out the sections annotated with //TODO:. I wrote several parsing helpers for you and placed them in a utility module called http.c. You will not need to modify this module.

Program interfaces

The client-cc and client-ka programs have the same command line parameters. They are as follows:

“` client-cc host port …resource — and — client-ka host port …resource where: host is a domain name, e.g., httpbin.org port is the port number, e.g., 80 resource is what you want from the host, e.g., /json Also note that the interface can support getting multiple resources from the server, for example

client-xx httpbin.org 80 / /json /http will make 3 requests to the server, one to get the root “http://httpbin.org/”, one to get json “http://httpbin.org/json” and one to get html “http://httpbin.org/html”.

Note that you can have as many resources as you want, the above example is just for 3.

Also, if you leave the command line arguments blank, defaults will be provided, see http.h for the default values. “`

What you need to do and hand in

Unlike other assignments, the written and coding parts will be combined. I provided a lot of the code for you so much of the written component will be you documenting code that I developed to demonstrate that you understand the code. If you just blindly document the code in the sections where I ask for it you will not receive any credit, your documentation should convey that you understand the code. Ideally, you should run the code through the debugger to get the best understanding.

What you need to do: 1. Start by getting the simple client-cc program working. Implement the coding //TODO: sections. Make sure the code compiles and runs properly. You can use the makefile I provided to compile and test your code. To compile just client-cc use the make client-cc command. You can run the program directly or I provided 2 ways to run from the makefile. make run-cc will make a single request to the httpbin server, and make run-cc3 will make 3 requests in a row to the httpbin server. This component will be graded only on your work in the client-cc.c file. The scaffold I provided makes one call to a helper function in http.c, but you don’t need to worry about that in this part.

1. Next take on getting client-ka working. This is the version with Connection: Keep-Alive. I provided a lot of scaffolding to make this easy for you. Start by making changes to client-ka.c so that your program functions properly. Follow the //TODO: directions carefully for coding. There are several helpers in http.c – just assume they work, you dont need to change them, and their function names should clearly identify what they do. You should not have to write very much code, but expect to spend a good bit of time studying my code and stubbing out things to increase your understanding. You can independently build client-ka by executing make client-ka. Note that just typing make will still work, but it will attempt to build both client-cc and client-ka. You can do this after you get both versions of your program to compile.

2. Next venture into http.c, there are 3 functions in there that I want you to carefully study and document. They are socket_connect(), get_http_header_len() and get_http_content_len(). You dont need to change these functions, however, you need to clearly document them in a way that demonstrates you understand what they do. There is some basic pointer arithmetic and possibly some runtime library functions that you might not be familiar with. Research the library functions online, and follow the code, either by hand-running, or better yet, by stepping through the functions in the debugger after you finish part 2. You will be graded on the quality of your documentation in that it demonstrates your understanding of the code. What do the variables do? How are they updated? and so on. Dont just comment that the pointer is updated.

3. Finally, do some research online to figure out how you can collect a timestamp from the operating system via C. Hint: check out the functions in &lt;time.h&gt;. Update both programs to get the start time of executing your program (first line in main), and the end time of executing your program (last lines just before main ends) to get the total runtime of your program. In other words (endTime – startTime). Run the makefile commands make client-ka3 and make client-cc3 several times and collect some data. Include with your submission a file called timing.txt that describes the duration of running both the Connection: Close and Connection: Keep-Alive versions. Explain if you saw improved response time with using Keep-Alive or not, and why you think you got about the same, worse or better response time between the two different program versions.
