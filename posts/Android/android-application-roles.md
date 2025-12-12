# Android Application Roles

**Original blog post:**  
🔗 https://www.forensafe.com/blogs/android-applicaiton-roles.html  

**Category:** Android forensics – system roles / default app assignment artifact  
**Status:** Public DFIR blog post with supporting notes in this repo.

---

## 1. Overview

Android Application Roles is a system artifact that records **which applications are assigned to specific system-defined roles** on the device.  
Roles define which app is trusted by the system to handle sensitive or core functions, such as:

- Default SMS handler  
- Default phone/dialer  
- Browser  
- Assistant  
- Home/launcher  
- Emergency or system-level services

From a DFIR perspective, this artifact helps identify **which app was trusted by the OS** to perform critical actions at a given time.

These notes complement the original blog and focus on forensic interpretation and investigative value.

---

## 2. Typical content

Depending on the Android version and OEM implementation, this artifact usually contains:

- **Role name** (e.g. SMS, DIALER, BROWSER, ASSISTANT)  
- **Assigned package name**  
- Optional metadata related to:
  - System defaults
  - User-selected changes
  - Role reassignment events

In some cases, only the **current role holder** is visible, not the full historical timeline.

---

## 3. DFIR value

From a forensic standpoint, Android Application Roles can be used to:

- Identify which app had **privileged handling rights** for sensitive functions.  
- Support investigations involving:
  - SMS interception
  - Call handling
  - Browser-based activity
  - Voice assistant abuse
- Validate or refute claims such as:
  - “This app never handled my messages”
  - “I never set this app as the default dialer”
- Highlight **potential abuse or persistence mechanisms**, where a malicious or unwanted app is assigned a powerful role.

This artifact is especially relevant in fraud, spyware, stalking, and social-engineering cases.

---

## 4. Tool parsing notes (e.g. ArtiFast)

When parsed by tools such as ArtiFast, examiners typically see:

- A **role-to-application mapping view**  
- Clear identification of:
  - Role name
  - Assigned package
- Integration with other application metadata (install time, version, permissions)

During analysis, examiners should verify:

- Whether the artifact shows **current state only** or includes historical changes.  
- Consistency between roles and:
  - Installed applications
  - App usage history
  - Permission assignments
- OEM-specific behavior that may affect role visibility.

---

## 5. Example investigation scenario

Example use case:

> A user reports that their SMS messages were being intercepted by an unknown application.

Using Android Application Roles, an examiner can:

- Identify the **default SMS role holder**.  
- Confirm which app was responsible for handling messages.  
- Cross-reference that app with:
  - App usage history
  - Permission grants
  - Network activity
- Determine whether the app assignment aligns with user intent or indicates abuse.

---

## 6. Related artifacts

Android Application Roles is often correlated with:

- **Installed Applications / Package Manager** – to confirm app presence and version.  
- **Android App Usage History** – to see when the role-holding app was active.  
- **Permissions and AppOps artifacts** – to validate access to sensitive resources.  
- **SMS / Call logs** – to assess real-world impact of role assignment.
