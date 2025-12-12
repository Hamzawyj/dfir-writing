# DFIR Writing Portfolio

This repository is a structured index of my **Digital Forensics & Incident Response (DFIR)** blog posts.

Each post is accompanied by supporting notes in this repository, including:
- A link to the original published article (e.g., Forensafe blog)
- A concise summary of the artifact or behavior
- DFIR-relevant observations (artifact paths, fields, parsing behavior, investigative value, etc.)

---

## 📚 Posts

- [Android Application Roles](posts/Android/android-application-roles.md) — Identifies which apps are assigned to system roles (SMS, dialer, browser, assistant) and their DFIR relevance.
- [Android Application Operations](posts/Android/android-application-operations.md) — Android system artifact that records permission-related operations performed by applications.
- [Android Application Icons](posts/Android/android-application-icons.md) — Launcher cache artifact for app labels/icons and last update times, useful for confirming app presence and context.
- [Android App Usage History](posts/Android/android-app-usage-history.md) — Usage statistics for app launches, foreground time, and configuration changes, ideal for rebuilding user activity and habits.
- [Android Calendar](posts/Android/android-calendar.md) — Built-in calendar database storing accounts, events, reminders, and instances, useful for reconstructing schedules and timelines.

> More posts will be added here as I publish new articles.

---

## 🧪 Focus Areas

- Cross-platform forensics: Android, iOS, Windows, macOS
- DFIR tool behavior and artifact parsing (e.g., ArtiFast and similar tools)
- Using artifacts to answer concrete investigative questions
