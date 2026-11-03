# Data and Limitations

## Data flow

The project stores a source cutoff PDF in `DATA/CSAB FOLDER.pdf`. `scripts/parse_pdf.py` extracts institute names, programme names, quota, seat type, gender pool, opening rank, and closing rank into `extracted/`. `scripts/seed_db.py` imports those files into `csab.db`.

The application combines database rows with `DATA/csab_institute_metadata.json` to determine institute type, state, and counsellor priority.

## Current coverage check

The included database contains:

- 108 institutes
- 185 programmes
- 3,337 cutoff records

The extracted CSV and JSON files contain the same counts as the SQLite database.

## Known metadata-name mismatch

The database and metadata file use exact institute-name matching. At present, only 24 database names exactly match a metadata name. Differences such as punctuation, spelling, parenthetical campus names, and abbreviations leave 84 database institutes unmatched.

For unmatched institutes, the application currently falls back to:

- `GFTI` as the institute type
- an empty state
- priority rank `90`

This affects institute-type filtering, state-based quota logic, home-state priority, and institute scoring. Recommendations that include unmatched institutes must be treated with extra caution until name normalization or a stable institute identifier is added.

## Other limitations

- The engine uses historical closing ranks only; it cannot estimate live demand, vacancies, or cutoff movement.
- It uses CRL rank only and does not model category rank.
- Programme matching relies on keywords. A programme with an unusual title may be missed or classified under a broader branch label.
- “Safe”, “Target”, and “Dream” are labels calculated from past cutoff ratios. They are not probabilities or guarantees.
- The recommendation score uses manually supplied institute priority values. It is not an official CSAB, NIRF, placement, or admission ranking.
- The PDF parser and database seeder are separate processes. Rebuilding either dataset changes the recommendations and should be reviewed before release.

## Responsible use

Use the software as a planning aid. Make your final counselling decisions from the official CSAB notices, information brochure, eligibility rules, vacancy data, and portal entries.
