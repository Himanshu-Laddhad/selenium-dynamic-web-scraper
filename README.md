# HW5 – JavaScript-Rendered Web Scraper with Selenium

**Course:** MGTA 590 – Web Data Analytics | Purdue University
**Skills:** Python · Selenium · WebDriver · Dynamic Content Scraping · Pandas · CSV Export

---

## Overview

This project scrapes quotes, authors, and tags from [quotes.toscrape.com/js/](http://quotes.toscrape.com/js/) — a site that renders its content via JavaScript, making it inaccessible to static HTTP scrapers like `urllib`. Selenium WebDriver automates a real Chrome browser to fully render each page, then extracts the data and exports it to a clean CSV file.

This demonstrates the critical distinction between static and dynamic web scraping, and how to handle JavaScript-rendered content in data collection pipelines.

---

## What It Does

1. **Launches a Chrome browser** via Selenium WebDriver
2. **Navigates to the quotes site** and waits for JavaScript rendering
3. **Extracts from each page:**
   - Quote text (cleaned of surrounding quote characters)
   - Author name
   - Tags (pipe-delimited)
4. **Detects and follows** the "Next →" pagination button automatically
5. **Loops until no next page exists**, collecting all quotes across all pages
6. **Exports results** to `quotes.csv` using Pandas

---

## Files

| File | Description |
|---|---|
| `laddhad_himanshu_hw5.ipynb` | Main notebook with scraper code and output |
| `quotes.csv` | Scraped dataset: 100 quotes with author and tags |

---

## Output Schema

```
Author, Quote, Tags
Albert Einstein, "The world as we have created it...", change|deep-thoughts|thinking|world
J.K. Rowling, "It is our choices Harry...", abilities|choices
```

---

## Sample Data

| Author | Quote | Tags |
|---|---|---|
| Albert Einstein | The world as we have created it is a process of our thinking... | change\|deep-thoughts\|thinking\|world |
| J.K. Rowling | It is our choices, Harry, that show what we truly are... | abilities\|choices |
| Mark Twain | If you tell the truth, you don't have to remember anything. | misattributed-mark-twain |

---

## Key Concepts Demonstrated

| Concept | Description |
|---|---|
| Selenium WebDriver | Browser automation for JS-rendered pages |
| `find_elements(By.CLASS_NAME)` | Locating multiple DOM elements |
| Pagination automation | Auto-clicking "Next" until exhausted |
| `time.sleep()` | Waiting for JS rendering between pages |
| Pandas `DataFrame` | Structuring scraped data |
| `df.to_csv()` | Exporting results to CSV |

---

## Why Selenium (Not urllib)?

The target site renders quotes using JavaScript — the HTML source contains no quote data. A standard `urllib` request returns an empty page. Selenium solves this by running a real browser that executes JavaScript before extraction.

```
Static scraper (urllib) → Empty page ❌
Selenium WebDriver      → Fully rendered content ✅
```

---

## Tech Stack

- **Language:** Python 3
- **Environment:** Jupyter Notebook
- **Libraries:** `selenium`, `pandas`
- **Browser:** Google Chrome + ChromeDriver

---

## Prerequisites

```bash
pip install selenium pandas
```

ChromeDriver must be installed and on your system PATH, or managed automatically via `webdriver-manager`.

---

## How to Run

1. Install dependencies: `pip install selenium pandas`
2. Ensure ChromeDriver is available (matching your Chrome version)
3. Open `laddhad_himanshu_hw5.ipynb` in Jupyter
4. Run all cells (`Kernel → Restart & Run All`)
5. `quotes.csv` will be saved in the working directory

---

## Output

After completion, the notebook prints:

```
Scraping complete. Saved quotes.csv with 100 quotes.
```
