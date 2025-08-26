# Population Growth Data Scraper

A comprehensive web scraper that extracts historical population data for top cities in China, India, and the United States from [populationstat.com](https://populationstat.com).

## Features

- **Multi-Country Support**: Scrapes top cities from China, India, and United States
- **Historical Data**: Extracts 86 years of population data (1950-2035) for each city
- **Intelligent Parsing**: Extracts data from JavaScript embedded in web pages
- **Robust Error Handling**: Graceful handling of network issues and parsing errors
- **Structured Output**: Saves data in organized JSON format
- **Respectful Scraping**: Includes delays and proper headers to avoid overwhelming servers

## Installation

1. Install required dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Basic Mode (City names and URLs only)
```bash
python scrape.py --no-history
```

### Full Mode (Including historical population data)
```bash
python scrape.py
```

The full mode will take several minutes as it fetches detailed data from individual city pages.

## Output

The scraper generates JSON files in the `data/` directory:

- `cities_data_full.json`: Complete data with historical population by year
- `cities_data_basic.json`: Basic city information without historical data

### Data Structure

Each city entry contains:
```json
{
  "name": "Shanghai29 M",
  "url": "https://populationstat.com/china/shanghai",
  "population_text": "29",
  "country": "china",
  "population_history": {
    "1950": 4288000,
    "1951": 4590000,
    "...": "...",
    "2035": 34341000
  },
  "years_available": 86,
  "current_population": 34341000,
  "latest_year": 2035
}
```

## Sample Results

The scraper successfully extracts data for approximately:
- **50 cities** from each country (150 total)
- **86 years** of historical data per city
- **~12,900 total data points** across all cities

### Top Cities by Country

**China**: Shanghai, Beijing, Chongqing, Tianjin, Guangzhou, Shenzhen, Chengdu...
**India**: Delhi, Mumbai, Bangalore, Calcutta, Madras, Hyderabad, Ahmadabad...
**United States**: New York City, Los Angeles, Chicago, Houston, Dallas, Miami...

## Technical Details

### Data Extraction Method

The scraper uses intelligent parsing to extract data from:
1. **JavaScript Variables**: Primary method extracting from `chart_rows["total"]` arrays
2. **HTML Content**: Fallback method for current population figures
3. **Text Pattern Matching**: Alternative extraction for edge cases

### Rate Limiting

- 0.5-second delay between individual city requests
- 1-second delay between countries
- Proper HTTP headers to identify as legitimate browser

## Files

- `scrape.py`: Main scraper script with `PopulationScraper` class
- `requirements.txt`: Python dependencies
- `data/cities_data_full.json`: Output with complete historical data
- `README.md`: This documentation

## Error Handling

The scraper includes comprehensive error handling for:
- Network connectivity issues
- Missing or malformed data
- JavaScript parsing errors
- Rate limiting responses

## Limitations

- Data is limited to cities available on populationstat.com
- Historical data depends on site's data availability
- Respects robots.txt and includes appropriate delays
- Future population figures (2026-2035) are projections from the source
