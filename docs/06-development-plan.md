# JDHub Mobile – Flutter Development Plan

## 1. Overview

JDHub Mobile will be built using Flutter.

The first version focuses on the Meal Tracker module, but the project should be structured as a modular JDHub mobile app so future modules can be added later.

Future modules may include:

- Tasks
- Projects
- Journal
- Habits
- Fitness
- IMS tools
- Personal dashboard

## 2. Recommended Tech Stack

- Flutter
- Dart
- SQLite for local database
- Local notifications
- JSON backup/export later
- Google Drive backup later
- Future JDHub API sync later

## 3. Project Naming

Recommended project name:

```text
jdhub_mobile
```

Avoid naming the app only as Meal Tracker because the app will grow into a larger JDHub pocket multi-tool.

## 4. Recommended Folder Structure

```text
lib/
  main.dart
  app.dart

  core/
    constants/
    database/
    services/
    utils/
    widgets/

  modules/
    onboarding/
      screens/
      widgets/
      controllers/

    meal_tracker/
      screens/
      widgets/
      controllers/
      models/
      services/

    profile/
      screens/
      models/
      services/

    settings/
      screens/
      widgets/
      services/

    backup/
      screens/
      services/

  shared/
    models/
    widgets/
    theme/
```

## 5. Development Phases

## Phase 1: Project Setup

Tasks:

- Create Flutter project
- Set app name to JDHub Mobile
- Set up folder structure
- Add base theme
- Add basic navigation
- Add placeholder dashboard

Commands:

```bash
flutter create jdhub_mobile
cd jdhub_mobile
code .
flutter run
```

## Phase 2: Local Database Setup

Tasks:

- Add SQLite package
- Create database service
- Create migration/init logic
- Create tables
- Add seed/default data

Initial tables:

- user_profile
- user_settings
- goal_phases
- meal_logs
- food_library
- meal_categories
- daily_notes
- weight_logs
- reminder_settings
- streak_history
- backup_metadata

## Phase 3: Onboarding

Build step-based onboarding:

1. Personal Info
2. Body / Goal Info
3. Meal Tracking Setup
4. Schedule / Night Shift Setup
5. Notifications / Accountability Style
6. Finish Setup

Requirements:

- Save profile locally
- Save settings locally
- Create initial goal phase
- Seed default meal categories
- Mark onboarding as completed
- Add skip onboarding option for testing/development

## Phase 4: Dashboard

Build the main dashboard.

Dashboard should show:

- Current active day
- Current goal phase
- Meals for active day
- Planned meals
- Daily note preview
- Streak status
- Quick actions

Quick actions:

- Add Meal
- Add Weight
- Add Daily Note
- Copy Day

## Phase 5: Meal Logs

Build meal log features:

- Add meal
- Edit meal
- Delete meal
- Duplicate meal
- Copy day
- Mark planned/eaten/skipped
- Detect backfilled meals
- Show weighing tip for first few entries

Meal fields:

- Date
- Category
- Food name
- Amount
- Unit
- Status
- Confidence
- Notes

## Phase 6: Food Library

Build food memory and suggestions:

- Auto-save food names
- Show recent foods
- Show favorite foods
- Favorite/unfavorite food
- Hide/delete food suggestion
- Track usage count
- Track last used date

Rules:

- Save food name only.
- Do not save food amount inside the food library.
- Deleting a food suggestion does not delete old meal logs.

## Phase 7: Daily Notes

Build daily notes:

- Add note by date
- Edit note
- Display note on dashboard/date view

## Phase 8: Weight Logs

Build weight tracking:

- Add weight by date
- Edit weight log
- Delete weight log
- View weight history

## Phase 9: Schedule and Active Day Logic

Build logic for custom active days.

Requirements:

- Use tracking_day_reset_time to calculate active day
- Support night-shift users
- Use phone timezone by default
- Do not judge skipped day until active day ends

Example:

```text
Reset time: 4:00 AM
Active day: 4:00 AM today to 3:59 AM tomorrow
```

Night-shift example:

```text
Reset time: 2:00 PM
Active day: 2:00 PM today to 1:59 PM tomorrow
```

## Phase 10: Reminders / Notifications

Build local notification support.

Requirements:

- Reminder based on sleep time or custom time
- Reminder offset options: 2, 3, 4 hours before sleep
- Reminder tone options: normal, strict, savage
- Meal log reminder
- Weight log reminder later

## Phase 11: Streaks and Awards

Build streak tracking.

Rules:

- On-time eaten meals count.
- Backfilled logs do not repair streaks.
- Planned meals do not count until eaten.
- Skipped meals do not count.
- Empty past active days after first meal log date count as skipped logging days.

Awards can be simple in v1:

- First meal logged
- 3-day streak
- 7-day streak
- 30-day streak
- First planned meal completed

## Phase 12: Weekly Reports

Build basic reports without nutrition.

Reports should show:

- Logged days
- Skipped logging days
- Most eaten foods
- Total food weight by food name
- Planned vs eaten vs skipped meals
- Streak summary

Example:

```text
This Week:
Logged days: 5/7
Skipped days: 2
Cooked rice: 2.4kg
Chicken: 1.1kg
Eggs: 8 pieces
```

## Phase 13: Settings

Build settings screen.

Editable settings:

- Profile info
- Goal phase
- Wake time
- Sleep time
- Tracking reset time
- Night-shift mode
- Notification settings
- Reminder tone
- Food unit
- Weight unit
- Meal categories

Nothing should be permanent.

## Phase 14: Backup / Export Preparation

Build later, but prepare the structure early.

Future features:

- Export backup as JSON
- Import backup from JSON
- Google Drive backup
- Restore data
- Future JDHub cloud sync

## 6. Recommended Build Order

Recommended order:

1. Flutter project setup
2. Folder structure
3. Local database
4. Onboarding
5. Dashboard
6. Add meal
7. Food library suggestions
8. Edit/delete meal
9. Daily notes
10. Weight logs
11. Active day logic
12. Notifications
13. Streaks
14. Reports
15. Settings
16. Backup/export later

## 7. Important Development Rules

- Do not add nutrition calculation in v1.
- Do not use AI food estimation in v1.
- Do not hardcode reminder time to 8:30 PM.
- Do not assume all users follow midnight-to-midnight schedules.
- Do not count backfilled logs toward streak awards.
- Keep user settings editable.
- Use modular folders so JDHub Mobile can grow later.

## 8. Future Expansion Direction

After Meal Tracker v1, JDHub Mobile can grow into a pocket multi-tool connected to JDHub.

Possible future modules:

- Task manager
- Project manager
- Habit tracker
- Journal
- Fitness tracker
- Notifications center
- JDHub web sync
- IMS companion tools

The app structure should support this expansion from the beginning.
