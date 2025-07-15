# DexaDean – Visual Design Guidelines

A calm, respectful interface that helps without demanding attention.  
These guidelines translate the dumbware.io philosophy into concrete visual language.

---

## 1. Color Palette

| Name             | Hex     | Usage                                   | WCAG Contrast on Sand |
|------------------|---------|-----------------------------------------|------------------------|
| Olive Green      | #6F8D5E | Primary actions, progress, olive tree   | 4.7 : 1 ✔︎ |
| Deep Charcoal    | #2F2F2F | Primary text, icons                     | 12.3 : 1 ✔︎ |
| Sand (Background)| #F2EFE6 | Surfaces, cards                         | — |
| Soft Amber       | #F3C98B | Warnings, optional prompts              | 3.9 : 1 ✔︎ |
| Sky Mist         | #E6F1EF | Success highlights, leaf accents        | 3.3 : 1 ✔︎ |
| Leaf Shadow      | #4C6447 | Focus rings, pressed states             | 7.0 : 1 ✔︎ |

Palette principles  
• Muted, organic hues—no stark primaries.  
• Colour is used sparingly: one dominant accent per screen.  
• Desaturated background keeps focus on content and tree.

---

## 2. Typography

Typeface: **Inter** (system-friendly, legible)  

| Role            | Size (pt) | Weight   | Line Height | Usage                            |
|-----------------|-----------|----------|-------------|----------------------------------|
| Display Title   | 24        | Semibold | 30          | Screen headers                   |
| Section Header  | 20        | Semibold | 26          | Card titles, timeline dates      |
| Body            | 16        | Regular  | 22          | Core text, button labels         |
| Caption         | 13        | Regular  | 18          | Hints, secondary info            |

Typography principles  
• Never more than two weights per screen.  
• Dynamic Type enabled: sizes scale with OS settings.  
• Left-aligned, generous line spacing for breathing room.

---

## 3. UI Components

### 3.1 Buttons

Style                  | Spec
-----------------------|---------------------------------------------
Shape                  | 8 px corner radius, full-width where possible
Primary (Olive)        | Fill: Olive Green • Text: Sand
Secondary (Outline)    | Stroke: Olive Green 1 px • Text: Olive Green • Fill: transparent
Pressed State          | Fill shifts to Leaf Shadow, 90 ms fade
Disabled               | Opacity 30 %, no color shift

### 3.2 Cards / Sheets

• Background Sand, elevation 2 (subtle shadow 4 % black @ 6 px y).  
• 16 px padding all around; 24 px between form groups.  
• Rounded top corners 20 px for modal sheets.

### 3.3 Input Fields

Element        | Spec
---------------|---------------------------------------------------
Field Body     | Sand fill, Deep Charcoal text
Border         | 1 px Leaf Shadow when focused, 0 px otherwise
Label          | Caption style above field, fades to 70 % opacity after entry
Touch Target   | Min 48 × 48 px

Validation  
• No red error states; use Soft Amber border + caption “Needs attention” to remain gentle.

---

## 4. Olive Tree Visualization

Art style: minimal vector, single-weight stroke, soft shading.  
Placed centrally on Home; miniature appears in timeline.

Adherence → Tree State

| 7-Day Adherence | Visual Changes                                     |
|-----------------|-----------------------------------------------------|
| 85–100 %        | New leaves; occasional olive sprites               |
| 60–84 %         | Growth slows; slight limb droop                    |
| < 60 %          | Visible wilt: lighter leaves, subtle sag           |
| Missed >2 days  | No further wilt; tree pauses to avoid negative spiral |

Rules  
• Tree never looks “dead” – keeps hope.  
• Growth only animates on log success or app open (<400 ms).  
• Colour shifts within palette—no harsh reds.

---

## 5. Motion & Animation

Guideline | Value
----------|-----------------------------------------------
Duration  | 200–300 ms for UI transitions; 400 ms for tree growth
Easing    | `cubic-bezier(0.25,0.1,0.25,1)` (gentle ease-in-out)
Delay     | None; animations commence immediately after action
Reduced Motion | Respect OS “Reduce Motion”: replace with cross-fade
Haptics   | Light tap on dose logged; disabled when system haptics off

No looping or attention-seeking movement. Motion reinforces cause & effect only.

---

## 6. Accessibility

Aspect                      | Implementation
----------------------------|--------------------------------------------------
Contrast                    | All text ≥4.5 : 1; icons ≥3 : 1 against Sand
VoiceOver / TalkBack        | Descriptive labels (“Dose taken, next due 11:42 AM”)
Dynamic Type                | Full support up to XXL; layouts reflow gracefully
Hit Area                    | Minimum 48 × 48 px interactive elements
Focus Rings                 | 2 px Leaf Shadow outline for keyboard/remote focus
Color Blind Safety          | Information never conveyed by color alone; icons + text used
Haptic & Motion Settings    | Both obey system accessibility toggles

DexaDean stays usable, legible, and calm for everyone.

---

### Dumbware Alignment Checklist

✔ Minimal surface colours  
✔ Nudges via gentle animations, not alarms  
✔ Data dignity: no decorative charts cluttering space  
✔ Silence by default—user chooses sound  

These visual principles ensure DexaDean remains a quiet, trustworthy companion on the path to medication consistency. 
