# DexaDean — Wireframes

Calm, spacious layouts. Single primary action per screen. Monochrome lines simplify; colour applied later.

---

## 1. Home Screen  
_“Olive Tree & Today’s Status”_

```
┌───────────────────────────────────────────┐
│  🌿  DexaDean                             │
│                                           │
│               ╭───╮                      │
│              (  🌳  )   ← gentle SVG      │
│               ╰───╯                      │
│                                           │
│   ✔︎ First dose taken        7:42 AM      │
│   ○ Next dose in ~3 h        11:42 AM     │
│                                           │
│───────────────────────────────────────────│
│   + log another medication                │
└───────────────────────────────────────────┘
```
Notes  
• Olive tree occupies visual centre; animates on success.  
• Timeline summary is concise: ✓, ○, or – symbols only.  
• A single touch area at bottom for quick add/log.

---

## 2. Medication Setup Screen  
_One sheet, one breath._

```
┌──────────────────── Add Medication ────────────────────┐
│ Name: [ Metformin  ]                                   │
│ Dose: [ 500 mg ▼ ]                                     │
│ Required doses / day: [ 2 ▼ ]                          │
│ Interval between doses:  [ 12  h ▼ ]                   │
│ Optional extra dose?    (•) No   ( ) Yes               │
│ Last allowable dose:     [ 9 PM ▼ ]                    │
│                                                         │
│──────────┬──────────────┬──────────────┐               │
│  Cancel  │              │    Save ✓    │ ← primary      │
└──────────┴──────────────┴──────────────┘
```
Notes  
• Kept within a modal card; fields stacked for thumb reach.  
• Radio-button style toggle keeps binary choice explicit.

---

## 3. Daily Log View  
_A reflective vertical timeline._

```
┌─────────────────── Today ────────────────────┐
│                                               │
│  7:42 AM  ●  Metformin 500 mg   ✓             │
│ 11:42 AM  ○  Metformin 500 mg  (due)          │
│  3:42 PM  ○  Optional dose     —              │
│                                               │
│───────────────────────────────────────────────│
│   Olive tree mini-thumbnail grows subtly →    │
└───────────────────────────────────────────────┘
```
Legend  
• ● = logged dose (filled); ○ = pending; — = skipped.  
Swipe right on a row to mark ✓; long-press to edit.

---

## 4. Notification Interaction  
_Lightweight banners; zero urgency._

### 4.1 First-Dose Nudge  
```
╭─ DexaDean ───────────────╮
│ Ready for your first dose?│
│         [ Taken ✓ ]       │
╰───────────────────────────╯
```

### 4.2 Interval Reminder  
```
╭─ DexaDean ───────────────╮
│ Next dose window open.    │
│            [ Taken ✓ ]    │
│            [ Snooze 1h ]  │
╰───────────────────────────╯
```

### 4.3 Optional Dose Prompt  
```
╭─ DexaDean ───────────────╮
│ Extra dose fits before cut-off. │
│         Take it today?          │
│  [ Yes ]      [ Skip ]          │
╰─────────────────────────────────╯
```
Notes  
• Banners default to silent; haptic only if enabled.  
• Primary action always left-aligned for easy reach.

---

_End of wireframes._
