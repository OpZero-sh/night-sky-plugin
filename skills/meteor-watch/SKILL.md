---
name: meteor-watch
description: "Finds the next major meteor shower and plans when to watch it from a given place: peak date, the ideal hourly rate, how bright the moon is at the peak, and the dark, moon free hours on that night. Use when someone asks when the next meteor shower is, about the Perseids, Geminids, Leonids or another named shower, about shooting stars, or which shower this year has the darkest sky."
---

# Meteor watch

List the major annual showers, then turn one peak date into a watching window for a real place.

## When to use

- "When is the next meteor shower?"
- "Are the Geminids worth staying up for this year?"
- "What time should we go out for the Perseids near Bend, Oregon?"

Use `observing-plan` for planets and general stargazing. This skill covers the ten major annual showers the server lists. It has no data on minor showers, outbursts, fireballs or a meteor someone just saw.

## Tools

| Server key | Tool | Use it for |
| --- | --- | --- |
| `sky` | `meteor_showers` | Shower names, peak dates, ideal hourly rate, radiant constellation, moon brightness at the peak |
| `sun-moon` | `sun_times` | When astronomical twilight ends and begins on the peak night |
| `sun-moon` | `moon_times` | Moonrise and moonset around the peak night |
| `sky` | `sky_tonight` | A quick check of moon free dark hours for the peak night |

In Claude Code the full tool names follow the pattern `mcp__plugin_night-sky_sky__meteor_showers`.

## Workflow

1. Call `meteor_showers`.
   - With no `year` the list starts at the next upcoming peak and runs into the following year.
   - Pass `year` (1900 to 2050) for a specific year, listed January to December.
   - Pass `latitude` when you know the observing site.
2. Pick the shower. For "the next one", take the first entry. For "the best one this year", weigh the ideal rate against the moon note. A strong shower under a bright moon often shows fewer meteors than a modest one under a dark sky.
3. If the person gave a place, plan the night. Work out latitude, longitude and the IANA time zone, then:
   - Call `sky_tonight` for the peak date to get full dark start, full dark end and moon free hours.
   - If the moon is up for part of the night, call `moon_times` for the peak date and the next date to place the moon free hours on the clock.
4. Choose the window: full darkness, moon down, and as late as that allows. The server notes that best viewing is after midnight.
5. Give the window, the direction advice, and an honest rate.

## Reading the results

- **Peak date** is given as `peak around` a date, and the server warns it can shift by a day from year to year. Suggest the nights on either side as well.
- **Hourly rate** is `Up to about N per hour under ideal dark skies`. That is a ceiling for a perfect sky with the radiant overhead. Under suburban skies or moonlight expect far fewer. Never promise the listed number.
- **Moon at peak** comes with one of three notes: `dark skies`, `some moonlight`, or `bright moon washes out faint meteors`.
- **Radiant** is the constellation the meteors appear to stream from. Meteors can appear anywhere in the sky, so advise looking at the darkest open part of the sky, not straight at the radiant.

Shower by shower notes and hemisphere guidance are in [references/shower-notes.md](references/shower-notes.md).

## Edge cases

- **Southern Hemisphere sites.** Several showers on the list have far northern radiants. In test calls the result carried no latitude note even for far southern latitudes, so do not treat a missing note as confirmation. Check the hemisphere guidance in the reference file and say when a shower is poorly placed.
- **No full darkness on the peak night.** High latitude summer nights can rule a shower out. `sky_tonight` reports `No full darkness tonight`. Say so.
- **A shower not on the list.** Say the server covers only the major annual showers and do not supply dates from memory as if they came from the tool.
- **Peak falls in daylight for the site.** The tool gives a date, not an hour. Recommend the night before and the night of the listed date.

## Answer shape

```text
Shower: Geminids, peak around Mon Dec 14, 2026
Ideal rate: up to about 150 per hour under perfect dark skies; expect fewer
Moon: 23% lit at the peak, dark skies
Window at your site: full dark from <time>; best after midnight until <time> (<IANA time zone>)
Where to look: the darkest open part of the sky; the radiant is in Gemini
Not checked: cloud cover and local light pollution
```

For a list request, give a short table of shower, peak date, ideal rate and moon note, then recommend one.

## Limits to state

Peak dates and rates come from a fixed list of annual showers held by the server, not from a live forecast. Actual counts depend on sky darkness, radiant height, and weather. The servers do not know about cloud.

## Examples

**"When is the next meteor shower?"** Call `meteor_showers` with no arguments. Report the first entry with its peak date, ideal rate and moon note, and mention the next one if the first has a bright moon.

**"Plan the Perseids for us near Bend, Oregon."** Call `meteor_showers` for the year, read the Perseids peak date, then call `sky_tonight` for 44.06, -121.31 with `America/Los_Angeles` on that date. Give the dark, moon free span and suggest the hours after midnight.

**"Which shower next year has the least moonlight?"** Call `meteor_showers` with that `year`. Rank by the moon note first and the ideal rate second.
