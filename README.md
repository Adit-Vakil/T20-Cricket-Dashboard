# 🏏 T20 Cricket Dashboard — Best XI Selector

An interactive **Power BI** dashboard that analyzes T20 World Cup 2022 player
performance and builds a data-driven **best XI / final squad** by playing role
(anchors, finishers, all-rounders, specialist bowlers).

<!-- TODO(provenance): Confirm the data source line below and delete this comment.
     If the data is NOT the 2022 T20 World Cup, fix the first paragraph too. -->

> **Tech:** Power BI Desktop · Power Query (M) · DAX · Star-schema data model

---

## 📸 Preview

<!-- TODO(screenshots): THIS IS THE SINGLE MOST IMPORTANT FIX.
     A .pbix is invisible on GitHub. Without images, ~95% of visitors never see your work.
     1. Open T20_Cricket.pbix in Power BI Desktop.
     2. For each page: File ▸ Export ▸ Export to PDF, OR press PrtScn / use Snipping Tool.
     3. Save PNGs into a /screenshots folder in the repo.
     4. Replace the lines below with real paths. Keep the landing + Final12 + one detail page at minimum. -->

| Landing / Navigation | Final XI Selection |
|---|---|
| ![Landing page](screenshots/01-landing.png) | ![Final 12](screenshots/02-final12.png) |

| Role Analysis (e.g. All-Rounders) | Player Detail by Match |
|---|---|
| ![Role page](screenshots/03-role.png) | ![Player detail](screenshots/04-player-detail.png) |

---

## 🎯 What it does

The dashboard answers: **"Given match-level T20 data, which 11–12 players form the strongest balanced squad?"**

It does this by scoring players against role-specific criteria:

| Role | What the page evaluates |
|---|---|
| **Anchors / Middle Order** | High batting average, ability to bat through the innings |
| **Finishers / Lower-Order Anchors** | High strike rate, boundary %, scoring under pressure |
| **All-Rounders / Lower-Middle Order** | Combined batting + bowling contribution |
| **Specialist Fast Bowlers / Tail-End** | Economy, wickets, dot-ball %, bowling strike rate |
| **Final 12** | The selected squad, assembled from the role winners |
| **Player Detail (Batters / Bowlers / All-Rounders)** | Match-by-match breakdown for any chosen player |

---

## 🗂️ Data Model

Star schema with conformed dimensions feeding two fact tables:

```
        dim_players ─────┐
                         ├──< fact_batting_summary
   dim_match_summary ────┤
                         └──< fact_bowling_summary

        [ Key Measures ]  ← dedicated measures table (no data, DAX only)
```

| Table | Type | Holds |
|---|---|---|
| `dim_players` | Dimension | name, team, playing role, batting style, bowling style, player image |
| `dim_match_summary` | Dimension | match_id, match, match date, tournament stage |
| `fact_batting_summary` | Fact | runs, balls faced, innings, batting position (per player per match) |
| `fact_bowling_summary` | Fact | runs conceded, balls bowled, wickets, maidens (per player per match) |
| `Key Measures` | Measures | all DAX measures, kept separate for organization |

---

## 📐 Key Measures (DAX)

<!-- TODO(dax): The .pbix model is compressed, so these definitions are reconstructed
     from measure NAMES found in the report, not copied from your actual DAX.
     Open the model and paste your real formulas, or delete any you didn't implement. -->

**Batting**
- `Total Runs` — total runs scored
- `Total Balls Faced`, `Avg. Balls Faced`
- `Batting Avg` = Total Runs / dismissals
- `Strike Rate` = (Total Runs / Balls Faced) × 100
- `Boundary %` = boundary runs / total runs
- `Total Innings Batted`, `Batting Position`

**Bowling**
- `Wickets`, `Runs Conceded`, `Balls Bowled`
- `Economy` = Runs Conceded / overs bowled
- `Bowling Average` = Runs Conceded / Wickets
- `Bowling Strike Rate` = Balls Bowled / Wickets
- `Dot ball %` = dot balls / balls bowled
- `Total Innings Bowled`, maidens

---

## 📊 Report Pages

1. **Project – Sportan** — landing page with button navigation to every role
2. **Anchors / Middle Order**
3. **Finishers / Lower-Order Anchors**
4. **All-Rounders / Lower-Middle Order**
5. **Specialist Fast Bowlers / Tail-End**
6. **Final 12** — the selected squad
7. **Batters — player details by match**
8. **All-Rounders — player details by match**
9. **Bowlers — player details by match**

Built with area charts, KPI cards, pivot tables, scatter plots, slicers, and a
custom image visual for player photos, on a custom cricket-themed report theme.

---

## 🏆 Final Squad

<!-- TODO(result): List the 11–12 players the dashboard selected. This is your conclusion —
     a recruiter reading the README wants the answer, not just the method. -->

| # | Player | Role | Why selected |
|---|---|---|---|
| 1 | _TBD_ | Opener | _TBD_ |
| … | | | |

---

## 🚀 Open it yourself

1. Install [Power BI Desktop](https://www.microsoft.com/en-us/download/details.aspx?id=58494) (free, Windows).
2. Clone or download this repo.
3. Open `T20_Cricket.pbix`.

No `.pbix` viewer on Mac/Linux — use the screenshots above, or I'll add a
**Publish to Web** link.

<!-- TODO(publish): In Power BI Service, File ▸ Publish ▸ Publish to web, paste the link here.
     Note: Publish-to-web makes the report PUBLIC. Don't use it for sensitive data — this dataset is public, so it's fine. -->

---

## 📁 Repo structure

```
T20-Cricket-Dashboard/
├── T20_Cricket.pbix      # the dashboard
├── screenshots/          # page previews  ← add this
├── data/                 # raw CSVs / source  ← optional, add if you have them
└── README.md
```

---

## 🔧 Possible improvements

- Add the raw data and the Power Query / scraping steps for reproducibility
- Document the exact selection thresholds per role (what makes someone an "anchor")
- Add a data-refresh note (static snapshot vs. live)

---

## 📜 License

Released under the MIT License — see [LICENSE](LICENSE).
Player and match data sourced from ESPNCricinfo (T20 World Cup 2022); all rights to the underlying data belong to their respective owners.
