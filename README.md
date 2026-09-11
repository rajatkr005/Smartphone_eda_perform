# 📱 Smartphone EDA & Web Scraping Project

An end-to-end **Smartphone Data Analysis project** based on smartphone data collected from **Smartprix**.

This project demonstrates a complete data science workflow starting from **web scraping**, followed by **data extraction, data cleaning, feature engineering, exploratory data analysis (EDA), visualization, and correlation analysis**.

---

## 🚀 Project Overview

The goal of this project is to collect smartphone information from Smartprix and analyze the relationship between smartphone specifications, ratings, and prices.

The project is divided into two major parts:

1. **Web Scraping** – Collect smartphone information from Smartprix using Selenium.
2. **Data Analysis** – Clean, transform, visualize, and analyze the scraped smartphone data using Python.

### Workflow

```text
Smartprix Website
       ↓
Selenium Web Scraping
       ↓
smartprix.html
       ↓
BeautifulSoup / Pandas
       ↓
Data Cleaning
       ↓
Feature Engineering
       ↓
Exploratory Data Analysis
       ↓
Visualization
       ↓
Correlation Analysis
       ↓
Insights
```

---

## 📂 Project Files

```text
Smartphone_eda/
│
├── smartprix.py
├── smartprix.html
├── Smartphone.xlsx
├── Eda_perform.ipynb
└── README.md
```

### File Description

| File                | Description                                  |
| ------------------- | -------------------------------------------- |
| `smartprix.py`      | Selenium web-scraping script                 |
| `smartprix.html`    | HTML page saved after scraping               |
| `Smartphone.xlsx`   | Cleaned smartphone dataset used for analysis |
| `Eda_perform.ipynb` | Data cleaning, feature engineering and EDA   |
| `README.md`         | Project documentation                        |

---

## 🌐 1. Web Scraping

The smartphone data was collected from Smartprix using **Selenium WebDriver**.

The scraper:

* Opens the Smartprix mobile phones page.
* Applies the required filters.
* Loads additional smartphone records.
* Continues loading until no new content is available.
* Retrieves the complete HTML source.
* Saves the HTML locally as `smartprix.html`.

The scraper uses Selenium's Chrome WebDriver and XPath selectors to interact with the Smartprix page.

### Scraping Code

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
import time

s = Service("path/to/chromedriver.exe")

driver = webdriver.Chrome(service=s)

driver.get("https://www.smartprix.com/mobiles")

time.sleep(15)

# Apply filters
driver.find_element(
    by=By.XPATH,
    value='//*[@id="app"]/main/aside/div/div[5]/div[2]/label[1]/input'
).click()

time.sleep(15)

driver.find_element(
    by=By.XPATH,
    value='//*[@id="app"]/main/aside/div/div[5]/div[2]/label[2]/input'
).click()

time.sleep(15)
```

The script then repeatedly loads more products and compares the page height to determine when no additional products are being loaded.

Finally, the generated HTML is saved:

```python
html = driver.page_source

with open("smartprix.html", "w", encoding="utf-8") as f:
    f.write(html)
```

---

# 📊 2. Dataset

The final Excel dataset contains:

* **889 smartphone records**
* **13 columns**

### Main Columns

| Column      | Description                         |
| ----------- | ----------------------------------- |
| `model`     | Smartphone model name               |
| `price`     | Smartphone price                    |
| `rating`    | Smartphone rating                   |
| `sim`       | SIM and connectivity specifications |
| `processor` | Processor information               |
| `ram`       | RAM and internal storage            |
| `battery`   | Battery and charging information    |
| `display`   | Display specifications              |
| `camera`    | Camera specifications               |
| `card`      | Memory-card information             |
| `os`        | Operating system                    |

Example records contain specifications such as RAM, internal storage, processor cores and speed, battery capacity, charging speed, display resolution, refresh rate, camera specifications, and operating system.

---

# 🧹 3. Data Cleaning

The scraped data was not immediately ready for analysis because smartphone specifications were stored as text and contained multiple pieces of information in the same column.

The cleaning process included:

* Removing unwanted characters from price.
* Converting price into numerical format.
* Handling missing ratings.
* Standardizing brand names.
* Cleaning processor information.
* Separating RAM and internal storage.
* Extracting battery capacity.
* Extracting charging speed.
* Extracting display size.
* Extracting display resolution.
* Extracting refresh rate.
* Processing camera specifications.
* Processing operating-system information.
* Handling memory-card information.
* Identifying inconsistent or misplaced values from the scraped HTML.

---

# ⚙️ 4. Feature Engineering

One of the main parts of the project was converting unstructured smartphone specifications into useful analytical features.

### 📱 Brand

The smartphone brand was extracted from the model name.

### 📶 Connectivity

Features were created for:

* 5G
* NFC
* IR Blaster

### ⚡ Processor

Processor information was transformed into features such as:

* Processor brand
* Number of cores
* Processor speed

### 💾 Memory

The RAM column was separated into:

* RAM capacity
* Internal storage

### 🔋 Battery

Battery specifications were converted into:

* Battery capacity
* Fast-charging availability
* Charging capacity

### 🖥️ Display

Display specifications were transformed into:

* Screen size
* Resolution
* Refresh rate
* Resolution category

### 📷 Camera

Camera specifications were transformed into:

* Front camera information
* Rear camera information
* Number of front cameras
* Number of rear cameras
* Camera resolution

### 💿 Storage Expansion

Memory-card information was used to identify:

* Whether expandable storage is supported.
* Maximum expandable storage capacity.

---

# 📈 5. Exploratory Data Analysis

The cleaned dataset was analyzed using Python visualization and statistical techniques.

The EDA covers:

### Brand Analysis

* Smartphone count by brand
* Distribution of smartphone brands
* Average price by brand
* Comparison of major smartphone brands

### Price Analysis

* Price distribution
* Mean and median price
* Minimum and maximum price
* Box plot
* Histogram
* KDE distribution
* Outlier analysis
* Price skewness

### Rating Analysis

* Rating distribution
* Mean rating
* Median rating
* Minimum and maximum ratings
* Relationship between rating and price

### Hardware Analysis

Analysis of:

* RAM
* Internal storage
* Processor speed
* Processor cores
* Battery capacity
* Charging capacity
* Screen size
* Refresh rate
* Camera specifications

### Feature Analysis

Analysis of:

* 5G
* NFC
* IR Blaster
* Expandable storage
* Operating systems
* Camera configurations

---

# 📊 6. Correlation Analysis

Correlation analysis was performed to understand the relationship between smartphone price and numerical features.

Some of the stronger relationships observed in the analysis include:

| Feature                | Approx. Correlation with Price |
| ---------------------- | -----------------------------: |
| Processor Speed        |                           0.80 |
| Internal Memory        |                           0.74 |
| RAM                    |                           0.69 |
| Rating                 |                           0.64 |
| NFC                    |                           0.54 |
| Front Camera Count     |                           0.48 |
| Rear Camera Resolution |                           0.37 |
| Charging Capacity      |                           0.32 |
| Rear Camera Count      |                           0.32 |
| 5G                     |                           0.30 |
| Screen Size            |                           0.30 |

> **Important:** Correlation shows association between variables. It does not prove that one feature causes a smartphone to have a higher price.

---

# 🧠 7. Missing Value Analysis

Missing values were investigated as part of the data-cleaning process.

The final Excel dataset contains missing values primarily in the **rating** column.

Additional missing values may occur in engineered variables depending on whether the original smartphone specification was available.

A **KNN Imputer** was also used during the analysis to investigate the effect of numerical missing-value imputation on correlations.

---

# 🔎 8. Key Insights

Some important observations from the analysis include:

* Smartphone prices have a **right-skewed distribution**, with a smaller number of expensive premium smartphones.
* **Processor speed** has one of the strongest relationships with smartphone price.
* **RAM and internal storage** are strongly associated with smartphone price.
* Higher-rated smartphones tend to have higher prices in this dataset.
* Premium smartphone features such as **NFC and 5G** show positive associations with price.
* Refresh rate, display specifications, camera specifications, battery capacity, and charging speed provide useful ways to compare smartphones.
* Web-scraped data requires significant cleaning because specifications may not always appear consistently in the expected HTML structure.

---

# 🛠️ Technologies Used

```text
Python
│
├── Selenium
├── BeautifulSoup
├── Pandas
├── NumPy
├── Matplotlib
├── Seaborn
└── Scikit-learn
```

### Libraries

| Library          | Usage                               |
| ---------------- | ----------------------------------- |
| Selenium         | Web scraping and browser automation |
| BeautifulSoup    | HTML parsing                        |
| Pandas           | Data manipulation and analysis      |
| NumPy            | Numerical operations                |
| Matplotlib       | Data visualization                  |
| Seaborn          | Statistical visualization           |
| Scikit-learn     | KNN imputation                      |
| OpenPyXL         | Excel file handling                 |
| Jupyter Notebook | Data analysis                       |

---

# ▶️ How to Run

## 1. Clone the Repository

```bash
git clone <your-repository-url>
```

## 2. Install Dependencies

```bash
pip install selenium beautifulsoup4 pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
```

## 3. Run the Scraper

Before running `smartprix.py`, make sure ChromeDriver is installed and its path is correctly configured.

Update:

```python
s = Service("path/to/chromedriver.exe")
```

Then run:

```bash
python smartprix.py
```

The script will generate:

```text
smartprix.html
```

The scraper saves the browser's final page source into this HTML file.

## 4. Run the Analysis

Open:

```text
Eda_perform.ipynb
```

using Jupyter Notebook or JupyterLab.

```bash
jupyter notebook
```

Then run the notebook cells sequentially.

---

# 📌 Project Skills Demonstrated

This project demonstrates practical experience with:

* Web Scraping
* Selenium
* BeautifulSoup
* HTML Parsing
* Data Collection
* Data Cleaning
* Data Quality Assessment
* Missing Value Handling
* Feature Engineering
* Exploratory Data Analysis
* Statistical Analysis
* Data Visualization
* Correlation Analysis
* Python
* Pandas
* NumPy
* Scikit-learn

---

# 🔮 Future Improvements

Possible extensions of this project include:

* Automating the complete scraping pipeline.
* Handling dynamic web pages more robustly.
* Creating reusable scraping functions.
* Improving data validation for incorrectly positioned specifications.
* Building an interactive dashboard using **Power BI, Tableau, or Plotly**.
* Building a smartphone price prediction model.
* Creating a smartphone recommendation system.
* Comparing brands across different price ranges.
* Deploying the analysis as a web application.

---

# 👨‍💻 Author

## Rajat Kumar

**B.Sc. IT Graduate | Aspiring Data Scientist**

### Skills

`Python` `SQL` `Pandas` `NumPy` `Data Cleaning` `EDA` `Data Visualization` `Web Scraping`

---

## ⭐ If you find this project useful

Feel free to ⭐ the repository and explore the analysis.

Feedback and suggestions are welcome!
