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

### How many titles (Movies vs. TV Shows) are there?
```python
count_by_type = df.groupby('type')['title'].count()
print("Count by Type:\n", count_by_type, "\n")
```
### What’s the distribution of content types across countries?
```python

```
### What are the top 5 directors by number of titles?
```python
top_directors = df['director'].value_counts().head(5)
print("Top 5 Directors:\n", top_directors, "\n")
```

### Monthly trends in additions (by type)?
```python
trend=df.groupby(['year_added','type']).size().unstack(fill_value=0)
print("Yearly Trend by Type\n")
print(trend.head())
```

### Merge expanded genre/cast tables back to main DF for combined insights.
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
