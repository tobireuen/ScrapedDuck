# Endpoints

- Formatted: [`GET /data/events.json`](https://raw.githubusercontent.com/bigfoott/ScrapedDuck/data/events.json)
- Minimized: [`GET /data/events.min.json`](https://raw.githubusercontent.com/bigfoott/ScrapedDuck/data/events.min.json)

# Example Event Object

```
{
    "eventID": "legendaryraidhour20220601",
    "name": "Kyogre Raid Hour",
    "eventType": "raid-hour",
    "heading": "Raid Hour",
    "link": "https://www.leekduck.com/events/legendaryraidhour20220601/",
    "image": "https://www.leekduck.com/assets/img/events/raidhour.jpg",
    "start": "2022-06-01T18:00:00.000",
    "end": "2022-06-01T19:00:00.000"
}
```
# Fields

| Field           | Type     | Description
|---------------- |--------- |---------------------
| **`eventID`**   | `string` | The ID of the event. Also the last part of the event page's URL.
| **`name`**      | `string` | The name of the event.
| **`eventType`** | `string` | The type of the event. See [List of Event Types](#list-of-event-types)
| **`heading`**   | `string` | The heading for the event. Based on the event's type.
| **`link`**      | `string` | The URL to the event's page.
| **`image`**     | `string` | The header/thumbnail image for the event.
| **`start`**     | `string` | The start date of the event (Can be null). See [Note for Start/End dates](#note-for-startend-dates)
| **`end`**       | `string` | The end date of the event (Can be null). See [Note for Start/End dates](#note-for-startend-dates)

## List of Event Types

| Events/Misc.               | Research                  | Raids/Battle         | GO Rocket
|--------------------------- |-------------------------- |--------------------- |------------------------------
| `community-day`          | `research`              | `raid-day`         | `go-rocket-takeover`
| `event`                  | `timed-research`        | `raid-battles`     | `team-go-rocket`
| `live-event`             | `limited-research`      | `raid-hour`        | `giovanni-special-research`
| `pokemon-go-fest`        | `research-breakthrough` | `raid-weekend`
| `global-challenge`       | `special-research`      | `go-battle-league`
| `safari-zone`
| `ticketed-event`
| `location-specific`
| `bonus-hour`
| `pokemon-spotlight-hour`
| `potential-ultra-unlock`
| `update`

If you want to figure out what type of event a specific event on [LeekDuck.com/events](https://www.leekduck.com/events/) is, use your browser's dev tools to determine what class is setting the background color of that event. The class name is the same as the event type (except for `pokemon-go-fest` and `pokemon-spotlight-hour`, where the accented "é" is replaced with "e").

## Note for Start/End dates

The `start` and `end` fields are DateTime objects encoded in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601).

Most events in Pokemon GO occur based around a user's local timezone. However, there are also some events that happen at the same time globally.

If an event starts/ends at the same time globally, the `start` and `end` fields will have strings ending with "Z", signifying the DateTime is in UTC. Otherwise, the DateTime displayed is based on the user's local timezone.

Depending on the use case, many parsers (ex: Javascript's `Date.parse()`) will handle this automatically.
