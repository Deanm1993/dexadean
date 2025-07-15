# DexaDean – Humane Medication Tracker

DexaDean is a minimalist, offline-first app that helps people take their medications consistently without stress.  
Guided by the *dumbware.io* philosophy, it favors simplicity, respect, and calm technology over endless features and noisy reminders.

---

## Core Principles

1. **Simple** – Focused feature set, single-screen flows, zero clutter.  
2. **Respectful** – User data stays on-device; notifications are gentle nudges, not nags.  
3. **Calm** – Soothing visuals, subtle haptics, and a thriving olive tree that grows with adherence.

---

## Repository Structure

```
/
├── design/
│   ├── app_design_document.md
│   ├── wireframes.md
│   ├── user_flow.md
│   ├── visual_design.md
│   └── technical_architecture.md
└── README.md   ← you are here
```

### Key Design Documents

| File | What it Contains |
|------|------------------|
| **app_design_document.md** | Product goals, UX philosophy, feature descriptions, dose logic. |
| **wireframes.md** | Low-fidelity sketches of primary screens and notification banners. |
| **user_flow.md** | Diagram of the end-to-end user journey, including missed-dose paths. |
| **visual_design.md** | Color palette, typography, component specs, animation & accessibility guidelines. |
| **technical_architecture.md** | Platform stack, data models, notification engine, security measures, roadmap. |

Start with these files for a deep dive into DexaDean’s experience and technical blueprint.

---

## Getting Started

1. **Clone the repo**

   ```
   git clone https://github.com/your-org/dexadean.git
   ```

2. **Read the Design Docs**

   Familiarize yourself with the vision and constraints before coding.

3. **Choose a Platform**

   The architecture supports parallel iOS (SwiftUI) and Android (Jetpack Compose) implementations. Pick one and follow the guidelines in `technical_architecture.md`.

4. **Set Up the Project**

   - Generate an empty app shell.  
   - Add the encrypted SQLite layer (`SQLCipher`).  
   - Implement the Medication entity and Dose calculation logic (see pseudocode in the design doc).

---

## Next Steps

| Phase | Goal | Status |
|-------|------|--------|
| Foundations | Repo scaffolding, CI/CD, DB schema | 🔜 |
| MVP Core | Medication setup, dose logging, local notifications | |
| Accessibility & Polish | VoiceOver/TalkBack, dynamic type, haptics toggle | |
| Motivational Layer | Olive tree growth animations, adherence logic | |
| Export & Release | Data export, privacy review, store submission | |

Contributors are encouraged to tackle tasks in sequence to keep the product lean and coherent.

---

## Contributing

1. Fork → Feature Branch → Pull Request.  
2. Follow the coding conventions outlined in the platform folder.  
3. Respect the **dumbware** ethos—if a change adds complexity, question it first.

---

## License

Released under the MIT License. See `LICENSE` for details.

---

Made with 🍃 and care to keep technology quiet, helpful, and human-friendly.
