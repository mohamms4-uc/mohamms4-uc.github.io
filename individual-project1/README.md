# WAPH-Web Application Programming and Hacking

## Instructor: Dr. Phu Phung

## Student

**Name**: Salma Mohammad

**Email**: mohamms4@mail.uc.edu

**Short-bio**: Salma Mohammad hopes to learn more about ethical hacking and secure software development. 

<img src="headshot.jpg">

## Repository Information

Respository's URL: 

This is a public repository hosted on github.io for Project 1. The organization of this repository is as follows.


## Overview

Firstly, students delve into understanding the fundamentals of the web and the HTTP protocol by learning Wireshark for examining HTTP protocol and utilizing telnet while deploying Wireshark to comprehend HTTP messages.

Secondly, students explore basic web application programming by creating a CGI web application in C and simple PHP web applications with user input. 

Through this lab, we learned how to track HTTP GET and POST requests while utilizing Wireshark and curl and telnet for examination and comparison.

You can find Salma's completed lab using this Github URL: https://github.com/mohamms4-uc/waph-mohamms4/blob/main/labs/lab1

## Part 1: The Web and HTTP Protocol

### Task 1: Familiar with Wireshark tool and HTTP Protocol

First, I opened Mozilla firefox. I launched Wireshark using **sudo wireshark** in the terminal and this began packet capture. I inputted the given example url from the lecture into Mozilla to generate HTTP traffic. I filtered specifically for HTTP traffic and I analyzed the captured packets to understand the communication between the client and server, including request and response messages.

*HTTP Request for Example.com: Here, client is sending a request to server to access the URL.*

![HTTP Request for Example.com](Task1Req.png)

*HTTP Response for Example.com: This is the response message recieved from the server in response to the client's request.*

![HTTP Request for Example.com](Task1Resp.png)

*HTTP Stream for Example.com: This shows the sequence of HTTP packets exchanged between the client and server*

![HTTP Request for Example.com](Task1Resp.png)


### Task 2: Understanding HTTP using telnet and Wireshark

I first opened a terminal on my computer and initiated a telnet session in port 80 by typing the command **telnet www.example.com 80**. Once connected, I sent a HTTP GET request and write the host as example.com. With this request, I opened Wireshark and began packet capture. I located the HTTP GET request in Wireshark by using the filter. I clicked on the packet details to show information about the HTTP request and HTTP response as shown below.

*Start telnet session in port 80 for example.com*

![Start telnet session in port 80 for example.com](P1Task2.1.png)

*HTTP Request for telnet session captured through Wireshark*

![HTTP Request telnet session](p1Task2.2.png)

*HTTP Response for telnet session captured through Wireshark*

![Start telnet session in port 80 for example.com](p1Task2.3.png)


## Part 2: Basic Web Application Programming

### Task 1: CGI Web Applications in C

#### Part A

First, I ran the necessary commands shown in the lecture slides to make sure that the apache2 server is updated and running. I wrote the code to a normal Hello World program using C and saved to to **helloworld.c**. You can see the code file included below. I then compiled this .c file into a .cgi file using the command **gcc helloworld.c -o helloworld.cgi**. This creates a copy that converts the .c file into .cgi. I made sure that the new file, **helloworld.cgi**, is saved into the **/usr/lib/cgi-bin** of my computer directory so that it can successfully be deployed onto the server. I then navigated to my server using the URL: **http://localhost/cgi-bin/helloworld.cgi**. 

*Included file: helloworld.c*
```
#include <stdio.h>
int main(void) {
printf("Content-Type: text/plain; charset=utf-8\n\n");
printf("Hello World CGI! From Salma Mohammad, WAPH\n\n");
return 0;

}
```
*CGI file properly invoked to Apache*

![CGI file properly invoked to Apache](P2Task1a.png)

#### Part B

I repeated the exact same steps but created a file called **index.c** that implemented HTML code through the C CGI program. I had to change the content type in the first line to make sure that it could properly read the HTML in the printf statements. The code can be found below. I then converted a copy into a CGI file, made sure that it was copied into the **/usr/lib/cgi-bin** of my computer directory, and navigated to my server using the URL: **http://localhost/cgi-bin/index.cgi**. 

**Included file: index.c*
```
#include <stdio.h>

int main(void) {

    
    printf("Content-Type: text/html; charset=utf-8\n\n");

    
    printf("<!DOCTYPE html>\n");
    printf("<html>\n");
    printf("<head>\n");
    printf("<title>Salma's CGI Page for WAPH Course.</title>\n");
    printf("</head>\n");
    printf("<body>\n");
    printf("<h1>Web Application Programming and Hacking</h1>\n");
    printf("<h2>Webpage created by Salma Mohammad</h2>\n");
    printf("<p>This is a simple CGI-generated webpage written in C.<br>\n");
    printf("Instructor: Dr. Phu Phung<br>\n");
    printf("Student: Salma Mohammad<br>\n");
    printf("MNumber: M15119047</p>\n");
    printf("</body>\n");
    printf("</html>\n");

    return 0;
}
```
*New HTML-included C CGI file properly invoked to Apache*

![New HTML-included C CGI file properly invoked to Apache](P2Task1b.png)

### Task 2: A simple PHP Web Application with user input

#### Part A

I properly invoked a PHP file in Apache by first creating a PHP file that echoed a basic hello world print. I then added **phpinfo()** to show the PHP configuration data. I navigated to **http://localhost/helloworld.php** and found my deployed PHP file.

*PHP configuration data invoked to Apache*

![PHP file properly invoked to Apache](Part2Task2a.png)

#### Part B

Below is the demonstration of the web application using PHP where I requested data through my name as an input. The simple php web application creates security risks because of bad input validation and sanitization. There's a risk of XSS attacks which allows for malicious scripts to be executed in other user's browsers. It's also suseptible to SQL injection attacks because of the lack of authentication. 

*PHP Web application code*

```
<?php

echo $_REQUEST["data"];

?>
```

*Deployed web application using PHP*

![Deployed web application using PHP](Part2Task2b.png)

### Task 3: Understanding HTTP GET and POST requests

#### Part A

I used Wireshark to examine the HTTP GET request and response for the **echo.php** file with my name in data by first launching Wireshark then filtering HTTP traffic. I then accessed **http://localhost/echo.php** from my web page and then stopped packet capture. I opened them to analyze them as shown below. **The screenshot contains information for both the HTTP request and response.**


*HTTP REQUEST **AND** HTTP RESPONSE for echo.php using Wireshark capture*

![Deployed web application using PHP](Part2Task3a.png)

#### Part B

I started packet capture then I ran the command **curl -X POST -d "data= Hello World, from Salma Mohammad" http://localhost/echo.php** in my terminal. I stopped packet capture in Wireshark and filtered the HTTP protocols to get the information below. **The screenshot contains both the HTTP stream and the outcome of the curl program.**


*Deployed web application using PHP*

![Deployed web application using PHP](Part2Task3b.png)

#### Part C

The main difference between HTTP POST and HTTP GET requests is how they transmit data. With HTTP POST requests, data is sent within the request body, allowing for larger amounts of data to be transmitted securely. Meanwhile, HTTP GET requests append data to the URL, making them visible in the URL and limited in the amount of data they can transmit. In terms of the HTTP responses observed, both the responses to the HTTP POST and GET requests typically contain the requested resource's content. However, the specific content of the response may change depending on the server-side processing of the request, like either form submissions or database queries, but they adhere to the same HTTP protocol for response transmission.

