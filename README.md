# Flipkart TV Web Scraping Script

This Python script performs web scraping on the Flipkart website to extract information about TV products. It utilizes the BeautifulSoup library for HTML parsing and the requests library for making HTTP requests. The scraped data is organized using Pandas and exported to an Excel file.

## Requirements

Make sure you have the following libraries installed:

- BeautifulSoup (bs4)
- requests
- pandas

Install them using the following command:


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
```bash
import bs4 
from bs4 import BeautifulSoup as bs
import requests
import pandas as pd 
products=[]              #List to store the name of the product
prices=[]                #List to store price of the product
ratings=[]              #List to store rating of the product  
os = []                  #List to store operating system
hd = []                  #List to store resolution  
def webscrape(link):
    page = requests.get(link)
    soup = bs(page.content, 'html.parser')
    #it gives us the visual representation of data
    # rating.text
    #get other details and specifications of the product
   #specification.text
   # price=soup.find('div',class_='_30jeq3 _1_WHN1')
    #print(price)
   # price.text
    for data in soup.findAll('div',class_='_3pLy-c row'):
        names=data.find('div', attrs={'class':'_4rR01T'})
        price=data.find('div', attrs={'class':'_30jeq3 _1_WHN1'})
        rating=data.find('div', attrs={'class':'_3LWZlK'})
        specification = data.find('div', attrs={'class':'fMghEO'})
        for each in specification:
            col=each.find_all('li', attrs={'class':'rgWa7D'})
            os_  = col[0].text
            hd_ = col[1].text
        products.append(names.text) # Add product name to list
        prices.append(price.text) # Add price to list
        os.append(os_) # Add operating system specifications to list
        hd.append(hd_) # Add resolution specifications to list
        ratings.append(rating.text)   #Add rating specifications to list
for i in range(1,5):
    if i==1:
        link='https://www.flipkart.com/search?q=tv&as=on&as-show=on&otracker=AS_Query_TrendingAutoSuggest_8_0_na_na_na&otracker1=AS_Query_TrendingAutoSuggest_8_0_na_na_na&as-pos=8&as-type=TRENDING&suggestionId=tv&requestId=9c9fa553-b7e5-454b-a65b-bbb7a9c74a29'
        webscrape(link)
    else:
        l1="&page={0}".format(i)
        link='https://www.flipkart.com/search?q=tv&as=on&as-show=on&otracker=AS_Query_TrendingAutoSuggest_8_0_na_na_na&otracker1=AS_Query_TrendingAutoSuggest_8_0_na_na_na&as-pos=8&as-type=TRENDING&suggestionId=tv&requestId=9c9fa553-b7e5-454b-a65b-bbb7a9c74a29'+l1
        webscrape(link)
df=pd.DataFrame({'Product Name':products,'OS':os,"Resolution":hd,'Price':prices,'Rating':ratings})
data=df.head(96)
data.to_excel("webS.xlsx",index='false')
