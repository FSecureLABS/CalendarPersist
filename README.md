# CalendarPersist

JXA script to allow programmatic persistence via macOS Calendar.app alerts.

Fore full information read: https://labs.f-secure.com/blog/operationalising-calendar-alerts-persistence-on-macos

## Usage

Import the script in Mythic's Apfell payload using the following commands.

```js
jsimport
jsimport_call
```

Once imported, all of the functions within the script can be called. 

**List Calendars**

```js
list_calendars()
```

The `list_calendars` command will return a list of calendars configured within the target's Calendar application. The calendar type (https://developer.apple.com/documentation/eventkit/ekcalendartype) and UID is returned also.

**List Events**

```js
list_calendar_events(numberOfHours)
```

`list_calendar_events` will return events across all calendars between the current time and the number of hours specified as an argument. 

- *numberOfHours*: Number of hours in the future that form the time window for returned events.

For example, `list_calendar_events(24)` will return all of the events in the next 24 hours.

**Persist via Calendar Event**

```js
persist_calalert(title, target, delay, frequency, interval, end, uid)
```

This command creates new events and inserts them into the calendar with an alert that executes an application.

- *title*: Title of the created event(s)
- *target*: Full path to the application to execute as persistence.
- *delay*: Number of seconds in the future to create the first event.
- *frequency*: String representing the frequency of the calendar series. (daily, weekly, monthly, yearly)
- *interval*: Units of time between each event in the series. For example, if 2 and weekly, the events will be every second week.
- *end*: Number of events to insert before ending the series.
- *uid*: UID of the calendar to insert the event.

**Persist via Backdooring Existing Alert**

```js
persist_calalert_existing(uid, target)
```

This command adds a procedure alarm to an existing calendar event.

- *uid*: UID of the target event.
- *target*: Full path to the application to execute as persistence.

**Hide Calendar**

```js
hide_calendar(uid)
```

This function "unchecks" the show calendar button within Calendar.app. Whilst it can be trivially re-enabled, this might help hide the created events in some situations.

- *uid*: UID of the calendar to be hidden.
