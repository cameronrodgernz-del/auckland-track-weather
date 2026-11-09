# Ellerslie and Pukekohe Park track weather

Track weather for Auckland Thoroughbred Racing's two courses, Ellerslie (`/` and `/ellerslie`) and Pukekohe Park (`/pukekohe`). Each tab has the full hour-by-hour forecast plus:

- **Next meeting**: a written read of race day, a drawing of rain each hour and the running total from now to the end of racing with the 48 hour, 24 hour and 6:45am race-morning checks marked, racing hours hour by hour with the wind as the horses meet it in the home straight, the rain expected between each check and the next, and the last seven days' rain and evaporation for the track information sheet. Meetings more than a week out show the date until the forecast reaches them.
- **The rest of the season**: the remaining meetings, how far away they are and the break before each.
- **Rain radar**: the last two hours of RainViewer radar in ten-minute steps on a greyed OpenStreetMap base, with rings at 25 and 50 km.
- **On the track**: whether the track should wet up or dry out this week, the water lost to evaporation since the last day with 5 mm or more, rain in against evaporation out, soil moisture in the top 9 cm and from 9 to 27 cm, soil temperature for growth and oversowing, and a seven-day grid of thunderstorm hours and downpours of 5 mm or more in an hour.

It's a plain static site: `index.html`, `styles.css`, `app.js` and `track.js`. No build step and no keys.

## The courses

Each course is an entry in `PLACES` in `app.js`:

- `short`: the name used in the race section and on the radar pin
- `hand`: the direction of running. Both courses are right-handed, so the inside rail is on the horses' right for crosswinds in the straight
- `straight`: the bearing the horses run along the home straight to the post. Ellerslie's is about 299° (west-north-west, in front of the Ascot and Ellerslie stands) and Pukekohe's about 324° (north-west, in front of the stands on the Manukau Road side), both from the OpenStreetMap outlines of the tracks
- `soilNote` and `calendarNote`: the course's own line under the soil chart and under the season list
- `meetings`: the season's dates with the raceday name and racing hours (`from` and `to`, clock hours)

The 2026/27 dates come from ATR's calendar in its 2026 annual report. Racing hours come from the first race times on ATR's raceday pages, or the NZTR and TAB racing calendar where ATR hasn't posted one, plus the number of races. The 2027/28 dates need adding before August 2027.

Soil moisture, soil temperature and evaporation come from the Open-Meteo model for the area, not from the track, so the page uses them for direction rather than as readings.

## The rain blend

The daily rain figure in the summaries is a blend of six models: the European 9 km model (ECMWF IFS), the European AI model (AIFS), the UK Met Office, the US GFS, the German ICON and the Canadian GEM. With five or more models reporting, the highest and the lowest are dropped and the rest averaged. The US model's rain is left out from five days ahead, where it ran about half too low. The 51-run European ensemble is used for the chance of rain, not for the amount.

The line-up was chosen in November 2026 by scoring each model's past forecasts, one to seven days ahead, against the Auckland Airport and Hamilton Airport rain gauges from January 2024 to November 2026. At Auckland the blend's average miss on a day's rain, one to six days ahead, was about 4% lower than the previous blend's on the same days (2.53 mm down to 2.42 mm, from February 2025 on), and at five and six days ahead it caught about half the days of 10 mm or more, up from about four in ten. The airport gauge is about 13 km from Ellerslie and 25 km from Pukekohe, and the test covers daily totals, not the timing of showers within a day.

The rain for each hour, from today on, is the average of the six models for that hour, scaled so the day's hours add up to the day's blend. Against the gauges' six-hour totals that ran 13 to 19% closer than one model's hours on their own. Because averaging flattens a sharp burst, the "5 mm or more in the hour" flags still read the European 9 km model's own hours.

The chance tables give the chance of 1, 5, 10 and 20 mm falling in a stretch of hours. Each chance comes from the share of the models whose total reaches the amount and how far the blended total is from it, with weights fitted to what fell at the two gauges from February 2025 to November 2026. Fitted on one gauge and checked on the other, 70% came in at 64 to 75% for a day or more and 64 to 69% for part of a day.

## Hosting

Hosted on Vercel from this repository. `vercel.json` maps `/ellerslie` and `/pukekohe` to the page; the page picks the course from the address.

## Data and terms

Weather data from [Open-Meteo](https://open-meteo.com/) under CC BY 4.0. Open-Meteo's free service is for non-commercial use, so if the site is used commercially it needs an Open-Meteo API subscription. The [RainViewer](https://www.rainviewer.com/api.html) radar is free for personal use with credit, and the [OpenStreetMap](https://operations.osmfoundation.org/policies/tiles/) map tiles are fine for light use with credit.
