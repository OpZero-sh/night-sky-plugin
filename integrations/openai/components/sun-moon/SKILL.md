---
name: use-sun-moon
description: "Looks up sunrise, sunset, golden hour, twilight, day length, moonrise, moonset and moon phase with Sun and Moon. Use when someone asks when the sun rises or sets, when it gets dark, when the moon rises, or when the next full or new moon falls."
---

# Sun and Moon

1. Work out the latitude, longitude and IANA time zone of the place. Pass `time_zone` on every call. The default is UTC.
2. Call `sun_times` for sunrise, sunset, solar noon, day length, golden hour and the civil, nautical and astronomical twilight times.
3. Call `moon_times` for moonrise, moonset, phase and illumination on a calendar date.
4. Call `moon_phase` for a phase only question. It needs no place and lists the next four principal phases with approximate times.

Reading results:

- For "when does it get dark", give `Civil twilight ends` for everyday use and `Astronomical twilight ends` for stargazing.
- `moon_times` lists the events on the requested date. The moonset can come before the moonrise. Read the next date for the set that follows an evening rise.
- At high latitudes the tools return text such as `none; sun down all day` or `up all day`. Report it as returned and still give the twilight times.

Answer with the times as returned, the date written out and the time zone named. Times are calculated for a level horizon. Terrain and weather are not included.
