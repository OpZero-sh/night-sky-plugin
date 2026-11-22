---
name: use-aurora
description: "Checks the aurora outlook for a place and the NOAA planetary Kp forecast for the next three days with Aurora Forecast. Use when someone asks about the northern or southern lights, the Kp index, geomagnetic storms, or space weather alerts."
---

# Aurora Forecast

1. Work out the latitude and longitude of the viewing site.
2. Call `aurora_outlook`. Read the geomagnetic latitude, the Kp needed for an overhead aurora there, and the wording for each UTC day. A needed Kp above 9 is off the scale, which means an overhead aurora is not expected there.
3. Call `kp_forecast` for the three hour steps. All times are UTC. Convert the highest steps to the site's local date and time, and write the local date out.
4. Call `space_weather_alerts` only for a question about alerts or storms. The list is by recency, so compare each message's validity times with the current time before calling it active.

Reading results:

- Kp runs 0 to 9 in thirds. Kp 5 is a G1 storm, Kp 9 is G5.
- `Latest observed Kp` is a measurement with its own UTC time. Later values are forecasts.
- The outlook is a rule of thumb. It does not check darkness, cloud or moonlight at the site. Say that those are unknown unless the person supplies them.
- The forecast covers about three days. Say so for any later date.

Answer with the site, the needed Kp, the forecast peak with UTC and local time, the outlook wording as returned, and the source: NOAA Space Weather Prediction Center.
