# CWL Stats (2016–2019)

All data recovered by Activision's backend while I was working for MLG during the 2016-2019

Player-level match statistics from the **Call of Duty World League (CWL)** across four competitive seasons. Each row represents one player's performance in a single map/match.

The 2018 WWII season also includes **full structured JSON data** — one file per map played — with rich detail including hill rotations, round-by-round scores, team sides, and per-player breakdowns not available in the CSV format.

Data covers LAN events and select online leagues from the first four years of the CWL era.

---

## Seasons

| Folder | Game | Season |
|--------|------|--------|
| `2016-BO3/` | Black Ops 3 | 2016 CWL |
| `2017-IW/` | Infinite Warfare | 2017 CWL |
| `2018-WWII/` | WWII | 2018 CWL |
| `2019-BO4/` | Black Ops 4 | 2019 CWL |

---

## Events

### 2016 – Black Ops 3
| File | Event |
|------|-------|
| `BO3_MLG_Orlando.csv` | MLG Orlando |
| `BO3_MLG_Anaheim.csv` | MLG Anaheim |
| `BO3_NA_Stage1_Playoffs.csv` | NA Stage 1 Playoffs |
| `BO3_NA_Stage2_Playoffs.csv` | NA Stage 2 Playoffs |
| `BO3_Champs.csv` | CWL Championship |
| `Online/BO3_NA_Stage1.csv` | NA Stage 1 (Online League) |
| `Online/BO3_NA_Stage2.csv` | NA Stage 2 (Online League) |

### 2017 – Infinite Warfare
| File | Event |
|------|-------|
| `MLG_Dallas_2017.csv` | CWL Dallas |
| `MLG_Atlanta_2017.csv` | CWL Atlanta |
| `MLG_Anaheim_2017.csv` | CWL Anaheim |
| `GPL_Stage_1_2017.csv` | Global Pro League Stage 1 |
| `GPL_Stage_2_2017.csv` | Global Pro League Stage 2 |
| `GPL_Relegation_2017.csv` | GPL Relegation |
| `CWL_Champs_2017.csv` | CWL Championship |
| `fix/MLG_Vegas_2016.csv` | CWL Vegas (Dec 2016 – IW season opener) |

### 2018 – WWII
| File | Event | Structured JSON |
|------|-------|----------------|
| `data-2017-12-10-dallas.csv` | CWL Dallas | `structured/structured-2017-12-10-dallas/` (269 files) |
| `data-2018-01-14-neworleans.csv` | CWL New Orleans | `structured/structured-2018-01-14-neworleans/` (280 files) |
| `data-2018-03-11-atlanta.csv` | CWL Atlanta | `structured/structured-2018-03-11-atlanta/` (277 files) |
| `data-2018-04-01-birmingham.csv` | CWL Birmingham | `structured/structured-2018-04-01-birmingham/` (164 files) |
| `data-2018-04-08-proleague1.csv` | Pro League Stage 1 | `structured/structured-2018-04-08-proleague1/` (506 files) |
| `data-2018-04-19-relegation.csv` | Pro League Relegation | `structured/structured-2018-04-19-relegation/` (39 files) |
| `data-2018-04-22-seattle.csv` | CWL Seattle | `structured/structured-2018-04-22-seattle/` (272 files) |
| `data-2018-06-17-anaheim.csv` | CWL Anaheim | `structured/structured-2018-06-17-anaheim/` (270 files) |
| `data-2018-07-29-proleague2.csv` | Pro League Stage 2 | `structured/structured-2018-07-29-proleague2/` (508 files) |
| `data-2018-08-19-champs.csv` | CWL Championship | `structured/structured-2018-08-19-champs/` (296 files) |

Each CSV event has a corresponding `structured/` folder with one JSON file per map played (2,881 files total).

### 2019 – Black Ops 4
| File | Event |
|------|-------|
| `Vegas_BO4.csv` | CWL Vegas |
| `Fort_Worth_BO4.csv` | CWL Fort Worth |
| `London_BO4.csv` | CWL London |
| `Anaheim_BO4.csv` | CWL Anaheim |
| `PLQ_BO4.csv` | Pro League Qualifier |
| `Pro_League_BO4.csv` | Pro League |
| `Pro_League_Finals_BO4.csv` | Pro League Finals |
| `Champs_BO4.csv` | CWL Championship |
| `Full/BO4_Full.csv` | Combined full-season dataset |

---

## Data Columns

Columns vary slightly by year as the game and stat-tracking system evolved, but all files share a common core:

| Column | Description |
|--------|-------------|
| `match id` / `id` | Unique match identifier |
| `series id` | Series (best-of) identifier |
| `mode` | Game mode (Hardpoint, Search & Destroy, Control, Uplink) |
| `map` | Map name |
| `team` | Player's team |
| `player` | Player gamertag |
| `win?` / `team_score` | Result or score |
| `kills` | Total kills |
| `deaths` | Total deaths |
| `k/d` | Kill/death ratio |
| `assists` | Assists |
| `score` / `player_score` | Score or score-per-minute |

**Mode-specific columns** (present when applicable):

- Hardpoint: `hill time (s)`, `hill captures`, `hill defends`
- Search & Destroy: `snd rounds`, `snd firstbloods`, `bomb plants`, `bomb defuses`
- Control (2019): `ctrl rounds`, `ctrl captures`, `ctrl firstbloods`
- Uplink (2016): `uplink dunks`, `uplink throws`, `uplink points`

2017 and 2018 files include extended columns for weapon preferences, scorestreaks, accuracy, and kill streaks.

---

## Structured JSON Format (2018 WWII only)

Each JSON file in `2018-WWII/structured/` represents one map played. File names follow the pattern `structured-{unix_timestamp}-{match_id}.json`.

Top-level fields:

| Field | Description |
|-------|-------------|
| `id` | Match UUID |
| `series_id` | Series identifier (e.g. `champs-pool-A-3`) |
| `mode` | Game mode |
| `map` | Map name |
| `start_time_s` / `end_time_s` | Unix timestamps |
| `duration_ms` | Map duration in milliseconds |
| `platform` | Platform (ps4) |
| `hp_hill_names` | Hardpoint only — ordered hill names |
| `hp_hill_rotations` | Hardpoint only — number of hill rotations |
| `teams` | Array of two team objects (name, score, is_victor, round_scores, side) |
| `players` | Array of player stat objects |

Each `players` entry contains kills, deaths, assists, accuracy, weapon preferences, scorestreaks, hill time, S&D stats, and more — mirroring and extending the CSV columns.

---

## Notes

- All CSV data is per-player per-map (one row = one player in one map)
- 2016 data uses a slightly different schema (no series IDs, simplified columns)
- The `fix/` subfolder in 2017-IW contains a corrected file for CWL Vegas
- The `Full/BO4_Full.csv` in 2019 is a combined/merged version of all BO4 events
- Structured JSON is only available for the 2018 WWII season

---

## License

Data is shared for public research, analysis, and archival purposes.
