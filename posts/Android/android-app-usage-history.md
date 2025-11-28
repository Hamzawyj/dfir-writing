# Android App Usage History

**Original blog post:**  
🔗 https://www.forensafe.com/blogs/android-app-usage-history.html  

**Category:** Android forensics – app usage statistics  
**Status:** Public DFIR blog post with supporting notes in this repo.

---

## 1. Overview

Android App Usage History records how applications are used on the device.  
It logs launches, how long apps stay in the foreground, and configuration or state changes, making it extremely useful for reconstructing user behavior and app habits over time.

These notes expand on the DFIR aspects behind the original article.

---

## 2. Typical source / location

Usage history is stored in usage statistics files under the system user context:

- **Base path:**  
  `/data/system_ce/<user_id>/usagestats/`  

- **Subfolders (by interval):**  
  - `daily/`  
  - `weekly/`  
  - `monthly/`  
  - `yearly/`  

Each folder contains usage records for the corresponding period.

---

## 3. Key fields of interest

The ArtiFast representation (and underlying structures) typically expose:

- **Frequency / Interval** – The period covered by the record (daily, weekly, etc.).  
- **Event Type** – Type of usage event (e.g. activity resumed, paused, configuration change).  
- **Usage Type / State** – High-level usage category/state for the app.  
- **Package Name** – Identifier of the application.  
- **Class Name / Component Name** – Specific activity/component involved.  
- **Times Launched** – Number of times the app was started.  
- **Total Active Time** – Aggregate time the app spent active in the foreground.

---

## 4. DFIR value

From this artifact, an examiner can:

- Build **timelines of app usage**: when a given app was active and for how long.  
- Identify **frequently used apps** and user habits over days/weeks/months.  
- Correlate app launches with **specific events** (e.g. messages sent, calls made, data exfiltration).  
- Highlight potentially **suspicious or unexpected app behavior**, such as an app being active at unusual hours or excessively active compared to normal patterns.

This is powerful context when reconstructing what a user was doing around a specific incident window.

---

## 5. Tool parsing notes (ArtiFast)

With ArtiFast, Android App Usage History can be:

- Parsed via dedicated **Android App Usage History** artifact parsers.  
- Reviewed in **Artifact View** for tabular inspection and filtering.  
- Correlated in **Timeline View** with other artifacts like calendar events, notifications, or network activity.

Points to verify during analysis:

- How **time zones** and **epoch formats** are interpreted.  
- Whether **interval types** (daily/weekly/monthly/yearly) are clearly labeled.  
- Performance when loading large numbers of usage records.

---

## 6. Example investigation scenario

Example cases where this artifact is valuable:

- A suspect claims they **did not use** a certain social media or messaging app during a specific time window.  
- An examiner needs to show **patterns of usage** that support or contradict testimony (e.g. nightly gaming sessions, frequent opening of a finance app before fraudulent transactions).  
- Correlating application usage with **data theft**, harassment, or stalking allegations.

By analyzing usage intervals, event types, and total foreground time, an investigator can tell a much more precise story about how the device was used.

---

## 7. Related artifacts

Useful companions to this artifact include:

- Android Application Operations (permission operations)  
- Android Digital Wellbeing / other app usage metrics (where available)  
- Notifications, call logs, and messaging artifacts  
- Network traffic or proxy logs where obtainable
