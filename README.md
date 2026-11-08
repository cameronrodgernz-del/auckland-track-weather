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

## Hosting

Hosted on Vercel from this repository. `vercel.json` maps `/ellerslie` and `/pukekohe` to the page; the page picks the course from the address.

## Data and terms

Weather data from [Open-Meteo](https://open-meteo.com/) under CC BY 4.0. Open-Meteo's free service is for non-commercial use, so if the site is used commercially it needs an Open-Meteo API subscription. The [RainViewer](https://www.rainviewer.com/api.html) radar is free for personal use with credit, and the [OpenStreetMap](https://operations.osmfoundation.org/policies/tiles/) map tiles are fine for light use with credit.
