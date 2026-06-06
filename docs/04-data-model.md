# JDHub Mobile – Data Model Document

## 1. Overview

JDHub Mobile v1 should be local-first. The recommended local database is SQLite.

The data model should support the Meal Tracker module now, while leaving room for future JDHub modules.

The first version will not calculate nutrition, but nutrition-related columns may be included as nullable future fields.

## 2. Main Tables

Recommended tables:

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

## 3. user_profile

Stores basic local user information.

Fields:

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
name_or_alias TEXT NOT NULL
email TEXT NULL
phone TEXT NULL
age INTEGER NULL
height REAL NULL
height_unit TEXT DEFAULT 'cm'
current_weight REAL NULL
weight_unit TEXT DEFAULT 'kg'
first_meal_log_date TEXT NULL
onboarding_completed INTEGER DEFAULT 0
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Notes:

- Goal type should not be stored permanently here.
- Goal type belongs in goal_phases.
- first_meal_log_date is used to start skipped-day tracking.

## 4. user_settings

Stores editable app-wide user settings.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
preferred_food_unit TEXT DEFAULT 'g'
timezone_mode TEXT DEFAULT 'phone'
timezone_name TEXT NULL
wake_time TEXT NULL
sleep_time TEXT NULL
tracking_day_reset_time TEXT DEFAULT '04:00'
is_night_shift INTEGER DEFAULT 0
has_seen_weighing_tip INTEGER DEFAULT 0
weighing_tip_seen_count INTEGER DEFAULT 0
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Notes:

- timezone_mode can be `phone` or `custom` later.
- tracking_day_reset_time controls the user’s active day.

## 5. goal_phases

Stores goal history over time.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
goal_type TEXT NOT NULL
start_date TEXT NOT NULL
end_date TEXT NULL
notes TEXT NULL
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Goal types:

- bulk
- cut
- maintain
- general

Rules:

- Only one active goal phase should exist at a time.
- The active goal has end_date as NULL.
- When changing goals, close the old active goal and create a new one.

## 6. meal_logs

Stores individual meal/food entries.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
log_date TEXT NOT NULL
active_day_date TEXT NOT NULL
meal_category_id INTEGER NULL
meal_category_name TEXT NOT NULL
food_name TEXT NOT NULL
amount REAL NULL
unit TEXT DEFAULT 'g'
status TEXT DEFAULT 'eaten'
confidence TEXT DEFAULT 'estimated'
notes TEXT NULL
logged_at TEXT NOT NULL
is_backfilled INTEGER DEFAULT 0
is_auto_skipped INTEGER DEFAULT 0

-- Future nutrition fields, nullable for now
calories REAL NULL
protein REAL NULL
carbs REAL NULL
fat REAL NULL
serving_size REAL NULL
serving_unit TEXT NULL

created_at TEXT NOT NULL
updated_at TEXT NOT NULL
deleted_at TEXT NULL
```

Visible status options:

- planned
- eaten
- skipped

Internal flags:

- is_backfilled
- is_auto_skipped

Confidence options:

- exact
- estimated
- unknown

Notes:

- active_day_date is the app’s schedule-aware day, based on tracking_day_reset_time.
- log_date is the selected calendar date.
- logged_at is the actual timestamp when the entry was created.

## 7. food_library

Stores remembered food names for autocomplete and suggestions.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
food_name TEXT NOT NULL
preferred_unit TEXT DEFAULT 'g'
is_favorite INTEGER DEFAULT 0
usage_count INTEGER DEFAULT 0
last_used_at TEXT NULL
is_hidden INTEGER DEFAULT 0
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Rules:

- Save food name only.
- Do not save the amount inside the food name.
- Hiding/deleting a food suggestion should not delete old meal logs.

## 8. meal_categories

Stores default and custom meal categories.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NULL
name TEXT NOT NULL
is_default INTEGER DEFAULT 0
sort_order INTEGER DEFAULT 0
is_hidden INTEGER DEFAULT 0
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Default categories:

- Breakfast
- Lunch
- Dinner
- Snack
- Other

Future custom examples:

- Pre-workout
- Post-workout
- Midnight meal

## 9. daily_notes

Stores notes per active date.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
log_date TEXT NOT NULL
active_day_date TEXT NOT NULL
note TEXT NOT NULL
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Examples:

- Felt weak today
- Ate late
- Workout day
- Cheat day

## 10. weight_logs

Stores body weight logs.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
log_date TEXT NOT NULL
weight REAL NOT NULL
unit TEXT DEFAULT 'kg'
notes TEXT NULL
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
deleted_at TEXT NULL
```

## 11. reminder_settings

Stores local reminder preferences.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
reminder_type TEXT NOT NULL
is_enabled INTEGER DEFAULT 1
frequency TEXT NULL
reminder_time TEXT NULL
offset_hours_before_sleep INTEGER NULL
tone TEXT DEFAULT 'normal'
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Reminder types:

- meal_log
- weight_log
- backup

Tone options:

- normal
- strict
- savage

## 12. streak_history

Stores streak and award-related tracking.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
active_day_date TEXT NOT NULL
has_on_time_eaten_meal INTEGER DEFAULT 0
has_backfilled_log INTEGER DEFAULT 0
is_skipped_day INTEGER DEFAULT 0
streak_counted INTEGER DEFAULT 0
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Rules:

- On-time eaten meal counts.
- Backfilled meal does not repair streak.
- Planned meal does not count until eaten.
- Skipped meal does not count.

## 13. backup_metadata

Stores information about app backups.

```sql
id INTEGER PRIMARY KEY AUTOINCREMENT
user_id INTEGER NOT NULL
last_exported_at TEXT NULL
last_imported_at TEXT NULL
last_backup_location TEXT NULL
backup_version TEXT NULL
created_at TEXT NOT NULL
updated_at TEXT NOT NULL
```

Future backup locations:

- Local file
- Google Drive
- JDHub cloud

## 14. Future Nutrition Fields

The following fields are kept nullable for future use:

- calories
- protein
- carbs
- fat
- serving_size
- serving_unit

These fields should not be required in v1 forms.

## 15. Data Protection Notes

The app should be designed so local data survives normal app updates.

Users should be warned that uninstalling the app may remove local data unless they export or back up their data.

Future restore/import should support JSON backup files.
