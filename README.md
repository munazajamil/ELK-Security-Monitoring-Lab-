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

                ┌─────────────────────────┐
                │   Docker Desktop (Win)   │
                │  ┌────────────┐          │
                │  │Elasticsearch│◄────────┼── indexes: logs-*, metrics-*
                │  └─────┬──────┘          │
                │        │                 │
                │  ┌─────▼──────┐          │
                │  │   Kibana   │          │
                │  └────────────┘          │
                └───────────▲──────────────┘
                             │
                    ┌────────┴────────┐
                    │   Fleet Server   │
                    └────────▲────────┘
                             │
              ┌──────────────┴──────────────┐
              │                              │
     ┌────────▼────────┐          ┌──────────▼─────────┐
     │  Kali Linux Agent │          │  Windows Host       │
     │  (Elastic Agent)  │          │  Sysmon + YARA CLI  │
     └────────────────────┘         └─────────────────────┘


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

Setup walkthrough

1. Deploy the ELK stack

powershellcd "C:\Users\ELK-Lab"
docker compose up -d
docker compose ps

Confirms elasticsearch and kibana, both Up.

2. Configure Fleet Server


Kibana → Fleet → Agents → Add Fleet Server
Followed the guided setup, generated the Fleet Server policy and enrollment token


3. Enroll the Linux (Kali) agent


Ran the generated elastic-agent install command with the Fleet Server URL + enrollment token
Agent shows up in Fleet → Agents as kali, status Healthy


4. Verify data in Kibana


Discover → logs-* and Discover → metrics-* both show live documents from the
Fleet Server and Linux agent, timestamps updating in real time


5. Sysmon on Windows


Installed Sysmon with a baseline config
Confirmed Process Create (Event ID 1) events logging under
Applications and Services Logs → Microsoft → Windows → Sysmon → Operational


6. Custom YARA rule


Wrote Local_Lab_Malware_Test rule targeting a known string
Also tested a rule detecting EICAR test files across a sample directory
Ran via PowerShell, logged detections to yara.log



Troubleshooting notes


Had an orphaned elk-lab-fleet-server-1 container appear after a docker compose down -v /
up -d cycle — Compose flagged it but didn't block startup; cleaned up manually.
docker-compose.yml throws a warning that the top-level version key is obsolete in
Compose v2 — cosmetic, doesn't block deployment, but worth stripping out for a clean repo.


Why this project

Built to get hands-on with the exact stack SOC teams use day to day agent-based log
collection, host telemetry via Sysmon, and rule-based detection via YARA rather than just
reading about them. Next iteration closes the loop: raw detections → SIEM-visible alerts.


Author: Munnaza Jamil — SOC Analyst Intern | GitHub | LinkedIn
