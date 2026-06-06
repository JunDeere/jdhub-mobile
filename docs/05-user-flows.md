# JDHub Mobile – User Flows Document

## 1. Overview

This document describes the main user flows for JDHub Mobile v1, focused on the Meal Tracker module.

The app should be designed as JDHub Mobile first, with Meal Tracker as the first module.

## 2. First App Open Flow

```text
Open app
↓
Check local database
↓
If no profile or onboarding not completed:
    Show onboarding
Else:
    Go to dashboard
```

Optional restore flow:

```text
Open app
↓
No local profile found
↓
Show options:
    Start new setup
    Restore from backup
```

## 3. Onboarding Flow

The onboarding should be step-based.

```text
Step 1: Personal Info
↓
Step 2: Body / Goal Info
↓
Step 3: Meal Tracking Setup
↓
Step 4: Schedule / Night Shift Setup
↓
Step 5: Notifications / Accountability Style
↓
Step 6: Finish Setup
↓
Dashboard
```

### Step 1: Personal Info

Fields:

- Name or alias
- Email optional
- Phone optional

### Step 2: Body / Goal Info

Fields:

- Age
- Height
- Current weight
- Target weight optional
- Initial goal type
- Preferred weight unit

The selected goal should create the first goal phase.

### Step 3: Meal Tracking Setup

Fields:

- Preferred food unit
- Default meal categories
- Weighing tip acknowledgement

Show highlighted tip:

```text
For better consistency, weigh food after it is cooked.
Example: cooked rice 250g, cooked chicken 180g.
```

### Step 4: Schedule / Night Shift Setup

Fields:

- Normal or night-shift/unusual schedule
- Wake-up time
- Sleep time
- Tracking day reset time

The app should explain that reset time controls when a new tracking day begins.

### Step 5: Notifications / Accountability Style

Fields:

- Meal reminder enabled
- Reminder offset before sleep
- Custom reminder time optional
- Notification tone

### Step 6: Finish Setup

Show summary:

- Alias
- Goal
- Tracking unit
- Wake time
- Sleep time
- Reset time
- Reminder setting
- Tone

Action:

- Start Tracking

## 4. Dashboard Flow

```text
Open app
↓
Calculate active day
↓
Load meals for active day
↓
Load daily note
↓
Load current goal phase
↓
Load streak status
↓
Display dashboard
```

Dashboard should show:

- Current active day/date
- Current goal phase
- Meal status summary
- Meals logged today
- Planned meals
- Daily note preview
- Streak count
- Quick actions

Quick actions:

- Add Meal
- Plan Meal
- Add Weight
- Add Daily Note
- Copy Day

## 5. Add Meal Flow

```text
Tap Add Meal
↓
Select date
↓
Select meal category
↓
Enter food name
↓
Show recent/favorite food suggestions
↓
Enter amount
↓
Select unit
↓
Select status: planned/eaten/skipped
↓
Select confidence: exact/estimated/unknown
↓
Add notes optional
↓
Save
↓
Save meal log
↓
Update food library
↓
Return to dashboard/date view
```

Food library rule:

- If food name does not exist, add it.
- If it exists, update usage count and last used date.
- Do not save amount in the food library name.

## 6. Edit Meal Flow

```text
Open meal details
↓
Tap Edit
↓
Change meal fields
↓
Save changes
↓
Update dashboard/date view
```

Editable fields:

- Date
- Meal category
- Food name
- Amount
- Unit
- Status
- Confidence
- Notes

## 7. Delete Meal Flow

```text
Open meal details
↓
Tap Delete
↓
Confirm deletion
↓
Soft delete meal log
↓
Return to dashboard/date view
```

Deleting a meal should not delete the food library suggestion.

## 8. Duplicate Meal Flow

```text
Open meal details
↓
Tap Duplicate
↓
Choose target date
↓
Choose status for duplicated meal
↓
Save duplicate
```

Example:

- Duplicate breakfast to tomorrow
- Duplicate lunch to selected date

## 9. Copy Day Flow

```text
Open date view
↓
Tap Copy Day
↓
Choose source date
↓
Choose target date
↓
Preview meals to copy
↓
Confirm
↓
Copy all selected meals to target date
```

This supports meal planning.

Copied meals should usually be set as planned by default when copied to a future date.

## 10. Planned Meal Flow

```text
Create meal for future date
↓
Status: planned
↓
When active day arrives, show planned meal
↓
User marks as eaten or skipped
```

If the active day passes and the planned meal is not confirmed, it can be marked internally as auto-skipped.

## 11. Backfilled Meal Flow

```text
User selects old date
↓
Adds meal
↓
App checks if selected active day already ended
↓
If yes, mark meal as backfilled
↓
Save meal
```

Backfilled meals:

- Should appear in history
- Should count in reports
- Should not repair streaks
- Should be visually labeled as backfilled

## 12. Daily Note Flow

```text
Open date view
↓
Tap Add/Edit Daily Note
↓
Enter note
↓
Save
```

Daily notes are tied to date/active day.

## 13. Weight Log Flow

```text
Tap Add Weight
↓
Select date
↓
Enter weight
↓
Select unit
↓
Add note optional
↓
Save
```

Weight logs should support any date.

## 14. Food Library Flow

```text
Open Food Library
↓
View recent foods
↓
View favorite foods
↓
Search foods
↓
Favorite/unfavorite food
↓
Hide/delete unwanted suggestion
```

Hiding/deleting a suggestion should not delete previous meal logs.

## 15. Goal Phase Flow

```text
Open Settings or Goals
↓
View current goal phase
↓
Tap Change Goal
↓
Select new goal type
↓
Select start date
↓
Optionally add note
↓
Confirm
↓
Close previous active goal
↓
Create new active goal phase
```

Goal types:

- Bulk
- Cut / weight loss
- Maintain
- General

## 16. Reminder Flow

```text
App checks reminder settings
↓
Calculate reminder time based on sleep time or custom time
↓
If no meal logged or planned meals not resolved:
    Send local notification
```

Reminder example:

```text
Sleep time: 11:00 PM
Reminder offset: 3 hours
Reminder time: 8:00 PM
```

Night-shift example:

```text
Sleep time: 10:00 AM
Reminder offset: 3 hours
Reminder time: 7:00 AM
```

## 17. Streak Flow

```text
Active day ends
↓
Check if at least one on-time eaten meal exists
↓
If yes:
    Count streak
Else:
    Mark skipped day
```

Rules:

- On-time eaten meals count.
- Backfilled meals do not repair streaks.
- Planned meals do not count until marked eaten.
- Skipped meals do not count.

## 18. Backup / Restore Flow

Future flow:

```text
Open Settings
↓
Tap Export Backup
↓
Create JSON backup file
↓
User saves file locally or to cloud storage
```

Restore flow:

```text
Open app or Settings
↓
Tap Import Backup
↓
Select backup file
↓
Validate backup
↓
Restore data
```

Future storage options:

- Local JSON file
- Google Drive
- JDHub cloud sync
