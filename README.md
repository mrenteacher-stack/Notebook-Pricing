# Laptop Price Monitoring via API

An academic **Data Mining and Web Scraping** project that collects laptop offers from Google Shopping through the SerpApi and performs data cleaning, exploratory analysis, and price visualization.

> Results depend on the query and the time of collection. A new run may return different products and prices; notebook results should not be treated as permanent market data.

## Project objective

The project investigates the question: **What is the most common price range among the collected laptops, and which products have the lowest prices?**

The notebook implements an end-to-end data pipeline:

**API query → raw data storage → validation and cleaning → statistical analysis → charts and dashboard.**

## Data source and technologies

- **Data source:** Google Shopping offers queried through [SerpApi](https://serpapi.com/ ).
- **Recommended environment:** Google Colab, with Google Drive mounted to persist generated files.
- **Language:** Python.
- **Libraries:** `requests`, `pandas`, `numpy`, `matplotlib`, and `seaborn`.
- **Notebook:** `Monitoramentodenotebooks.ipynb`.

## Requirements

1. A SerpApi account and a valid API key. Usage is subject to the account's limits and terms.
2. A Google account to run the notebook in Colab and, if desired, save files to Google Drive.
3. Internet access to query the API.

The notebook's setup cell installs the Python libraries. The API key is not hard-coded: the notebook prompts for it without displaying it, using `getpass`.

## How to run

1. Open `Monitoramentodenotebooks.ipynb` in [Google Colab](https://colab.research.google.com/ ) or upload the file to Colab.
2. Run the cells in order, from top to bottom.
3. When prompted, enter your SerpApi key. Do not publish or share the key.
4. Authorize Google Drive mounting when prompted. The notebook creates a `projeto_notebooks` folder in `My Drive`.
5. Wait for the Google Shopping query and the data processing, analysis, and visualization steps to finish.
6. Review the tables and charts displayed in the notebook. Persisted files are saved under `My Drive/projeto_notebooks/`.

The query is configured for the term `notebook`, Brazil, Portuguese, and up to 40 results per request. These parameters can be changed in the notebook's collection section. Changes may affect the number of results, API usage, and comparability across runs.

## Pipeline steps

1. **Setup:** installs/imports libraries and creates working directories.
2. **Authentication and test:** accepts the SerpApi key without displaying it and validates a query to the Google Shopping engine.
3. **Collection:** queries the API and preserves the original JSON response.
4. **Extraction and validation:** organizes fields such as product name, price, store, URL, rating, review count, product ID, category, and collection timestamp; checks that product names and prices are present.
5. **Preprocessing:** normalizes text, converts prices to numeric values, removes records without a name or price, filters out prices below BRL 1,000.00, and removes duplicates by URL and by product name/price.
6. **Analysis:** calculates descriptive statistics, examines the price distribution, identifies the lowest-priced offers, and compares stores/sources when enough data is available.
7. **Visualization:** displays price distribution, a ranking of up to ten lowest-priced offers, and average price by store (or an alternative visualization when there are not enough stores), along with a dashboard of key indicators.

## Generated files

The notebook saves files to Google Drive under `My Drive/projeto_notebooks/`:

| Folder | Files | Contents |
|---|---|---|
| `dados_brutos/` | `resposta_api_bruta.json` | Original SerpApi response, preserved as JSON. |
| `dados_brutos/` | `dados_brutos.csv` | Fields extracted from the response before cleaning. |
| `dados_tratados/` | `dados_tratados.csv` | Validated and processed data, including the numeric `preco` column. |
| `graficos/` | `grafico_1_distribuicao_precos.png`, `grafico_2_ranking_barra.png`, `grafico_3_preco_medio_loja.png` | Individual visualizations produced during analysis. The third chart may show an alternative price distribution if there is not enough data to compare stores. |
| `saida/` | `dashboard_notebooks.png` | Final dashboard with record count, average, minimum and maximum prices, and charts. |

CSV files are written using UTF-8 with BOM (`utf-8-sig`), which helps compatibility with spreadsheet applications that expect this encoding.

## Limitations and considerations

- Collection is a one-time snapshot limited to results returned by Google Shopping/SerpApi; it may not represent all offers available in the Brazilian market.
- Prices, availability, stores, and search results may change at any time.
- Offers may refer to different laptop configurations, and source links may point to Google Shopping rather than directly to store product pages.
- The BRL 1,000.00 price threshold and deduplication rules affect the analyzed sample.
- Optional fields, such as ratings, review counts, and previous prices, may be missing.
- Store comparisons should account for the number of offers per store and product differences. The lowest observed average does not, by itself, mean that a store is generally the cheapest.
- The project uses an API rather than scraping individual store pages. Follow SerpApi's terms and do not attempt to bypass CAPTCHAs, authentication, or usage limits.
- Do not share the API key or save it in public versions of the notebook.

## Team

Project developed at **Unifor** for the course **F105 — Data Mining and Web Scraping**.

- Ezequias Pereira Sousa — 2523533
- Eduardo Medeiros Alencar Holanda — 2523614
- Nataniel Miranda da Silva — 2523548
- Pedro Enrique de Souza Simões — 2513694
- Renata Lima Lira — 2425231
