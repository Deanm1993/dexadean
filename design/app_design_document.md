# DexaDean – Humane Medication Tracker  
*A calm companion for everyday consistency.*

---

## 1. Purpose

DexaDean helps people take their medications reliably without stress.  
It embodies dumbware.io principles—technology that is:

* **Simple**: minimal features, no clutter.  
* **Respectful**: puts user autonomy first, never shames or nags.  
* **Calm**: soothing visuals, gentle haptics, silence by default.

---

## 2. Design Principles & UX Philosophy

| Principle | Practical Expression |
|-----------|----------------------|
| Minimal Footprint | One-hand gestures, single-screen flows, no hidden settings forests. |
| Agency over Automation | User chooses when to be reminded; app adapts to real behaviour rather than dictating times. |
| Soft Feedback | Positive reinforcement (olive tree growth) instead of streaks, badges, or alarms. |
| Ambient, Not Demanding | Default notification is a low-key banner with no sound. Missed doses ≠ push storm. |
| Data Dignity | All data lives on-device; export is explicit. No 3rd-party analytics beyond crash logs. |
| Legible Design | Large hit areas, dyslexia-friendly fonts, high contrast optional theme. |

---

## 3. High-Level Architecture

```
┌────────────┐      schedule      ┌──────────────┐
│   UI Layer │ ─────────────────▶ │ Notification │
│  (SwiftUI) │                   │   Engine     │
└─────▲──────┘                   └─────▲────────┘
      │ binding                         │ triggers
┌─────┴────────┐   LiveData stream  ┌───┴─────────┐
│   ViewModel  │───────────────────▶│   Domain    │
│  (Compose /  │                    │  Logic      │
│   Redux)     │◀───────────────────┘(Dose calc)  │
└─────▲────────┘    local store         ▲         │
      │                                  │         │
┌─────┴────────┐  encrypted SQLite   ┌───┴─────────┐
│ Persistence  │◀───────────────────▶│  Sync /     │
│   Layer      │                    │  Export     │
└──────────────┘                    └─────────────┘
```

* **Offline-first**: entire app functional without connectivity.  
* **Background task** recalculates next-dose windows.  
* **Notification Engine** respects user-set quiet hours.

---

## 4. Core Components

### 4.1 Medication Setup
Field | Notes
------|------
Name | free text with autocomplete (no database fetch).
Dose | numeric + units picker.
Required doses / day | 1–8 range.
Interval | hours & minutes picker.
Optional extra dose | toggle.
Cut-off time | time picker; obeys circadian preference.

Flow: Add → Review summary → Save. All in one card sheet.

### 4.2 Daily Log & Notification Logic
1. Day begins at first *Taken* tap.  
2. Next dose time = last dose + interval.  
3. If optional dose window ends before cut-off, prompt: “Would you like an extra dose today?” (Yes/Skip).  
4. Log view: a vertical timeline with tactile dots; green = taken, hollow = pending, grey = skipped.

### 4.3 Motivational Olive Tree
State driver: percentage of scheduled doses taken last 7 days.

% Adherence | Tree State
------------|-----------
85–100% | new leaves / olives
60–84%  | slow growth, mild wilt
<60%    | visible droop, no leaf loss (no guilt)

Tree animates only on log screen open—never interruptive.

### 4.4 Settings & Privacy
* Quiet Hours  
* Export Data (.csv or Apple Health optional)  
* Delete All Data  
* Theme (Light / Dark / High-contrast)  

No sign-up, no cloud account by default.

---

## 5. Interaction Model & Flows

1. **First Run**  
   Welcome → Add first medication → Explain olive tree → Done.

2. **Daily Use**  
   a. Notification “Ready for your first dose?” → Tap “Taken”.  
   b. Timeline shows ✔️.  
   c. Olive tree gently grows a leaf (200 ms spring animation).  
   d. Device returns to idle.

3. **Missed Dose**  
   If no action within recommended window:  
   • Timeline dot turns amber.  
   • Next reminder is a passive badge count, not a push.

---

## 6. Visual & Motion Guidelines

Colour palette (WCAG AA contrast):

* Olive Green #6F8D5E (primary)  
* Sand #F2EFE6 (background)  
* Deep Charcoal #2F2F2F (text)  
* Soft Amber #F3C98B (warning)

Typography:  
* Headings – **Inter**, 20 pt, semibold  
* Body – **Inter**, 16 pt, regular

Motion:  
* Max 300 ms, cubic-bezier(0.25,0.1,0.25,1)  
* Reduced Motion setting disables leaf animations.

---

## 7. Implementation Guidelines

Platform targets:  
* iOS 16+, Android 11+ (Kotlin + Jetpack Compose)  
* Use native notification schedulers (UNUserNotificationCenter / WorkManager).  
* Encrypt SQLite with SQLCipher.  
* Unit test dose-calculation logic incl. DST edge cases.  
* Accessibility: VoiceOver/ TalkBack labels for each control; timeline supports dynamic type.  
* Analytics-lite: local count of active days; no remote logging.

---

## 8. Future Extensions / Non-Goals

Possible:  
* Multi-user (caregiver) mode  
* Refill reminders based on pill count

Out of scope:  
* Complex drug-interaction warnings  
* Food diary, vitals tracking  
* Social sharing, leaderboards

---

### Appendix A – Dose Calculation Pseudocode

```
nextDose(now, lastDose, interval, cutOff):
    candidate = lastDose + interval
    if candidate.time <= cutOff:
        return candidate
    else:
        return tomorrow.morning
```

---

DexaDean embraces *enough* technology—no more, no less—to support healthy routines with dignity.
