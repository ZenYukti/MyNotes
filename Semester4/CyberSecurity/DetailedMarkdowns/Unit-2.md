# 🟣 ZenYukti
### Smart Notes for Serious Students
> 🌐 [zenyukti.in](https://zenyukti.in)

---

# 🔐 Cybercrime: Mobile & Wireless Devices — Exam Notes
> **Last-Minute Prep | To The Point**

---

## 1. Introduction to Mobile & Wireless Devices

- **Mobile devices** = smartphones, tablets, laptops, PDAs, wearables
- **Wireless devices** = any device communicating without physical cables (Wi-Fi, Bluetooth, NFC, 4G/5G)
- Mobile computing = ability to use computing devices **while moving**
- These devices are now primary targets for cybercriminals due to:
  - Massive adoption worldwide
  - Store sensitive personal & financial data
  - Always connected to internet
  - Often less secured than desktops

---

## 2. Proliferation of Mobile & Wireless Devices

- **Proliferation** = rapid spread and increase in number of mobile devices
- Key drivers:
  - Affordable smartphones and data plans
  - Growth of mobile apps (banking, shopping, social media)
  - 4G/5G network expansion
  - IoT (Internet of Things) — billions of connected devices
  - BYOD (Bring Your Own Device) culture in workplaces
- **Impact:**
  - More attack surface for cybercriminals
  - Personal and corporate data at risk
  - Difficult to monitor and secure all devices

---

## 3. Trends in Mobility

| Trend | Description |
|-------|-------------|
| **BYOD** | Employees use personal devices for work — blurs personal/corporate boundary |
| **Mobile Banking** | Banking via apps — target for financial frauds |
| **Mobile Commerce (m-Commerce)** | Shopping via mobile — credit card data at risk |
| **Cloud Sync** | Data auto-synced to cloud — breach affects all devices |
| **5G Networks** | Faster speeds but new security vulnerabilities |
| **IoT Integration** | Smart devices connected — weak IoT security = easy entry point |
| **Mobile Payments** | UPI, NFC payments — fraud and interception risks |
| **Social Media on Mobile** | Personal info shared — social engineering target |
| **Remote Work** | Work from any location — insecure home/public networks |

---

## 4. Credit Card Frauds in Mobile & Wireless Computing Era

### Types of Credit Card Frauds

| Fraud Type | Description |
|------------|-------------|
| **Phishing** | Fake SMS/email redirects to fake payment page to steal card details |
| **Smishing** | SMS phishing — fake bank alerts with malicious links |
| **Skimming** | Device attached to ATM/card reader captures card data wirelessly |
| **Man-in-the-Middle (MitM)** | Intercept card data over unsecured Wi-Fi |
| **Fake Apps** | Malicious banking/payment apps steal credentials |
| **SIM Swapping** | Attacker gets duplicate SIM to receive OTPs |
| **Card Not Present (CNP) Fraud** | Using stolen card details for online purchases (no physical card needed) |
| **Wireless Sniffing** | Capture unencrypted payment data over Wi-Fi |
| **Vishing** | Fake bank calls asking for card number/CVV/OTP |

### How SIM Swap Works
```
Attacker → gets victim's personal info (social engineering)
         → contacts telecom provider
         → requests new SIM for victim's number
         → receives all OTPs → bypasses 2FA → account hijacked
```

### Prevention
- Never share OTP/CVV over phone or SMS
- Enable alerts for all transactions
- Use virtual cards for online purchases
- Avoid saving card details on apps/browsers
- Report lost/stolen card immediately

---

## 5. Security Challenges Posed by Mobile Devices

| Challenge | Description |
|-----------|-------------|
| **Lost/Stolen devices** | Physical theft → direct access to all data |
| **Unsecured Wi-Fi** | Connecting to public Wi-Fi exposes data |
| **Malicious Apps** | Apps from unofficial sources carry malware |
| **Outdated OS** | Unpatched vulnerabilities exploited by attackers |
| **Weak Authentication** | Simple PINs/no lock → easy unauthorized access |
| **Bluetooth Attacks** | Bluejacking, Bluesnarfing exploit Bluetooth |
| **Lack of Encryption** | Unencrypted data easily intercepted |
| **BYOD risks** | Personal and corporate data mixed on one device |
| **Jailbreaking/Rooting** | Removes OS security controls → highly vulnerable |
| **Location Tracking** | GPS data misused for stalking or targeted attacks |
| **Insecure Apps** | Poor coding practices → data leakage |
| **Phishing via SMS/WhatsApp** | Mobile users click links more impulsively |

---

## 6. Registry Settings for Mobile Devices

- **Registry** = database that stores configuration settings for OS and applications
- In mobile context, **device configuration/policy settings** managed by MDM (Mobile Device Management)

### Key Registry/Configuration Settings for Security:
- **Password/PIN enforcement** — minimum length, complexity requirements
- **Auto-lock timeout** — lock screen after inactivity (e.g., 1–2 minutes)
- **Encryption settings** — enforce full-device encryption
- **Remote wipe capability** — erase device data remotely if lost
- **App installation restrictions** — allow only from trusted/official stores
- **VPN enforcement** — force VPN for corporate network access
- **Bluetooth/Wi-Fi restrictions** — disable auto-connect to unknown networks
- **Camera/microphone access controls** — restrict for sensitive environments
- **Disable USB debugging** — prevents unauthorized data access via USB

---

## 7. Authentication Service Security

- **Authentication** = verifying identity of user before granting access
- Mobile authentication methods:

| Method | Description | Security Level |
|--------|-------------|----------------|
| **PIN/Password** | Numeric or alphanumeric code | Low–Medium |
| **Pattern lock** | Swipe pattern on screen | Low (smudge attacks) |
| **Biometrics** | Fingerprint, Face ID, Iris scan | High |
| **Two-Factor Auth (2FA)** | Password + OTP | High |
| **Certificate-based** | Digital certificates for enterprise | Very High |
| **Token-based** | Hardware/software token generates code | High |

### Security Risks in Authentication
- **Shoulder surfing** — someone watches you enter PIN
- **Brute force** — try all PIN combinations
- **SIM swap** — attacker receives OTP
- **Fake biometric** — photo used to bypass face recognition
- **Keyloggers** — record typed passwords

### Best Practices
- Use **biometrics + PIN** combination
- Enable **2FA** wherever possible
- Avoid pattern locks (leave smudge trail)
- Use **strong alphanumeric passwords**

---

## 8. Attacks on Mobile/Cell Phones

| Attack | Description |
|--------|-------------|
| **Vishing** | Fraudulent voice calls to extract info |
| **Smishing** | Malicious SMS with fake links |
| **Bluejacking** | Send unsolicited messages via Bluetooth |
| **Bluesnarfing** | Unauthorized access to device data via Bluetooth |
| **Bluebugging** | Full control of phone via Bluetooth (calls, messages) |
| **MitM Attack** | Intercept communication on public Wi-Fi |
| **Evil Twin Attack** | Fake Wi-Fi hotspot mimics legitimate one — captures traffic |
| **Malware/Spyware** | Apps that steal data, track location, record calls |
| **Ransomware** | Lock/encrypt phone data, demand payment |
| **IMSI Catching (Stingray)** | Fake cell tower intercepts calls and texts |
| **SIM Swapping** | Get duplicate SIM to hijack account |
| **Tap and Pay Fraud** | Clone NFC signals for unauthorized payments |
| **Call Interception** | Intercept calls on unencrypted networks (SS7 flaw) |
| **Grayware/Adware** | Unwanted apps tracking behavior and showing ads |
| **Jailbreak Exploits** | Exploit rooted/jailbroken device security gaps |

### Bluetooth Attack Summary
| Attack | What it Does |
|--------|-------------|
| **Bluejacking** | Send anonymous messages |
| **Bluesnarfing** | Steal contacts, calendar, messages |
| **Bluebugging** | Take complete control of device |

---

## 9. Mobile Devices: Security Implications for Organizations

- Employees using mobile devices for work creates **serious security risks:**

| Risk | Implication |
|------|-------------|
| **Data leakage** | Corporate emails, files accessed on personal unsecured device |
| **Malware entry point** | Infected personal device connects to corporate network |
| **Lost/stolen device** | Sensitive corporate data compromised |
| **Uncontrolled app use** | Employees install unapproved apps with data access |
| **Shadow IT** | Employees use unauthorized cloud services/apps |
| **Network compromise** | Device connected to untrusted Wi-Fi → corporate VPN tunneled through compromised network |
| **Compliance violations** | Sensitive data (healthcare, finance) on mobile may violate HIPAA/GDPR |
| **Insider threat** | Employee deliberately leaks data via personal device |

### Why Mobile Security is Harder for Orgs
- Devices not always owned by organization (BYOD)
- Employees resistant to corporate controls on personal devices
- Mix of personal and professional data on same device
- Constant OS and app updates hard to manage at scale

---

## 10. Organizational Measures for Handling Mobile Devices

### MDM — Mobile Device Management ⭐
- Software platform that **monitors, manages, and secures** mobile devices remotely
- Key MDM capabilities:
  - **Remote wipe** — erase data if device lost/stolen
  - **Policy enforcement** — enforce passwords, encryption
  - **App management** — control which apps can be installed
  - **Location tracking** — track device location
  - **Blacklisting/Whitelisting apps**
  - **Containerization** — separate corporate and personal data on same device

### Technical Measures
- **Encryption** — encrypt all data on device and in transit
- **VPN** — mandatory VPN for accessing corporate resources
- **Mobile Antivirus** — detect and block malware
- **App Whitelisting** — only approved apps allowed
- **Network Access Control (NAC)** — only compliant devices access network
- **Regular OS patching** — enforce latest security updates
- **Multi-factor authentication (MFA)** — for all corporate logins

### Administrative Measures
- **Device registration** — all devices accessing corporate data must be registered
- **Acceptable Use Policy (AUP)** — rules on how devices can be used
- **Security awareness training** — educate employees on mobile threats
- **Incident response plan** — what to do if device compromised/lost
- **Regular audits** — check compliance with security policies

---

## 11. Organizational Security Policies in Mobile Computing Era

### Key Policies Every Organization Must Have

#### BYOD Policy (Bring Your Own Device)
- Define which personal devices are allowed
- Specify what corporate data can be accessed
- Employee consent for MDM installation
- Right to remote wipe in case of loss
- Clear separation of personal vs corporate data

#### Mobile Security Policy
- **Mandatory PIN/password** of minimum length
- **Auto-lock** after defined inactivity period
- **Prohibition on jailbreaking/rooting**
- **Approved app list** — only install from official stores
- **No storage of sensitive data** on local device
- **Mandatory encryption** for data at rest and in transit
- **Prohibition of public Wi-Fi** without VPN

#### Data Classification Policy
- Classify data (Public / Internal / Confidential / Top Secret)
- Restrict which classification can be accessed on mobile
- Confidential data must not leave corporate network

#### Incident Response Policy
- Report lost/stolen device immediately
- Remote wipe initiated within defined timeframe
- Forensic investigation if breach suspected

#### Employee Exit Policy
- Remove MDM profile and wipe corporate data on employee exit
- Revoke all credentials and access tokens
- Audit for any data taken out

### Policy Framework Summary
```
📋 Organizational Mobile Security = 
   MDM Tools + Security Policies + Employee Training + Incident Response
```

---

## 12. Quick Cheatsheet

| Term | One-Line Definition |
|------|-------------------|
| **BYOD** | Employees use personal devices for work |
| **MDM** | Software to manage & secure org mobile devices remotely |
| **SIM Swapping** | Attacker gets duplicate SIM to hijack OTPs |
| **Bluejacking** | Send anonymous messages via Bluetooth |
| **Bluesnarfing** | Steal device data via Bluetooth |
| **Bluebugging** | Full remote control via Bluetooth |
| **Evil Twin** | Fake Wi-Fi hotspot to intercept traffic |
| **IMSI Catcher/Stingray** | Fake cell tower intercepting calls/texts |
| **Smishing** | Phishing via SMS |
| **Vishing** | Phishing via voice/phone call |
| **Remote Wipe** | Erase device data remotely if lost/stolen |
| **Containerization** | Separate personal and corporate data on same device |
| **Jailbreaking/Rooting** | Remove OS security restrictions — highly risky |
| **2FA** | Two-factor authentication — password + OTP |
| **CNP Fraud** | Card Not Present — online fraud using stolen card details |

---

> 💡 **Last-minute tips:**
> - Bluejacking = messages only | Bluesnarfing = data theft | Bluebugging = full control
> - SIM Swap = most dangerous attack on mobile banking
> - Evil Twin = fake Wi-Fi hotspot (very common in coffee shops)
> - MDM = organization's tool to manage and secure mobile devices remotely
> - BYOD = biggest organizational security challenge today
> - Jailbroken/rooted phone = bypasses all OS security = very vulnerable
> - Remote wipe = first action when corporate device is lost
> - 2FA via SMS is vulnerable to SIM swap — use authenticator apps instead
> - Containerization = keeps work data separate from personal data on BYOD device
> - CNP fraud = most common credit card fraud for online transactions

---

---

**🟣 ZenYukti** | *Empowering learners with smart, structured study resources.*

🌐 [zenyukti.in](https://zenyukti.in)

© 2026 ZenYukti. All rights reserved. This material is intended for personal educational use only. Unauthorized reproduction or distribution is prohibited.