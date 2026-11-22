---
name: use-sky
description: "Plans planet viewing and meteor watching for a place and date with Night Sky Tonight. Use when someone asks what planets are visible tonight, where to look for a planet, when it gets fully dark, or when a meteor shower peaks."
---

# Night Sky Tonight

1. Work out the latitude, longitude and IANA time zone of the observing site. Pass `time_zone` on every call. The default is UTC.
2. For a night at a glance, call `sky_tonight` with the evening date. It returns sunset, full dark start and end, moon phase, moon free dark hours, and each visible planet's time span and best moment with altitude and direction.
3. For one clock time, call `planet_positions` with `local_time` as 24 hour `HH:MM`. A negative altitude means the object is below the horizon.
4. For meteor showers, call `meteor_showers`. With no `year` it lists upcoming peaks first. The hourly rate is a ceiling for ideal dark skies, so say that real counts are lower. Peak dates can shift by a day.

Reading results:

- Times after midnight in a `sky_tonight` result fall on the next calendar date. Write the date out.
- Lower magnitude is brighter.
- Only Mercury, Venus, Mars, Jupiter and Saturn are covered. Do not add stars, comets or other planets from memory.
- When the result reads `none` or `No full darkness tonight`, report that as returned.

Answer with a local time window, a direction, and the reason. State that positions are calculated to about a degree and that cloud, light pollution and terrain are not checked.
