# Shower notes

## What the server lists

`meteor_showers` returns these ten showers. Names and radiants are as returned by the server. Peak dates below are approximate month positions only. Always read the actual date from the tool, because it shifts by a day between years.

| Shower | Usual peak | Radiant | Ideal rate returned |
| --- | --- | --- | --- |
| Quadrantids | Early January | Bootes | about 110 per hour |
| Lyrids | Late April | Lyra | about 18 per hour |
| Eta Aquariids | Early May | Aquarius | about 50 per hour |
| Southern Delta Aquariids | Late July | Aquarius | about 25 per hour |
| Perseids | Mid August | Perseus | about 100 per hour |
| Draconids | Early October | Draco | about 10 per hour |
| Orionids | Late October | Orion | about 20 per hour |
| Leonids | Mid November | Leo | about 15 per hour |
| Geminids | Mid December | Gemini | about 150 per hour |
| Ursids | Late December | Ursa Minor | about 10 per hour |

The server words every rate as `Up to about N per hour under ideal dark skies` and adds that rates seen in practice are usually lower.

## Why the real count is lower

The ideal rate assumes a perfectly dark sky, the radiant straight overhead, and an observer who sees the whole sky. Each of these cuts the count:

- A low radiant. Fewer meteors are above the horizon when the radiant is low. Rates climb as the radiant rises, which is why the hours after midnight are usually best.
- Moonlight and city light. Most meteors are faint. A bright sky hides them first.
- A partly blocked sky, or eyes that have not adapted to the dark. Dark adaptation takes roughly 20 to 30 minutes, and a phone screen resets it.

Give the listed figure as a ceiling and say that a typical observer sees a fraction of it.

## Moon notes

The server attaches one of three notes to the moon's illumination at the peak:

| Note | What to tell the reader |
| --- | --- |
| `dark skies` | Moonlight is not a factor |
| `some moonlight` | Watch while the moon is down if the timing allows |
| `bright moon washes out faint meteors` | Only the brighter meteors will show. Consider another shower |

The note reflects illumination only. A partly lit moon that has already set costs nothing, so check `moon_times` for the site before writing off a peak.

## Hemisphere guidance

The server's list is the same for every latitude. In test calls at 35 north, 45 south and 80 south no latitude flag appeared in the result, so apply this guidance yourself.

- Radiants in far northern constellations never rise, or stay very low, for mid southern latitudes. This applies to the Quadrantids (Bootes), Perseids (Perseus), Draconids (Draco) and Ursids (Ursa Minor).
- The Eta Aquariids and Southern Delta Aquariids favor the Southern Hemisphere and the tropics. From mid northern latitudes their radiant stays low and rates are well under the listed figure.
- The Geminids, Orionids, Leonids and Lyrids can be seen from both hemispheres, with the Geminids and Lyrids better from the north.

When a shower is poorly placed for the site, say so and offer the next well placed one.

## Practical advice worth passing on

- No telescope or binoculars. Meteors cross large parts of the sky and the unaided eye sees the most.
- Lie back and take in as much sky as possible, facing away from the brightest lights.
- Allow at least an hour. Meteors arrive in bursts with quiet gaps.
