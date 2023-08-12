# Flipkart TV Web Scraping Script

This Python script performs web scraping on the Flipkart website to extract information about TV products. It utilizes the BeautifulSoup library for HTML parsing and the requests library for making HTTP requests. The scraped data is organized using Pandas and exported to an Excel file.

## Requirements

Make sure you have the following libraries installed:

- BeautifulSoup (bs4)
- requests
- pandas

Install them using the following command:

```bash
pip install beautifulsoup4 requests pandas

Import Libraries: Import the necessary libraries for web scraping and data manipulation.

Lists Initialization: Initialize empty lists to store extracted data.

Function Definition: Define the webscrape function to extract product information from a given URL. The function uses BeautifulSoup to parse HTML content and extract relevant data such as product names, prices, ratings, operating systems, and resolutions.

Loop for Pagination: Iterate through multiple pages of Flipkart search results. Generate the page URLs and call the webscrape function to extract data from each page.

DataFrame Creation: Create a Pandas DataFrame named df to organize the extracted data.

Data Truncation: Limit the DataFrame to the first 96 rows using the .head(96) method.

Excel Export: Export the truncated DataFrame to an Excel file named "webS.xlsx".
Usage
Replace the URL in the code with the Flipkart search URL of your choice.

Run the script using the following command:
python web_scraping_script.py
Note
Ensure that your web scraping activities comply with the website's terms of use and legal regulations.
Website structures may change over time, requiring adjustments to the code.

Replace `web_scraping_script.py` with the name of your Python script if it's different. This `README.md` format provides a clear overview of the purpose, requirements, usage, and precautions related to the web scraping script.

