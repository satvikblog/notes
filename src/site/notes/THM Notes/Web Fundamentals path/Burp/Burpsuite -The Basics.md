---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/burp/burpsuite-the-basics/","title":"BurpSuite: The Basics- THM","tags":["web","burpsuite"]}
---

### Burp Suite Basics - Structured Notes for Cybersecurity Beginners

#### **Overview**
Burp Suite is a Java-based framework widely used for web application penetration testing. It intercepts HTTP/HTTPS traffic between a browser and a web server, allowing manipulation of requests and responses, essential for manual web application testing. This guide focuses on the Burp Suite Community Edition.

### **Task 2: What is Burp Suite?**
- **Definition**: Burp Suite is a comprehensive tool for web application penetration testing.
- **Key Capabilities**:
  - Intercept, view, and modify HTTP/HTTPS traffic.
  - Route traffic to various Burp Suite tools.
- **Editions**:
  - **Community Edition**: Free for non-commercial use, limited features.
  - **Professional Edition**: Includes advanced features like automated vulnerability scanning, a fuzzer, project saving, and more.
  - **Enterprise Edition**: Automated, continuous scanning for vulnerabilities on a server.
- **Usage**: Primarily for web and mobile applications.

### **Task 3: Features of Burp Community**
- **Proxy**: Intercept and modify requests and responses.
- **Repeater**: Capture, modify, and resend requests for testing.
- **Intruder**: Brute-force and fuzz endpoints (rate-limited in Community Edition).
- **Decoder**: Encode and decode data.
- **Comparer**: Compare data at the word or byte level.
- **Sequencer**: Analyze randomness of tokens (e.g., session cookies).
- **Extensions**: Enhance functionality via Burp Suite Extender and the BApp Store.

### **Task 4: Installation**
- **Downloads**: Available for Windows, macOS, and Linux from the Burp Suite download page.
- **Kali Linux**: Pre-installed, but can be installed via apt repositories if missing.
- **Installation**: Follow platform-specific instructions, generally straightforward with default settings.

### **Task 5: The Dashboard**
- **Initial Setup**: Launch Burp Suite, accept terms, select a project type, and configure settings.
- **Dashboard Layout**:
  - **Tasks**: Manage background tasks like "Live Passive Crawl".
  - **Event Log**: Track actions performed by Burp Suite.
  - **Issue Activity**: Display vulnerabilities (Professional Edition).
  - **Advisory**: Detailed information on identified vulnerabilities.

### **Task 6: Navigation**
- **Module Selection**: Top menu bar to switch between modules (e.g., Proxy, Repeater).
- **Sub-Tabs**: Secondary menu for module-specific settings.
- **Detaching Tabs**: View multiple tabs separately via the Window menu.
- **Keyboard Shortcuts**:
  - `Ctrl + Shift + D`: Dashboard
  - `Ctrl + Shift + T`: Target tab
  - `Ctrl + Shift + P`: Proxy tab
  - `Ctrl + Shift + I`: Intruder tab
  - `Ctrl + Shift + R`: Repeater tab

### **Task 7: Options**
- **Global Settings**: Apply to the entire Burp Suite installation.
- **Project Settings**: Specific to the current project, not saved in Community Edition.
- **Settings Navigation**:
  - **Search**: Find specific settings.
  - **Type Filter**: Filter for User or Project settings.
  - **Categories**: Group settings by functionality.
- **Key Categories**:
  - **Sessions**: Includes "Cookie jar".
  - **Suite**: Controls update behavior.
  - **Hotkeys**: Change keybindings for shortcuts.
  - **Client-Side TLS Certificates**: Can override on a per-project basis.

### **Task 8: Introduction to the Burp Proxy**
- **Intercepting Requests**: Modify, forward, or drop requests.
- **Capture and Logging**: Logs requests and responses for later analysis.
- **WebSocket Support**: Captures WebSocket communications.
- **Proxy Settings**:
  - **Response Interception**: Customize rules for intercepting server responses.
  - **Match and Replace**: Use regex to modify requests dynamically.

### **Task 9: Connecting through the Proxy (FoxyProxy)**
- **Configure FoxyProxy Extension**:
  - Install FoxyProxy in Firefox.
  - Create a proxy configuration with IP `127.0.0.1` and Port `8080`.
  - Enable the proxy configuration and intercept traffic through Burp Suite.
- **Testing**: Verify setup by intercepting a request from the browser.

### **Task 10: Site Map and Issue Definitions**
- **Site Map**: Automatically map web applications by browsing them.
- **Issue Definitions**: Reference list of vulnerabilities Burp can identify.
- **Scope Settings**: Define the target scope to focus on specific applications.

### **Task 11: The Burp Suite Browser**
- **Built-in Browser**: Pre-configured Chromium browser for easier setup.
- **Running as Root**: Use "Allow Burp's browser to run without a sandbox" option if needed (use caution).

### **Task 12: Scoping and Targeting**
- **Set Scope**: Add targets to the scope to focus and filter traffic.
- **Proxy Settings**: Configure to intercept only in-scope traffic for cleaner analysis.

### **Task 13: Proxying HTTPS**
- **Certificate Issue**: Manually add the PortSwigger CA certificate to the browser’s trusted authorities.
- **Instructions**: Download and install the CA certificate to avoid HTTPS errors.

These notes provide a structured overview of Burp Suite's basic functionalities, installation process, and navigation tips, aimed at cybersecurity beginners preparing for certifications like CEH and eJPT.