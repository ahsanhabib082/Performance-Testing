# Performance_Testing on Restful-booker

Testing Site - https://restful-booker.herokuapp.com

# Introduction
This document details a performance test conducted on https://restful-booker.herokuapp.com using Apache JMeter. 
The test simulates 3,000 concurrent users with a 10-second ramp-up period and one iteration, covering various API functionalities.
We'll explore the core setup and introduce some enhancements to the standard approach.

# Prerequisites

- As of JMeter 5.6.3, Java 8+ and above are supported.
- we suggest multicore cpus with 4 or more cores.
- Memory 16GB RAM is a good value.


# Installations

Step 1: Check if Java is Installed

Open your terminal or command prompt.Type the following command and press Enter:
```
java --version
```
If Java is installed, you'll see a message displaying the Java version.
```
java 22.0.1 2024-04-16
Java(TM) SE Runtime Environment (build 22.0.1+8-16)
Java HotSpot(TM) 64-Bit Server VM (build 22.0.1+8-16, mixed mode, sharing)
```
Step 2: Install Java JDK (if not installed)

If you don't see a Java version, you'll need to install it:

* Download Java JDK:
Go to the official Oracle website and download the latest JDK version suitable for your operating system (Windows, macOS, or Linux).
* Install Java JDK:
Follow the on-screen instructions to install the JDK. This usually involves running an installer file and accepting the license agreement.

Step 3: Set Up the Environment Variables (Windows)

To ensure your computer can find the Java installation, you'll need to set up environment variables:

* Open System Properties:
 Right-click on "This PC" and select "Properties."
* Go to Advanced System Settings:
Click on "Advanced system settings."
* Click on Environment Variables:
Click on the "Environment Variables" button.
* Edit the System Variables:
Under "System variables," find the "Path" variable and click "Edit."
Add the path to your Java installation's bin directory. For example, if you installed Java in ``` C:\Program Files\Java\jdk-21\bin```, add this to the Path variable.
Create a New System Variable (Optional):
Click on "New" under "System variables."
Set the Variable name to "JAVA_HOME" and the Variable value to the path of your Java installation directory ``` (e.g., C:\Program Files\Java\jdk-21).```

Step 4: Verify the Installation

Open a new terminal or command prompt and type java -version again. You should now see the Java version.
Now you're ready to use JMeter!
  
Java
```bash
  https://www.oracle.com/java/technologies/downloads/
```
JMeter  
```
https://jmeter.apache.org/download_jmeter.cgi
```


# Test Components:
* Thread Group: This component defines the virtual users (VUs) performing the test. We'll configure 3000 VUs with a ramp-up period of 10 seconds.

* HTTP Header Manager: This element adds necessary headers to each request.
     * Content-Type: application/json
     * Accept: application/json 

* HTTP Request Samplers: These represent the actual API calls. Here's a breakdown for each functionality:

  - Auth :
  
      This depends on the API's authentication mechanism. Implement the appropriate sampler based on the method (e.g., Basic Auth, OAuth).
  - Create Booking:
  
       This POST request sends booking details using user variables or CSV data. Capture response time and relevant data points (e.g., booking ID).
  - Get Booking:
  
       This GET request retrieves a booking by ID obtained in the Create Booking step. Consider using a Regular Expression Extractor to capture the booking ID from the previous response.
  - Update Booking:
  
       This PUT request updates an existing booking (use the captured ID) with modified data.
  -  Partial Update Booking:
  
       This PATCH request updates specific fields of a booking. Explore the API documentation for details.
  - Delete Booking:
  
       This DELETE request removes a booking (use the captured ID).
  - Ping:
  
       It include a GET request to a known-good endpoint (e.g., /ping) to measure overall server responsiveness.
  - Response Assertions:

       Add assertions to verify expected response codes (e.g., 200 for success) and content (e.g., presence of specific data in the response body).
  - Listeners:
  
       Include listeners to capture and analyze test results:
  - View Results Tree:
  
       Provides a detailed view of individual requests and responses.
  - Aggregate Report:
  
       Generates a high-level report summarizing key metrics like average response time, throughput, and error rate.



# Test Plan
- Testplan > Add > Threads (Users) > Thread Group (this might vary dependent on the jMeter version you are using)
- Testplan => ADD => Thread(Users) => Thread Group
- Then, Thread Group => Add => Sampler => HTTP Request(example : Auth) renaming the name
- Then, select Auth => Config Element => HTTP Header Manager
- Then, select Auth => Add => Listner => View Result Tree
- Then, select Auth => Add => Listner => View Summary Report
- Then, select Auth => Add => Listner => Aggregate User

- Name: Threads (Users)

- Number of Threads (users): 1 to 3000

- Ramp-Up Period (in seconds): 10

- Loop Count: 1

# Test execution (from the Terminal)

- Save your jmx file in bin folder
- JMeter should be initialized in non-GUI mode.
- Make a report folder in the bin folder.
- Run Command in jmeter\bin folder
- Assertion and listner should be disabled.

# Command

Jtl file generate command

```
jmeter -n -t performance_t3000.jmx -l report\performance_t3000.jtl

```

Report Generate command

```
jmeter -g report\performance_t3000.jtl -o report\performance_t3000.html

```
