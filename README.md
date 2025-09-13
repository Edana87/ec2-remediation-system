# 🚨 EC2 Monitoring & Remediation Workflow: ServiceNow × AWS Integration

---

## 🛠️ **Technologies Used**
- **ServiceNow Personal Developer Instance (PDI)** – Yokohama Release  
- **AWS Integration Server** (Netflix internal)  
- **Draw.io** – for system architecture diagramming  
- **Slack Webhook** – for DevOps notifications  

---

## 🏢 **System Overview**

**Netflix**—streaming to over 260 million subscribers globallyrelies on AWS EC2 instances to power its recommendation engine, content delivery network, and streaming infrastructure.  
A recent EC2 failure exposed workflow gaps:

> **Incident Details:**  
> - ❌ **EC2 instance failure was not flagged in time**  
> - 🕒 **45-minute delay in detection**  
> - 📉 **Resulted in degraded streaming quality and potential subscriber churn**  
> - 📂 **DevOps engineers had to manually search for remediation steps**  
> - ⚠️ **No centralized system for incident creation or automated guidance**  

---

## 🎯 **Objective**

Build a semi-automated incident response system that:
- **Detects EC2 instance failures in real time**
- **Creates incidents automatically in ServiceNow**
- **Retrieves remediation guidance using AI Search**
- **Sends Slack notifications to DevOps engineers**
- **Enables one-click remediation via ServiceNow UI**
- **Logs all remediation attempts for audit and analysis**

---

## 👩‍💻 **Edana's Role**

As a **ServiceNow Administrator and Jr Developer** on Netflix’s IT Infrastructure team, she was tasked with architecting a scalable, integrated solution that closes the gap between AWS monitoring and ServiceNow incident management.

---

## 📝 **Implementation Steps**

### 🔧 **Step 1: Scoped Application Setup**
- Created scoped app: **EC2 Monitoring and Remediation**
- Scope name auto-generated: `x_snc_ec2_monito_0`
- Ensured compatibility with AWS Integration Server

### 📊 **Step 2: Table Configuration**
- **EC2 Instance Table:**  
  - Tracks instance name, ID, and status (`ON`/`OFF`)
  - Auto-populated every minute by AWS Integration Server
- **Remediation Log Table:**  
  - Captures remediation attempts, payloads, timestamps, and HTTP status codes

### 🔐 **Step 3: AWS Integration Setup**
- **Connection Alias:** AWS Integration Server C C Alias  
- **Host:** codon-staging.emaginelc.com  
- **Base path:** `/api/v1/queue/start`  
- **Credentials:** Basic Auth using ServiceNow login

### 🖱️ **Step 4: UI Action & Script Include**
- **UI Action:** Trigger EC2 Remediation – adds button to EC2 form
- **Script Include:** `EC2RemediationHelper.js` – handles API calls to AWS

### 🔁 **Step 5: Flow Designer Workflow**
- **Trigger:** EC2 status = `OFF`
- **Actions:**  
  - Create incident  
  - Run AI Search Custom Action  
  - Send Slack notification with KB article  
- Used “Force Save” to ensure all components were captured

### 🧠 **Step 6: AI Search Integration**
- **Parameters:**  
  - Search Term: EC2-related keywords  
  - Enable Detailed Logging: ✅  
  - Search App: Identified via AI Search Admin Home > Applications  
- Verified functionality via system logs and test queries

### 📚 **Step 7: Knowledge Base Article**
- Created KB article with remediation instructions:  
  > “Run the UI Action ‘Trigger EC2 Remediation’ on the associated record.”
- Included keywords for AI discoverability:  
  `EC2, server, instance, restart, AWS, virtual machine, cloud server, reboot`

### ✅ **Step 8: Testing & Validation**
- EC2 table auto-populated every minute
- Instances turned “OFF” every 10 minutes for testing
- Verified incident creation, Slack notification delivery, and KB retrieval
- Confirmed remediation logs were captured correctly

---

## 🗺️ **Architecture Diagram**

Visual representation of the complete system flow (created in Draw.io):

![Insert Diagram.png here]

---

## 📸 **Screenshot Placeholders**

Succesful Knowledge Article Fetch- <img width="1725" height="911" alt="Knowledge article fetch" src="https://github.com/user-attachments/assets/4e7ad778-bc27-4498-96e9-b32ef232fca0" />
Knowledge Article creation- <img width="987" height="939" alt="Knowledge Article creation" src="https://github.com/user-attachments/assets/e6ef244a-59ba-4cad-a4c3-7f20e2456865" />
Workflow- <img width="987" height="939" alt="Knowledge Article creation" src="https://github.com/user-attachments/assets/06d04b80-5797-4946-8b22-0f2dbed33cdd" />
Succesful Slack Message- <img width="1363" height="290" alt="image" src="https://github.com/user-attachments/assets/07666495-7bd9-495f-b7f9-d385dcd97f63" />


---

## 🧪 **Areas of Optimization**

Even with a fully functional EC2 remediation system, there are opportunities to enhance usability, clarity, and operational efficiency.  
Below are key areas identified for future refinement:

### 📝 **Incident Record Description Enhancement**
The current **“Create Incident”** action in Flow Designer generates a generic incident record when an EC2 instance fails. However, the default description lacks context, which can slow down triage and resolution.
<img width="1897" height="923" alt="image" src="https://github.com/user-attachments/assets/92b80b27-0169-4155-b6ad-b83888ea0b26" />


> **Optimization Opportunity:**  
> - **Dynamic Descriptions:** Include instance name, ID, failure timestamp, and remediation instructions directly in the incident description.  
> - **Suggested Format:**  
>   ```  
>   EC2 Instance [Name] ([ID]) failed at [Timestamp].
>   Remediation: [Instructions or reference to KB article].
>   ```  
>   This ensures DevOps engineers have immediate clarity without needing to cross-reference other tables or documentation.

---

## 🚀 **Future Enhancements**

- **Slack Interactivity:** Enable Slack buttons for “Acknowledge” or “Remediate” directly from the message

---

## 🙏🏾 **Thanks for Scrolling This Far**

If you’ve made it all the way down here, you’re either really into EC2 workflows… or just appreciate a well-structured README. Either way, I salute you.  
Feel free to reach out if you want to collaborate or optimize further.

_Built with curiosity, caffeine, and a touch of chaos 🤯_.
