---
name: sun-moon-times
description: "Looks up sunrise, sunset, solar noon, day length, golden hour, civil, nautical and astronomical twilight, moonrise, moonset, and the moon's phase for a place and date. Use when someone asks what time the sun rises or sets, when golden hour or blue hour is, how long the day is, when it gets dark, when the moon rises, what phase the moon is in, or when the next full moon or new moon falls."
---

# Sun and moon times

Give calculated sun and moon times for one place and date, in that place's own time zone.

## When to use

- "What time is sunset in Lisbon on Saturday?"
- "When does golden hour start for a shoot in Moab tomorrow?"
- "When is the next full moon?"
- "How many hours of daylight does Tromsø get on the winter solstice?"

Use `observing-plan` when the person wants a full night plan with planets, `meteor-watch` for meteor showers and `aurora-watch` for the aurora. This skill does not cover eclipses, tides, solstice or equinox instants, or prayer times.

## Settle these first

1. **Place.** `sun_times` and `moon_times` need decimal latitude and longitude. Work them out from the named place and state them. `moon_phase` needs no place.
2. **Time zone.** Pass the place's IANA zone, for example `Europe/Lisbon`. The default is `UTC`, which gives times the reader cannot use directly.
3. **Date.** `YYYY-MM-DD` in the place's own calendar. The default is today in the given time zone.

## Tools

All three are on the `sun-moon` server (Sun and Moon).

| Tool | Returns |
| --- | --- |
| `sun_times` | Sunrise, sunset, solar noon, day length, when morning golden hour ends, when evening golden hour starts, and the start and end of civil, nautical and astronomical twilight |
| `moon_times` | Moonrise, moonset, phase name and percent illuminated for a place and date |
| `moon_phase` | Phase name and percent illuminated for a date, and the next four principal phases with approximate times |

In Claude Code the full tool names follow the pattern `mcp__plugin_night-sky_sun-moon__sun_times`.

## Workflow

1. Pick the tool from the question. Sun events: `sun_times`. Moonrise or moonset: `moon_times`. Phase or "next full moon": `moon_phase`.
2. Call it with the place, date and `time_zone`.
3. For a span of dates, call once per date. For more than about a week, sample the dates that matter, such as each weekend, and say that you sampled.
4. Answer with the times as returned, the time zone, and the date written out.

## Reading the results

- **Golden hour.** The tool gives when the morning golden hour ends and when the evening one starts. The morning one begins at sunrise and the evening one ends at sunset. The server does not state the sun altitude it uses.
- **Blue hour** is not returned. The nearest returned span is civil twilight: from `Civil twilight begins` to sunrise, and from sunset to `Civil twilight ends`. Say that this is an approximation.
- **"When does it get dark?"** For everyday purposes give `Civil twilight ends`. For stargazing give `Astronomical twilight ends`. If the purpose is unclear, give both with one line each.
- **Moonrise and moonset** are the events on the requested calendar date. The moonset can come before the moonrise. The set that follows tonight's rise is on the next date's result.
- **Moon phase times** are approximate, such as `about 11:00 AM`. Give the date with confidence and the hour as approximate.
- **Illumination** can differ by a few percent between `moon_phase` and `moon_times` for the same date, because each is computed for a different moment. `moon_times` labels its figure as the 9 pm phase.

Field lists and the twilight definitions are in [references/sun-moon-fields.md](references/sun-moon-fields.md).

## Edge cases

- **Polar day and polar night.** The tool returns text such as `Sunrise and sunset: none; sun down all day`. Pass that on and still give the twilight times, which are often what the person needs.
- **Moon up or down all day.** `Moonrise: up all day` and `Moonset: none this day` are valid answers.
- **Ambiguous place.** Ask which one when the name fits more than one well known place.
- **Daylight saving changes.** The IANA zone handles them. Do not add or subtract an hour yourself.
- **A tool error.** Report it and offer to retry. Do not calculate times by hand.

## Answer shape

For a single question, one line is enough:

```text
Sunset in Flagstaff on Sun Nov 22, 2026 is 5:18 PM (America/Phoenix). Civil twilight ends at 5:46 PM.
```

For a planning question, give a short table of the events asked for, in clock order, with the time zone named once.

## Limits to state

Times are calculated for a level horizon at the given coordinates. Mountains, buildings and weather change when the sun or moon is actually seen. For a location inside a deep valley, say that the visible sunrise will be later and the visible sunset earlier than listed.

## Examples

**"Golden hour tomorrow evening in Moab?"** Call `sun_times` for 38.57, -109.55 with `America/Denver`. Give `Evening golden hour starts` and `Sunset` as the span.

**"When is the next new moon?"** Call `moon_phase` with the person's time zone. Read `New moon` from the next phases and give the date, with the hour as approximate.

**"Will the moon be up at 10 pm Saturday in Austin?"** Call `moon_times` for Saturday and, if the moonset listed is in the early morning, for Sunday too. Work out from the rise and the following set whether 10 pm falls between them.
