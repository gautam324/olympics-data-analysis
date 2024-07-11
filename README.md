# Olympics Analysis Project

This project is an analysis tool for the Summer Olympics, utilizing data from athlete events and NOC regions to provide insightful visualizations and statistics through a Streamlit web application.

## Dataset
Dataset Link: https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results


## Project Structure

- **preprocessor.py**: Handles data preprocessing tasks.
- **helper.py**: Contains various helper functions for data manipulation and analysis.
- **app.py**: Streamlit application to visualize the Olympics data.

## Data

- `athlete_events.csv`: Contains information about athletes and their performance in different events.
- `noc_regions.csv`: Maps NOC (National Olympic Committees) codes to their respective regions.

## Preprocessing

The `preprocessor.py` script filters the data for the Summer Olympics, merges it with region information, drops duplicates, and performs one-hot encoding on the Medal column.

```python
import pandas as pd

def preprocess(df, region_df):
    df = df[df['Season'] == 'Summer']
    df = df.merge(region_df, on='NOC', how='left')
    df.drop_duplicates(inplace=True)
    df = pd.concat([df, pd.get_dummies(df['Medal'])], axis=1)
    return df
```

## Helper Functions

The `helper.py` script provides several functions for data manipulation and analysis:

- `fetch_medal_tally(df, year, country)`: Fetches the medal tally for a given year and country.
- `country_year_list(df)`: Returns lists of unique years and countries in the dataset.
- `data_over_time(df, col)`: Analyzes data over time for a specified column.
- `most_successful(df, sport)`: Lists the most successful athletes in a specified sport.
- `yearwise_medal_tally(df, country)`: Provides a yearly medal tally for a specified country.
- `country_event_heatmap(df, country)`: Creates a heatmap of events won by a specified country.
- `most_successful_countrywise(df, country)`: Lists the most successful athletes for a specified country.
- `weight_v_height(df, sport)`: Analyzes weight vs height distribution for athletes in a specified sport.
- `men_vs_women(df)`: Compares male vs female participation over the years.

## Streamlit Application

The `app.py` script sets up a Streamlit web application to visualize the processed Olympics data. Users can select different analysis options from the sidebar, such as Medal Tally, Overall Analysis, Country-wise Analysis, and Athlete-wise Analysis.

### Medal Tally

Displays the medal tally based on the selected year and country.

### Overall Analysis

Provides top statistics and visualizations for editions, hosts, sports, events, athletes, and participating nations over the years.

### Country-wise Analysis

Shows the medal tally, event performance, top athletes, and heatmaps for a selected country.

### Athlete-wise Analysis

Analyzes age distribution, weight vs height, and male vs female participation trends for athletes.

## How to Run

1. Ensure you have Python and necessary libraries installed. You can install required libraries using:
   ```sh
   pip install pandas streamlit plotly matplotlib seaborn
   ```
2. Place the data files `athlete_events.csv` and `noc_regions.csv` in the same directory.
3. Run the Streamlit application:
   ```sh
   streamlit run app.py
   ```

## Conclusion

This project provides a comprehensive tool to analyze Summer Olympics data, offering insights into medal distributions, athlete performance, and participation trends across different countries and sports.


