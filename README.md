# CSAB Choice Planner

CSAB Choice Planner is a local web application that turns a student's JEE Main rank and preferences into a suggested CSAB Special Round choice order.

It combines historical opening and closing ranks with category, gender, quota, state, institute-type, and branch preferences. Results are grouped as **Dream**, **Target**, and **Safe** choices, then ordered from aspirational to safer options.

> This tool is decision support, not an admission guarantee. Always verify eligibility, seat availability, official cutoffs, and the final choice order on the CSAB portal.

## What it does

- Collects a CRL rank, category, gender, home state, preferred institute types, and branch order.
- Filters historical cutoffs for compatible category, gender, quota, rank range, branch, and institute type.
- Classifies each eligible choice:
  - **Safe:** closing rank is at least 10% higher than the student's rank.
  - **Target:** closing rank is within 10% of the student's rank.
  - **Dream:** closing rank is up to 25% better than the student's rank.
- Scores choices using branch preference (50%), institute priority (40%), and historical cutoff margin (10%).
- Provides a searchable results table and supports light and dark themes.

## Quick start

### Prerequisites

- Python 3.10 or later
- Node.js 18 or later and npm, only when rebuilding the frontend

### Run the included application

The repository includes a prebuilt frontend and a SQLite database. On Windows, run:

```powershell
.\run_app.ps1
```

Then open [http://localhost:8000](http://localhost:8000).

If PowerShell execution is restricted, run `run_app.bat` instead.

### First-time Python setup

If the included virtual environment is unavailable, create one and install the backend requirements:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```

## How to use it

1. Open **Start Choice Filling**.
2. Enter your **CRL rank**, category, gender, and home state.
3. Select institute types and arrange branches from most to least preferred.
4. Choose the lowest branch you would accept and a state preference.
5. Select **Generate Recommendations**.
6. Review the Dream, Target, and Safe tabs, then independently confirm every final choice in the official counselling portal.

Read the detailed [user guide](DOCS/USER_GUIDE.md) before using recommendations in counselling.

## Development

Start the API from the repository root:

```powershell
.\.venv\Scripts\python.exe app.py
```

In a second terminal, start the React development server:

```powershell
cd frontend
npm install
npm run dev
```

The frontend runs at [http://localhost:4173](http://localhost:4173) and proxies `/api` requests to the backend on port 8000.

To rebuild the static frontend that the backend serves:

```powershell
cd frontend
npm run build
```

## Project layout

```text
app.py                    FastAPI application and static frontend host
recommendation_engine/    Filtering, classification, scoring, and ranking logic
frontend/                 React, TypeScript, Vite, and Tailwind user interface
DATA/                     Source CSAB PDF and institute metadata
extracted/                Parsed institute, programme, and cutoff datasets
db/schema.sql             SQLite schema
scripts/                  PDF parsing and database-seeding utilities
csab.db                   SQLite database used by the application
DOCS/                     User documentation and data notes
```

## Data and limitations

The cutoff data is derived from the PDF in `DATA/`. It is historical data, so it cannot predict vacancies, round-specific movement, or current-year policy changes.

There is also a current metadata-name matching issue: many institute names in `csab.db` do not exactly match the names in `DATA/csab_institute_metadata.json`. This can make the app fall back to a generic institute type, empty state, or default priority for affected institutes. See [data notes](DOCS/DATA_AND_LIMITATIONS.md) before relying on results.

## Rebuilding data

The source PDF can be parsed and the database can be rebuilt with:

```powershell
.\.venv\Scripts\python.exe scripts\parse_pdf.py
.\.venv\Scripts\python.exe scripts\seed_db.py
```

The database seeding script replaces `csab.db`. Back up the file first if you have made local changes.

## Contributing

Please keep changes focused and update relevant documentation with any adjustment to the counselling rules, data source, filtering, or scoring logic. Do not treat generated recommendations as official counselling advice.

## License

No license has been selected yet. Add a license file before publishing the repository if you want to define how others may use, modify, or distribute the project.
