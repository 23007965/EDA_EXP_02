```
P PARTHIBAN
21222330145
```
# Exp - 2 Netflix Shows & Movies

## Aim

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

## Procedure / Algorithm

1)Load dataset (netflix_titles.csv).

2)Count movies vs TV shows.

3)Group by country → top contributors.

4)Create pivot table (release year vs type).

5)Visualize with bar & line charts.

## Program

###  Movies vs TV Shows
```python
count_by_type = df.groupby('type')['title'].count()
print("Count by Type:\n", count_by_type, "\n")
```
###  Country vs Type Pivot Table
```python
pivot_country_type = df.pivot_table(
index='country',
columns='type',
values='title',
aggfunc='count',
fill_value=0
)
# 🔹
 Add "Total" column and find max country
pivot_country_type['Total'] = pivot_country_type.sum(axis=1)
max_country = pivot_country_type['Total'].idxmax()  # country with most titles
max_count = pivot_country_type['Total'].max()       
# number of titles
print("Pivot Table (Country vs Type):\n", pivot_country_type.head(), "\n")
print(f"Largest Overall: {max_country} with {max_count} titles\n")
```
### Top 5 Directors
```python
top_directors = df['director'].value_counts().head(5)
print("Top 5 Directors:\n", top_directors, "\n")
```

### Yearly Trend of Additions (Movies vs TV Shows)
```python
trend=df.groupby(['year_added','type']).size().unstack(fill_value=0)
print("Yearly Trend by Type\n")
print(trend.head())
```

### Expand Genres
``` python
df_genre = (
df[['show_id','listed_in']]
.dropna()
.assign(listed_in=df['listed_in'].str.split(', '))
.explode('listed_in')
)
# Merge expanded genres back
df_expanded = df.merge(df_genre, on='show_id', how='left')
# Check merged columns
print("Columns after merge:\n", df_expanded.columns)
# Show sample of expanded genres
print("\nExpanded Genre Sample:\n",
df_expanded[['title','listed_in_y']].head())
# 🔹
 Top 5 Genres (extra useful for insights)
top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")
```
## Ouptut

## Result 
Helps Netflix in content planning & investments.
