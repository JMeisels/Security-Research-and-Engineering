# Security Research & Engineering

A collection of independent cybersecurity research, threat hunts, incident investigations, and security engineering projects.

This repository documents my approach to identifying threats, investigating suspicious activity, developing detections, and building practical security tools.

My work focuses on **incident response, threat hunting, detection engineering, and security automation**, with an emphasis on translating investigative findings into actionable security improvements.

## Repository Structure

### 🔍 001 | Incident Investigations

**[Explore Investigations](./001-Incidents/)**

Technical investigations documenting suspicious activity, evidence correlation, attack timelines, and response considerations.

Each investigation aims to demonstrate a structured analytical approach, including findings, supporting evidence, and investigative limitations.

### 🎯 002 | Threat Hunts

**[Explore Threat Hunts](./002-Hunts/)**

Hypothesis-driven threat hunting research focused on adversary behavior, persistence mechanisms, identity threats, and emerging techniques.

Hunts may include:

- Threat intelligence and MITRE ATT&CK mapping
- Hunting hypotheses and methodology
- Microsoft Sentinel KQL queries
- Detection opportunities and false-positive considerations
- Findings, validation status, and limitations

**Featured Research**

[Twill Typhoon Persistence Hunt](./002-Hunts/twill-typhoon-persistence-hunt/)

Research and KQL hunting content focused on investigating suspected persistence activity.

### ⚙️ 003 | Security Engineering Projects

**[Explore Projects](./003-Projects/)**

Tools and engineering experiments focused on improving security detection, investigation, and response workflows.

Projects explore Python development, API integrations, containerization, security automation, and practical detection engineering.

**Featured Project**

[Password Spray Analyzer with AI Summaries](https://github.com/JMeisels/Password-Spray-Analyzer-with-AI-Summaries)

A Python-based prototype that analyzes synthetic Microsoft Entra-style authentication events for potential password spraying, generates AI-assisted summaries, and supports local or Docker execution.

## Technologies & Skills

| Area | Technologies |
|---|---|
| Threat Detection & Hunting | KQL, Microsoft Sentinel, Microsoft Defender |
| Security Engineering | Python, PowerShell, REST APIs |
| Development & Tooling | Git, GitHub, Docker, VS Code |
| Identity & Cloud Security | Microsoft Entra ID, Microsoft Azure |
| Security Research | MITRE ATT&CK, threat intelligence, detection analysis |

## Research Principles

My research and projects follow several principles:

1. **Evidence-driven analysis:** Investigative conclusions should be supported by observable evidence.
2. **Practical detection development:** Queries and tools should address identifiable security behaviors.
3. **Transparent validation:** Research should distinguish tested detections from hypotheses and illustrative examples.
4. **Reproducibility:** Document assumptions, required telemetry, methodology, and relevant limitations.
5. **Continuous improvement:** Refine techniques and tooling through hands-on experimentation.

## Disclaimer

This repository contains independent research, public-source analysis, and personal engineering projects. It does not represent the views of my employer.

No confidential employer data, internal investigation details, or proprietary detection content are intended to be published here.

Some examples use synthetic data or controlled test scenarios. Validation status is documented where applicable.

## Connect

**Website:** [jordanmeisels.com](https://jordanmeisels.com)

**LinkedIn:** [linkedin.com/in/jordanmeisels](https://linkedin.com/in/jordanmeisels/)

**GitHub:** [JMeisels](https://github.com/JMeisels)