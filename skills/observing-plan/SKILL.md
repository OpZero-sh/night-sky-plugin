---
name: observing-plan
description: "Plans a night of stargazing or planet viewing for a place and date: when it gets fully dark, which of the five naked eye planets are up, where to look, and how much the moon interferes. Use when someone asks what is visible in the sky tonight, when or where to see Venus, Jupiter, Saturn, Mars or Mercury, the best time to stargaze, whether the moon will wash out the sky, or which night this week is darkest."
---

# Observing plan

Turn a place and a date into a bounded local time window, a direction to face, and the reason for the choice.

## When to use

- "What can I see in the sky tonight from Flagstaff?"
- "When is Saturn up and which way do I look?"
- "Find a dark, moon free hour this weekend."

Use `meteor-watch` for meteor showers, `aurora-watch` for the northern or southern lights, and `sun-moon-times` for a plain sunrise, sunset, twilight or moon phase question. This skill does not cover stars, constellations, comets, satellites, eclipses, Uranus or Neptune, because the servers return none of them. Say so instead of filling the gap from memory.

## Settle these first

1. **Place.** The tools take decimal latitude and longitude. Work them out from the named place and state the coordinates you used. Ask only when the name is ambiguous, for example two towns with the same name.
2. **Time zone.** Pass the IANA zone of the observing site, for example `America/Phoenix`. The tools default to `UTC`, so a call without `time_zone` returns times the reader cannot use.
3. **Date.** Use the local evening the session starts. A night that runs past midnight still belongs to that evening's date in `sky_tonight`.
4. **Target.** A general look, one planet, or the darkest hours.

## Tools

| Server key | Tool | Use it for |
| --- | --- | --- |
| `sky` | `sky_tonight` | One night at a glance: sunset, full dark start and end, moon phase, moon free hours, and each planet's visible span and best moment |
| `sky` | `planet_positions` | Altitude, compass direction and brightness of each planet, the sun and the moon at one clock time |
| `sun-moon` | `sun_times` | Exact twilight stages when the plan depends on them |
| `sun-moon` | `moon_times` | Moonrise and moonset for a calendar date |
| `sun-moon` | `moon_phase` | The date of the next new moon when tonight is too bright |

In Claude Code the full tool names follow the pattern `mcp__plugin_night-sky_sky__sky_tonight`.

## Workflow

1. Call `sky_tonight` with `latitude`, `longitude`, `time_zone` and `date`. Read the summary line, then the darkness block, then the planets.
2. Decide the window.
   - For faint targets or general stargazing, the window is the part of full dark when the moon is down. `Moon free darkness: 7.5 of 11 hours` tells you how much exists. To place it on the clock, call `moon_times` for the evening date and for the next date, because moonset after midnight is listed under the next date.
   - For a bright planet, moonlight matters little. Use the planet's `Visible` span and `Best` time.
3. When the person names a clock time, or you need to confirm a direction, call `planet_positions` with `local_time` as 24 hour `HH:MM`. A negative altitude means the object is below the horizon at that moment.
4. To compare several nights, call `sky_tonight` once per date and compare moon free hours first, then planet placement. Hand a comparison of more than three nights or two sites to the `viewing-window` agent.
5. Write the answer in the shape below.

## Reading the results

- **Full dark** is the end of astronomical twilight. Planets and the moon are visible well before it. Faint stars and the Milky Way are not.
- **Magnitude** runs backwards: lower is brighter, and negative values are the brightest.
- **Angle to the sun** under about 20 degrees means the planet sits low in twilight for a short time. Tell the reader they need a clear, flat horizon in that direction.
- **Times after midnight** in a `sky_tonight` result fall on the next calendar date. Write that date out.
- Positions are approximate, good to about a degree. That is enough to point a person, not a telescope mount.

Field by field notes are in [references/output-fields.md](references/output-fields.md). Twilight stages, moonlight and high latitude cases are in [references/darkness-and-moonlight.md](references/darkness-and-moonlight.md).

## Edge cases

- **No full darkness.** At high latitudes in summer the result reads `Full dark starts: none` and `Stargazing: No full darkness tonight`. Report that plainly. Bright planets may still be visible in twilight if the planet list shows them.
- **No planets listed.** The summary says `no bright planets well placed`. Do not add planets from memory.
- **Bright moon all night.** `Moon free darkness: 0 of 11 hours` rules out faint targets. Offer the nearest darker date, using `moon_phase` from the `sun-moon` server to find the next new moon.
- **A tool error or timeout.** Say which lookup failed, give what the other calls returned, and offer to retry. Do not estimate rise or set times yourself.

## Answer shape

Lead with the window, then the support.

```text
Best window: 6:45 PM to 1:20 AM, Wed Dec 2 into Thu Dec 3 (America/Phoenix)
Look for: Saturn, 55 degrees up in the south around 8:10 PM, in view until 1:20 AM
Moon: waning crescent, 31% lit, 7.5 of the 11 dark hours are moon free
Why: full dark starts at 6:45 PM and Saturn drops out of view at 1:20 AM
Not checked: cloud cover, light pollution, terrain
```

Name the coordinates and the time zone once. Keep every time in the observing site's zone.

## Limits to state

The times and positions are calculated, not observed. The servers know nothing about cloud, haze, smoke, light pollution or the local horizon. Point the person to a local weather forecast for the sky conditions.

## Examples

**"What planets can I see tonight in Flagstaff?"** Call `sky_tonight` for 35.20, -111.65 with `America/Phoenix`. List each planet with its visible span, best time, altitude and direction. Flag the ones that appear only before dawn on the next date.

**"Where is Jupiter at 10 pm?"** Call `planet_positions` with `local_time: "22:00"`. If the altitude is negative, say Jupiter has not risen yet and give its `Visible` span from `sky_tonight`.

**"Which night this weekend is best for the Milky Way?"** Call `sky_tonight` for each night and compare moon free darkness. Say that the servers do not return Milky Way position, so the answer covers darkness only.
