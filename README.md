# Předpověď úspěchu kampaní na Kickstarteru

Semestrální projekt 4IZ582

Autoři:

- Michal Dvořák
- Hana Veselá

## Obsah balíčku

| Soubor / složka | Popis |
| --- | --- |
| `main.ipynb`, `main.html` | Hlavní notebook (analýza dat, preprocessing, modely, AI část, vyhodnocení, závěr) a jeho HTML export. |
| `notebooks/01_data_collection.ipynb` (+ `.html`) | Stažení a spojení snapshotů Web Robots. Ke spuštění vyžaduje surová data (přes 9 GB), která v balíčku nejsou. Výsledek je v `_data/prepared/`. |
| `notebooks/02_llm_features.ipynb` | Generování LLM příznaků přes školní LiteLLM endpoint. Výstupy uložené v notebooku pocházejí z plného běhu. |
| `notebooks/02_llm_features.full_run.html` | HTML export notebooku 02 s výstupy plného běhu. |
| `notebooks/02_llm_features.pilot_run.html` | Archivní záznam pilotního běhu (309 kampaní) včetně kontroly konzistence a odhadu nákladů. Texty odpovídají starší verzi notebooku, použité dotazníky jsou již finální. Slouží k ověření čísel z pilotu uvedených v `main.ipynb` (sekce 5.1). |
| `_data/prepared/` | Připravený dataset (kampaně spuštěné v roce 2025), rozdělený do čtyř CSV souborů. V balíčku odevzdaném v InSIS chybí, viz [Data](#data). |
| `_data/ai/llm_features_*.csv` | Vygenerované LLM příznaky, které načítá hlavní notebook. |
| `_data/ai/schema_*.json` | Použité dotazníky (schémata), původní návrh modelu a jeho upravená verze. |
| `_data/ai/*_sample_ids.csv` | ID kampaní z discovery a pilotu, hlavní notebook je zařazuje do trénovací sady. |
| `_data/ai/pilot_features_*.csv`, `run_stats_*.csv`, `discovery_raw_response.txt` | Výsledky pilotu, statistiky běhů (dotazy, tokeny, čas) a původní odpověď modelu v discovery. |
| `requirements.txt`, `.env.example` | Použité balíčky a vzor konfigurace pro notebook 02 (API klíč v balíčku není). Soubor `.env.example` je skrytý (začíná tečkou). |

## Spuštění

```bash
pip install -r requirements.txt
jupyter notebook main.ipynb
```

Pokud jsou data ve složce `_data/prepared/`, `main.ipynb` běží offline a „Restart Kernel and Run All Cells“ trvá přibližně 4–6 minut. Notebook je potřeba spouštět z kořenové složky balíčku (všechny cesty jsou relativní).

Notebook `02_llm_features.ipynb` není nutné spouštět, protože jeho výsledky jsou uložené v `_data/ai/`. Opakované spuštění by vyžadovalo API klíč ke školnímu endpointu (`.env` podle `.env.example`) a odeslalo by všechny dotazy znovu, protože cache odpovědí kvůli velikosti v balíčku není.

## Data

Celý projekt včetně dat je v repozitáři [github.com/MandelOwO/kickstarter-success-prediction-public](https://github.com/MandelOwO/kickstarter-success-prediction-public).

Balíček odevzdaný v InSIS kvůli limitu velikosti neobsahuje složku `_data/prepared/` (přibližně 190 MB). Pokud v ní soubory chybí, `main.ipynb` je při prvním spuštění sám stáhne z repozitáře (vyžaduje připojení k internetu). Soubory lze stáhnout i ručně a uložit do `_data/prepared/`:

- [kickstarter_projects_2025_part_001.csv](https://raw.githubusercontent.com/MandelOwO/kickstarter-success-prediction-public/refs/heads/main/_data/prepared/kickstarter_projects_2025_part_001.csv)
- [kickstarter_projects_2025_part_002.csv](https://raw.githubusercontent.com/MandelOwO/kickstarter-success-prediction-public/refs/heads/main/_data/prepared/kickstarter_projects_2025_part_002.csv)
- [kickstarter_projects_2025_part_003.csv](https://raw.githubusercontent.com/MandelOwO/kickstarter-success-prediction-public/refs/heads/main/_data/prepared/kickstarter_projects_2025_part_003.csv)
- [kickstarter_projects_2025_part_004.csv](https://raw.githubusercontent.com/MandelOwO/kickstarter-success-prediction-public/refs/heads/main/_data/prepared/kickstarter_projects_2025_part_004.csv)

Zdroj dat: [Web Robots Kickstarter Datasets](https://webrobots.io/kickstarter-datasets/).
