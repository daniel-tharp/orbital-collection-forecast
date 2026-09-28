# Orbital Collection Forecast

A Python and astrodynamics pipeline that forecasts Chinese imaging reconnaissance satellite overpasses for specified ground coordinates to identify unobserved operational security (OPSEC) windows.

### Features
- Ingests public CelesTrak TLE orbital ephemeris data using Skyfield and SGP4.
- Filters optical platforms (Gaofen, Jilin) using a 45° elevation cutoff and JPL `de421.bsp` solar ephemeris to enforce daylight-only collection.
- Models Synthetic Aperture Radar (SAR) platforms (Yaogan) at a 20° elevation threshold (day/night capable).
- Validates TLE epoch age against orbital decay thresholds.
- Generates a chronological Zulu (UTC) timeline highlighting usable collection gaps vs. operational micro-gaps.

### Tech Stack & Dependencies
- Python 3.x
- skyfield
- sgp4
- pandas / numpy
- jplephem (for solar ephemeris calculations)

### Sample Output (UTC / Zulu)
text
09-28 20:37 to 09-28 21:03 | [O] ALL CLEAR     |  26.2 min
09-28 21:03 to 09-28 21:05 | [X] SAT OVERHEAD  |   1.3 min
09-28 21:05 to 09-28 21:09 | [-] MICRO-GAP     |   4.3 min (Too short: <15m)
09-28 21:09 to 09-28 21:10 | [X] SAT OVERHEAD  |   1.2 min
09-28 21:10 to 09-28 22:04 | [O] ALL CLEAR     |  54.2 min

 ### How to use
- Download Celestrak TLE files from https://celestrak.org/NORAD/elements/gp.php?GROUP=active&FORMAT=tle and save the file name as active_sats.txt.
- Edit the coordinates under # Coordinates input to your desired location.
