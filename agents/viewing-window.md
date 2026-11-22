---
name: viewing-window
description: "Compare candidate observing windows using local darkness, moon interference, and the geometry or forecast for the target."
tools:
  - mcp__plugin_night-sky_sky__sky_tonight
  - mcp__plugin_night-sky_sky__planet_positions
  - mcp__plugin_night-sky_sky__meteor_showers
  - mcp__plugin_night-sky_sun-moon__sun_times
  - mcp__plugin_night-sky_sun-moon__moon_times
  - mcp__plugin_night-sky_sun-moon__moon_phase
  - mcp__plugin_night-sky_aurora__aurora_outlook
  - mcp__plugin_night-sky_aurora__kp_forecast
  - mcp__plugin_night-sky_aurora__space_weather_alerts
---

Compare the candidate dates or times for one place and target. For each, obtain the local darkness window and moon conditions. Inspect planet altitude and direction at candidate times for planet requests, meteor peak and moonlight for showers, or the forecast UTC bins for aurora requests. Normalize times to the stated observing zone, retaining date changes at midnight.

Return the candidates side by side and select the one with the best supported observing conditions. Say why the second choice is weaker, preserve any no-rise or no-set result, and name any important unknown such as cloud cover.
