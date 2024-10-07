### Project Description:
**Title:** Web Scraping and Data Visualization of Fortune 500 Companies Using Python and Power BI

1. **Objective:**
   - Collect data from a website (https://www.50pros.com/fortune500) about Fortune 500 companies.
   - Clean and transform the data using Power BI.
   - Create visualizations in Power BI for meaningful insights.

2. **Steps:**

   **Step 1: Web Scraping using Python**
   - Collected the data from the website using Python and libraries such as `requests` and `BeautifulSoup`.
   - Extracted relevant data fields, such as company name, rank, revenue, and other key metrics.

   **Step 2: Loading Data into Power BI**
   - Exported the scraped data into a CSV file format.
   - Loaded the CSV file into Power BI for further processing.

   **Step 3: Data Cleaning and Transformation in Power BI**
   - Used Power BI's Power Query Editor to handle missing values, rename columns, and ensure consistency in data types.
   - Filtered out unnecessary fields to focus on key metrics, such as revenue, profit, and rank.

   **Step 4: Data Visualization in Power BI**
   - Created interactive dashboards and reports using Power BI visuals like bar charts, line charts, and tables.
   - Designed filters and slicers to enable users to explore different aspects of the data (e.g., companies by industry, revenue growth trends).

3. **Conclusion:**
   - Visualized the trends and insights from the Fortune 500 data to analyze company performance based on revenue, profit, and industry type.

---

### Python Web Scraping Code:

```python
import requests
from bs4 import BeautifulSoup
import csv

url = 'https://www.50pros.com/fortune500'

response = requests.get(url)

if response.status_code == 200:
    soup = BeautifulSoup(response.content, 'html.parser')
    table = soup.find('table')  # Adjust based on the structure of the page
    data = []
    for row in table.find_all('tr'):
        cols = row.find_all('td')
        cols = [col.text.strip() for col in cols]
        if cols:
            data.append(cols)
    csv_file = 'fortune500_data.csv'
    with open(csv_file, mode='w', newline='', encoding='utf-8') as file:
        writer = csv.writer(file)
        writer.writerow(['Rank', 'Company', 'Revenue', 'Profit', 'Employees'])
        writer.writerows(data)

    print(f"Data successfully scraped and saved to {csv_file}")
else:
    print(f"Failed to retrieve data. Status code: {response.status_code}")
```
