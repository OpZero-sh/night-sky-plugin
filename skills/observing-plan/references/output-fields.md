# Output fields: `sky_tonight` and `planet_positions`

Every line below was read from live results of the `sky` server (Night Sky Tonight). Quote values as returned. Do not add precision the tools do not give.

## `sky_tonight`

Arguments: `latitude` and `longitude` are required. `date` is the evening as `YYYY-MM-DD` and defaults to today in the time zone. `time_zone` defaults to `UTC`.

| Line | Meaning | Notes |
| --- | --- | --- |
| Summary line | Planets visible, moon illumination, a stargazing rating | Ratings seen: `good`, `poor, the moon is up most of the dark hours`, `no full darkness tonight` |
| `Sunset` | Local sunset on the evening date | `none` when the sun does not set |
| `Full dark starts` | End of evening astronomical twilight | Matches `Astronomical twilight ends` from `sun_times` |
| `Full dark ends` | Start of morning astronomical twilight | Falls on the next calendar date |
| `Moon` | Phase name and percent lit | |
| `Moon free darkness` | Hours of full dark with the moon down, out of the total dark hours | `0 of 0 hours` when there is no full darkness |
| `Stargazing` | The rating in words | Based on darkness and moonlight only |
| Planet heading | Planet name, magnitude, and a `Visible` span in local time | A span such as `12:40 AM to 6:40 AM` belongs to the morning after the evening date |
| `Best` | The best moment in that span, with altitude in degrees and a compass direction | |
| `Angle to the sun` | Angular separation between the planet and the sun | Small values mean a short, low appearance in twilight |

The footer names the time zone used and repeats that lower magnitude is brighter.

A planet missing from the list is not well placed that night. The tool lists only Mercury, Venus, Mars, Jupiter and Saturn.

## `planet_positions`

Arguments: `latitude` and `longitude` are required. `date` defaults to today. `local_time` is 24 hour `HH:MM` and defaults to `21:00`. `time_zone` defaults to `UTC`, so a call without it reads `21:00` as UTC.

| Line | Meaning | Notes |
| --- | --- | --- |
| `Sun altitude` | Degrees above the horizon, negative when below | Comes with a label such as `fully dark` |
| `Moon` | Altitude, compass direction, percent lit | |
| `Altitude` | Degrees above the horizon for each planet | Negative means below the horizon. All five planets are always listed |
| `Direction` | Compass point and azimuth in degrees | Azimuth counts clockwise from north: 90 is east, 180 south, 270 west |
| `Magnitude` | Apparent brightness | Lower is brighter |
| `Angle to the sun` | Same quantity as in `sky_tonight` | |
| `RA and Dec` | Right ascension in hours and declination in degrees | Only useful to someone with a star chart or a mount. Leave it out unless asked |

The footer reads `Positions are approximate, to about a degree.`

## Turning numbers into directions

- Altitude 0 is the horizon and 90 is straight overhead. A fist at arm's length covers roughly 10 degrees.
- Under about 10 degrees an object is easily hidden by trees, buildings or hills. Say that a clear horizon is needed.
- Give the compass point first and the azimuth only if the person wants numbers.

## What the server says about itself

The server describes its positions as approximate, good to about a degree, and fine for naked eye viewing. It also states that requests are not stored.
