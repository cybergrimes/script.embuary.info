# Changelog

Embuary Info (`script.embuary.info`) was created by **sualfred**
(https://github.com/sualfred/script.embuary.info) and is licensed under
**Apache-2.0** (unchanged). This is a fork maintained by **Cybergrimes**
(https://github.com/cybergrimes/script.embuary.info) targeting Kodi 21 Omega.

## 2.0.9 (fork; based on upstream `matrix` 2.0.10)

Not yet tested in a Kodi runtime. No language files or strings.po were touched. No features were removed.

- **OMDb title lookup fixed** (`resources/lib/omdb.py`): `urllib.quote` was used without `urllib` being imported (NameError on Python 3). Now uses `urllib.parse.quote`.
- **OMDb DVD/release date fixed** (`resources/lib/omdb.py`): the call `date_format(..., scheme=...)` used a parameter that does not exist, raised TypeError on every OMDb response, caused 3 repeated requests and prevented caching. Replaced by a small parser (`omdb_dvd_date`); the `release` property now actually gets a value (visible change, formatted with the Kodi long date format).
- **No retry on HTTP 4xx** for OMDb and Trakt (`omdb.py`, `trakt.py`); 5xx/network errors still retry as before. TMDB already behaved this way.
- **Shared `requests.Session`** (keep-alive) for TMDB, OMDb, Trakt and the YouTube check (`helper.py`, `tmdb.py`, `omdb.py`, `trakt.py`, `video.py`).
- **YouTube thumbnail check** (`resources/lib/video.py`): only YouTube videos are checked (others were dropped later anyway), 5 s timeout, and a failed check logs and keeps the video instead of raising.
- **`date_year` fix** (`resources/lib/helper.py`): returned an unbound variable (UnboundLocalError) on unparsable dates; now returns the input value, like `date_format`.
- **Removed dead Python 2 code** (`resources/lib/helper.py`): `unicode()` conversion in `json_call`.
- **Metadata** (`addon.xml`): version 2.0.9, provider credits sualfred and the Cybergrimes fork, `<source>` points to the fork, `<news>` added. License Apache-2.0 kept.
- **Added** this `CHANGELOG.md`.

### Deferred candidates (not implemented; need owner's OK)

- TMDB image size `original` -> smaller size (visual change).
- Pre-index local library in `tmdb_check_localdb`.
- Parallel YouTube HEAD checks.
- Faster `nextaired` matching.
- Brief negative cache of OMDb misses.
- Reading `filter_daydelta` via `getSettingInt` (legacy settings.xml slider; left as is).
