# ELK Security Monitoring Lab

## Overview

This project demonstrates the deployment of an ELK Stack security monitoring environment on Windows with centralized log collection and endpoint monitoring.

## Technologies

- Elasticsearch
- Kibana
- Fleet Server
- Elastic Agent
- Windows Defender
- Sysmon
- YARA
- Docker

## Features

- Deploy ELK Stack locally on Windows
- Configure Fleet Server
- Enroll Linux Elastic Agent
- Collect Linux system logs
- Integrate Windows Defender
- Integrate Sysmon security events
- Develop custom YARA rules
- Visualize security events in Kibana

## Project Architecture

(Add your architecture image here.)

## Screenshots

### ELK Stack Running

![ELK](screenshots/01-ELK-Running.png)

### Fleet Server

![Fleet](screenshots/02-Fleet-Server.png)

### Linux Elastic Agent

![Linux](screenshots/03-Linux-Agent.png)

### Windows Defender Logs

![Defender](screenshots/05-Windows-Defender.png)

### Sysmon Events

![Sysmon](screenshots/06-Sysmon.png)

### Custom YARA Rule

![YARA Rule](screenshots/07-YARA-Rule.png)

### YARA Detection Output

![YARA Output](screenshots/08-YARA-Output.png)

## Skills Demonstrated

- SIEM Deployment
- Log Collection
- Fleet Management
- Endpoint Monitoring
- Windows Defender Integration
- Sysmon Configuration
- Custom YARA Rule Development
- Security Event Analysis

## Future Improvements

- Complete end-to-end YARA log ingestion into Elasticsearch
- Create Kibana Detection Rules for YARA matches
- Automate YARA scanning
- Build custom dashboards for YARA detections
