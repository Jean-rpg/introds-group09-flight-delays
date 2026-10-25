# Which flight routes should an airline review for chronic delay?
IT135IU – Introduction to Data Science, course project.

## Team

| Name | Student ID | Role |
|---|---|---|
| VAN NGO CHI THIEN | ITDSIU25042 | Product owner / Team leader |
| NGUYEN TRI TIN | ITDSIU25047 | Data engineer – sources |
| NGUYEN MINH KHOI | ITDSIU25017 | Data engineer – integration |
| NGUYEN HAI QUAN | ITDSIU25032 | Data analyst |
| TRUONG TRUNG TIN | ITDSIU25048 | Visualisation lead |
| VO NGOC QUYNH NHU | ITDSIU24060 | Reproducibility lead |
| NGUYEN PHAM NHAT MINH | ITDSIU25022 | Ethics and privacy officer |

## Decision question

Which flight routes should an airline review for chronic delay?

The project compares carrier–origin–destination routes using NYC flight
records from 2013. The intended user is an airline operations manager.

The planned ranking considers routes with at least 100 observed arrival
outcomes. A delayed arrival means an arrival delay of at least 15 minutes.
Missing outcomes, flight counts, median delays and monthly consistency
will be considered when interpreting the results.

## Data

- **Source 1:** nycflights13 flights — 336,776 rows and 19 columns,
  covering NYC departures in 2013.
- **Source 2:** nycflights13 airlines — 16 rows and 2 columns,
  containing carrier codes and airline names.
- **Original package:** https://github.com/tidyverse/nycflights13
- **Publisher:** Hadley Wickham / tidyverse; original flight records
  from the US Bureau of Transportation Statistics.
- **Python package used:** nycflights13==0.0.3.
- **Original retrieval date recorded by the group:** 21 October 2026.
- **Licence:** CC0, as declared by the original nycflights13 package.

> Merge: flights and airlines are combined using a left join on `carrier`.
> The notebook checks that airline carrier codes are unique, all flights
> receive an airline name, and the join preserves all 336,776 flight rows.
> The merged working table contains 20 columns.

> Cleaning decisions: missing outcomes are retained rather than replaced
> with zero. Negative delays represent early departures or arrivals.
> Extreme delays are checked for consistency and retained unless there
> is evidence that they are invalid. Missing departure time is used as
> a cancellation proxy; missing arrival outcomes do not establish that
> a flight was diverted.

Source details, versions and recorded checksums are available in
`docs/source_record.md`.

The data describe 2013 operations. Results should not be interpreted
as current airline performance or evidence of what caused a delay.

## How to run

The repository does not include the raw CSV files. The notebook imports
the two tables from the nycflights13 Python package and generates the
CSV files locally.

**1. Download and extract the repository:**

https://github.com/Jean-rpg/introds-group09-flight-delays

Open the extracted project folder in VS Code.

**2. Install Python 3.12** and the Python and Jupyter extensions
for VS Code.

**3. Open Terminal in the project folder**, which contains
`notebook.ipynb` and `requirements.txt`.

**4. Create an environment and install the libraries:**

```powershell
py -3.12 -m venv .venv312
.\.venv312\Scripts\python.exe -m pip install -r requirements.txt
```

The requirements file records the group's Windows environment.
Other operating systems may require adjustments to platform-specific
packages.

**5. Create the data folders if they do not already exist:**

```powershell
New-Item -ItemType Directory -Force -Path data/raw, data/processed
```

**6. Open `notebook.ipynb` and select the kernel** whose path ends in:

```text
.venv312\Scripts\python.exe
```

Click **Run All**, check that no cells report errors, and save the
notebook with its outputs.

**7. Generated files appear in:**

| File | Content |
|---|---|
| `data/raw/flights.csv` | Original flight table exported from the Python package |
| `data/raw/airlines.csv` | Original airline lookup table exported from the Python package |
| `data/processed/flights_working.csv` | Merged flight table with airline names, before cleaning |

The current notebook also displays the data profile and cleaning checks.
After cleaning, its in-memory DataFrame has 24 columns. The saved
`flights_working.csv` remains the 20-column table exported before cleaning.

## Random seed

The current notebook does not perform random sampling, splitting or
model training, so no random seed is required.

If random operations are added later, a fixed seed will be recorded
and used consistently.

## Repository structure

- `data/raw/`: locally generated source CSV files.
- `data/processed/`: locally generated working dataset.
- `docs/source_record.md`: source, version and checksum information.
- `notebook.ipynb`: data loading, merging, profiling, cleaning and outputs.
- `README.md`: project description and instructions.
- `requirements.txt`: installed packages and versions.
- `.gitignore`: files and folders excluded from version control.

## AI tool use

ChatGPT assisted with Python environment troubleshooting and README
drafting. The notebook was run by a group member, who reported no errors
after selecting the Python 3.12 environment. Members will review the
content and verify the parts they submit.

## Repository link

https://github.com/Jean-rpg/introds-group09-flight-delays

## D2 outputs

Running all notebook cells generates:

- `data/raw/flights.csv`
- `data/raw/airlines.csv`
- `data/processed/flights_working.csv`
- `data/processed/data_profile.csv`
- `data/processed/cleaning_log.csv`
- `data/processed/route_summary.csv`

The working CSV contains the merged table before further cleaning.
Later transformations are performed in memory.

## Export the executed notebook

Run all cells and save the notebook before exporting:

```bash
python -m jupyter nbconvert --to html notebook.ipynb
```

Open the generated HTML in a browser and use Print → Save as PDF.
Check that all code, text and outputs are visible.

The environment includes `setuptools<81` because `nycflights13==0.0.3`
depends on `pkg_resources`.