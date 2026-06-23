# portfolio-evidence-after-platform-shock
Reproducibility code for a course paper on Counter-Strike 2 skin prices as a digital asset market. Includes Steam market data collection, portfolio construction, CAPM and APT estimation, Ramsey RESET tests, and Dimson thin-trading corrections.
# CS2 Skin Market Course Paper Code

This folder contains the reproducibility notebook for the course paper:

**Portfolio Evidence on the Credibility of a Centrally Governed Digital Asset Market After a Platform-Induced Shock**

The notebook combines:

- Steam Community Market data collection for Counter-Strike 2 item price histories.
- Portfolio construction for knives, non-knives, rarity groups, StatTrak groups, wear groups, and weapon-type groups.
- Descriptive statistics, ADF tests, residual diagnostics, CAPM estimates, APT estimates, Ramsey RESET checks, dummy-interaction tests, and Dimson thin-trading corrections.

## Files

- `cs2_skin_market_pipeline.ipynb` - the combined publication notebook.
- `outputs/` - created automatically when the notebook runs; stores generated tables using the final paper numbering, for example `table5_descriptive_prices_volumes.xlsx`, `table9_capm_ew.xlsx`, and `table17_dimson_apt_stattrak_knives.xlsx`.

The notebook expects this workbook when running the analysis section:

- `cs2_price_history.xlsx`

Expected sheets:

- `Items`
- `Price Matrix`
- `Volume Matrix`
- `Name Map`

To rebuild the workbook from Steam, place an item catalog in the same folder:

- `all_skins_complete.txt`

The notebook can also read the older `Skins.xlsx` format if `CATALOG_FILE` is changed accordingly.

## Dependencies

Install the Python packages below:

```bash
pip install numpy pandas scipy statsmodels matplotlib requests openpyxl python-calamine
```

`python-calamine` is optional but speeds up reading large Excel workbooks.

## Running The Analysis

1. Put `cs2_price_history.xlsx` next to the notebook.
2. Open `cs2_skin_market_pipeline.ipynb`.
3. Keep `RUN_COLLECTION = False`.
4. Run the notebook from top to bottom.

The analysis uses the pre-event period ending on `2025-10-08`, the post-event period starting on `2025-11-06`, and excludes the two-week adjustment window around the `2025-10-23` CS2 update.

## Rebuilding The Data

Data collection is disabled by default because Steam price history requests require authenticated cookies and can take a long time.

Before setting `RUN_COLLECTION = True`, define your Steam cookies as environment variables:

```bash
export STEAM_LOGIN_SECURE="your steamLoginSecure cookie"
export STEAM_SESSIONID="your sessionid cookie"
export STEAM_LANGUAGE="english"
```

Do not commit these values to GitHub. The notebook intentionally reads them from the environment rather than storing them in code.

## Notes

The raw data workbook is large and may be better distributed separately from the code repository. The notebook is written so GitHub can show the full computation pipeline without exposing private Steam session data.
