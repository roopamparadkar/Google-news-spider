# Google News Spider

A Python-based web crawler designed to validate website URLs by checking their presence in Google News search results. The project automatically processes a list of URLs from an Excel file and determines their approval status based on whether they appear in Google News search results.

## Features

- **Automated URL Validation**: Crawls through a list of URLs to check their status
- **Google News Integration**: Uses Google News search to validate if websites are approved news sources
- **Excel File Processing**: Reads URLs from and writes results back to an Excel (XLSX) file
- **Error Handling**: Includes exception handling and continuous failure monitoring to prevent infinite loops
- **Status Tracking**: Marks URLs as "Approved" or "Not Approved" based on search results

## Dependencies

Make sure you have the following Python packages installed:

```bash
pip install requests beautifulsoup4 openpyxl
```

- `requests` - For HTTP requests
- `BeautifulSoup4` - For HTML parsing
- `openpyxl` - For Excel file manipulation

## File Structure

```
Google-news-spider-master/
├── GoogleNewsSpider.py    # Main crawler script
├── README.md             # Project documentation
└── test.xlsx             # Input/output Excel file
```

## Usage

### Setup

1. **Prepare your Excel file**: Add website URLs to the first column of `test.xlsx`
2. **Set initial status**: Ensure the second column contains "null" for new entries that need to be processed
3. **Navigate to project directory**: Make sure you're in the directory containing `GoogleNewsSpider.py`

### Running the Script

```bash
python GoogleNewsSpider.py
```

### How it Works

1. **Input Processing**: Reads URLs from the first column of `test.xlsx`
2. **URL Validation**: For each URL with "null" status in the second column:
   - Constructs a Google News search query using the URL
   - Scrapes the Google News search results page
   - Checks if the original URL appears in the search results
3. **Status Update**: Updates the second column with:
   - "Approved" - if the URL is found in Google News results
   - "Not Approved" - if the URL is not found in Google News results
4. **File Save**: Automatically saves results back to `test.xlsx`

## Safety Features

- **Continuous Failure Monitoring**: Stops processing after 5 consecutive failures to prevent infinite loops
- **Exception Handling**: Gracefully handles network errors and parsing issues
- **Progress Logging**: Prints the current URL being processed to the console

## Important Notes & Best Practices

### Rate Limiting
- Google may identify the script as a bot and temporarily block requests
- If you encounter frequent exceptions, wait for some time before running the script again
- Consider adding delays between requests to avoid being detected as a bot

### Troubleshooting
- **"An exception occurred" errors**: This usually means Google has temporarily blocked your IP. Wait 10-15 minutes before retrying
- **No results found**: Ensure your URLs are properly formatted in the Excel file
- **File not found errors**: Make sure `test.xlsx` exists in the same directory as the script

### Recommendations
- Process URLs in small batches to avoid detection
- Monitor the console output for any error patterns
- Keep backups of your Excel file before running large batches

## Example Excel File Format

| Column A (URLs) | Column B (Status) |
|----------------|-------------------|
| example1.com   | null             |
| example2.com   | null             |
| example3.com   | Approved         |
| example4.com   | Not Approved     |

## Use Cases

This tool is particularly useful for:
- **Content Creators**: Verify if websites are recognized as legitimate news sources
- **Digital Marketers**: Check news source credibility for link building
- **Journalists**: Validate source authenticity
- **SEO Professionals**: Assess domain authority in news context

## Technical Details

The script uses Google News search with the following parameters:
- Safe search: Active
- Search type: News (tbm=nws)
- Custom search filters for more accurate results

## Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.

## License

This project is open source. Please use responsibly and in accordance with Google's Terms of Service.

