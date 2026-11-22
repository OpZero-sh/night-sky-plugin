---
name: aurora-watch
description: "Checks the chance of seeing the aurora from a place over the next three days using the NOAA planetary Kp forecast, then lines the forecast up with local darkness. Use when someone asks about the northern lights, southern lights, aurora borealis or australis, tonight's Kp index, a geomagnetic storm, a G1 to G5 storm watch, or NOAA space weather alerts."
---

# Aurora watch

Answer "can I see the aurora from here, and when should I look" with the forecast activity, the activity this site needs, and the hours that are actually dark.

## When to use

- "Any chance of northern lights near Fairbanks this weekend?"
- "What is the Kp forecast for tonight?"
- "Is there a geomagnetic storm watch right now?"

Use `observing-plan` for planets and stargazing. This skill covers the next three days only. It cannot say anything about a trip weeks away beyond darkness and moon conditions.

## Tools

| Server key | Tool | Use it for |
| --- | --- | --- |
| `aurora` | `aurora_outlook` | A per day outlook for one latitude and longitude, with the site's geomagnetic latitude and the Kp it needs |
| `aurora` | `kp_forecast` | Forecast Kp in three hour UTC steps for 1 to 3 days, plus the latest observed value |
| `aurora` | `space_weather_alerts` | The latest NOAA alert, watch and warning messages, 1 to 15 of them |
| `sun-moon` | `sun_times` | Whether and when the site is dark |
| `sun-moon` | `moon_times` | Moonlight during the window |

In Claude Code the full tool names follow the pattern `mcp__plugin_night-sky_aurora__aurora_outlook`.

## Workflow

1. Work out the site's latitude, longitude and IANA time zone. State the coordinates you used.
2. Call `aurora_outlook` with `latitude` and `longitude`. Read three things: the geomagnetic latitude, the line `Needed for an overhead aurora here: about Kp N`, and the wording for each day.
3. Call `kp_forecast` with `days: 3`. Find the three hour steps where the forecast Kp is highest. All times are UTC.
4. Convert those steps to the site's local date and time. A UTC step often lands on the previous or next local date. Write the local date out.
5. Call `sun_times` for each candidate local date with the site's `time_zone`. Keep only the steps that fall after nautical twilight ends and before it begins again. In high latitude summer there may be none.
6. Call `space_weather_alerts` only when the person asks about alerts or storms, or when the forecast reaches Kp 5 or more. Check each message's validity times against the current time before calling it active.
7. Answer in the shape below.

## Reading the results

- **Kp** runs from 0 to 9 in thirds, so 2.3 and 3.7 are normal values. Kp 5 is the threshold for a G1 geomagnetic storm.
- **Needed Kp** is a rule of thumb for an aurora overhead at that geomagnetic latitude. A value above 9 is off the scale: an overhead aurora is not expected there at any forecast level. Report it that way, not as a target.
- **Outlook wording** seen from the server, from best to worst: `Likely overhead or high in the sky if dark and clear`, `Unlikely; only a faint glow on the horizon in a strong burst`, `Very unlikely at this activity level`. Quote the wording returned.
- **Day labels** in both tools are UTC dates. The first and last day can be partial.
- **Latest observed Kp** is a measurement with its own UTC time. Everything after it is forecast.

The Kp scale, what it does and does not predict, and how to read alert messages are in [references/kp-and-alerts.md](references/kp-and-alerts.md).

## Edge cases

- **Date beyond the forecast.** Say the Kp forecast covers about three days. Offer what can be calculated: darkness from `sun_times` and moonlight from `moon_phase`, both on the `sun-moon` server.
- **No darkness.** If `sun_times` shows no nautical or astronomical darkness, say the aurora cannot be seen from that site on that date whatever the Kp.
- **Low latitude site.** When the needed Kp is far above the forecast, say plainly that a sighting is very unlikely. Do not soften it into a maybe.
- **Old alerts.** `space_weather_alerts` returns the most recent messages even when they have expired. Compare `Valid Until` or `Valid To` with the current UTC time and label expired ones as past.
- **A tool error.** Say the NOAA forecast could not be read just now and give the darkness times alone. Do not guess a Kp.

## Answer shape

```text
Site: Fairbanks, Alaska (64.84, -147.72), geomagnetic latitude 66
Needs: about Kp 1 for an overhead aurora
Forecast peak: Kp 4.0 around 12:00 UTC Mon Nov 23, which is 3:00 AM Mon Nov 23 in America/Anchorage
Dark then: yes or no, from the sun_times result
Outlook: "Likely overhead or high in the sky if dark and clear"
Unknown: cloud cover. Forecast, not a guarantee.
Source: NOAA SWPC planetary Kp forecast, latest observed Kp 0.7 at 18:00 UTC Nov 22
```

Give one best window and one fallback. Keep UTC beside the local time for the forecast steps so the reader can check them.

## Limits to state

- The outlook is a rule of thumb from planetary Kp. Kp is a planet wide three hour index. It does not say what the sky above one town will do in a given minute.
- Cloud, haze, moonlight and city light are not in the data.
- Forecasts change. The server describes its outlook as not a guarantee.
- For decisions about power, radio, satellite or aviation operations, send the person to the NOAA Space Weather Prediction Center at https://www.swpc.noaa.gov/. This skill is for sky watching.

## Examples

**"Northern lights tonight in Minneapolis?"** `aurora_outlook` for 44.98, -93.27 returns geomagnetic latitude 54 and a needed Kp of about 7. If the forecast peak is 4, quote the outlook wording and say a sighting is unlikely, with a faint glow low in the north the most to hope for.

**"What is the Kp forecast?"** Call `kp_forecast`. Give the latest observed value with its time, then the peak step for each UTC day. Add local times only if a place is known.

**"Which of the next two nights is better near Fairbanks?"** Run the full workflow for both nights and compare peak Kp during dark hours. Hand a comparison of several sites or many nights to the `viewing-window` agent.
