# Darkness and moonlight

## Twilight stages

The `sun-moon` server labels three twilight stages. The server does not print the sun angles. The angles below are the standard definitions used by the US Naval Observatory.

| Stage | Sun below the horizon | What it means outside |
| --- | --- | --- |
| Civil twilight | 0 to 6 degrees | Enough light to see without lamps. Only the brightest planets show |
| Nautical twilight | 6 to 12 degrees | The horizon is still visible. Bright stars and planets are out |
| Astronomical twilight | 12 to 18 degrees | The sky looks dark to most people. Faint objects are still washed out |
| Night | More than 18 degrees | Full darkness |

`sky_tonight` reports full dark as the span between the end of evening astronomical twilight and the start of morning astronomical twilight. In one check the two servers agreed to the minute.

Use the stage that fits the target:

- Bright planets and the moon: any time after sunset while the object is up.
- Meteors and constellations: after nautical twilight ends, better after astronomical twilight ends.
- The Milky Way and faint aurora: full darkness with the moon down.

## Moonlight

- Phase alone does not decide the night. A bright moon that sets before the window opens does no harm. Check rise and set times.
- `moon_times` lists the moonrise and moonset that fall on the requested calendar date. The moonset shown can come before the moonrise on that date. To find when the moon that rises this evening sets, read the next date's moonset.
- Illumination figures from different tools can differ by a few percent because each is computed for a different moment. `moon_times` labels its figure as the 9 pm phase.
- Around full moon the moon is up for most of the night. Around new moon it is up mostly in daylight.
- For a moon free window, combine full dark start and end with the two moon events on either side of the night.

## High latitudes

The servers return plain words when an event does not happen. Pass them on as returned.

| Returned text | Tool | Situation |
| --- | --- | --- |
| `Sunrise and sunset: none; sun down all day` | `sun_times` | Polar night. Twilight times are still listed and are worth giving |
| `Sunset: none`, `Full dark starts: none`, `No full darkness tonight` | `sky_tonight` | Midnight sun or all night twilight |
| `Moonrise: up all day`, `Moonset: none this day` | `moon_times` | The moon stays above the horizon all day |

Do not replace `none` with an estimate. Explain what it means for the plan.

## What darkness times leave out

Calculated darkness ignores cloud, haze, smoke, city light and terrain. A valley wall or a tree line can hide the lowest 10 degrees or more. State these as unknown and point to a local forecast.
