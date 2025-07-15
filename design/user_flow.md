# DexaDean User Flow

This diagram illustrates the user journey through the DexaDean app, highlighting its calm, respectful approach to medication management.

## Core User Flow

flowchart TD
    Start([App First Launch]) --> Intro[Welcome & Philosophy Introduction]
    Intro --> AddFirst[Add First Medication]
    AddFirst --> TreeIntro[Introduce Olive Tree Concept]
    TreeIntro --> HomeScreen[Home Screen]
    
    %% Medication Setup Flow
    HomeScreen --> |"Tap + Add Medication"| MedSetup[Medication Setup Screen]
    MedSetup --> |"Enter medication details"| ReviewMed[Review Summary]
    ReviewMed --> |"Confirm"| SaveMed[Save Medication]
    SaveMed --> HomeScreen
    
    %% Daily Usage Primary Path
    HomeScreen --> |"Morning"| FirstDoseNotif[First Dose Notification]
    FirstDoseNotif --> |"Tap 'Taken'"| LogDose[Log First Dose]
    LogDose --> |"Subtle tree growth"| WaitInterval[Wait for Next Interval]
    WaitInterval --> |"Interval elapsed"| NextDoseNotif[Next Dose Notification]
    NextDoseNotif --> |"Tap 'Taken'"| LogNextDose[Log Next Dose]
    LogNextDose --> |"More doses today?"| DoseDecision{More Doses?}
    DoseDecision --> |"Yes"| WaitInterval
    DoseDecision --> |"No"| DayComplete[Day Complete]
    DayComplete --> |"Next day"| FirstDoseNotif
    
    %% Optional Dose Path
    WaitInterval --> |"Optional dose window"| OptionalPrompt{Optional Dose?}
    OptionalPrompt --> |"Yes"| LogOptional[Log Optional Dose]
    OptionalPrompt --> |"Skip"| SkipOptional[Skip Optional Dose]
    LogOptional --> WaitInterval
    SkipOptional --> WaitInterval
    
    %% Missed Dose Handling
    NextDoseNotif --> |"No response"| Missed[Missed Dose Window]
    Missed --> |"Passive badge only"| LaterReminder[Later Reminder]
    LaterReminder --> |"User opens app"| LogLate[Log Late Dose]
    LogLate --> WaitInterval
    Missed --> |"Past cut-off time"| EndDay[End of Day]
    EndDay --> |"Tree slightly wilts"| FirstDoseNotif
    
    %% Settings & Review
    HomeScreen --> |"Tap timeline"| LogView[Daily Log View]
    LogView --> |"Swipe on dose"| EditDose[Edit Dose Entry]
    EditDose --> LogView
    HomeScreen --> |"Tap settings"| Settings[Settings Screen]
    Settings --> |"Adjust preferences"| HomeScreen
    
    %% Visual styling
    classDef primary fill:#4672b4,color:white,stroke:#333,stroke-width:1px
    classDef success fill:#47956f,color:white,stroke:#333,stroke-width:1px
    classDef warning fill:#de953e,color:white,stroke:#333,stroke-width:1px
    classDef neutral fill:#555555,color:white,stroke:#333,stroke-width:1px
    classDef decision fill:#4672b4,color:white,stroke:#333,stroke-width:1px,shape:diamond
    
    class Start,HomeScreen,MedSetup primary
    class LogDose,LogNextDose,LogOptional,DayComplete success
    class Missed,LaterReminder warning
    class WaitInterval,Settings,LogView neutral
    class DoseDecision,OptionalPrompt decision

## Key Principles Illustrated

1. **Non-Demanding Notifications**: The app sends gentle reminders without creating pressure
2. **User-Initiated Timing**: First dose starts the day's schedule, adapting to user's natural rhythm
3. **Positive Reinforcement**: Tree growth provides subtle motivation without gamification
4. **Graceful Failure Handling**: Missed doses don't trigger anxiety-inducing alerts
5. **Minimal Decision Points**: Simple yes/no choices reduce cognitive load

The flow emphasizes user autonomy and calm technology principles throughout the medication management experience.
