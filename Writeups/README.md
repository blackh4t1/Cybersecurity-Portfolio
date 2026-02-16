# Documentation of labs (TryHackMe, Hack The Box, PortSwigger)

** DOCUMENTATION TEMPLATE EXAMPLE:
create a new .md file (e.g., SQL-Injection-Lab.md)

# Lab Report: [Lab Name]
**Date:** February 2026
**Platform:** [e.g., PortSwigger Academy / Hack The Box]
**Difficulty:** [Easy/Medium/Hard]

---

## 🎯 Executive Summary
During this lab, I successfully identified and exploited a **[Vulnerability Name]** on the **[Target Component, e.g., Login Page]**. This flaw could allow an attacker to **[Business Impact, e.g., view private user data]**.

## 🛠️ Methodology & Steps
### 1. Reconnaissance
I started by intercepting traffic using **Burp Suite**. I noticed that the `id` parameter in the URL was visible.
* **Target URL:** `https://example.com/user/profile?id=100`

### 2. Vulnerability Identification
I attempted to change the `id` parameter from `100` to `101`. 
* **Observation:** The server returned the profile details for a different user without requiring authentication.

### 3. Exploitation (Proof of Concept)
By automating this request using Burp Intruder, I was able to dump the first 50 user profiles in the database.

> [!IMPORTANT]
> **Payload used:** `GET /user/profile?id=§1§ HTTP/1.1`

## 📉 Risk Assessment
* **Likelihood:** High (No special tools required)
* **Impact:** High (Confidentiality breach of all user data)
* **Overall Severity:** **CRITICAL**

## 💡 Remediation
To fix this, the application should implement **Object-Level Access Control**. The server must verify that the currently logged-in user has permission to view the requested `id` before returning data.
