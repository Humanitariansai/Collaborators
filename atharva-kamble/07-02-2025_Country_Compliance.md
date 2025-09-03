# Twilio Long Code International Support Scraper

## Overview

This Python script scrapes country-specific SMS guidelines from Twilio’s website to extract information about long code international support. The final output is saved to a CSV file (`twilio_longcode_.csv`) with the following columns:

* **Country Name**
* **Country Code**
* **Long code international** (i.e., Operator network capability: Supported / Not Supported / Partially Supported)

---

## Goals

* Visit Twilio's guideline pages for each country
* Extract the country dialing code
* Extract the operator support status for long code international SMS
* Save the data in a structured CSV format

---

## Technologies Used

* `requests` – for HTTP requests
* `BeautifulSoup` (from `bs4`) – for HTML parsing
* `re` – for regular expressions and pattern matching
* `csv` – to write the scraped data to a file
* `iso3166` – to access ISO country codes and names
* `time.sleep()` – to add delay between requests and avoid server overload

---

## Script Workflow

### 1. Constants and Setup

```python
BASE = "https://www.twilio.com"
URL_TM = "/en-us/guidelines/{iso}/sms"
HEAD = {"User-Agent": "Mozilla/5.0 (educational scraper, contact if problems)"}
PAUSE = 0.5
```

Defines the base URL, a URL template for country guidelines, and a custom User-Agent header. Introduces a pause between requests to be respectful of Twilio's servers.

---

### 2. Fetch and Parse HTML

```python
def fetch_tree(path):
    url = urljoin(BASE, path)
    try:
        r = requests.get(url, headers=HEAD, timeout=15)
        if r.status_code == 200:
            return BeautifulSoup(r.text, "html.parser")
    except requests.RequestException:
        pass
    return None
```

Fetches the page and returns a parsed HTML tree. If the page doesn't exist or fails to load, returns `None`.

---

### 3. Extract Dial Code

```python
def parse_dial_code(soup):
    label = soup.find(string=re.compile(r"\\bDialing code\\b", re.I))
    if label:
        plus = label.find_next(string=re.compile(r"\\+\\d{1,4}"))
        if plus:
            return plus.strip().lstrip("+")
    m = re.search(r"\\+(\\d{1,4})\\b", soup.get_text())
    return m.group(1) if m else None
```

Locates the "Dialing code" label and extracts the numeric code.

---

### 4. Extract Long Code International Support

```python
def parse_longcode_status(soup):
    h = soup.find(lambda t: t.name in ("h2", "h3") and re.search(r"long codes?.*short codes?", t.get_text(), re.I))
    if not h:
        return None
    table = h.find_next("table")

    col_index = None
    header_row = table.find("tr")
    for idx, cell in enumerate(header_row.find_all(["th", "td"])):
        if re.search(r"long code[^a-z]*international", cell.get_text(" ", strip=True), re.I):
            col_index = idx
            break
    if col_index is None:
        return None

    for tr in table.find_all("tr"):
        cells = tr.find_all(["th", "td"])
        if not cells:
            continue
        if re.search(r"operator network capability", cells[0].get_text(), re.I):
            if len(cells) <= col_index:
                return None
            cell_text = cells[col_index].get_text(" ", strip=True)
            m = re.search(r"(Supported|Not Supported|Partially Supported)", cell_text, re.I)
            return m.group(1) if m else cell_text
    return None
```

Navigates to the appropriate table, finds the column labeled “Long code international,” and extracts the operator network capability status.

---

### 5. Scrape Each Country

```python
def scrape_country(iso):
    soup = fetch_tree(URL_TM.format(iso=iso.lower()))
    if soup is None:
        return None

    return {
        "Country Name": countries.get(iso).name,
        "Country Code": parse_dial_code(soup) or "Unknown",
        "Long code international": parse_longcode_status(soup) or "Unknown",
    }
```

Given a country code, fetches the page and returns a dictionary with the required information.

---

### 6. Run and Save

```python
def main():
    rows = []
    for c in sorted(countries, key=lambda x: x.alpha2):
        data = scrape_country(c.alpha2)
        if data:
            rows.append(data)
            print(f"✓ {data['Country Name']} ({data['Country Code']}) — {data['Long code international']}")
        else:
            print(f"× page missing {c.alpha2}")
        time.sleep(PAUSE)

    if rows:
        with open("twilio_longcode_.csv", "w", newline="") as f:
            writer = csv.DictWriter(f, rows[0].keys())
            writer.writeheader()
            writer.writerows(rows)
        print(f"\nSaved {len(rows)} rows to twilio_longcode_.csv")
```

Sorts countries by code, scrapes each one, prints progress, and saves the final results to CSV.

---

## How to Run the Script

```bash
python3 -m venv venv
source venv/bin/activate
pip install requests beautifulsoup4 iso3166
python scrape_twilio.py
```

After running, the terminal output will confirm which countries were processed and display their long code support status.

---

## Final Output

A CSV file named `twilio_longcode_.csv` will be created with rows like:

```
✓ United Arab Emirates (971) — Not Supported
✓ Albania (355)              — Supported
× page missing AQ            # (Antarctica, no page)
```

This output helps verify which countries support international long codes according to Twilio’s guidelines.

---

## Notes

* Some countries may show "Unknown" if Twilio does not provide enough data.
* The script uses a respectful 0.5s delay between requests to avoid overloading the server.
* This tool is built for educational and research purposes only.
