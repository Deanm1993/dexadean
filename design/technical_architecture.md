# DexaDean – Technical Architecture

A concise blueprint for building a humane, offline-first medication tracker that respects user autonomy and privacy.

---

## 1. Technology Stack

Platform | Layer | Recommendation | Rationale
---------|-------|----------------|----------
iOS | UI | **SwiftUI** | Declarative, lightweight, adaptive to Dynamic Type
 | State | **Combine** + ObservableObject | Reactive bindings minimise boiler-plate
 | Data | **Core Data** backed by **SQLCipher** | Encrypted SQLite, zero cloud dependency
 | Notifications | **UNUserNotificationCenter** + **BGTaskScheduler** | Local scheduling, background refresh
 | Animation | **SwiftUI Animations** | Built-in spring curves, Reduce Motion compliance
Android | UI | **Jetpack Compose** | Modern, declarative, material-agnostic
 | State | **Kotlin Flow + ViewModel** | Structured concurrency, lifecycle-aware
 | Data | **Room** + **SQLCipher** | Encrypted DB, compile-time schema checks
 | Notifications | **WorkManager** + **AlarmManager** (API 31-) | Battery-friendly, Doze-aware
 | Animation | **Compose Animations** | Respect system motion settings
Shared | Crypto | **SQLCipher 4**, **AES-256** | Proven encryption
 | Serialization | **Kotlinx/Swift Codable** (JSON/CSV) | Simple export
 | Testing | **JUnit 5 / XCTest**, **MockK/CombineSchedulers** | Deterministic dose-logic tests

---

## 2. Data Models & Storage

Entity | Fields | Notes
-------|--------|------
Medication | `id` UUID<br>`name` String<br>`doseAmount` Float<br>`doseUnit` String<br>`dosesPerDay` Int<br>`intervalMins` Int<br>`allowOptional` Bool<br>`cutOffTime` LocalTime | Immutable after creation except dose settings
DoseLog | `id` UUID<br>`medicationId` FK<br>`timestamp` Instant<br>`type` Enum(required/optional)<br>`status` Enum(taken/skipped) | Primary timeline source
OliveTreeState | `id` (singleton)<br>`lastGrowthDate` Date<br>`adherenceScore7d` Float | Derived data but cached for fast render
UserPrefs | `quietHoursStart` LocalTime<br>`quietHoursEnd` LocalTime<br>`hapticsEnabled` Bool<br>`theme` Enum | Stored in encrypted shared prefs / Keychain

Storage strategy  
1. Single encrypted SQLite file per installation.  
2. All writes go through a repository layer emitting Kotlin Flow / Combine Publishers.  
3. Optional export produces a CSV or JSON sent via OS share sheet—no automatic sync.  
4. Migration scripts versioned; integrity verified on launch.

---

## 3. Notification System Architecture

```
+--------------------------+
| DoseScheduler (Service)  |
+-----------+--------------+
            |
            v
+--------------------------+
| DoseEngine               |
| 1. Fetch last DoseLog    |
| 2. Calculate next time   |
| 3. Check quiet hours     |
+-----------+--------------+
            |
         schedule
            v
+--------------------------+
| OS Notification Center   |
+--------------------------+
```

Workflow  
1. App launch or dose logged → `DoseEngine` computes next required/optional dose.  
2. If `now + interval` falls within quiet hours, schedule at quietHoursEnd.  
3. Engine writes a **PendingDose** row to persist intent across reboots.  
4. OS delivers silent banner with action buttons *Taken* / *Snooze*.  
5. Button taps captured via notification intents → repository logs `DoseLog` → Engine recalculates.

Reliability  
• On iOS, `BGAppRefreshTask` re-schedules missed notifications.  
• On Android, `WorkManager` with `setExactAndAllowWhileIdle` for critical dose windows.

---

## 4. Privacy & Security

Concern | Measure
--------|---------
Data-at-rest | Full-DB encryption (SQLCipher) using device-secure key
Data-in-motion | None by default; export only via user-initiated share
Analytics | Disabled; optional, anonymised opt-in later using self-hosted instance
Personal Identifiers | No account, no email; all IDs are random UUID v4
Permissions | Request *Notifications* only; no location, contacts, or health data unless user enables Apple Health / Health Connect export
Crash Reporting | OS-native symbolicated logs, no 3rd-party SDKs
GDPR / CCPA | User can wipe data in Settings (`DELETE FROM *` + key purge). No server copies means fulfillment within seconds.
Threat Model | Local attacker with device access → relies on OS secure storage; remote attacker → no surface.

---

## 5. Implementation Roadmap

Phase | Duration | Goals | Key Deliverables
------|----------|-------|-----------------
0. Foundations | 2 wks | Repo, CI, coding style, DB schema | Skeleton app, unit tests running
1. MVP Core | 4 wks | Add medication, log doses, local notifications | iOS & Android functional parity, basic tree graphic
2. Accessibility & Polish | 3 wks | VoiceOver/TalkBack, Dynamic Type, haptics toggle | WCAG AA audit pass
3. Motivational Layer | 2 wks | Full olive tree growth logic, animations | SVG assets, state machine
4. Data Export & Import | 2 wks | CSV/JSON share, HealthKit/Health Connect optional write | Settings UI, permission flows
5. Hardening & Release | 3 wks | Security pen-test, battery profiling, store compliance | App Store / Play listing, privacy policy

Total: ~16 weeks for v1. Continuous integration enables earlier TestFlight / Internal Play tracks after Phase 1.

---

### Alignment with dumbware.io

✔ Offline-first, device-only storage  
✔ Minimal permissions, no surveillance  
✔ Silent, respectful notifications  
✔ Incremental roadmap—ship value early without bloat

DexaDean’s architecture keeps the user at the centre—empowered, not exploited. 
