---
name: observing-plan
description: "Plan stargazing, meteor watching, moon viewing, or aurora viewing for a place and date using local darkness and celestial positions."
---

# Night Sky

Establish the observing date, approximate coordinates, IANA time zone, and target. Use the local evening as the starting date and spell out the calendar date when a window crosses midnight.

- For a night overview, use `sky_tonight`. For a specific moment, use `planet_positions` with `local_time`; list altitude, compass direction, and magnitude for the requested target. A low object needs an unobstructed horizon.
- Use `sun_times` for twilight and `moon_times` for moonrise or moonset. Use `moon_phase` for phase-only questions. At high latitudes, explicitly report a returned absence of rise, set, or full darkness.
- For meteors, call `meteor_showers` for the requested year and latitude, then check the dark and moon-free window locally. Describe the listed peak rate as an ideal dark-sky rate. Give a practical window using the actual light conditions.
- For aurora, use `aurora_outlook` for the location and `kp_forecast` for the relevant three-hour UTC bins within its three-day horizon. Convert forecast bins to the observing site's local date and time before comparing them with darkness. Use `space_weather_alerts` only for a requested bulletin or active event. Tell the reader which quantity is an estimate and when weather is unknown.

Recommend a bounded local time window, viewing direction when available, and the observation or calculation that explains the choice. If the date lies beyond the available aurora forecast, give the calculable darkness and moon conditions and state the forecast horizon.
