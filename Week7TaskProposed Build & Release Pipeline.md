**Proposed Build & Release Pipeline**

**1. Introduction**

This document outlines a proposal for a CI/CD pipeline to automate builds.The goal is to improve productivity and reliability, helping us meet deadlines with consistent, working, platform‑compatible builds.

* * *

**2. Proposed Technology Stack**

### **CI/CD Platform**

We will be using **Jenkins** as our automation server.

Jenkins is a free, open‑source tool that is easy to set up, configure, and distribute across machines for team workflows. It is also highly extensible through its plugin architecture, allowing a wide range of capabilities.

### **Build Tools**

For this project, we will be using **Unreal Engine** with the **Unreal Automation Tool (UAT)**, a command‑line host program.Combined with Jenkins, this provides a powerful CI/CD pipeline.We will be using both Windows and Linux SDKs.

### **Supporting Tools**

* **Artifact storage:** GitHub Artifacts
* **Team notifications:** Microsoft Teams
* **Distribution:** itch.io butler

* * *

**3. Hardware / Cloud Requirements**

### **Build Machine Requirements**

* **CPU:** A modern multi‑core processor to handle parallel compilation and asset processing
* **RAM:** 32 GB minimum, 64 GB recommended for Unreal projects
* **Storage:** 1–2 TB SSD for fast asset importing, shader compilation, and temporary build artifacts, plus additional cloud storage for long‑term retention
* **GPU Requirements:** A mid‑range GPU may be required for shader compilation or editor‑based automation tasks
* **OS Requirements:** Windows 10/11 for Windows builds, and an Ubuntu‑based runner for Linux builds

### **Cloud Runner Requirements**

**Self‑hosted runners**

* Pros: predictable performance, no per‑minute billing, full control over installed tools
* Cons: upfront hardware cost, ongoing maintenance, physical space and power requirements

**Cloud‑hosted runners**

* Pros: scalable, no maintenance, fast setup, pay‑as‑you‑go
* Cons: ongoing cost, limited customisation

Larger projects benefit from self‑hosted runners, while smaller ones may prefer cloud‑hosted options.

For a small team, **1 concurrent build** is sufficient.For multiple developers with frequent commits, **2–3 concurrent builds** is recommended.

### **Storage Requirements**

* **Artifact storage:**
* Windows builds typically range from 1–5 GB. Recommended allocation is 100–200 GB for short‑term artifacts, with cloud storage for long‑term retention.
* **Retention policy:**
  * CI builds: 7–14 days
  * Release candidates: 3–6 months
  * Final releases: kept indefinitely

* * *

**4. Cost Estimates**

### **Initial Costs**

**Hardware**

* Workstation: £1,200–£2,000 for a mid‑range PC (8–16 core CPU, 32–64 GB RAM, 1–2 TB SSD)
* Optional GPU: £200–£300 if required for Unreal shader compilation
* Networking and storage: £100–£300 for additional NAS or external storage

**Cloud Setup**

* Initial setup: £0
* Optional self‑hosted cloud VM: £20–£60 per month depending on CPU/RAM
* Storage buckets: £0.01–£0.02 per GB per month

**Licensing**

* Game engine: Unreal is free until reaching £1 million in revenue, then 5% royalty
* Platform SDKs: £0
* Build tools: Visual Studio Build Tools for Windows are free

### **Ongoing Costs**

* **Cloud compute:** £20–£100 per month depending on usage
* **Storage:** GitHub artifact storage at £0.01–£0.02 per GB per month
* **Maintenance of build machines:**
  * Electricity and wear‑and‑tear: £5–£10 per month
  * Occasional hardware replacement every 3–5 years
  * OS/SDK maintenance time
* **Distribution platform fees:** itch.io butler is free, with optional revenue share

* * *

**5. Target Platform Support**

### **Windows Build Pipeline**

**Required SDKs:**Visual Studio Build Tools, Windows 10/11 SDKs, Unreal’s UBT (UnrealBuildTool) and UAT (Unreal Automation Tool)

**Build Steps:**

1. Checkout source code from the repository
  
2. Install or activate the required engine version
  
3. Restore dependencies (packages, plugins, SDKs)
  
4. Run automated build command: RunUAT BuildCookRun -platform=Win64 -build -cook -pak
  

5. Execute automated tests (unit tests, static analysis, smoke tests)
6. Package the build output into a distributable format
7. Upload packaged Windows build to itch.io using butler, targeting the appropriate channel

* * *

### **Linux Build Pipeline**

**Required SDKs:**Linux toolchain, Unreal Linux cross‑compile toolchain (provided by Epic), required runtime libraries

**Build Steps:**

1. Checkout source code from the repository
  
2. Install or activate the engine with Linux build support
  
3. Ensure Linux toolchain and required libraries are installed
  
4. Run automated build command: RunUAT BuildCookRun -platform=Linux -build -cook -pak
  

5. Run automated tests (headless tests where supported)
6. Package the Linux build into a portable format
7. Upload packaged Linux build to itch.io using butler, targeting the appropriate channel

* * *

**6. Automation Diagram**

[img]

* * *

**7. Distribution Strategy**

### **Internal Distribution**

* **Shared drive/NAS:** Packaged builds will be automatically uploaded to a shared network drive accessible to the development team.
* **Cloud storage link:** Alternatively, Jenkins can upload builds to a cloud storage provider.
* **Automated upload from CI:** Jenkins will handle uploads automatically at the end of the pipeline.

### **External Distribution (itch.io)**

**How builds are uploaded:**Jenkins runs the `butler push` command as the final stage of the pipeline.Only changed files are uploaded, reducing time and bandwidth.Authentication is handled via API keys stored securely in Jenkins credentials.

**Channel/Branch Management:**itch.io supports multiple release channels:

* `windows-beta` / `linux-beta` for internal testers and early access
* `windows-release` / `linux-release` for stable builds

**Automation Steps for Deployment:**

1. Jenkins completes the build and packaging stages
2. Jenkins retrieves the itch.io API key from secure credentials storage
3. Jenkins runs the appropriate butler command for Windows and Linux builds
4. itch.io updates the specified channel and makes the build available immediately
5. Jenkins posts a notification via Teams including:
  * itch.io build link
  * channel name
  * version number
  * commit hash

* * *

**8. Conclusion**

The benefits of a CI/CD pipeline include increased reliability, faster iteration, consistent output, multi‑platform support, streamlined distribution, and improved visibility.

Expected workflow improvements include reduced time spent manually packaging and uploading builds, more predictable release cycles through automation, better collaboration between developers and designers, earlier detection of issues, and clearer traceability for debugging and release management.
