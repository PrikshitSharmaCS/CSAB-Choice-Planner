# User Guide

## Before you begin

Keep your JEE Main **Common Rank List (CRL)** rank, category, gender, home state, and preferred branches ready. The tool uses the CRL rank rather than a category rank.

The tool gives a suggested ordering from historical data. It does not know live vacancies, current-round seat availability, document eligibility, or CSAB policy changes. Use it to prepare and compare choices, then confirm every choice in the official CSAB portal.

## Start the application

From the repository folder, run:

```powershell
.\run_app.ps1
```

Open [http://localhost:8000](http://localhost:8000) when the server starts.

## Complete your profile

### CRL rank

Enter your positive JEE Main Common Rank List rank. A lower rank number is better.

### Category and gender

Select the category and gender that apply to your counselling eligibility. The current filtering model considers these seat types:

| Candidate category | Considered seat types |
| --- | --- |
| GN | OPEN |
| EWS | EWS, OPEN |
| OBC-NCL | OBC-NCL, OPEN |
| SC | SC, OPEN |
| ST | ST, OPEN |

Gender-neutral pools are considered for every user. Female-only pools are considered for female users.

### Institute types

Choose one or more of NIT, IIIT, and GFTI. Deselecting an institute type removes it from the suggested list.

### Branch preference

Arrange branches in the order you prefer them. The application gives the first branch the highest score, then reduces the score for each later branch. Set **Minimum Acceptable Branch** to exclude branches you would not take.

### State preference

| Preference | Effect |
| --- | --- |
| Home State Only | Considers compatible home-state choices only. |
| Home State Priority | Keeps compatible choices nationwide and gives a small score bonus to home-state institutes. |
| Any State | Considers compatible choices nationwide without a home-state score bonus. |

The tool still applies quota eligibility rules. Selecting **Any State** does not make another state's home-state quota available.

## Read the results

The results page groups choices using the historical closing rank relative to your rank.

| Group | Historical closing-rank ratio | Meaning |
| --- | --- | --- |
| Dream | 0.75 to less than 0.91 | Aspirational choices within the configured reach. |
| Target | 0.91 to less than 1.10 | Choices near your historical rank. |
| Safe | 1.10 or higher | Choices whose historical closing rank was at least 10% higher than yours. |

The final order places Dream choices first, followed by Target and Safe choices. Choices within each group are ordered by their desirability score:

```text
0.50 × branch score + 0.40 × institute score + 0.10 × historical cutoff score
```

When **Home State Priority** is selected, a compatible home-state institute receives an additional 5 points.

## Make a final choice list

1. Read the complete suggested list, not only the first few rows.
2. Remove any programme, location, fee level, or institute you would not genuinely accept.
3. Add any eligible choices you would prefer that the tool did not surface.
4. Verify programme names, quotas, eligibility, vacancy, and official cutoffs on the CSAB site.
5. Enter the final list yourself on the official portal before its deadline.

## If something looks wrong

- Confirm that your rank is a CRL rank and not a category rank.
- Check your category, gender, state preference, and selected institute types.
- Confirm that your chosen minimum branch is included in your branch preference list.
- Review [data limitations](DATA_AND_LIMITATIONS.md), especially the current institute-metadata matching issue.
