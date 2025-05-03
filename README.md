# 📺 Netflix Data Analysis

This project involves exploratory data analysis (EDA) on the Netflix Movies and TV Shows dataset. The objective is to understand content trends, gain business insights, and discover patterns in Netflix’s catalog using data analysis and visualization techniques.

![](https://github.com/psyccho00/Netflix-Data_Analysis_with_Pandas/blob/main/netflix.png)

## 📊 Project Overview

Netflix is one of the leading streaming platforms globally, offering a wide range of movies and TV shows. This project analyzes various attributes such as release year, genre, country of origin, ratings, and more to identify trends and answer business-related questions using Python.

The notebook performs:
- Data cleaning and preprocessing
- Descriptive statistics
- Visual analysis of key variables
- Insight generation from the data

---

## 🗂️ Dataset

**Source:** [Netflix Dataset on Kaggle](https://www.kaggle.com/shivamb/netflix-shows)

**File used:** `mymoviedb.csv`

### Key Columns:
- `title`: Title of the show
- `director`: Director name(s)
- `cast`: Cast member(s)
- `country`: Country of origin
- `date_added`: Date the content was added to Netflix
- `release_year`: Year the content was released
- `rating`: Content rating (TV-MA, PG, etc.)
- `duration`: Duration of the content
- `listed_in`: Genre(s)
- `description`: Summary description

---

## 📌 Objectives

- Identify the content distribution between movies and TV shows
- Discover the most frequent content genres
- Analyze release year trends
- Examine country-wise content production
- Explore how Netflix's catalog has evolved over time
- Identify top contributing directors and actors

---

## 🛠️ Libraries Used

- **pandas** – Data manipulation and analysis
- **numpy** – Numerical operations
- **seaborn** – Statistical data visualization
- **matplotlib** – Plotting graphs

---

## 🧾 Code Explanation

### 1. Importing Required Libraries
```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```

### 2. Reading the Dataset
```python
data = pd.read_csv('mymoviedb.csv', lineterminator='\n')
```

### 3. Inspecting the Dataset
```python
data.info()
data.duplicated().sum()
data.describe()
```

### 4. Formatting Release Dates
```python
data['Release_Date'] = pd.to_datetime(data['Release_Date'])
data['Release_Date'] = data['Release_Date'].dt.year
```

### 5. Dropping Unnecessary Columns
```python
data.drop(['Overview','Original_Language','Poster_Url'], axis=1, inplace=True)
```

### 6. Categorizing Vote Averages
```python
def catigorize_col(data, col, labels):
    edges = [data[col].describe()['min'],
             data[col].describe()['25%'],
             data[col].describe()['50%'],
             data[col].describe()['75%'],
             data[col].describe()['max']]
    data[col] = pd.cut(data[col], edges, labels=labels, duplicates='drop')
    return data

labels = ['not_popular', 'below_avg', 'average', 'popular']
catigorize_col(data, 'Vote_Average', labels)
data['Vote_Average'].unique()
```

### 7. Missing Value Detection
```python
data.isna().sum()
```

### 8. Value Counts and Grouping
```python
data['Vote_Average'].value_counts()
data.groupby('Genre')['Vote_Average'].value_counts()
```

### 9. Most Frequent Genre Visualization
```python
sns.catplot( y='Genre', data = data, kind = 'count', order = data['Genre'].value_counts().index)
plt.title('Genre column distribution')
plt.show()
```

### 10. Popularity by Genre
```python
data[data['Popularity'] == data['Popularity'].max()][['Title','Popularity','Genre']]
```

### 11. Vote Average Distribution
```python
sns.catplot( y='Vote_Average' , data=data , kind='count' , order=data['Vote_Average'].value_counts().index )
plt.title('votes destribution')
plt.show()
```

### 12. Yearly Movie Releases
```python
data['Release_Date'].hist()
plt.title('Release_Date column distribution')
plt.show()
```

---

## 🛠️ Tools & Technologies

- **Jupyter Notebook**
- **Pandas** – Data manipulation
- **Matplotlib & Seaborn** – Data visualization

---

## 📈 Key Insights

Some of the main insights generated through the analysis:
- Netflix offers more movies than TV shows
- The majority of the content was released after 2010
- The United States produces the highest amount of content
- TV-MA is the most frequent rating
- Drama is the most common genre listed
- 2019 saw a peak in the number of new titles added

---

## ▶️ Getting Started

To run this project locally:

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/netflix-analysis.git
   cd netflix-analysis
   ```

2. Install the dependencies:
   ```bash
   pip install pandas matplotlib seaborn jupyter
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook Netflix.ipynb
   ```

---

## 📌 Project Structure

```
📦 netflix-analysis/
├── Netflix.ipynb        # Main notebook with code and visualizations
├── README.md            # Project documentation
└── netflix_titles.csv   # Dataset (optional; or link to Kaggle)
```

---

## 📄 License

This project is licensed under the MIT License. Feel free to use, modify, and distribute it with attribution.

---

## 🙌 Acknowledgements

- Dataset provided by [Kaggle - Shivam Bansal](https://www.kaggle.com/shivamb/netflix-shows)
- Inspired by the growing importance of data-driven content strategy in the entertainment industry

---

## 👨‍💻 Author

Made by [@psyccho00](https://github.com/psyccho00)

If you liked this, please ⭐ the repo!

*Happy Analyzing! 🍕*
