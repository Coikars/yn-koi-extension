# Privacy Policy

**Last Updated:** March 4, 2026  
**Effective Date:** March 4, 2026  
**Version:** 1.0.0

**Contact:** [coikars@outlook.com](mailto:coikars@outlook.com)

---

## Table of Contents

- [Introduction](#introduction)
- [Information We Do NOT Collect](#information-we-do-not-collect)
- [How the Extension Works](#how-the-extension-works)
- [Permissions Explained in Detail](#permissions-explained-in-detail)
  - [activeTab Permission](#activetab-permission)
  - [Host Permission (younow.com)](#host-permission-younowcom)
  - [Scripting Permission](#scripting-permission)
  - [Storage Permission](#storage-permission)
  - [Tabs Permission](#tabs-permission)
- [Subscription Verification Process](#subscription-verification-process)
- [GitHub Configuration System](#github-configuration-system)
- [Local Data Storage](#local-data-storage)
- [Third-Party Services](#third-party-services)
- [Data Security](#data-security)
- [Your Rights and Choices](#your-rights-and-choices)
- [Children's Privacy](#childrens-privacy)
- [Changes to This Policy](#changes-to-this-policy)
- [Contact Information](#contact-information)

---

## Introduction

YouNow Koi Addons ("the Extension", "we", "our") is a browser extension designed for YouNow broadcasters. This Privacy Policy explains what data the Extension accesses, how it's used, what we do NOT collect, and your privacy rights.

### Core Privacy Principle

**YouNow Koi Addons operates entirely within your browser and does not collect, store, or transmit any personal information to external servers** (except for configuration fetching from GitHub, which contains no user data).

---

## Information We Do NOT Collect

To be absolutely clear, the Extension does **NOT** collect, store, or transmit:

### ❌ Personal Information
- No names, email addresses, or contact information
- No demographic data (age, gender, location)
- No identification numbers or user IDs

### ❌ Browsing Data
- No browsing history
- No website visits outside younow.com
- No search queries
- No cookies or tracking data

### ❌ YouNow Content
- No chat message contents (beyond what's temporarily processed for chat bot features)
- No stream content or recordings
- No private messages or communications
- No payment or financial information

### ❌ Device Information
- No device fingerprinting
- No IP address collection
- No hardware or software specifications
- No installed extensions or applications list

### ❌ Tracking
- No analytics services (Google Analytics, etc.)
- No advertising trackers
- No cross-site tracking
- No usage statistics transmitted to servers

### What This Means

**We have no servers that store your data.** We have no databases with user information. We cannot identify you, track you, or share your data because we simply don't have it.

---

## How the Extension Works

### Technical Architecture

The Extension operates entirely as a **client-side application** within your Chrome browser:

1. **Local Processing Only**
   - All features run in your browser
   - No data is sent to our servers (we don't have servers)
   - Settings stored locally using Chrome's storage API

2. **YouNow Page Interaction**
   - Extension injects scripts into younow.com pages you visit
   - Scripts automate tasks like collecting chests or moderating chat
   - All processing happens in your browser, not on remote servers

3. **Configuration Fetching**
   - Extension fetches a configuration file from GitHub
   - This file contains access control lists (blocked users, override users)
   - No user data is sent to GitHub - this is a read-only fetch

### Data Flow Diagram

```
Your Browser
├── Extension Installed
│   ├── Loads settings from Chrome local storage
│   ├── Fetches config from GitHub (no user data sent)
│   └── Injects scripts into younow.com pages
│
├── YouNow.com Interaction
│   ├── Reads page content (subscriber list for verification)
│   ├── Automates actions (collecting chests, sending chat messages)
│   └── All processing in browser (no external transmission)
│
└── Local Storage
    └── Saves preferences locally (never transmitted)
```

> **Key Point:** Data flows within your browser only. Nothing is transmitted to external servers except the one-way GitHub configuration fetch (which contains no user data).

---

## Permissions Explained in Detail

Chrome extensions require explicit permissions to function. Here's exactly what each permission does and why it's needed:

### activeTab Permission

**What It Does:**  
Allows the Extension to interact with the currently active tab when you click the extension icon.

**Why It's Needed:**
- Check if you're on a YouNow page before injecting features
- Access the current page's content to enable/disable features
- Verify subscription status by reading public YouNow profile information

**What It Does NOT Do:**
- ❌ Access tabs you haven't explicitly activated the extension on
- ❌ Access tabs from other websites
- ❌ Run in the background on all tabs
- ❌ Track your browsing across tabs

> **Technical Details:** The `activeTab` permission is triggered ONLY when you click the extension icon. It does not grant persistent access to tabs or background monitoring.

---

### Host Permission (younow.com)

**What It Does:**  
Allows the Extension to access and interact with pages on younow.com domain.

**Why It's Needed:**

#### 1. Subscription Verification
- Navigate to @Coi's YouNow profile page
- Read the publicly visible subscriber list
- Check if your username appears in the list
- Store verification result locally

#### 2. Auto-Chest Collection
- Detect when chest notifications appear on screen
- Automatically click the collection button
- Monitor chest availability during broadcasts

#### 3. Chat Bot Functionality
- Read incoming chat messages
- Detect command triggers (e.g., !help, !commands)
- Send automated responses via the chat interface
- All processing happens locally in your browser

#### 4. Moderation Tools
- Access user list in chat
- Detect rule violations based on your configured rules
- Automatically silence users (auto-silencer feature)
- Grant temporary moderator status (auto temp referee)

#### 5. Auto-Refresh
- Monitor stream connection status
- Detect disconnections or buffering issues
- Automatically refresh the page when needed

#### 6. Discord Integration
- Monitor chat messages to bridge to Discord
- Detect "Go Live" status changes
- Send webhook messages to Discord (if you configure it)

**What It Does NOT Do:**
- ❌ Access any websites other than younow.com
- ❌ Transmit chat messages to external servers (except Discord webhooks you configure)
- ❌ Store chat history beyond current session
- ❌ Share your YouNow activity with third parties

> **Technical Details:** The `host_permissions` for `*://www.younow.com/*` grants access ONLY to younow.com and its subdomains. The Extension cannot access google.com, facebook.com, or any other website.

---

### Scripting Permission

**What It Does:**  
Allows the Extension to inject JavaScript code into YouNow pages.

**Why It's Needed:**

Chrome extensions can't directly modify web pages without this permission. Scripting enables:

1. **Feature Injection**
   - Auto-chest script injected when you enable the feature
   - Chat bot script injected when you turn it on
   - Each feature is a separate injectable script

2. **DOM Manipulation**
   - Add buttons to the YouNow interface (e.g., shrink chest button)
   - Modify page elements for better usability
   - Create overlays and notifications

3. **Event Monitoring**
   - Listen for chat messages
   - Detect chest notifications
   - Monitor stream status changes

**What It Does NOT Do:**
- ❌ Inject ads or tracking scripts
- ❌ Modify pages on other websites
- ❌ Execute remote code (see GitHub Configuration section)
- ❌ Run scripts when features are disabled

> **Technical Details:** Scripts are only injected when: (1) You're on younow.com, (2) You've explicitly enabled a feature, (3) The Extension is active. Scripts are removed when you disable features or close tabs.

---

### Storage Permission

**What It Does:**  
Allows the Extension to save data locally on your device using Chrome's storage API.

**Why It's Needed:**  
Without storage, the Extension would lose all your settings every time you close your browser.

**What We Store Locally:**

#### 1. Feature Toggle States
```javascript
{
  autoChestEnabled: true,
  chatBotEnabled: false,
  autoRefreshEnabled: true
  // ... etc
}
```

#### 2. Feature Settings
```javascript
{
  chatBotCommands: {
    "!help": "Available commands: !help, !discord, !socials"
  },
  autoRefreshInterval: 300000, // 5 minutes
  autoSilencerRules: ["badword1", "badword2"]
}
```

#### 3. Subscription Status
```javascript
{
  user_is_subscribed: true,
  subscription_check_completed: true,
  subscription_check_timestamp: 1709516400000,
  subscription_check_username: "YourUsername"
}
```

#### 4. Debug Logs
```javascript
{
  debugLogs: [
    {
      timestamp: 1709516400,
      category: "Chat Bot",
      message: "Command triggered: !help"
    }
  ]
}
```

**What We Do NOT Store:**
- ❌ Chat message contents (beyond current session)
- ❌ Your password or login credentials
- ❌ Payment information
- ❌ Personal identification information
- ❌ Browsing history

**Where Is This Data Stored:**

All data is stored using `chrome.storage.local`, which means:
- Stored on YOUR device only
- Not synchronized across devices (unless you enable Chrome sync)
- Not accessible to other extensions
- Not transmitted to external servers
- Deleted when you uninstall the extension

> **Technical Details:** Chrome's storage API provides isolated storage per-extension. Data is stored in Chrome's internal database on your hard drive, encrypted at the OS level. No other extensions or websites can access this data.

---

### Tabs Permission

**What It Does:**  
Allows the Extension to interact with browser tabs (open, close, navigate).

**Why It's Needed:**

1. **Subscription Verification**
   - Open @Coi's YouNow profile in a new tab or background tab
   - Check subscriber list automatically
   - Close tab after verification completes

2. **Feature Navigation**
   - Open Discord setup guide in new tab
   - Open YouNow subscription page when you click "Subscribe to @Coi"

**What It Does NOT Do:**
- ❌ Monitor all your open tabs
- ❌ Track which tabs you visit
- ❌ Access content of tabs not related to the extension
- ❌ Close tabs you didn't ask to close

> **Technical Details:** The Extension only opens tabs when you trigger an action (click subscription button, enable Discord feature, etc.).

---

## Subscription Verification Process

### Why Verification is Required

The Extension requires an active subscription to @Coi on YouNow to unlock features. This serves two purposes:
1. Support ongoing development and maintenance
2. Ensure only legitimate users access automation features

### How Verification Works

#### Initial Setup

1. **You Install Extension**
   - Extension is locked by default
   - Popup shows "Subscription Required" overlay

2. **You Subscribe to @Coi on YouNow**
   - Visit younow.com/coi
   - Click subscribe button (standard YouNow subscription)
   - This is through YouNow's platform, not our extension

3. **You Trigger Verification**
   - Click "I'm Already Subscribed" button in extension popup
   - OR wait for automatic verification on next YouNow page visit

4. **Extension Performs Check**
   - Opens @Coi's YouNow profile (in background)
   - Locates the "Subscribers" button on profile
   - Clicks the button to open subscriber modal
   - Reads the publicly visible subscriber list
   - Searches for your YouNow username in the list
   - Stores result: subscribed = true/false
   - Closes the profile/modal
   - Returns you to your original page

5. **Verification Result**
   - **If Found:** Extension unlocks, features available for 3 days
   - **If Not Found:** Overlay remains, shows "Not subscribed" message

#### Automatic Re-Verification

Every 3 days, the Extension automatically re-checks your subscription:
- Happens in background when you visit YouNow
- Takes 5-10 seconds
- If still subscribed → Extension continues working
- If subscription expired → Extension locks again

### What Data is Accessed During Verification

**Data READ (from YouNow):**
- @Coi's public profile page content
- Publicly visible subscriber list (same list anyone can see)
- Your logged-in YouNow username (to match against list)

**Data STORED (locally only):**
- Your YouNow username: "YourUsername"
- Subscription status: true/false
- Verification timestamp: 1709516400000
- Next check due: 1709602800000

**Data TRANSMITTED:**
- ❌ **NOTHING** is transmitted to external servers
- Your username is never sent anywhere
- Verification happens entirely in your browser
- No API calls to our servers (we don't have servers)

### Privacy Considerations

#### Is This Invasive?

**No.** The Extension only reads publicly visible information:
- Your subscriber list is already public on YouNow
- Anyone can click your profile and see your subscribers
- We're just automating what anyone could do manually

#### Can @Coi See My Activity?

**No.** The verification only checks if you're subscribed. It doesn't:
- Report what features you're using
- Track when you use the extension
- Monitor your broadcasts or chat activity
- Send any usage data to @Coi or anyone else

#### What If I Unsubscribe?

- Extension will detect this on next check (within 3 days)
- Features will be locked
- All your settings remain saved locally
- You can re-subscribe anytime to regain access

---

## GitHub Configuration System

### What It Is

The Extension fetches a configuration file from GitHub to manage access control and emergency features.

### Configuration URL

```
https://raw.githubusercontent.com/Coikars/yn-koi-extension/refs/heads/main/override-users.json
```

### What This File Contains

**Example Configuration:**

```json
{
  "disableAll": {
    "enabled": false,
    "message": "Extension disabled for maintenance"
  },
  "blocked": [
    {
      "username": "violator123",
      "reason": "Terms of Service violation"
    }
  ],
  "overrides": [
    {
      "username": "moderator1",
      "reason": "Staff member"
    }
  ]
}
```

**Fields Explained:**

- **disableAll:** Emergency kill switch to disable extension for everyone
- **blocked:** List of YouNow usernames banned from using extension
- **overrides:** List of users with permanent access (no subscription check)

### Why We Use GitHub

#### Advantages

1. **Emergency Control**
   - Can instantly disable extension if critical bug found
   - Can block abusive users without releasing extension update
   - Can grant override access to staff/moderators

2. **Transparency**
   - GitHub provides public version history
   - You can see all changes to configuration
   - Open-source approach builds trust

3. **Security**
   - HTTPS connection (encrypted)
   - Read-only access (extension can't modify file)
   - No executable code (only JSON data)

4. **No Servers Required**
   - We don't need to maintain servers
   - GitHub handles hosting and CDN
   - Free and reliable infrastructure

### How Configuration Fetching Works

#### Process

1. **Cache Check (5-minute cache)**
   ```
   If config fetched within last 5 minutes:
     → Use cached version (no GitHub request)
   ```

2. **GitHub Fetch**
   ```
   Fetch https://raw.githubusercontent.com/.../override-users.json
   
   If successful:
     → Cache result for 5 minutes
     → Apply configuration
   
   If failed (GitHub down, no internet, etc.):
     → Disable extension entirely
     → Show error message to user
   ```

3. **Configuration Application**
   ```
   Check user's YouNow username against configuration:
   
   If disableAll.enabled = true:
     → Show "Extension Disabled" overlay to everyone
   
   If username in blocked list:
     → Show "Access Blocked" overlay with reason
   
   If username in overrides list:
     → Skip subscription check, grant permanent access
   
   Else:
     → Perform normal subscription verification
   ```

### What Data is Sent to GitHub

**Data SENT to GitHub:**  
❌ **NOTHING**

The GitHub fetch is a **read-only HTTP GET request**. No data is transmitted:
- No user data sent
- No usernames sent
- No usage statistics sent
- No identifiers sent

**Data RECEIVED from GitHub:**  
✅ **Configuration JSON only** (~1-5 KB)

### Privacy Implications

#### Potential Concerns Addressed

**"Can GitHub track me?"**
- GitHub's servers see an HTTP request from your IP address
- This is the same as visiting any website
- GitHub's privacy policy applies (we don't control GitHub)
- Request contains no identifying information beyond IP

**"What if GitHub is hacked?"**
- Worst case: Attacker could add your username to block list
- Result: Your extension would be disabled (inconvenience, not data breach)
- Attacker CANNOT access your data (we don't have your data)
- Attacker CANNOT install malware (only JSON config, no code)

**"What if developer goes rogue?"**
- Developer could disable everyone's extension via disableAll
- Developer could block specific users
- Developer CANNOT access your settings, data, or activity
- All your data remains local - nothing transmitted to us

### Fallback Behavior

**If GitHub is Unreachable:**

```
1. Check cache
   → If valid cache exists (< 5 minutes old): Use cached config
   → If no cache or expired: Proceed to step 2

2. Attempt GitHub fetch
   → If successful: Use fetched config, update cache
   → If failed: Proceed to step 3

3. Disable Extension
   → Show overlay: "Cannot connect to configuration server"
   → User cannot use extension until GitHub is reachable
   → This is intentional (security measure)
```

**Why Disable on Fetch Failure:**
- Prevents unauthorized use if block list can't be checked
- Ensures emergency disable works
- Security-first approach

---

## Local Data Storage

### Storage Technology

The Extension uses `chrome.storage.local` API, which:
- Stores data in Chrome's internal database
- Located in Chrome's profile directory on your hard drive
- Encrypted at the operating system level
- Isolated per-extension (other extensions can't access it)

### Storage Location

**Windows:**  
```
C:\Users\[YourName]\AppData\Local\Google\Chrome\User Data\Default\Local Storage\
```

**macOS:**  
```
~/Library/Application Support/Google/Chrome/Default/Local Storage/
```

**Linux:**  
```
~/.config/google-chrome/Default/Local Storage/
```

### Data Retention

**How Long Data is Stored:**
- Until you uninstall the extension (then deleted automatically)
- Until you manually clear via "Reset Subscription Timer" button
- Until you clear Chrome data via browser settings

**What Happens on Uninstall:**
- Chrome automatically deletes ALL extension data
- Settings are not recoverable after uninstall
- You must reconfigure if you reinstall

---

## Third-Party Services

The Extension interacts with three third-party services:

### 1. YouNow.com

**What It Is:** YouNow is a live streaming platform where the Extension provides automation features.

**How We Interact:**
- Extension reads public page content (subscriber lists, chat messages)
- Extension sends actions (chat messages, clicks buttons)
- All interaction through web interface (no private APIs)

**YouNow's Privacy Policy:** [younow.com/policy/en/privacy](https://www.younow.com/policy/en/privacy)

**Your Responsibility:**
- Ensure your use of automation complies with YouNow's Terms of Service
- Use automation features responsibly

### 2. GitHub (Microsoft)

**What It Is:** GitHub hosts the configuration file the Extension fetches.

**How We Interact:**
- Single HTTP GET request every 5 minutes (when extension is active)
- Fetch configuration file from public repository
- No data transmitted, read-only

**GitHub's Privacy Policy:** [docs.github.com/en/site-policy/privacy-policies](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement)

**Data Shared with GitHub:**
- Your IP address (standard for any web request)
- Browser User-Agent (standard HTTP header)
- Timestamp of request
- NO extension-specific data, usernames, or identifiers

### 3. Discord (Optional)

**What It Is:** Discord integration is OPTIONAL. You must explicitly configure it.

**How It Works:**
- You provide a Discord webhook URL (optional)
- Extension sends chat messages to your Discord server via webhook
- Extension sends "Go Live" notifications when you start streaming

**Discord Integration is Optional:**
- Disabled by default
- You must explicitly configure a webhook URL
- You can disable anytime in settings

**Discord's Privacy Policy:** [discord.com/privacy](https://discord.com/privacy)

---

## Data Security

### Security Measures

1. **No Central Database**
   - We have no servers storing user data
   - No database to hack or breach
   - Your data exists only on your device

2. **Local Storage Security**
   - Chrome's storage API provides isolation
   - Encrypted at OS level
   - Not accessible to other extensions or websites

3. **HTTPS Only**
   - GitHub configuration fetch uses HTTPS (encrypted)
   - YouNow interactions through HTTPS

4. **No Analytics or Tracking**
   - No Google Analytics or similar services
   - No tracking pixels or cookies
   - No telemetry or crash reporting

5. **Minimal Permissions**
   - Only request permissions necessary for functionality
   - No camera, microphone, or location access

### Potential Risks

1. **Local Device Compromise**
   - If someone gains physical access to your computer, they could access Chrome data
   - This is a general computer security issue
   - Mitigation: Use strong device passwords, lock screen when away

2. **GitHub Outage/Compromise**
   - If GitHub is compromised, attacker could modify configuration
   - Worst case: Extension disabled or you're blocked
   - NO risk to your personal data (we don't have your data)

---

## Your Rights and Choices

### What You Can Do

1. **View Stored Data**
   - Right-click extension icon → Inspect
   - Application tab → Storage → Local Storage
   - See all data stored by extension

2. **Delete Stored Data**
   - Click "Reset Subscription Timer" in settings
   - Uninstall extension (deletes all data)
   - Chrome Settings → Privacy → Clear browsing data

3. **Opt Out Completely**
   - Uninstall the extension
   - All local data automatically deleted

4. **Control Features**
   - Toggle any feature on/off in extension popup
   - Disable features you don't want
   - Extension respects your choices immediately

### GDPR Rights (EU Users)

Under GDPR, you have rights regarding personal data. However:

**We Have No Personal Data:**
- Right to Access: We have no data to provide
- Right to Deletion: Uninstall extension
- Right to Portability: Export via DevTools (manual process)

### CCPA Rights (California Users)

Under CCPA, California residents have rights regarding personal information. However:

**We Don't Sell Your Data:**
- We don't collect personal information
- We don't sell, rent, or share data with third parties
- No advertising or marketing use

---

## Children's Privacy

**Age Requirement:**

YouNow requires users to be at least 13 years old. Our extension follows the same requirement:
- Not intended for children under 13
- Requires YouNow account (which has age restriction)
- We do not knowingly collect data from children

**Parental Controls:**
- Parents can uninstall extension from child's browser
- Parents can use Chrome's supervised user features

---

## Changes to This Policy

### How We Update

**When We May Update:**
- New features added requiring additional permissions
- Changes to third-party services we interact with
- Legal requirements or best practices evolve

**How You'll Be Notified:**
1. Version number change at top of document
2. Extension update through Chrome
3. Notification in extension popup for major changes

**Where to Find Latest Version:**
- [GitHub Repository](https://github.com/Coikars/yn-koi-extension/blob/main/PRIVACY_POLICY.md)
- Chrome Web Store listing

---

## Contact Information

### How to Reach Us

**Email:** [coikars@outlook.com](mailto:coikars@outlook.com)

**Response Time:** We aim to respond within 7 business days.

**What to Contact Us About:**
- Privacy concerns or questions
- Security vulnerability reports
- Request to be added to override list (staff/moderators)
- Bug reports affecting privacy

**Security Vulnerabilities:**

If you discover a security vulnerability:

1. Email: [coikars@outlook.com](mailto:coikars@outlook.com)
2. Subject: "Security Vulnerability - YouNow Koi Addons"
3. Include:
   - Description of vulnerability
   - Steps to reproduce
   - Potential impact

**Our Commitment:**
- Acknowledge receipt within 48 hours
- Investigate promptly
- Not pursue legal action against responsible disclosure

---

## Summary

### Key Privacy Points

✅ **No Data Collection** - We don't collect, store, or transmit personal data  
✅ **Local Storage Only** - All settings saved on your device  
✅ **Transparent Operation** - Configuration file publicly viewable on GitHub  
✅ **Minimal Permissions** - Only what's necessary for functionality  
✅ **No Tracking** - No analytics, cookies, or cross-site tracking  
✅ **Your Control** - Uninstall anytime to delete all data  
✅ **Third-Party Transparency** - Clear disclosure of GitHub and YouNow interaction  
✅ **Security First** - No servers to hack, no databases to breach  

**Questions?** Contact [coikars@outlook.com](mailto:coikars@outlook.com)

---

**Last Updated:** March 4, 2026  
**Version:** 1.0.0  
**Effective Date:** March 4, 2026
