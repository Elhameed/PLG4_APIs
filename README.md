# *Web Scraping and APIs Assignment PLD4*

This repository contains the code and resources for a Api Intranet Task 0, web scraping and APIs assignment. The tasks involve scraping tabular data from ScrapethisSite, scraping product images and labels from Amazon, and saving the results into CSV and image formats.

## *Table of Contents*
- [Overview](#overview)
- [Project Structure](#project-structure)
- [API Task](#api-task)
- [Data Scraping Process](#data-scraping-process)
  - [Task 1: Scraping ScrapethisSite](#task-1-scraping-scrapethissite)
  - [Task 2: Scraping Amazon Product Categories](#task-2-scraping-amazon-product-categories)
- [How to Run the Project](#how-to-run-the-project)

---

## *Overview*

This project focuses on:
1. *Web Scraping:* Extracting data from a webpage using BeautifulSoup.
2. *APIs:* Making HTTP requests to scrape product data from Amazon.com and implement a function that queries the SWAP API.
3. *Data Storage:* Storing scraped data in CSV files and saving product images from Amazon.

### *Objectives*
- Implement a funnction to return ships from the SWAP API that can hold a given numbeer of passengers.
- Scrape tabular data from [ScrapethisSite](https://www.scrapethissite.com/pages/forms/).
- Scrape product images and names from at least 5 product categories on Amazon.
- Save scraped data in CSV format and product images in a local folder.
  
### *Tools Used*
- Python
- BeautifulSoup (for web scraping)
- Pandas (for data handling)
- Requests (for making HTTP requests)
- Jupyter Notebook

---

## *Project Structure*

The repository is organized as follows:

    📁 PLG4_APIs/
    ├── ...
    ├── 📁 Intranet_Task-0/  
    │   ├── 0-main.py 
    │   ├── 0-passengers.py             
    │   └── ...  
    ├── 📁 images/   
    │   ├── consoles_1.jpg  
    │   ├── handbags_1.jpg     
    │   ├── keyboards_1.jpg     
    │   ├── printers_1.jpg    
    │   ├── wigs_1.jpg    
    │   └── ...  
    ├── README.md
    ├── scrape1.csv  
    ├── web_scraping.ipynb
    └── ...

---

## **API Task**

### **Using the SWAPI API**

In addition to the web scraping tasks, we implemented a method to retrieve a list of starships that can hold a specified number of passengers using the [SWAPI API](https://swapi.dev/).

#### **Function: `availableShips(passengerCount)`**

- **Prototype:** `def availableShips(passengerCount):`
- **Description:** This function returns a list of starship names that can hold the given number of passengers, considering pagination.

```python
import requests

def availableShips(passengerCount):
    """
    Returns a list of ships that can hold a specified number of passengers.
    """
    url = "https://swapi-api.alx-tools.com/api/starships/"
    ships = []
    while url:
        response = requests.get(url)
        data = response.json()
        for ship in data["results"]:
            if (
                ship["passengers"] != "n/a"
                and ship["passengers"] != "unknown"
                and ship["passengers"] != "0"
                and ship["passengers"] != "none"
            ):
                ship["passengers"] = ship["passengers"].replace(",", "")
                if int(ship["passengers"]) >= passengerCount:
                    ships.append(ship["name"])
        url = data["next"]
    return ships

Example Usage:
```
# Get a list of ships that can hold at least 50 passengers
available_ships = availableShips(50)
print(available_ships)

```
---

## **Data Scraping Process**

### **Task 1: Scraping ScrapethisSite**

In this task, we scrape tabular data from the [ScrapethisSite forms page](https://www.scrapethissite.com/pages/forms/) using BeautifulSoup. The scraped data is stored in a CSV file (`scraped_data.csv`).

- **URL:** https://www.scrapethissite.com/pages/forms/
- **Methodology:** 
  - We loop through the pages, parse the HTML table, and extract the rows.
  - The data is saved in `scraped_data.csv`.

### **Task 2: Scraping Amazon Product Categories**

For the second task, we scrape product images and labels from Amazon in five different categories: **consoles, handbags, printers, wigs, and keyboards**.

- **URL Example:** https://www.amazon.com/s?k=consoles
- **Methodology:** 
  - We make requests to each Amazon product category page.
  - For each category, the first product image and label are saved locally in the `images/` directory.
  - **Note:** Amazon's HTML structure may change, so this is a basic demonstration using `BeautifulSoup`.

---


