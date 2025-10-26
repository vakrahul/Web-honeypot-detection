# 🕸️ Web Honeypot Detection Project

[![Project Status](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/vakrahul/YOUR_REPO_NAME/actions)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/vakrahul/YOUR_REPO_NAME?style=social)](https://github.com/vakrahul/YOUR_REPO_NAME/stargazers)

---

## 🎯 Project Overview

This project implements a **low-interaction web honeypot** designed to simulate a secure login portal. Its core mission is to **detect, capture, and analyze malicious login attempts**, such as brute force attacks, credential stuffing, and vulnerability scanning, without compromising real systems.

It features a realistic user-facing login page (`index.html`) that acts as the trap, and a separate, secure admin dashboard (`admin.html`) for monitoring and analyzing the data collected from attackers in real-time.

---

## ✨ Core Features

### 🍯 Honeypot (User-Facing)

* **Realistic Login & Signup:** A convincing "Secure Login Portal" (`index.html`) and "Account Signup" (`signup.html`) are presented to appear as a legitimate service, encouraging interaction from attackers.
* **Credential Capture:** Every login attempt, including both username and password, is securely captured and logged to a Firebase Realtime Database for later analysis.
* **Brute Force Detection:** The system actively tracks failed login attempts from a single IP address. After a configurable threshold of failures, it triggers alerts and can automatically block the offending IP.
* **Automatic IP Blocking:** Malicious IPs that exceed the predefined failed login limit are temporarily blocked from accessing the honeypot portal, mitigating continuous attacks.
* **Client-Side Honeytokens:** The honeypot's client-side code (`index.html`) intentionally includes fake, commented-out credentials and API keys (`honeyTokens`). Any attempt to access, copy, or use these tokens is logged as a suspicious activity, indicating a more advanced attacker.

### 📊 Admin Dashboard

* **Secure Admin Login:** A dedicated, private login page (`admin.html`) for administrators ensures monitoring access is restricted. It uses distinct, hardcoded credentials, completely separate from the public-facing honeypot.
* **Data Visualization:** The dashboard provides dynamic and insightful charts (powered by Chart.js) to visualize key attack metrics:
    * `Login Attempts Over Time`: Track attack frequency and patterns.
    * `Most Common Usernames Attempted`: Identify common targets (e.g., "admin", "root", "test").
* **Real-time Statistics:** Get live updates on crucial metrics, including total login attempts, detected brute force attacks, unique attacking IP addresses, and daily attempt counts.
* **Detailed Attempt Logs:** A comprehensive table displays all recent login attempts, providing granular data like timestamp, captured username, captured password, attacker's IP address, and User Agent string.
* **Manual IP Management:** The administrator can easily view a list of all currently blocked IP addresses, understand the reason for each block, and manually unblock any IP if necessary.

---

## 🛠️ Technologies Used

* **Frontend:** HTML5, CSS3, JavaScript
* **Backend & Database:** [Firebase](https://firebase.google.com/) (Realtime Database & Authentication)
* **Libraries:**
    * [Bootstrap 5](https://getbootstrap.com/): For a responsive and modern user interface across all pages.
    * [Chart.js](https://www.chartjs.org/): For creating interactive and informative data visualizations in the admin dashboard.

---

## 🚀 Setup and Installation

To deploy and run this web honeypot, follow these steps to configure it with your own Firebase project.

1.  **Create a Firebase Project:**
    * Navigate to the [Firebase Console](https://console.firebase.google.com/) and create a new project.
    * Within your new Firebase project, enable the **Authentication** service and configure the "Email/Password" sign-in method.
    * Also, create a **Realtime Database** instance.

2.  **Get Firebase Configuration:**
    * In your Firebase project settings, locate and copy your "Web app" configuration object. It will resemble the structure below:
        ```javascript
        const firebaseConfig = {
          apiKey: "AIzaSyC...",
          authDomain: "your-project-id.firebaseapp.com",
          databaseURL: "[https://your-project-id-default-rtdb.firebaseio.com](https://your-project-id-default-rtdb.firebaseio.com)",
          projectId: "your-project-id",
          storageBucket: "your-project-id.appspot.com",
          messagingSenderId: "1234567890",
          appId: "1:234567890:web:abcdef123456"
        };
        ```

3.  **Update Project Files with Firebase Config:**
    * Copy the entire `firebaseConfig` object.
    * Paste this configuration into the `<script>` section (typically at the bottom, before the closing `</body>` tag) of *all four* HTML files:
        * `index.html`
        * `signup.html`
        * `admin.html`
        * `dashboard.html`

4.  **Set Secure Admin Credentials:**
    * Open `admin.html` in your code editor.
    * Locate the following lines within the `<script>` section and **change the values** to your desired secure admin email and password:
        ```javascript
        // Admin credentials - ***CHANGE THESE TO SECURE VALUES!***
        const ADMIN_EMAIL = "your_admin_email@example.com"; // e.g., "admin@myhoneypot.com"
        const ADMIN_PASSWORD = "your_strong_admin_password"; // e.g., "SuperSecretAdmin123!"
        ```
    * **⚠️ This is a critical security step!** Do not leave the default or easily guessable credentials.

5.  **Deploy Your Honeypot:**
    * Host these static HTML and JavaScript files on any preferred static web hosting service (e.g., Firebase Hosting, GitHub Pages, Netlify, Vercel).
    * Your honeypot's public-facing login portal will be accessible via `index.html`.
    * You can monitor captured data and manage IPs by visiting `admin.html` (after securely logging in with your chosen admin credentials).

---

## 📁 File Structure

```
.
├── admin.html       # The secure, password-protected admin dashboard for monitoring collected data and managing IPs.
├── dashboard.html   # A fake, static user dashboard displayed to attackers after a "successful" login to create a more convincing trap.
├── index.html       # The main public-facing login page – this is the core of the honeypot.
└── signup.html      # A simulated user registration page to enhance the honeypot's legitimacy.
```

---

## 🤝 Contributing

Contributions are welcome! If you have suggestions for improvements, bug fixes, or new features, please open an issue or submit a pull request.

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Made with ❤️ by Rahul Vakiti
</p>
