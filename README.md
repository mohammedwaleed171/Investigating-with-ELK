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
- We can view the source IP addresses of the relevant events in the Fields
  <p align="center"><img src="https://miro.medium.com/v2/resize:fit:828/format:webp/1*RQQExrC8kooHY-jlQbjE-A.png" height="40%" width="40%" /><p/></p> <br/>
