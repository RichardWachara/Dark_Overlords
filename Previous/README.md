# Previous
To study our approach we are going to start with a retire 
box previous. This will help in acquiring a basic understanding
of what tools are used and how we approach a target. With this knowledge we will be ready to try out our first box on our own.

* Currently the box is available on the IP address 10.129.2.235.

### *Lesson* 
* What is an IP address?
     - An IP address is a unique identification number assigned to every 
device on the internet. As you read this your device is connected to the internet so it has an IP address.
You can confirm your IP address by running the command *ifconfig* on Linux or *ipconfig* on Windows. Depending on the type of network you are using the IP address of your computer will show up. 

     - To see if we can reach the machine across the internet we use the ping command as *ping 10.129.2.235*. The ping command uses the ICMP (Internet Control Protocol) to send a ICMP Echo Request packet to the specified destination. If the machine is online and reachable it responds with an
ICMP Echo Reply message

* What is ICMP
     - It is a network layer protocol of the OSI model used to report errors and diagnose network issues. It allows network devices to send
feedback (ICMP Echo Reply message) about packet delivery failure. It is also used by the command *tracroute 10.129.2.235* to trace the path a packet takes before reaching its destination

     - ![ping image](./img/Ping.png)

     - Using the above information we can now understand what our ping command output is saying.
With our target up and reachable we need to perform some orientation

### *Orientation*
* The goal here is not deep scanning it is to understand what king of system we are targeting.
     - The main questions to answer include:
        - Is it web-facing?
        - Is it internal?
        - Is authentication involved?
* We are not looking for vulnerabilities at this point. We are building a mental map.
* For orientation we are going to use nmap to determine what ports are open. 
     #### Lesson
      * What is a port and why is it important?
         - It is a virtual endpoint on a device that directs traffic to the correct application.
 It is identified by a number between 0 and 65535
         - Ports are important because the allow a single IP address to host multiple services.

         * To determine the open port we use the following command *nmap -p- 10.129.2.235 -T5*
         ![nmap scan](./img/Nmapscan.png)
         - From the results we see that 2 ports are open and each port is running a service:
 Port 22 is running ssh and Port 80 is running http.
         - We know http is used on the internet and ssh is used to access a machine remotely.
This answers our questions, The machine is web-facing and authentication is involved as ssh is a secure protocol.

### *Lightweight reconnaisance*
* We now know two ports are open 22 and 80 in this phase we need to enumerate what services this ports are running and any further information we can gather.
To do this we still use nmap to scan. Using the command *nmap -p22,80 -sC -sV 10.129.2.235 --min-rate=10000* in this command we have specified we want to run scans on only port 22 and 80 we have also commanded nmap to run default scripts with *-sC* and also enumerate what services are running on the port using the *-sV* flag 
* In this section we are looking for what stand out not for answers. We are looking for potential entry points.
![nmap scan](./img/nmapresults.png)
* From our scan we not that port 22 looks normal however we see port 80 redirected to http://previous.htb meaning there is a web site and with no login credentials for the ssh our possible entry point is through a web vulnerability on the website.
* To effectively navigate to the website we add the IP address to our /etc/host file so that we dont have to remember the IP address each time we visit the website.
* Once it is added we can navigate to the website with the http://previous.htb link.
![nmap scan](./img/Website.png)
* Looking at the website landing page there is nothing that interesting other than the 2 buttons that redirect us to a login page. We note the URL we are being redirected to as http://previous.htb/api/auth/signin?callbackUrl=%2Fdocs



