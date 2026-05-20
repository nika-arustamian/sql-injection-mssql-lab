# SQL Injection and MSSQL Enumeration Lab

## Repository Name

sql-injection-mssql-lab

## Description

Practical cybersecurity lab focused on SQL Injection, DVWA exploitation, MSSQL authentication, enumeration, and password hash analysis using Metasploit.

## Overview

This project is a practical cybersecurity lab focused on SQL Injection, database enumeration, password hash analysis, and MSSQL exploitation in a controlled environment.

The main goal of this lab was to understand how SQL Injection works in practice, how sensitive data can be extracted from a vulnerable web application, and how MSSQL enumeration can be performed after gaining valid credentials.

This homework was challenging but very useful because it required not only following instructions, but also troubleshooting errors, checking different approaches, and understanding why each step works.

## Lab Objectives

- Identify and exploit a SQL Injection vulnerability in DVWA.
- Extract usernames and password hashes from the database.
- Analyze and crack password hashes.
- Authenticate to an MSSQL server using valid credentials.
- Enumerate MSSQL server information.
- Check available databases and SQL logins.
- Practice working with Metasploit modules for MSSQL.

## Tools Used

- DVWA
- MSSQL Server
- Metasploit Framework
- CyberChef
- CrackStation
- Terminal
- Browser

## Lab Environment

The lab was performed in a local controlled environment.

Main components:

- Vulnerable web application: DVWA
- Database server: MSSQL Server
- Testing framework: Metasploit
- Operating system: macOS
- Browser-based testing for SQL Injection
- Terminal-based testing for MSSQL enumeration

## Steps Performed

## 1. Accessing the Vulnerable Web Application

I opened DVWA and navigated to the SQL Injection section.

The security level was set to Low, which allowed testing basic SQL Injection payloads in a controlled lab environment.

## 2. Testing SQL Injection

I tested the input field with a basic SQL Injection payload to check whether the application was vulnerable.

Payload used:

1' OR '1'='1' #

The application returned multiple users instead of only one result, confirming that the SQL Injection was successful.

## 3. Extracting Users and Password Hashes

Using UNION-based SQL Injection, I extracted usernames and password hashes from the users table.

Payload used:

-1' UNION SELECT user, password FROM users #

The output included several users, such as:

- admin
- gordonb
- 1337
- pablo
- smithy

The password hashes were displayed in the output and could be used for further analysis.

## 4. Password Hash Analysis

One of the extracted hashes was checked using CyberChef and CrackStation.

Hash example:

e99a18c428cb38d5f260853678922e03

Cracked password:

abc123

This demonstrated how weak passwords can be recovered when password hashes are exposed and stored without strong protection.

## 5. MSSQL Authentication with Metasploit

After identifying valid MSSQL credentials, I used Metasploit to authenticate to the MSSQL server.

The login was successful, and an MSSQL session was opened.

Result:

Login Successful
MSSQL session opened

This confirmed that the credentials were valid and that the MSSQL service was accessible.

## 6. SQL Server Version Enumeration

Inside the MSSQL session, I executed a query to identify the SQL Server version.

Query used:

SELECT @@version;

The result showed that the target was running Microsoft SQL Server 2022 Developer Edition on Linux.

## 7. Database Enumeration

I listed available databases using the following query:

SELECT name FROM master.dbo.sysdatabases;

The output showed default system databases and a test database created during the lab.

Example databases:

- master
- tempdb
- model
- msdb
- YouAreHacked

## 8. MSSQL Login Enumeration

I also used Metasploit modules to enumerate SQL Server logins and confirm privileges.

The results showed that the sa account had sysadmin privileges, which represents a serious security risk if exposed or protected with weak credentials.

## Key Findings

- The DVWA SQL Injection page was vulnerable to SQL Injection.
- UNION-based SQL Injection allowed extraction of usernames and password hashes.
- At least one MD5 hash was successfully identified.
- MSSQL authentication was successful using valid credentials.
- The MSSQL server allowed enumeration of version, databases, and logins.
- The sa account had high privileges.
- Weak or exposed credentials can lead to serious database compromise.

## Screenshots

## Successful MSSQL Login
<img width="2048" height="1280" alt="01_successful_mssql_login" src="https://github.com/user-attachments/assets/cc6f2e96-13a0-4469-bf39-b86bd5e041f8" />

## SQL Server Version
<img width="2048" height="1280" alt="02_sql_server_version" src="https://github.com/user-attachments/assets/ddb52cde-df23-40f9-924d-8c46f937c6dc" />


## Database Enumeration
<img width="1562" height="1656" alt="03_database_enumeration_youarehacked" src="https://github.com/user-attachments/assets/2cbadadd-7f23-442f-bf72-a662292974b0" />

## DVWA SQL Injection Result
<img width="782" height="437" alt="04_dvwa_sql_injection_users_hashes" src="https://github.com/user-attachments/assets/4058c6ea-10b9-4418-989e-7f1e2b6b4a57" />



## Hash Cracking Result
<img width="1566" height="1666" alt="05_hash_cracking_result" src="https://github.com/user-attachments/assets/2c6746d2-e35e-4dec-9bba-b5a4b3f95d64" />


## MSSQL Login Enumeration
<img width="1566" height="1662" alt="06_mssql_login_enumeration" src="https://github.com/user-attachments/assets/43b70ced-f95e-4fcf-9516-e69b9403695a" />


## What I Learned

This lab helped me better understand how SQL Injection works in practice and how database misconfigurations or weak credentials can be exploited.

The most useful part was seeing how theory becomes real practice: SQL Injection, password hashes, Metasploit, MSSQL sessions, and enumeration all connected together in one workflow.

It was also important to troubleshoot errors during the process, because it helped me understand the logic behind the commands instead of only copying them.

After completing this lab, I feel more motivated to continue practicing hands-on cybersecurity tasks and improve my practical skills.

## Security Recommendations

To prevent similar vulnerabilities in real systems:

- Use prepared statements and parameterized queries.
- Validate and sanitize user input.
- Never store passwords as plain MD5 hashes.
- Use strong password hashing algorithms such as bcrypt, Argon2, or PBKDF2.
- Disable or restrict high-privileged accounts such as sa.
- Use strong and unique passwords.
- Limit database access from external networks.
- Monitor authentication attempts and suspicious database activity.
- Keep database servers and applications updated.
- Apply the principle of least privilege.

## Conclusion

This lab demonstrated how SQL Injection can be exploited to extract sensitive data from a vulnerable application and how valid database credentials can be used to enumerate an MSSQL server.

It was a valuable practical exercise that improved my understanding of web application security, database security, password hash analysis, and basic penetration testing workflow.
