# Web Honeypot Detection Project

This project is a low-interaction web honeypot designed to simulate a secure login portal. Its primary purpose is to detect, capture, and analyze malicious login attempts, such as brute force attacks, credential stuffing, and vulnerability scanning.

It features a realistic user-facing login page (`index.html`) that acts as the trap, and a separate, secure admin dashboard (`admin.html`) for monitoring and analyzing the data collected from attackers.

---

## Core Features

### Honeypot (User-Facing)
* **Realistic Login & Signup:** A convincing "Secure Login Portal" (`index.html`) and "Account Signup" (`signup.html`) to appear as a legitimate service.
* **Credential Capture:** All login attempts (both username and password) are captured and logged to a Firebase Realtime Database for analysis.
* **Brute Force Detection:** The system tracks failed login attempts from a single IP. After a set number of failures, it triggers alerts and can block the IP.
* **Automatic IP Blocking:** Malicious IPs that exceed the failed login threshold are automatically and temporarily blocked from accessing the portal.
* **Client-Side Honeytokens:** The login page's code intentionally includes fake, commented-out credentials and API keys (`honeyTokens`) as a trap. Any attempt to access or use these tokens is logged.

### Admin Dashboard
* **Secure Admin Login:** A separate, private login page (`admin.html`) for the administrator, using hardcoded credentials to keep it separate from the public-facing honeypot.
* **Data Visualization:** The dashboard features dynamic charts (built with Chart.js) to visualize:
    * Login Attempts Over Time
    * Most Common Usernames Attempted
* **Real-time Statistics:** View live-updating counters for total login attempts, detected brute force attacks, unique IPs, and attempts today.
* **Detailed Attempt Logs:** A table shows all recent login attempts, including the timestamp, username, password (captured), IP address, and User Agent.
* **Manual IP Management:** The admin can view all blocked IPs, see the reason for the block, and manually unblock any IP address.

---

## Technologies Used

* **Frontend:** HTML5, CSS3, JavaScript
* **Backend & Database:** Firebase (Realtime Database & Authentication)
* **Libraries:**
    * [Bootstrap 5](https://getbootstrap.com/): For the responsive UI of all pages.
    * [Chart.js](https://www.chartjs.org/): For data visualization in the admin dashboard.

---

## Setup and Installation

To get this project running, you need to configure it with your own Firebase project.

1.  **Create a Firebase Project:**
    * Go to the [Firebase Console](https://firebase.google.com/) and create a new project.
    * In your project, enable **Authentication** (with the "Email/Password" sign-in method).
    * In your project, create a **Realtime Database**.

2.  **Get Firebase Config:**
    * In your Firebase project settings, find your "Web app" configuration object. It will look like this:
        ```javascript
        const firebaseConfig = {
          apiKey: "AIza...",
          authDomain: "YOUR-PROJECT.firebaseapp.com",
          databaseURL: "[https://YOUR-PROJECT-default-rtdb.firebaseio.com](https://YOUR-PROJECT-default-rtdb.firebaseio.com)",
          projectId: "YOUR-PROJECT",
          storageBucket: "YOUR-PROJECT.appspot.com",
          messagingSenderId: "...",
          appId: "..."
        };
        ```

3.  **Update Project Files:**
    * Copy your `firebaseConfig` object.
    * Paste it into the `<script>` section at the bottom of all four HTML files:
        * `index.html`
        * `signup.html`
        * `admin.html`
        * `dashboard.html`

4.  **Set Admin Credentials:**
    * Open `admin.html` in a code editor.
    * Near the top of the `<script>` section, find these lines and change them to your own secure admin credentials:
        ```javascript
        // Admin credentials
        const ADMIN_EMAIL = "your@mail";
        const ADMIN_PASSWORD = "password";
        ```
    * **This is critical!** Do not leave the default credentials.

5.  **Deploy:**
    * Host these files on any static web hosting service (like Firebase Hosting, GitHub Pages, Netlify, etc.).
    * Your honeypot is now live at `index.html`.
    * You can monitor it by visiting `admin.html`.

---

## File Structure
