# 📊 Splunk Access Logs Dashboard Project

### Overview
Task Assignment – Splunk Access Logs Dashboard Project
- Assigned By (Manager):
- Role: Cybersecurity Analyst
- Objective: Document Splunk installation process and create a professional dashboard visualizing access logs data.

### Task Assigned To (Employee):

Role: Cybersecurity Analyst

### Project Scope:
You are assigned to document and complete the following:

- Splunk Installation

- Document step-by-step installation of Splunk Enterprise on Linux (manual method).

- Document step-by-step installation of Splunk on Windows using Docker.

- Log File Preparation

- Ingest provided secure.log sample data simulating SSH login attempts (both success and failure).

- Dashboard Development

### Create a Splunk Dashboard with the following:

- Pie Chart for Top Invalid Users.

- Bar Chart for Top Source IP Addresses.

- Time Range Picker to filter data by time.

- Dynamic Dropdown Filters (e.g., protocol selection).

- Data Table displaying fields like src_ip, user, src_port, and protocol.

- Documentation

This README.md file contains:

- Installation guides.

- Dashboard details and screenshots.

- Sample SPL queries used in each panel.

- Organize project folder in GitHub with clear sections for easy reviewer understanding.

### Expected Deliverables:

✅ Complete and working Splunk dashboard

✅ Complete project documentation (README.md)

✅ GitHub repository link for portfolio reference

✅ Screenshots of dashboards with sample data



---

### 📁 Project Structure
```plaintext
/Splunk-Access-Logs-Dashboard
│
├── Linux_Splunk_Installation.md
├── Windows_Docker_Splunk_Installation.md
├── Dashboard_Screenshots/
│   ├── pie_chart_top_invalid_users.png
│   ├── bar_chart_source_ip_count.png
│   └── table_linux_secure_logs.png
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
- We are using two log files in this project `access.log` and `secure.log` file containing simulated access logs and SSH login attempts (both failed and successful).

#### 🎯 Dashboard Goals
- This Dashboard contains multiple panels and use searches (Splunk SPL Searches) to generate Vizualizations.
- Analyze failed and successful SSH login attempts.
- Track top usernames involved in failed logins.
- Identify top source IPs.
- Monitor trends over time using time range selectors.

#### 📊 Dashboard Visualizations
- We first create Custom Dashboard layout called 'Access Log Dashboard' using Classic Dashboards (you can also use Dashboard Studio)

<div align="center">
<img src =src/DashboardCreate.png width="500"> 
 
 <img src =src/DashboardCreate2.png width="300">
</div>
 </br>

 - Then We can see the Empty Dashboard without any panels, we then create the dashboardas per the request
  <div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/Empty%20Dashboard.png> 
</div>
 </br>

- For the dashboard, we can approach using either UI or using source.
- Instead of adding the query from the dashboard, we first create our SPL and create appropiate vizualization from the query and we add to this existing dashboard layout
- I am using the below query for the Top CategoryId using SPL query
  
```SPL
sourcetype=access_combined_wcookie | top categoryId
```
<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/top%20Search.png> 
 </div>
 </br>
 
- Then, we check for the right visualzation and add the panel to the existing dashboard, in our case Dashboard name is "Access Log Dashboard"
  
<div align="center">
<img src =src/top.png> 
 </div>
 </br>

- Now lets go for the second search "clientIP", the query is

```SPL
sourcetype=access_combined_wcookie | stats count by clientip
```
<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/clientip%20search.png> 
 </div>
 </br>
 
- Then, we check for the right visualzation and add the second panel to the same existing dashboard "Access Log Dashboard"

<div align="center">
<img src =src/clientip.png> 
 </div>
 </br>

- Lets go to the dashboard and check for any adjustments needed for the dashboard, if not we can continue with the next search

<div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/Layout%20disorder.png> 
 </div>
 </br>

 - The dashboard looks unorganized to continue further, so we first make the adjustments. Using Edit, we can drag the panels the way we want

<div align="center">
<img src =src/EditedinOrder.png> 
 </div>
 </br>

- Now, lets work on Adding input like time range and submit button
- Choose Time from Add Inputs
  
<div align="center">
<img src =src/TimePicker.png> 
 </div>
 </br>
- Edit the Time Range settings as needed

<div align="center">
<img src =src/TimelineSettings.png> 
 </div>
 </br>

- After refining the time range settings, we need to synchronize this input with the panels. So they can update when we change the Time Range
- For this Go to Edit Search for each panel and update the Tiem Range from there.

<div align="center">
<img src =src/EditSearch.png> 
 </div>
 </br>
 
<div align="center">
<img src =src/SynchronizeTimeline.png> 
 </div>
 </br>

- Next, we will choose the submit buttom from Add inputs, this feature helps to confirm the inputs added before
- 
 <div align="center">
<img src =src/SubmitButton.png> 
 </div>
 </br>

- Now, The output looks like this:

 <div align="center">
<img src =src/Partial.png> 
 </div>
 </br>

- Then, we go back to Search, to continue with our next panel for the dashboard using the query:

```spl
sourcetype=linux_secure | stats count by src, user
```
  
 <div align="center">
<img src =src/NewQueryforSecure.png> 
 </div>
 </br>

- We add the finalized panel to the existing dashboard
  
 <div align="center">
<img src =src/AfterSecureadd.png> 
 </div>
 </br>

- For the new panel, if the user wants to add any dynamic Secure logs to the table, can be used with the text input
  
  <div align="center">
<img src =src/AddText.png> 
 </div>
 </br>

- Edit the Add text settings and copy the token using here to synchronize with the table search string
  
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

- Now, lets say the user is unawre of exact field names what they are looking for, so in order to avoid this issue, we can use the drop down
- Here, we provide the static options as the inbuilt options to choose from the drop down
  
<div align="center">
<img src =src/DropDown.png> 
 </div>
 </br>

 <div align="center">
<img src =src/DropDownStaticOptions.png> 
 </div>
 </br>

- Like we did before, we need to synchronize the settings using the token asscoicate with the search String
  
 <div align="center">
<img src =src/DropDownSync.png> 
 </div>
 </br>

- The final output looks like the professional realworld use case, we can build similar dashboards using this as the reference
  
 <div align="center">
<img src =src/FinalOutput.png> 
 </div>
 </br>


#### ✅ Final Summary
This project highlights practical Splunk skills: log ingestion, parsing, field extraction, and dashboarding with a focus on security use cases.

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
