# JDHub Mobile – Feature Requirements Document

## 1. Overview

This document defines the feature requirements for JDHub Mobile v1, focused on the Meal Tracker module.

The first version should work as a practical food log and meal planner. It should not attempt to be a complete nutrition tracker yet.

## 2. Onboarding Requirements

### 2.1 Step-Based Setup

The app must use a step-based onboarding process instead of one long scrolling form.

Recommended steps:

1. Personal Info
2. Body / Goal Info
3. Meal Tracking Setup
4. Schedule / Night Shift Setup
5. Notifications / Accountability Style
6. Finish Setup

### 2.2 Personal Info

Fields:

- Name or alias
- Email optional
- Phone optional

### 2.3 Body / Goal Info

Fields:

- Age
- Height
- Height unit
- Current weight
- Weight unit
- Target weight optional
- Initial goal type

Goal types:

- Bulking / weight gain
- Cutting / weight loss
- Maintain
- General tracking

The goal type must be stored as a goal phase, not as a permanent profile value.

### 2.4 Meal Tracking Setup

Fields:

- Preferred food weight unit
- Default meal categories
- Weighing tip acknowledgement

The app should highlight this message during onboarding:

> For better consistency, weigh food after it is cooked. Example: cooked rice 250g, cooked chicken 180g.

### 2.5 Schedule / Night Shift Setup

Fields:

- Normal schedule or night-shift/unusual schedule
- Wake-up time
- Sleep time
- Tracking day reset time
- Timezone mode

The app should use the phone timezone by default. A custom timezone option can be added later.

### 2.6 Notification Setup

Fields:

- Reminder enabled/disabled
- Reminder timing
- Reminder tone

Reminder timing options:

- 2 hours before sleep
- 3 hours before sleep
- 4 hours before sleep
- Custom time
- Never

Reminder tone options:

- Normal
- Strict
- Funny / savage

## 3. Meal Log Requirements

### 3.1 Add Meal

Users must be able to add a meal for any date.

Fields:

- Log date
- Meal category
- Food name
- Amount
- Unit
- Meal status
- Logging confidence
- Notes

Future nullable fields:

- Calories
- Protein
- Carbs
- Fat
- Serving size
- Serving unit

### 3.2 Meal Status

Visible statuses:

- Planned
- Eaten
- Skipped

Internal statuses/flags:

- Auto-skipped
- Backfilled

### 3.3 Edit Meal

Users must be able to edit:

- Date
- Category
- Food name
- Amount
- Unit
- Status
- Confidence
- Notes

### 3.4 Delete Meal

Users must be able to delete a meal log.

A deleted meal should not delete the related food suggestion from the food library.

### 3.5 Duplicate Meal

Users must be able to duplicate a meal to another date.

Example:

- Duplicate breakfast to tomorrow
- Duplicate lunch to another selected date

### 3.6 Copy Day

Users must be able to copy all meals from one date to another date.

This supports meal planning.

Example:

- Copy Monday meals to Tuesday

## 4. Food Library Requirements

### 4.1 Auto-Save Food Names

When a user logs a food, the app should save the food name to the food library if it does not already exist.

The app should only save the food name, not the amount.

Correct:

- Cooked rice

Incorrect:

- 250g cooked rice

### 4.2 Recent Foods

The app should show recently used foods when adding a meal.

### 4.3 Favorite Foods

Users should be able to mark food items as favorites.

Favorite foods should appear before non-favorite foods.

### 4.4 Hide/Delete Food Suggestion

Users should be able to hide or delete a food suggestion so it does not appear in autocomplete.

This should not delete previous meal logs.

## 5. Meal Category Requirements

Default categories:

- Breakfast
- Lunch
- Dinner
- Snack
- Other

Users should be able to add custom categories later.

Examples:

- Pre-workout
- Post-workout
- Midnight meal

## 6. Daily Notes Requirements

Users should be able to add notes per date.

Examples:

- Felt weak today
- Ate late
- Workout day
- Cheat day
- Forgot to weigh lunch

## 7. Weight Log Requirements

Users should be able to log body weight by date.

Fields:

- Log date
- Weight
- Unit
- Notes

The app should support weight reminders.

## 8. Goal Phase Requirements

Users must be able to change goals over time.

A goal phase should include:

- Goal type
- Start date
- End date
- Notes

Rules:

- Only one goal phase should be active at a time.
- When the user changes goals, the old active goal should be closed with an end date.
- The new goal should start from the selected start date.

## 9. Active Day / Schedule Requirements

The app must support custom active days.

A user’s active day is calculated from the tracking reset time, not always midnight.

Example:

- Reset time: 4:00 AM
- Active day: 4:00 AM today to 3:59 AM tomorrow

Night-shift example:

- Reset time: 2:00 PM
- Active day: 2:00 PM today to 1:59 PM tomorrow

The app should only judge skipped days after the active day ends.

## 10. Reminder Requirements

Meal reminders should be based on the user’s sleep time or custom reminder setting.

The app should not hardcode a default such as 8:30 PM.

Example:

- Sleep time: 11:00 PM
- Reminder offset: 3 hours before sleep
- Reminder time: 8:00 PM

Night-shift example:

- Sleep time: 10:00 AM
- Reminder offset: 3 hours before sleep
- Reminder time: 7:00 AM

## 11. Streak and Award Requirements

The app should support streaks and simple awards.

Streak rules:

- At least one on-time eaten meal during the active day counts toward the streak.
- Planned meals do not count until marked eaten.
- Skipped meals do not count.
- Backfilled meals are allowed but do not repair streaks.
- Empty past active days after the first meal log date count as skipped logging days.

Awards should only be given for on-time logs.

## 12. Backup / Export Requirements

The app should be designed for future backup support.

Future backup features:

- Export data to JSON
- Import data from JSON
- Backup to Google Drive
- Restore from backup
- Future JDHub cloud sync

The app should protect local data during app updates. Users should be warned that uninstalling the app may remove local data unless a backup exists.
