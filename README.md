# Automated Security Scan Toolkit

A collection of free tools for performing automated security scans on web applications and JavaScript projects.

## 1. Semgrep - Static Code Analysis

### Install

```bash
# Option 1: Snap (recommended)
sudo snap install semgrep

# Option 2: Pip
# sudo python3 -m pip install semgrep --break-system-packages
```

### Run Scan

```bash
semgrep scan --config auto
```

---

## 2. ESLint Security Plugin

### Initialize Project

```bash
npm init -y
```

### Install Dependencies

```bash
npm install --save-dev eslint eslint-plugin-security
```

### Create `eslint.config.js`

```javascript
import pluginSecurity from "eslint-plugin-security";

export default [
  pluginSecurity.configs.recommended,
  {
    rules: {
      // Disable noisy rule to focus on real issues
      "security/detect-object-injection": "off"
    }
  }
];
```

### Run Scan

```bash
npx eslint . > security_report.txt
```

Results will be saved to:

```text
security_report.txt
```

---

## 3. Retire.js - Detect Vulnerable JavaScript Libraries

### Install

```bash
npm install --save-dev retire
```

### Run Scan

```bash
npx retire
```

---

## 4. TruffleHog - Secret Detection

### Install

```bash
curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sudo sh -s -- -b /usr/local/bin
```

### Verify Installation

```bash
trufflehog --version
```

### Scan Filesystem

```bash
sudo trufflehog filesystem .
```

---

## 5. Nikto - Web Server Scanner

### Install

```bash
sudo apt update
sudo apt install nikto -y
```

### Scan Local Web Server

```bash
nikto -h http://localhost/
```

---

## 6. Wapiti - Web Application Vulnerability Scanner

### Install

```bash
pip install wapiti3 --break-system-packages
```

### Run Scan

```bash
wapiti -u https://localhost/ --scope folder -d 10 --max-links-per-page 100 -S insane --verify-ssl 0 -f html -o ./wapiti_report
```

Results will be saved to:

```text
./wapiti_report/
```

---

# Recommended Workflow

Run the following tools in order:

1. **Semgrep** → Source code security analysis
2. **ESLint Security Plugin** → JavaScript security linting
3. **Retire.js** → Vulnerable dependency detection
4. **TruffleHog** → Secret and credential discovery
5. **Nikto** → Web server vulnerability assessment
6. **Wapiti** → Web application vulnerability scanning (XSS, injection, misconfigurations)

## Example

```bash
semgrep scan --config auto

npx eslint . > security_report.txt

npx retire

sudo trufflehog filesystem .

nikto -h http://localhost/

pip install wapiti3 --break-system-packages
wapiti -u https://localhost/ --scope folder -d 10 --max-links-per-page 100 -S insane --verify-ssl 0 -f html -o ./wapiti_report
```

---

## Tools Covered

| Tool | Purpose |
|--------|---------|
| Semgrep | Static Application Security Testing (SAST) |
| ESLint Security Plugin | JavaScript security linting |
| Retire.js | Detect vulnerable JS dependencies |
| TruffleHog | Secret scanning |
| Nikto | Web server vulnerability scanning |
| Wapiti | Web application vulnerability scanning (DAST) |

## License

Use these tools only on systems and applications you own or have explicit permission to test.
