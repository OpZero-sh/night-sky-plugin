# Kp, the outlook and alert messages

## Contents

- The Kp index
- What Kp does not tell you
- NOAA G scale
- Reading `kp_forecast`
- Reading `aurora_outlook`
- Reading `space_weather_alerts`
- Where to look and when

## The Kp index

Kp is the planetary K index, a 0 to 9 measure of how disturbed the Earth's magnetic field is. It is built from ground magnetometer readings around the world and is reported for three hour intervals. Values come in thirds, which the server prints as decimals such as 1.3, 1.7 and 2.3.

Higher Kp pushes the auroral oval toward the equator, so more places can see it.

## What Kp does not tell you

- **Not local.** Kp is one number for the whole planet. It says nothing about cloud or the sky over one site.
- **Not instantaneous.** Each value summarizes three hours. Bright displays often come in bursts of minutes inside a quiet looking interval, and a high Kp interval can still have dull stretches.
- **Not a visibility score.** The aurora also needs a dark sky. High latitude summer has none.
- **Not certain.** The values after the latest observation are forecasts. Skill falls with lead time, so the third day is the least reliable.

## NOAA G scale

NOAA rates geomagnetic storms from G1 to G5 by Kp.

| Kp | G level | NOAA name |
| --- | --- | --- |
| 5 | G1 | Minor |
| 6 | G2 | Moderate |
| 7 | G3 | Strong |
| 8 | G4 | Severe |
| 9 | G5 | Extreme |

Below Kp 5 the server labels a day `below storm level`.

## Reading `kp_forecast`

Argument: `days`, 1 to 3, default 3.

- The header gives `Latest observed Kp` with a UTC date and time. That is the newest measurement the server has. The server does not state how often it refreshes, so quote this time as the data's age.
- Each day line is a UTC date with its peak Kp and storm label, followed by clock times and values in three hour steps: 00:00, 03:00, 06:00 and so on.
- The server does not say which end of the interval a clock time marks. NOAA publishes the same forecast as intervals such as 00 to 03 UT. Treat a labeled time as the start of a three hour interval and give the window with that width.
- The first day shows only the steps still ahead. A final day may show a single step.

Converting to local time: subtract or add the site's UTC offset for that date, then recheck the calendar date. Example: 12:00 UTC on Nov 23 is 3:00 AM on Nov 23 in Alaska (UTC minus 9) and 9:00 PM on Nov 23 in Tokyo (UTC plus 9). 03:00 UTC on Nov 23 is 6:00 PM on Nov 22 in Alaska.

## Reading `aurora_outlook`

Arguments: `latitude`, `longitude`.

- The header gives the site's **geomagnetic latitude**. The auroral oval is centered on the geomagnetic poles, not the geographic ones, so two towns at the same geographic latitude can have different chances.
- `Needed for an overhead aurora here: about Kp N` is the server's rule of thumb. Values seen: about Kp 1 at geomagnetic latitude 66, about Kp 7 at 54, about Kp 12 at 43. Anything above 9 cannot occur on the Kp scale.
- Each day line is a UTC date with the peak forecast Kp and one sentence of outlook wording.
- The footer reads `A rule of thumb from the NOAA Kp forecast; darkness and clear skies are also needed.`

The outlook compares the day's peak Kp with the needed Kp. It does not check whether that peak falls in darkness at the site. Do that step yourself with `kp_forecast` and `sun_times`.

## Reading `space_weather_alerts`

Argument: `limit`, 1 to 15, default 5.

The tool returns the latest NOAA Space Weather Prediction Center messages, newest first, each with a title, an issue time in UTC and the message text.

| Message type | Meaning in NOAA usage |
| --- | --- |
| WATCH | Conditions are favorable for activity in the coming days |
| WARNING | Activity is expected soon. Carries `Valid From` and `Valid To` |
| EXTENDED WARNING | An earlier warning now runs longer. Carries `Now Valid Until` |
| ALERT | A threshold has been reached. Carries `Threshold Reached` |
| SUMMARY | A report after an event |

Things to check before repeating a message:

- **Is it still in force?** The list is by recency, not by status. In one check the three latest messages were three days old and all expired. Compare the validity times with the current UTC time.
- **Is it about the aurora?** The feed carries every kind of space weather message. Geomagnetic K index and G scale messages bear on the aurora. Radio blackout (R scale), solar radiation storm (S scale) and electron flux messages do not.
- **Which scale level?** The text names it, for example `NOAA Scale: G1 - Minor`.

## Where to look and when

- From sites well below the needed Kp, the aurora sits low toward the pole: north in the Northern Hemisphere, south in the Southern Hemisphere. A clear, dark horizon in that direction matters most.
- From sites at or above the needed Kp, it can be overhead or anywhere in the sky.
- Displays are possible at any dark hour. Give the forecast peak that falls in darkness and say that activity often comes in bursts.
- Phone cameras on a night setting pick up color the eye cannot. Worth a mention for faint displays.

## Official source

NOAA Space Weather Prediction Center: https://www.swpc.noaa.gov/. Send people there for the current forecast discussion and for anything that affects operations or safety.
