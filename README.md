# Night Sky

Choose a time to head outside. Night Sky combines naked-eye planet positions, meteor shower peaks, local darkness, and moonrise with NOAA space weather when the target is the aurora.

[Connect with Claude, ChatGPT, Muse Code, or Grok](PROVIDERS.md)

## Try it

- Find a moon-free hour to look for planets in Flagstaff this weekend. Which direction should I face?
- Which of the next two nights looks better for an aurora outing near Fairbanks?

## Install in Claude

In Claude Code, run the following commands.

```text
/plugin marketplace add OpZero-sh/plugins
/plugin install night-sky@opzero
```

In Claude chat or Cowork, open the installed plugin’s **Connectors** tab and connect the listed services. The hosted services use public data and require no sign-in. Then ask a question or use the `observing-plan` skill. In Cowork or Claude Code, the `viewing-window` agent can handle a deeper comparison.

## Sources and coverage

Solar and lunar times and planet positions are calculated for the observing site. Aurora guidance uses NOAA SWPC short-range Kp data. Cloud cover, terrain, and light pollution require separate local information.

- [night-sky-tonight](https://night-sky-tonight.mcp.opzero.sh/) · [Privacy](https://night-sky-tonight.mcp.opzero.sh/?page=privacy) · [Support](https://night-sky-tonight.mcp.opzero.sh/?page=support)
- [sun-and-moon](https://sun-and-moon.mcp.opzero.sh/) · [Privacy](https://sun-and-moon.mcp.opzero.sh/?page=privacy) · [Support](https://sun-and-moon.mcp.opzero.sh/?page=support)
- [aurora-forecast](https://aurora-forecast.mcp.opzero.sh/) · [Privacy](https://aurora-forecast.mcp.opzero.sh/?page=privacy) · [Support](https://aurora-forecast.mcp.opzero.sh/?page=support)

## In use

Examples from the connected services in Claude.

![Planet visibility from Mauna Kea](media/planets.webp)

- [NOAA’s three-day Kp forecast](media/kp-forecast.webp)
- [Winter solstice solar times in Tromsø](media/polar-night.webp)
