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
<img src =src/DashboardCreate.png width="500"> <img src =src/DashboardCreate2.png width="300">
</div>
 </br>

 - Then We can see the Empty Dashboard without any panels, we then create the dashboardas per the request
  <div align="center">
<img src =https://github.com/Bharathkasyap/Splunk_Dashboard/blob/main/src/Empty%20Dashboard.png width="500"> 
</div>
 </br>
 
- 🟣 **Pie Chart** → Top Invalid Users.
  - _Example Screenshot:_  
  `![Pie Chart](Dashboard_Screenshots/pie_chart_top_invalid_users.png)`
- 🟣 **Bar Chart** → Top Source IPs.
  - _Example Screenshot:_  
  `![Bar Chart](Dashboard_Screenshots/bar_chart_source_ip_count.png)`
- 🟣 **Table** → Detailed view of login events.
  - _Example Screenshot:_  
  `![Table](Dashboard_Screenshots/table_linux_secure_logs.png)`
- 🟣 **Dropdown Input** → Dynamic filters for user or status.
- 🟣 **Time Range Picker** → Flexible timeline selection.

#### 💻 Sample Queries Used
##### Failed logins by user
```spl
source="secure.log" | rex "Failed password for (invalid user )?(?<user>\S+)" | stats count by user
```
##### Successful logins by user
```spl
source="secure.log" | search "Accepted password" | rex "Accepted password for (?<user>\S+)" | stats count by user
```
##### Top source IP addresses
```spl
source="secure.log" | rex "from (?<src>\d{1,3}(?:\.\d{1,3}){3})" | stats count by src
```

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
