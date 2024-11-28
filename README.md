# Cybersecurity Investigation Project: Employee Data Breach Analysis

## Overview
A client reported an employee data breach within their organization. As a startup, the company faced significant budget constraints, limiting their ability to invest in robust security infrastructure and comprehensive employee training. During the investigation, the client provided several suspicious emails and a USB drive found on their premises. The objective of this project was to analyze the contents of the USB drive, investigate any potentially malicious files, and determine whether the breach could have been caused by these items.

---

## Investigation Process

### 1. Client Briefing and Initial Assessment
I was initially briefed by the client regarding the breach. The client had a limited security budget, and the breach was suspected to have stemmed from compromised employee data. They reported finding suspicious emails and a USB drive left on their premises, which seemed to be the focal point of the investigation.

### 2. Collecting Suspicious Evidence
During the site visit, I collected two primary pieces of evidence:
- A set of suspicious emails that could potentially be phishing attempts or social engineering attacks.
- A USB drive that an employee had found on the company premises, which might contain malicious files.

### 3. Preparing the Analysis Environment
To begin the analysis, I utilized **Remnux**, a specialized Linux-based distribution for malware analysis. Remnux is equipped with a variety of tools that help in the safe examination of suspicious files, such as those found on the USB drive.

### 4. Extracting Files from the USB Drive
Upon connecting the USB drive to the Remnux environment, I extracted the contents from the drive into a secure working directory to isolate any potentially harmful files and minimize the risk of further compromise.
  
![](https://i.imgur.com/cCB9sQ6.png)

### 5. Unzipping the Files for Analysis
Several files on the USB drive were compressed in `.zip` format. I proceeded to unzip these files to make them accessible for further inspection. This step was essential to uncover all potential files that might have been hidden inside the compressed archive.

![](https://i.imgur.com/AulcG7l.png)
![](https://i.imgur.com/voK3gYV.png)

### 6. Verifying the Integrity of the Extracted Files
Once the files were unzipped, I performed an integrity check by generating hashes for the extracted files. By calculating the SHA256 hash values for each file, I was able to ensure the integrity of the files and later check them against known databases to verify if they had been flagged as malicious in the past.
![](https://i.imgur.com/ikNo4Bk.png)

### 7. Verifying the Signature of the PDF File
Among the extracted files, there was a PDF document. Opening the PDF file directly could potentially activate any embedded malicious code. To mitigate this risk, I first examined the file's signature using a hex dump tool. By inspecting the file's header, I confirmed that it was indeed a PDF document and not some other type of potentially harmful file masquerading as a PDF.
![](https://i.imgur.com/HHUQX6I.png)

![](https://i.imgur.com/jc0ku2b.png)

### 8. Analyzing the PDF File’s Structure
After confirming that the file was a legitimate PDF, I used **PPDF (PDF Parsing and Dissection Tool)** to analyze its internal structure. This allowed me to examine the individual components of the PDF, such as embedded scripts, objects, and other elements, which could potentially be used for malicious purposes.
![](https://i.imgur.com/s4MI0E7.png)

### 9. Identifying Suspicious Objects within the PDF
While parsing the PDF, I identified several suspicious objects, particularly **Object 27** and **Object 28**, which seemed to exhibit unusual behavior. I closely examined these objects to understand their function and determine if they posed any security risks.
![](https://i.imgur.com/oqE7Ovo.png)

![](https://i.imgur.com/lGxvEtZ.png)

### 10. Investigating Object 27: Command Execution Attempt
Object 27 appeared to reference `cmd.exe`, a command prompt executable, which is commonly used in Windows environments. The object seemed to be trying to execute a command that would open a file located in the **System32** directory, which is often targeted by malware. This behavior indicated that the PDF might be attempting to execute system commands without user consent.
![](https://i.imgur.com/bkamrEx.png)

### 11. Investigating Object 3: Auto-Action (AA) Mechanism
I also examined **Object 3**, which contained an **AA (Auto-Action)** action. The AA action is a feature in PDF files that triggers automatic execution of a command when the document is opened. This was a significant red flag, as it indicated the potential for this PDF to execute malicious activity upon being viewed by an unsuspecting user.
![](https://i.imgur.com/HKkalBi.png)

### 12. Submitting the PDF to VirusTotal for Analysis
To validate my findings and cross-check the PDF for known threats, I submitted the file to **VirusTotal**, an online service that scans files using multiple antivirus engines. The scan results confirmed my suspicions, as the file was flagged by several antivirus engines as malicious.
![alt text](https://i.imgur.com/LBZwRCx.png)

---

## Conclusion and Recommendations
The analysis confirmed that the PDF file was indeed malicious. It attempted to execute unauthorized commands on the system and contained auto-execution actions that could trigger further harm. Based on this investigation, I provided the client with the following recommendations:

### 1. Employee Training
Conduct regular cybersecurity awareness training to prevent employees from falling victim to phishing and social engineering attacks.

### 2. Endpoint Protection
Implement stronger endpoint security measures, such as antivirus and endpoint detection software, to identify and block malicious files before they can cause damage.

### 3. USB Drive Management
Establish a strict policy for using USB drives within the organization. Ensure that all external devices are scanned for malware before being connected to the company’s network.

### 4. File Integrity Monitoring
Regularly monitor and verify file integrity using hash-based checks to detect unauthorized or malicious files before they can compromise the system.

---

