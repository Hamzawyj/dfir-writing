# Android Application Icons

**Original blog post:**  
🔗 https://www.forensafe.com/blogs/android-application-icons.html  

**Category:** Android forensics – launcher icon cache artifact  
**Status:** Public DFIR blog post with supporting notes in this repo.

---

## 1. Overview

Android Application Icons represent records of app labels and icons cached by the launcher.  
They help confirm that an application was present on the device, show which component was represented by the icon entry, and record when that entry was last refreshed.

These notes complement the original blog post and focus on the DFIR interpretation of the artifact.

---

## 2. Typical source / location

According to the blog and testing, this artifact is stored in a launcher database:  

- **Database:** `app_icons.db`  
- **Example path:**  
  `/data/data/com.google.android.apps.nexuslauncher/databases/app_icons.db`  

(Exact paths and package names may vary between devices and launchers.)

---

## 3. Key fields of interest

Common fields of interest include:

- **Label** – The user-visible name of the app.  
- **Component Name** – Full component identifier (package/class) associated with the icon.  
- **Profile ID** – Indicates which Android user/profile the icon belongs to.  
- **Icon (hi-res / low-res)** – Cached icon bitmaps stored as BLOBs.  
- **System State / Version** – Context and version information saved with the entry.  
- **Database Row ID** – Internal row identifier within the source database.

---

## 4. DFIR value

From a forensic perspective, this artifact can help:

- **Confirm app presence** even if the app is later uninstalled or data is partially removed.  
- Show **which component or activity** was represented on the launch
