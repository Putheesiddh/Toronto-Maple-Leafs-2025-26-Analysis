# Why Did the Toronto Maple Leafs Fall 30 Points in 2025-26?

**A SQL + Tableau analysis of the Leafs' drop from 108 points (2024-25) to 78 points (2025-26).**

📊 **Interactive dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/sochea.putheesiddh/viz/Leafsseasonanalysis/Dashboard1)

![Dashboard](dashboard.png)

---

## The Question

In 2024-25, the Leafs went 52-26-4 (108 points) and finished 1st in their division. The next season, they went 32-36-14 (78 points), missed the playoffs, fired their GM on March 30, and won the draft lottery.

**Why did they fall so far, and what should the team fix first?**

Many fans blamed losing Marner, Matthews' injury, poor defending, or the team tanking for a top draft pick. This project uses data to test which of these explanations actually holds up.

## Summary

The data shows the collapse was mostly caused by goaltending, not tanking. At 5-on-5, the Leafs allowed 71 more goals than the year before, but the quality of chances they allowed only explains about 21 of them. About 70% of the extra goals against came from below-expected goaltending, led by Stolarz's drop.

## Key Findings

**1. Goals against caused the collapse, not scoring.**
Goal differential fell from +38 to -43. Goals for dropped only a little (267 → 252), but goals against rose by 66 (229 → 295). Special teams weren't the main problem: the power play got worse (24.8% → 21.3%), but the penalty kill actually improved (77.9% → 81.2%).

**2. Goaltending did more damage than the defence.**
At 5-on-5, expected goals against rose 12% (2.39 → 2.67 per 60), but actual goals against rose 50% (2.01 → 3.01 per 60). Goals saved above expected (GSAx) went from +26.1 to -23.4.

**3. It wasn't tanking.**
Before the GM was fired on March 30, the Leafs had already lost -17.6 of their -23.4 GSAx. Scoring did drop in the last 8 games, but that's a small sample, and Matthews was injured at the time.

**4. Stolarz's drop was the biggest single factor.**

| Goalie | 2024-25 GSAx | 2025-26 GSAx | Change |
|---|---|---|---|
| Anthony Stolarz | +24.2 | -10.6 | -34.7 |
| Joseph Woll | +7.4 | -8.8 | -16.2 |
| Dennis Hildeby | -3.8 | +3.7 | +7.5 |

Stolarz and Woll together fell by about 51 goals, roughly the team's whole goaltending decline. After missing about two months with an injury from November, Stolarz never got back to his 2024-25 form.

## Recommendation

**Fix goaltending first.** Focus on Stolarz's health and workload, and add a reliable backup, before spending big to rebuild the defence. The defence got somewhat worse (+12% expected goals against), but the goaltending got much worse (+50% actual goals against).

## Data

- **[MoneyPuck.com](https://moneypuck.com/data.htm)**: Leafs game-by-game team data (2024-25 and 2025-26) and season goalie data.
- **StatMuse**: power play and penalty kill percentages.
- **News reports** for injury context (see Sources).

All stats are **5-on-5** (even strength) unless noted. This removes power plays and penalty kills, which is the standard way to compare teams.

## Method

1. **Checked the data:** 82 games × 5 game situations per season, and goal totals matched official numbers (267/229 and 252/295).
2. **Compared seasons:** shots, expected goals and goals against per 60 minutes (`GROUP BY`).
3. **Measured goaltending:** GSAx = expected goals against − actual goals against.
4. **Tested the tanking theory:** split 2025-26 into before/after March 30 (`CASE WHEN`).
5. **Tracked the season game by game:** running GSAx total (window function `SUM() OVER`).
6. **Compared goalies:** joined the two seasons' goalie tables (`JOIN`).
7. **Built the dashboard** in Tableau and checked it matched the SQL results.

## Tools

Google Colab (Python, pandas) · SQLite + JupySQL · Tableau Public · Excel

## Limitations

- **GSAx isn't pure goalie skill.** It includes some luck and depends on MoneyPuck's expected-goals model.
- **After March 30 is only 8 games**, so the late-season results are a hint, not proof.
- **Matthews' injury overlaps** with the late-season scoring drop, so it can't be separated from the team giving up.
- **Injury details come from news reports**, not the dataset.
- **Goalie data is season-level**, so it can't show which goalie played each game.

## Files

- `leafs_analysis.ipynb`: SQL analysis notebook
- `dashboard.png`: dashboard screenshot
- `data/leafs_games.csv`: Leafs game-by-game team data, both seasons
- `data/leafs_goalies.csv`: Leafs goalies, both seasons

## Sources

- Data: [MoneyPuck.com](https://moneypuck.com/data.htm)
- Special teams: [StatMuse](https://www.statmuse.com/nhl/ask/maple-leafs-stat)
- Stolarz injury: [The Leafs Nation](https://theleafsnation.com/news/anthony-stolarz-sophomore-toronto-maple-leafs-season-injury-poor-play)
- Matthews injury: [Daily Faceoff](https://www.dailyfaceoff.com/news/auston-matthews-mcl-tear-surgery-injury-12-weeks-recovery-toronto-maple-leafs)

---

*By Sochea Putheesiddh · Business Analytics, George Brown College*
