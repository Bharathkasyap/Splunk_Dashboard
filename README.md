# 📊 Splunk Access Logs Dashboard Project

## Overview
This project outlines the process of deploying Splunk Enterprise and developing a comprehensive dashboard for visualizing access and SSH login attempts. It serves as a practical demonstration of Splunk's capabilities in security analytics.

Task Assignment – Splunk Access Logs Dashboard Project
- Assigned By (Manager):
- Role: Cybersecurity Analyst
- Objective: Document Splunk installation process and create a professional dashboard visualizing access logs data.

## Role & Objective
- Role: Cybersecurity Analyst
- Objective: To document the Splunk installation process and create a professional dashboard for visualizing access log data, specifically focusing on SSH login attempts.

## Project Scope:
You are assigned to document and complete the following:

### Splunk Installation
- Document step-by-step installation of Splunk Enterprise on Linux (manual method).
- Document step-by-step installation of Splunk on Windows using Docker.

### Log File Preparation

- ✅ Ingest pre-simulated log files (`secure.log` and `access.log`) into Splunk.

### Dashboard Development
Create a Splunk Dashboard with the following:

- Pie Chart for Top CategoryId's.
- Bar Chart for Client IP Addresses.
- Time Range Picker to filter data by time.
- Dynamic Input Option (eg., src_port)
- Dynamic Dropdown Filters (e.g., protocol selection).
- Data Table displaying fields like src_ip, user, src_port, and protocol.
- Documentation

### This README.md file contains:
- Installation guides.
- Dashboard details and screenshots.
- Sample SPL queries used in each panel.
- Organize project folder in GitHub with clear sections for easy reviewer understanding.

### Expected Deliverables:

- ✅ Complete and working Splunk dashboard
- ✅ Complete project documentation (README.md)
- ✅ GitHub repository link for portfolio reference
- ✅ Screenshots of dashboards with sample data

---

### 📁 Project Structure
```plaintext
/Splunk-Access-Logs-Dashboard
│
├── Linux_Splunk_Installation.md
├── Windows_Docker_Splunk_Installation.md
├── Dashboard_Screenshots/
├── Dashboard_XML_Code.xml
├── Sample_Search_Queries.md
└── secure.log
```

---

<details>
<summary>### 💻 Linux Installation Steps</summary>

#### Step 1: Download Splunk Binary
- Go to: https://www.splunk.com/en_us/download/splunk-enterprise.html
- Use `wget` to download the `.deb` package.

#### Step 2: Install Splunk
```bash
sudo dpkg -i splunk-version.deb
```

#### Step 3: Install net-tools
```bash
sudo apt install net-tools
```

#### Step 4: Start Splunk
```bash
cd /opt/splunk/bin
./splunk start
```

</details>

<details>
<summary>### 🖥️ Windows Installation Using Docker</summary>

#### Step 1: Install Docker Desktop
- Reference: https://docs.docker.com/desktop/install/windows-install/

#### Step 2: Deploy Splunk Container
```bash
docker pull splunk/splunk:latest
docker run -d -p 8000:8000 -p 8088:8088 -p 9997:9997 \
-e SPLUNK_START_ARGS="--accept-license" \
-e SPLUNK_PASSWORD="Password@123" splunk/splunk:latest
```

#### Step 3: Access Splunk
- Go to: http://localhost:8000

</details>

---

### 📊 Dashboard Description

#### 📂 Dataset Used
- This project utilizes two simulated log files: access.log for web access events and secure.log for SSH login attempts, encompassing both successful and failed authentication events.

#### 🎯 Dashboard Goals

- Visualize and analyze both failed and successful SSH login attempts.
- Identify and track top usernames associated with failed login attempts.
- Determine and monitor prevalent source IP addresses for web access.
- Observe trends over time through the use of time range selectors.
- Generate comprehensive visualizations using Splunk Processing Language (SPL) searches across multiple panels.

#### 📊 Dashboard Visualizations

- We begin by creating a custom dashboard layout named 'Access Log Dashboard' using Classic Dashboards (though Dashboard Studio is also an option).
- Upon creation, the dashboard will initially appear empty. Panels will then be added according to the specified requirements.
- Dashboard construction can be approached through either the Splunk UI or by directly editing the source XML. For this project, we primarily leverage the UI to build panels from pre-defined SPL queries.
- To illustrate, we'll first create an SPL query for Top Category IDs from access_combined_wcookie sourcetype:

<div align="center">
<img src =src/DashboardCreate.png width="500"> 
 
 <img src =src/DashboardCreate2.png width="300">
</div>
 </br>

 - Here, We see the Empty Dashboard without any panels, we then create the dashboardas per the request
   
  <div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/Empty%20Dashboard.png> 
</div>
 </br>

- Query used for the Top CategoryId:
  
```SPL
sourcetype=access_combined_wcookie | top categoryId
```

- After executing the query, we select the appropriate visualization (e.g., a Pie Chart) and add the panel to our 'Access Log Dashboard'.
- Next, we create a search for client IP addresses from access_combined_wcookie sourcetype to count occurrences:


<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/top%20Search.png> 
 </div>
 </br>
 
- We then choose a suitable visualization, such as a Bar Chart, and add this second panel to the 'Access Log Dashboard'.
  
<div align="center">
<img src =src/top.png> 
 </div>
 </br>

- Now lets go for the second Panel "clientIP", the query is

```SPL
sourcetype=access_combined_wcookie | stats count by clientip
```
<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/clientip%20search.png> 
 </div>
 </br>
 

- Initially, the dashboard layout might appear unorganized.


<div align="center">
<img src =src/clientip.png> 
 </div>
 </br>

- We can easily adjust the arrangement of panels by dragging and dropping them into desired positions within the Edit mode, ensuring a more coherent presentation.

<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/Layout%20disorder.png> 
 </div>
 </br>

 - The dashboard looks unorganized to continue further, so we first make the adjustments. Using Edit, we can drag the panels the way we want

<div align="center">
<img src =src/EditedinOrder.png> 
 </div>
 </br>

- Now, we proceed to add interactive input elements, starting with a Time Range Picker.

- Select 'Time' from the Add Inputs menu.
  
<div align="center">
<img src =src/TimePicker.png> 
 </div>
 </br>
 
- Configure the Time Range settings as required for data filtering.

<div align="center">
<img src =src/TimelineSettings.png> 
 </div>
 </br>

- To ensure that panels update dynamically with the selected time range, synchronize the input. This is achieved by editing the search for each panel and linking it to the newly configured time input.

<div align="center">
<img src =src/EditSearch.png> 
 </div>
 </br>

 - Following the time range input, we integrate a Submit Button from the Add Inputs menu. This button allows users to confirm input selections before applying them to the dashboard.
   
<div align="center">
<img src =src/SynchronizeTimeline.png> 
 </div>
 </br>

- Next, we will choose the submit buttom from Add inputs, this feature helps to confirm the inputs added before
  
 <div align="center">
<img src =src/SubmitButton.png> 
 </div>
 </br>


- The dashboard, with the added time picker and submit button, now appears as follows:
  
 <div align="center">
<img src =src/Partial.png> 
 </div>
 </br>

- Next, we return to the search interface to create a panel for SSH login attempts, using a query to count occurrences by source and user:

```spl
sourcetype=linux_secure | stats count by src, user
```
  
 <div align="center">
<img src =src/NewQueryforSecure.png> 
 </div>
 </br>

- This finalized panel is then added to the existing dashboard.

<div align="center">
<img src =src/AfterSecureadd.png> 
</div>
</br>

- For enhanced interactivity, a Text Input can be added, allowing users to dynamically filter secure logs within the table.
  
  <div align="center">
<img src =src/AddText.png> 
 </div>
 </br>

- Configure the text input settings and copy the associated token to link it with the table's search string.
  
- Embed the token within the table's search string to enable dynamic filtering based on user input.
  
  <div align="center">
<img src =src/EditAddText.png> 
 </div>
 </br>

  <div align="center">
<img src =src/AfterAddText.png> 
 </div>
 </br>

- Use the token used for the Add Text settings and Provide with the search String to associate with the input settings
  
  <div align="center">
<img src =src/AfterSyncDynamicLogTest.png> 
 </div>
 </br>

- To assist users unfamiliar with exact field names, a Dropdown Input can be implemented. This provides a predefined set of static options for selection.
  
<div align="center">
<img src =src/DropDown.png> 
 </div>
 </br>

 <div align="center">
<img src =src/DropDownStaticOptions.png> 
 </div>
 </br>

- Similar to the text input, synchronize the dropdown's token with the relevant search string to enable dynamic filtering based on dropdown selections.

 <div align="center">
<img src =src/DropDownSync.png> 
 </div>
 </br>

- The completed dashboard showcases a professional and practical real-world application of Splunk's dashboarding capabilities, serving as a valuable reference.
  
 <div align="center">
<img src =src/FinalOutput.png> 
 </div>
 </br>


#### ✅ Final Summary
This project effectively demonstrates key Splunk proficiencies, including log ingestion, data parsing, field extraction, and dashboard creation, with a strong emphasis on security-related use cases.

---

### 📌 How to Use This Project
- 📥 Import `.xml` file into Splunk to replicate the dashboard.
- 💻 Use installation markdown files to deploy Splunk.
- 📝 Customize search queries if you use different log files.

---

### 👨‍💻 Author
- **Prepared by:** Venkata Bharath Devulapalli
- **LinkedIn:** [https://www.linkedin.com/in/venkatadevu/](https://www.linkedin.com/in/venkatadevu/)
- **GitHub Portfolio:** [https://github.com/Bharathkasyap](https://github.com/Bharathkasyap)

---

### 📄 License
This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.
