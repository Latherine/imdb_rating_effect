# IMDb Functional Analysis

Functional-driven analysis of an IMDb SQLite snapshot (data snapshot: 2022-03-27).  
This repository contains Jupyter analyses that explore how director experience and runtime relate to IMDb ratings using SQL-driven Python code (SQLAlchemy + pandas) and reproducible visualizations.

---

## Contents

- `imdb_analysis.ipynb` — Main Jupyter notebook with the analyses:
  - `genres(dbcon, genre, min_rating)`: finds top directors within a genre and compares their directing experience (number of titles) to average ratings.
  - `rating_by_runtime(dbcon, min_minutes, max_minutes)`: groups titles into runtime categories (Short / Medium / Long) and compares average ratings.
- `analysis.html` — (optional) HTML export of the notebook for quick viewing.
- `.gitignore` — ignores common Python/Jupyter artifacts (and `imdb.db` by default).
- (not tracked) `imdb.db` — the SQLite database snapshot (see Data section to download).
- LICENSE 
---

## Quickstart

1. Clone the repository:
   ```
   git clone <your-repo-url>
   cd <your-repo-name>
   ```

2. Install dependencies (use virtualenv/venv):
   ```
   python -m venv .venv
   source .venv/bin/activate    # Linux / macOS
   .venv\Scripts\activate       # Windows PowerShell
   pip install -r requirements.txt
   ```
   If you don't have a requirements file, install the main packages:
   ```
   pip install sqlalchemy pandas numpy matplotlib jupyterlab
   ```

3. Download the IMDb SQLite database and place it in the repository root as `imdb.db` (see Data section below).

4. Open and run the notebook:
   ```
   jupyter lab         # or `jupyter notebook`
   # then open imdb_analysis.ipynb
   ```

---

## Data — download the SQLite database

The dataset used for these analyses is provided as an SQLite database file. You can download it from the following link:

- Database download link (SharePoint):  
  https://dickinson0-my.sharepoint.com/:u:/g/personal/vot_dickinson_edu/IQCncRWQVQYKQ5oSfftxkRm8Ad2Y0PfqOpcjbZmFQpr3KAM?e=LQoRUE

Important notes:
- The SharePoint link may require authentication (your institution or Microsoft account). If the link prompts you to sign in, complete the sign-in to access the file.
- If the link is publicly accessible you can download it directly from the browser, or with command-line tools (see examples). If authentication is required, download via your browser and then move the file into the repo.

Browser download (recommended if authentication is needed)
1. Click the link (or paste it into your browser).
2. If asked, sign in with the appropriate account.
3. Click the file → "Download" (or the download icon).
4. Save the file as `imdb.db` and move it into the repository root:
   ```
   mv ~/Downloads/imdb.db /path/to/your/repo/imdb.db
   ```

Command-line download (may work if the link is publicly accessible)
- curl (Linux / macOS):
  ```
  curl -L -o imdb.db "https://dickinson0-my.sharepoint.com/:u:/g/personal/vot_dickinson_edu/IQCncRWQVQYKQ5oSfftxkRm8Ad2Y0PfqOpcjbZmFQpr3KAM?e=LQoRUE"
  ```
- wget (Linux):
  ```
  wget -O imdb.db "https://dickinson0-my.sharepoint.com/:u:/g/personal/vot_dickinson_edu/IQCncRWQVQYKQ5oSfftxkRm8Ad2Y0PfqOpcjbZmFQpr3KAM?e=LQoRUE"
  ```
- PowerShell (Windows):
  ```
  Invoke-WebRequest -Uri "https://dickinson0-my.sharepoint.com/:u:/g/personal/vot_dickinson_edu/IQCncRWQVQYKQ5oSfftxkRm8Ad2Y0PfqOpcjbZmFQpr3KAM?e=LQoRUE" -OutFile .\imdb.db
  ```

If the command-line approach fails with an authorization or redirect error, use the browser method described above.

Verify the download
- Confirm the file is present in the repo root:
  ```
  ls -lh imdb.db
  ```
- Optionally inspect the DB (requires sqlite3):
  ```
  sqlite3 imdb.db ".tables"
  sqlite3 imdb.db "PRAGMA integrity_check;"
  ```

Note: This repository's `.gitignore` includes `imdb.db` by default to avoid accidentally committing the database file. If you want to store the DB in the repo, remove it from `.gitignore` and consider the repository size / policy implications.

---

## Key functions (notebook)

- `genres(dbcon, genre, min_rating)`  
  Identifies top directors for `genre` (by average rating), prints a top-10 table, computes the group's average rating, and plots number-of-titles for top directors.

- `rating_by_runtime(dbcon, min_minutes, max_minutes)`  
  Classifies titles into `Short` (<=90), `Medium` (91–180) and `Long` (>180) and reports average rating and runtime for each category, with a bar chart.

---

## Output & Visualizations

- The notebook produces summary tables and matplotlib plots for:
  - Top directors per genre and a bar chart of director productivity.
  - Average rating by runtime category with a bar chart.

To export a static HTML preview:
```
jupyter nbconvert --to html imdb_analysis.ipynb
```

---

## Recommended repository topics (tags)
imdb, sqlite, pandas, sqlalchemy, jupyter-notebook, python, data-analysis, data-science, matplotlib, visualization

---

## License

This repository's code and notebooks are licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

Data: the SQLite database (imdb.db) is not included in this repository. If you download the database from the provided SharePoint link, please obey any separate terms or access restrictions that apply to that dataset; those terms may differ from the code license above. If you intend to redistribute the database, check the database owner's permissions before doing so.

If you accept contributions, by contributing code you agree that those contributions will be licensed under the same license (MIT) unless otherwise noted.

---

## Contributing
- Open issues for bugs, feature requests, or data questions.
- If you add derived data or large files, place them under a `data/` folder and note them in `.gitignore` if they should not be tracked.
- Please include reproducible steps when filing issues.



