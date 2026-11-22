# Sun and moon fields

Every line below was read from live results of the `sun-moon` server (Sun and Moon).

## `sun_times`

Arguments: `latitude` and `longitude` are required. `date` defaults to today in the time zone. `time_zone` defaults to `UTC`.

Lines returned on an ordinary day, in this order:

| Line | Notes |
| --- | --- |
| `Sunrise`, `Sunset` | 12 hour clock in the requested zone |
| `Solar noon` | When the sun is highest. It is rarely 12:00 on the clock |
| `Day length` | Hours and minutes between sunrise and sunset |
| `Morning golden hour ends` | The morning golden hour runs from sunrise to this time |
| `Evening golden hour starts` | The evening golden hour runs from this time to sunset |
| `Civil twilight begins`, `Civil twilight ends` | Morning start and evening end |
| `Nautical twilight begins`, `Nautical twilight ends` | Morning start and evening end |
| `Astronomical twilight begins`, `Astronomical twilight ends` | Morning start and evening end. Full darkness lies outside these |

On a polar night date the sunrise and sunset line reads `none; sun down all day`, and the day length and golden hour lines are absent. Solar noon and the twilight lines are still returned.

## Twilight definitions

The server labels the stages but does not print the sun angles. These are the standard definitions used by the US Naval Observatory.

| Stage | Sun below the horizon | Everyday meaning |
| --- | --- | --- |
| Civil | 0 to 6 degrees | Outdoor activity without lights is still possible |
| Nautical | 6 to 12 degrees | The horizon is still visible at sea. Most people call it dark |
| Astronomical | 12 to 18 degrees | The sky is dark except for the faintest objects |

Evening order: sunset, civil twilight ends, nautical twilight ends, astronomical twilight ends. Morning order is the reverse.

At high latitudes in summer the later stages may not occur. Report what the tool returns.

## `moon_times`

Arguments: same as `sun_times`.

| Line | Notes |
| --- | --- |
| `Moonrise`, `Moonset` | Events on the requested calendar date. Seen at high latitude: `Moonrise: up all day` with `Moonset: none this day`. Pass on whatever wording is returned for a missing event |
| `Phase (9 pm)` | Phase name at 9 pm local time |
| `Illuminated` | Percent of the disk lit |

The moon rises about 50 minutes later each day on average, so one of the two events can skip a calendar date. In a check for the same site, the result for Nov 22 listed moonrise 3:38 PM and moonset 5:02 AM, and the result for Nov 23 listed moonset 6:12 AM. The moon that rose at 3:38 PM on the 22nd therefore set at 6:12 AM on the 23rd.

## `moon_phase`

Arguments: `date` and `time_zone`, both optional. No place is needed because the phase is the same everywhere.

Returns the phase name and percent illuminated for the date, then the next four principal phases, each with a weekday, date and an approximate clock time in the requested zone.

Phase names in order through a cycle: new moon, waxing crescent, first quarter, waxing gibbous, full moon, waning gibbous, last quarter, waning crescent. A full cycle takes about 29.5 days.

## When the moon is up, by phase

A rough guide for sanity checking, not a substitute for `moon_times`:

| Phase | Rises around | Sets around |
| --- | --- | --- |
| New moon | Sunrise | Sunset |
| First quarter | Midday | Midnight |
| Full moon | Sunset | Sunrise |
| Last quarter | Midnight | Midday |

## What the server says about itself

The server describes these as computed sun and moon times and states that requests are not stored.
