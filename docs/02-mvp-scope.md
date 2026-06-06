# JDHub Mobile – MVP Scope Document

## 1. MVP Name

JDHub Mobile v1 – Meal Tracker Module

## 2. MVP Goal

The MVP goal is to build a local-first Flutter app module that helps users plan and log meals consistently without relying on inaccurate nutrition estimates.

The MVP is focused on:

- Meal planning
- Meal logging
- Food quantity tracking
- Weight logging
- Daily notes
- Schedule-aware reminders
- Streaks and consistency
- Local data safety

## 3. Included in Version 1

### 3.1 First-Time Setup

The app should use a step-based onboarding flow so users do not need to scroll through one long form.

Steps:

1. Personal Info
2. Body / Goal Info
3. Meal Tracking Setup
4. Schedule / Night Shift Setup
5. Notifications / Accountability Style
6. Finish Setup

The setup should be editable later. Nothing should be permanent.

A skip onboarding option may be added for development/testing. If skipped, the app should create a safe default local profile.

### 3.2 Date-Based Meal Logs

Users can add meals for any date, including:

- Today
- Yesterday
- Last week
- Two weeks ago
- Future dates
- Custom selected dates

This allows users to backfill meals they forgot to log.

### 3.3 Meal Planning

Users can create planned meals for future dates.

Meal status options:

- Planned
- Eaten
- Skipped

Internally, the app may also track:

- Auto-skipped
- Backfilled

### 3.4 Food Quantity Tracking

Version 1 should focus on practical quantity tracking, not nutrition tracking.

Default tracking should encourage:

- Grams
- Kilograms when grams exceed 1000g

Examples:

- Cooked rice – 250g
- Cooked chicken – 180g
- Cooked rice this week – 2.4kg

The app should encourage users to weigh food after cooking for consistency.

### 3.5 Food Library

When a user logs a food, the food name should be saved to a local food library.

The app should save the food name only, not the amount.

Example:

- Save: Cooked rice
- Do not save: 250g cooked rice

Food library features:

- Recent foods
- Favorite foods
- Hide/delete food suggestions
- Usage count
- Last used date

### 3.6 Meal Categories

Default meal categories:

- Breakfast
- Lunch
- Dinner
- Snack
- Other

The user should be able to add custom categories later, such as:

- Pre-workout
- Post-workout
- Midnight meal

### 3.7 Food Preparation State

The app should support practical food naming and preparation state.

Examples:

- Cooked rice
- Uncooked rice
- Cooked chicken
- Raw chicken
- Boiled egg
- Fried egg

For v1, this can be handled through the food name field. A separate preparation state field can be added later.

### 3.8 Logging Confidence

Users should be able to mark how confident they are with the logged amount.

Options:

- Exact
- Estimated
- Unknown

This prevents the user from feeling forced to be perfect while still keeping logs useful.

### 3.9 Daily Notes

Users can add notes per date.

Examples:

- Felt weak today
- Ate late
- Workout day
- Cheat day
- Forgot to weigh lunch

### 3.10 Weight Logs

Users can log body weight by date.

Weight logs should support:

- Any date
- kg/lb units
- Notes

Weight reminder frequency should be configurable.

### 3.11 Goal Phases

Goal type should be adjustable over time using goal phases.

Examples:

- Bulking for 4 months
- Cutting / weight loss for 6 months
- Maintenance after that

Goal phases should have:

- Goal type
- Start date
- End date
- Notes

The current goal is the active goal phase.

### 3.12 Custom Active Day Schedule

The app should not assume that every user’s day is midnight to midnight.

Users should be able to set:

- Wake-up time
- Sleep time
- Tracking day reset time
- Night-shift / unusual schedule mode

The active day should be based on the tracking reset time.

Example normal schedule:

- Reset: 4:00 AM
- Active day: 4:00 AM today to 3:59 AM tomorrow

Example night-shift schedule:

- Reset: 2:00 PM
- Active day: 2:00 PM today to 1:59 PM tomorrow

### 3.13 Notifications

Notifications should not be hardcoded to a fixed time such as 8:30 PM.

Instead, reminders should be based on the user’s sleep time.

Options:

- 2 hours before sleep
- 3 hours before sleep
- 4 hours before sleep
- Custom time
- Never

Notification tones:

- Normal
- Strict
- Funny / savage

### 3.14 Streaks and Awards

The app should support streaks and simple awards.

Streaks should only count on-time logs.

Backfilled logs should save correctly but should not repair streaks.

### 3.15 Backup / Export Planning

The MVP should be built with future backup and export in mind.

Version 1 may start with local storage only, but the app should later support:

- Export backup as JSON
- Import backup from JSON
- Google Drive backup
- Future JDHub cloud sync

## 4. Not Included in Version 1

The following should not be included in v1:

- Calorie calculation
- Protein calculation
- Carbohydrate calculation
- Fat calculation
- AI food estimation
- External nutrition database
- Barcode scanning
- Automatic nutrition guessing
- Automatic cup-to-gram conversion
- Full cloud sync

Nutrition-related columns may exist in the data model as nullable future fields, but they should not be required in the UI.

## 5. MVP Success Criteria

The MVP is successful if the user can:

- Complete onboarding
- Add meals by date
- Plan future meals
- Mark meals as eaten or skipped
- Backfill old meals
- Use recent and favorite foods
- Track food quantity by weight
- Add daily notes
- Log body weight
- Receive schedule-aware reminders
- See basic streaks and weekly reports

## 6. Main MVP Principle

The first version should be simple, honest, and useful.

It should help users build the habit of logging meals first. Nutrition calculations can come later when the app has a more accurate and reliable data source.
