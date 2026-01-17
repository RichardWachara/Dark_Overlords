# Previous
To study our approach we are going to start with a retire 
box previous. This will help in acquiring a basic understanding
of what tools are used and how we approach a target. With this knowledge we will be ready to try out our first box on our own.

Currently the box is available on the IP address 10.129.2.235.

*### Lesson *
* What is an IP address?
     - An IP address is a unique identification number assigned to every 
device on the internet. As you read this your device is connected to the internet so it has an IP address.
You can confirm your IP address by running the command *ifconfig* on Linux or *ipconfig* on Windows. Depending on the type of network you are using the IP address of your computer will show up. 

To see if we can reach the machine across the internet we use the ping command as *ping 10.129.2.235*. The ping command uses the ICMP (Internet Control Protocol) to send a ICMP Echo Request packet to the specified destination. If the machine is online and reachable it responds with an
ICMP Echo Reply message

* What is ICMP
     - It is a network layer protocol of the OSI model used to report errors and diagnose network issues. It allows network devices to send
feedback (ICMP Echo Reply message) about packet delivery failure.
