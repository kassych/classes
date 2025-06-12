# Cybersecurity Detection Skills Guide for Students

by @***0xPh4z3d0ut*** 

This guide is designed for students eager to master the cybersecurity detection techniques .

 It builds on the need to understand data sources like *Event Tracing for Windows* (ETW), the *Windows Registry*, command line spoofing, and the limitations of simplistic detection methods.   
This guide progresses from foundational knowledge to advanced skills, with technical exercises to ensure hands-on learning. By the end, you’ll be equipped to analyze and detect sophisticated threats effectively.

**Learning Objectives**  
Understand the limitations of basic detection methods (e.g., *EventID*, *CommandLine*).

Master advanced data sources (*ETW*, *Registry*) for reliable detection.

Recognize and counter evasion techniques like command line spoofing.

Develop a structured approach to detection engineering.

**Prerequisites**

- [ ] Basic knowledge of *Windows* operating systems.  
- [ ] Familiarity with command-line interfaces (e.g., *PowerShell*, *CMD*).  
- [ ] A virtual machine (e.g., VirtualBox with *Windows* 10/11) for safe experimentation.  
- [ ] Administrative privileges on your VM for some exercises.

## 

## Module 1: Foundations of Detection Engineering 

Duration: 1-2 weeks

**Goal**: Grasp the basics and limitations of traditional detection methods.

**Key Concepts**  
Detection often relies on EventIDs (e.g., **4688** for process creation) and CommandLine data, but these can be spoofed or misinterpreted.

Diverse telemetry (e.g., ETW, Registry) is critical for robust detection.

Techniques (e.g., process injection) are distinct from tools (e.g., specific malware).

**Resources**  
Microsoft Digital Defense Report 2024  

[https://www.microsoft.com/en-us/security/business/microsoft-digital-defense-report-2024](https://www.microsoft.com/en-us/security/security-insider/intelligence-reports/microsoft-digital-defense-report-2024)

**Focus**: *Chapter 1 on telemetry diversity.*  
MITRE ATT\&CK: Overview  

[https://attack.mitre.org/](https://attack.mitre.org/)

**Focus**: *Introduction to techniques vs. tools.*

### **Exercise 1.1:** Analyze Basic Telemetry

Setup: Boot your Windows VM and open Event Viewer (eventvwr.msc).

**Task**: Trigger a process creation event by running notepad.exe from CMD.

**Action**: Navigate to *Windows Logs* \> *Security*, filter for *EventID* **4688**, and note the CommandLine and Process Information fields.

**Reflection**: How might an attacker manipulate this data? Document your findings (e.g., spoofing the CommandLine with a legitimate process name).

**Deliverable**  
Write a 200-word summary on why relying solely on *EventID* **4688** is risky, citing your exercise observations.

## **Module 2**: *Mastering Event Tracing for Windows (ETW)*

Duration: 2-3 weeks  
**Goal**: Leverage ETW for advanced detection.  
Key Concepts  
ETW provides kernel- and user-mode telemetry, resistant to user-level tampering.

Requires understanding providers (e.g., *Microsoft-Windows-Security-Auditing*) and event sessions.

**Resources**  
Microsoft Learn: Event Tracing \- Getting Started    
[*https://learn.microsoft.com/en-us/windows/win32/etw/event-tracing-portal*](https://learn.microsoft.com/en-us/windows/win32/etw/event-tracing-portal)

Elastic Security Labs: Kernel ETW is the Best ETW    
[*https://www.elastic.co/security-labs/kernel-etw-is-the-best-etw*](https://www.elastic.co/security-labs/kernel-etw-best-etw)

### **Exercise 2.1:** Set Up an ETW Trace

**Setup**: Open *PowerShell* with admin rights.

**Task**: Create an ETW session to log security events.  
**Command**: logman create trace MyETWTrace \-ow \-o C:\\ETWLogs\\trace.etl \-p "Microsoft-Windows-Security-Auditing" 0xffffffffffffffff 4

**Start it:** logman start MyETWTrace  
**Action**: Run *notepad.exe,* wait 10 seconds, then stop the trace (logman stop MyETWTrace).

**Analysis**: Use tracerpt MyETWTrace.etl \-o output.xml to convert the log, then open output.xml in a text editor to identify process creation events.

**Reflection**: Compare ETW data with *EventID* **4688**. What additional details (e.g., thread IDs) does ETW provide?

### **Exercise 2.2**: Detect ETW Provider Registration

**Task**: Monitor ETW provider registrations (*EventID* **8** from *Microsoft-Windows-Kernel-EventTracing*).

**Action**: Repeat the trace setup, filtering for *EventID* **8**. Note the volume of events (as mentioned in the Prelude blog).

**Reflection**: Propose a strategy to filter out benign registrations (e.g., baseline known providers).  
**Deliverable**  
Create a 300-word report on ETW’s advantages over traditional logs, including exercise findings.

## **Module 3:** *Registry Analysis for Detection*

Duration: 2 weeks  
**Goal**: Use the Registry as a reliable data source.  
**Key Concepts**  
The Registry logs malware footprints (e.g., Run keys, persistence mechanisms).

Hard to spoof due to kernel-level enforcement.

Requires careful analysis to distinguish malicious entries.

**Resources**  
**Splunk: From Registry With Love \- Malware Registry Abuses**    
[https://www.splunk.com/en\_us/blog/learn/from-registry-with-love-malware-registry-abuses.html](https://www.splunk.com/en_us/blog/security/from-registry-with-love-malware-registry-abuses.html)

**Microsoft: Windows Registry Security Guide**    
[https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/)

### **Exercise 3.1:** Inspect Registry for Persistence

Setup: Open Registry Editor (*regedit*) with admin rights.

**Task**: Navigate to HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run.

**Action**: Add a test entry (e.g., **TestKey** with value notepad.exe) and reboot the VM.

**Analysis**: Verify notepad launches on startup. Remove the entry afterward.

**Reflection**: How could this mechanism be abused by malware? Suggest a detection rule.

**Deliverable**  
Develop a 200-word guide on monitoring Run keys, including your exercise insights.

## **Module 4:** *Countering Command Line Spoofing*

Duration: 1-2 weeks

**Goal**: Recognize and mitigate command line evasion.  
**Key Concepts**  
Attackers spoof CommandLine data (e.g., mimicking legitimate processes).

Detection requires cross-referencing with ETW or network logs.

* *MITRE T1036.005 (Masquerading)* covers this technique.

**Resources**

**Medium**: Command Line Spoofing by S12-H4CK  

[https://medium.com/@s12deff/command-line-spoofing-64ea1ef3f536](https://medium.com/@s12deff/command-line-spoofing-64ea1ef3f536)

**MITRE ATT\&CK: T1036.005**    
[https://attack.mitre.org/techniques/T1036/005/](https://attack.mitre.org/techniques/T1036/005/)

### **Exercise 4.1:** Simulate Command Line Spoofing

**Setup**: Use a PowerShell script or the GitHub repo *Procmon-Process-Argument-Spoofer*.

**Task**: Modify a process (e.g., *cmd.exe*) to spoof its CommandLine as *svchost.exe*.

**Action**: Check *EventID* **4688** and compare with ETW data from Module 2.

**Reflection**: How does ETW reveal the spoof? Propose a detection strategy.

**Deliverable**  
Write a 250-word analysis of spoofing risks and your detection approach.

## 

## 

## 

## **Module 5:** *Integrating Skills for Effective Detection*

Duration: 2 weeks

**Goal**: Synthesize knowledge into a detection workflow.  
**Key Concepts**  
Combine ETW, Registry, and network logs for comprehensive monitoring.

Develop baselines to filter noise (e.g., known ETW providers).

Align with industry best practices (e.g., SANS methodologies).

**Resources**  
**SANS Institute**: *Advanced Incident Detection and Response Survey* ( Requires Registration)    
[https://www.sans.org/white-papers/sans-2024-detection-response-survey/](https://www.sans.org/white-papers/sans-2024-detection-response-survey/)

**PowerShell Gallery**: *ETW Scripts*    
[https://www.powershellgallery.com/packages?q=ETW](https://www.powershellgallery.com/packages?q=ETW)

### **Exercise 5.1**: Build a Detection Workflow

**Task**: Create a script to monitor ETW (security events) and Registry (Run keys) simultaneously.

**Action**: Use PowerShell to log anomalies (e.g., new Run key entries) and correlate with ETW process creation events.

**Analysis**: Test with a benign process (e.g., *calc.exe*) and note alerts.

**Reflection**: Refine the script to reduce false positives.  
**Deliverable**  
Submit your script and a 400-word workflow document, explaining its logic and limitations.

## 

## 

## Capstone Project

Duration: 1-2 weeks

**Goal**: Demonstrate mastery with a simulated detection scenario.  
**Task**: Set up a VM, inject a spoofed process (using Exercise 4.1), and detect it using your **Module 5** workflow.

**Deliverable**: A 500-word report with screenshots, detailing your detection process and lessons learned.

**Recommended Learning Path**

* Weeks 1-2: Module 1 (Foundations).  
* Weeks 3-5: Module 2 (ETW) and Module 3 (Registry).  
* Weeks 6-7: Module 4 (Spoofing).  
* Weeks 8-9: Module 5 (Integration) and Capstone.

**Additional Tips**  
Join cybersecurity forums (e.g., Reddit’s r/netsec) for peer support.

**Explore the SANS FOR508 course Material**   
[https://www.sans.org/cyber-security-courses/advanced-incident-response-threat-hunting-training/](https://www.sans.org/cyber-security-courses/advanced-incident-response-threat-hunting-training/)  
 for advanced labs (free previews available).

**NOTE**:  
Practice in a lab environment to avoid real-world risks.  
Exercises assume a controlled VM environment; do not run malicious code on production systems.

**X** \>  @0xPh4z3d0ut
