# Android Calendar

**Original blog post:**  
🔗 https://www.forensafe.com/blogs/android-calendar.html  

**Category:** Android forensics – calendar and scheduling data  
**Status:** Public DFIR blog post with supporting notes in this repo.

---

## 1. Overview

Android Calendar is the system calendar service used to manage schedules across one or more accounts (for example, Google accounts).  
It stores calendars, events, reminders, attendees, and instances of recurring events, making it a rich source for reconstructing timelines, commitments, and account usage.

These notes extend the DFIR perspective provided in the original blog post.

---

## 2. Typical source / location

Calendar data is stored in an application-private database:

- **Database name:** `calendar.db`  
- **Typical path:**  
  `/data/data/com.android.providers.calendar/databases/calendar.db`  

The exact path follows the standard app-private structure for `com.android.providers.calendar`.

---

## 3. Key fields of interest

The artifact can be split conceptually into **calendar-level** and **event-level** information.

### Calendar-level (accounts / settings)

Examples of relevant fields:

- **Visible** – Whether this calendar is shown in apps.  
- **Is Primary** – Indicates the default calendar for the account.  
- **Account Type** – Provider type (e.g. Google).  
- **Account Name / Owner Account** – Account identifier tied to the calendar (often an email).  
- **Timezone / Calendar Timezone** – Default time zone used for events.  
- **Sync Events** – Whether event syncing is enabled.  
- **ID** – Local calendar ID.  
- **Access Level / Permissions** – Level of access granted to the user/device.  
- **Max Reminders / Reminder settings** – Limits around reminders per event.  
- **Deleted** – Soft-delete marker for calendars no longer active.

### Event-level (entries in the calendar)

Examples of event fields:

- **Title** – Event title or subject line.  
- **Start / End Date** – Event time range.  
- **Event Timezone** – Time zone applied to the event.  
- **Location** – Free-text location string.  
- **Organizer / Is Organizer** – Who created and owns the event.  
- **Self Attendee Status** – The device account’s RSVP state (accepted/declined/etc.).  
- **Event Status** – Tentative / confirmed / cancelled.  
- **Availability** – Free / busy flag.  
- **Has Alarm** – Whether reminders are set.  
- **UID (e.g. UID2445)** – Global unique identifier for cross-device/event linking.

---

## 4. DFIR value

The calendar database can help an examiner:

- Reconstruct **schedules and timelines** around key dates (meetings, calls, travel).  
- Show **which accounts** were actively used on the device and how they were configured.  
- Identify **recurring events and instances**, useful to see long-term patterns (e.g., weekly meetings).  
- Corroborate or challenge statements such as “I was in a meeting at that time” or “I didn’t plan this event.”  
- Track **deletions or changes** to events (via status and deleted flags where available).

Combined with other artifacts, calendar data adds strong context to a user’s activities.

---

## 5. Tool parsing notes (ArtiFast)

In ArtiFast, Android Calendar artifacts can be:

- Parsed via dedicated **Android Calendar** parsers.  
- Viewed as both **calendar metadata** (accounts/settings) and **event lists** (including recurring instances).  
- Correlated in **Timeline View** with app usage, communications, and other activity.

When using this artifact, pay attention to:

- How **time zones** and **daylight saving** are handled.  
- Whether **recurring instances** are expanded and shown as individual items.  
- How **deleted or cancelled events** appear in the interface.

---

## 6. Example investigation scenario

Typical scenarios where Android Calendar is valuable:

- Verifying whether a subject **had an appointment, meeting, or trip scheduled** at a particular time.  
- Correlating calendar events with **location data**, call logs, or messaging to confirm participation.  
- Establishing **routine patterns** (e.g. weekly recurring meetings with specific participants).  
- Highlighting **last-minute changes or cancellations** that may relate to an incident.

---

## 7. Related artifacts

Artifacts that work well together with Android Calendar include:

- Email or messaging records related to invitations and changes  
- Location data (GPS, cell records, Wi-Fi) around event times  
- Android App Usage History and notifications for context during calendar events  
- Account-level artifacts showing when accounts were added or removed
