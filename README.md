# Investigating with ELK | Tryhackme's Itsybitsy CTF

### What is ELK ? 
<p align="center"><img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*EWVcV8N-DskE9ZA21arKmA.png" height="40%" width="40%" /><p/></p> <br/>
- ELK is the acronym for three open source projects: Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a stash like Elasticsearch. Kibana lets users visualize data with charts and graphs in Elasticsearch.<br/>

### What is an Intrusion Detections System (IDS) and Command and Control Server (C2C) ? 
<p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*co1Zeos8DrhMV_OOhEYEKw.png" height="40%" width="40%" /><p/></p> <br/>
- An Intrusion Detection System (IDS) is a monitoring system that detects suspicious activities and generates alerts when they are detected. Based upon these alerts, a security operations center (SOC) analyst or incident responder can investigate the issue and take the appropriate actions to remediate the threat.<br/>
- A command and control [C&C] server is a computer controlled by an attacker or cybercriminal which is used to send commands to systems compromised by malware and receive stolen data from a target network.<br/>
<p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*_ad1xCAeVQwhQSTFrGdNCA.png" height="40%" width="40%" /><p/></p> <br/>

## Scenario - Investigate a potential C2 communication alert

- During normal SOC monitoring, Analyst John observed an alert on an IDS solution indicating a potential C2 communication from a user Browne from the HR department. A suspicious file was accessed containing a malicious pattern THM:{ ________ }. A week-long HTTP connection logs have been pulled to investigate. Due to limited resources, only the connection logs could be pulled out and are ingested into the connection_logs index in Kibana.
- Our task in this room will be to examine the network connection logs of this user, find the link and the content of the file, and answer the questions.

## Solving the questions

**Q1: How many events were returned for the month of March 2022?** <br/>
```A1: 1482```
- By adjusting the time filter to cover the month of March, we can see the number of events.
  <p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*bOg03UU7OmJrqYcOFWdsEQ.png" height="40%" width="40%" /><p/></p> <br/>
**Q2: What is the IP associated with the suspected user in the logs?** <br/>
```A2: 192.166.65.54```
- We can view source ip adresses by choosing source_ip field.
  <p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*RQQExrC8kooHY-jlQbjE-A.png" height="40%" width="40%" /><p/></p> <br/>
- There is traffic from the source IP address “192.166.65.54” to the destination IP address “104.23.99.190”. When we search the relevant destination IP address, we can see that the IP address 104.23.99.190 is classified in the Command and Control IPs category by reliable cyber intelligence resources.
  ```https://otx.alienvault.com/indicator/ip/104.23.99.190```
**Q3: The user’s machine used a legit windows binary to download a file from the C2 server. What is the name of the binary?** <br/>
```A3: bitsadmin```
- Bitsadmin is a command-line tool used to create, download or upload jobs, and to monitor their progress.
- We can add the source ip filter by clicking on the + sign or by typing it on the search feild.
- And by inspecting the info we will see a parameter called user_agent refer to the tool that were used to download the file
  <p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*8Sp-VgNa6AWuxAKTLAkf9g.png" height="40%" width="40%" /><p/></p> <br/>
**Q4: The infected machine connected with a famous filesharing site in this period, which also acts as a C2 server used by the malware authors to communicate. What is the name of the filesharing site?** <br/>
```A4: pastebin.com```
- We can find the domain address by carefully inspecting the parameters.
  <p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*s0TW7LjwpWLtpfCkQg1dzQ.png" height="40%" width="40%" /><p/></p> <br/>
**Q5: What is the full URL of the C2 to which the infected host is connected?** <br/>
```A5: pastebin.com/yTg0Ah6a```
- When we examine other information detected about the relevant event, we can determine the full URL address.
  <p align="center"><img src="" height="40%" width="40%" /><p/></p> <br/>
**Q6: A file was accessed on the filesharing site. What is the name of the file accessed?** <br/>
```A6: secret.txt```
- By opening the full URL on your browser you will see the name of the file.
  ```pastebin.com/yTg0Ah6a```
<p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*i0d9Zv5WEKpqz94AyaQMNA.png" height="40%" width="40%" /><p/></p> <br/>

**Q7: The file contains a secret code with the format THM{_____}?** <br/>
```A7: THM{SECRET__CODE}```
<p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*88Iw7_Uyl-zo9KX8BB1wsw.png" height="40%" width="40%" /><p/></p> <br/>

## Conclusion
**This walkthrough guides us through the Tryhackme's ItsyBitsy challenge, demonstrating the process of investigating a potential C2 communication alert using ELK.**

