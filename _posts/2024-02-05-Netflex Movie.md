# Investing Netflix Movies and Guest Stars in the Office

공부: Python (https://www.notion.so/Python-a4e48bf8fdd94e8b8c667b2562637862?pvs=21)
과목: Datacamp
세부계획 계획 비율: 0
Status: Done

[제목 없는 데이터베이스](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/%E1%84%8C%E1%85%A6%E1%84%86%E1%85%A9%E1%86%A8%20%E1%84%8B%E1%85%A5%E1%86%B9%E1%84%82%E1%85%B3%E1%86%AB%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%E1%84%87%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%203bc4a9ec43274fd494d429a002f70ff0.csv)

[https://github.com/EhabR98/Investigating-Netflix-Movies-and-Guest-Stars-in-The-Office](https://github.com/EhabR98/Investigating-Netflix-Movies-and-Guest-Stars-in-The-Office)

# **1. Loading your friend's data into a dictionary**

![https://assets.datacamp.com/production/project_1237/img/netflix.jpg](https://assets.datacamp.com/production/project_1237/img/netflix.jpg)

Netflix! What started in 1997 as a DVD rental service has since exploded into the largest entertainment/media company by [market capitalization](https://www.marketwatch.com/story/netflix-shares-close-up-8-for-yet-another-record-high-2020-07-10), boasting over 200 million subscribers as of [January 2021](https://www.cbsnews.com/news/netflix-tops-200-million-subscribers-but-faces-growing-challenge-from-disney-plus/).

Given the large number of movies and series available on the platform, it is a perfect opportunity to flex our data manipulation skills and dive into the entertainment industry. Our friend has also been brushing up on their Python skills and has taken a first crack at a CSV file containing Netflix data. For their first order of business, they have been performing some analyses, and they believe that the average duration of movies has been declining.

As evidence of this, they have provided us with the following information. For the years from 2011 to 2020, the average movie durations are 103, 101, 99, 100, 100, 95, 95, 96, 93, and 90, respectively.

If we're going to be working with this data, we know a good place to start would be to probably start working with `pandas`. But first we'll need to create a DataFrame from scratch. Let's start by creating a Python object covered in [Intermediate Python](https://learn.datacamp.com/courses/intermediate-python): a dictionary!

```python
# Create the years and durations lists
years = [2011,2012,2013,2014,2015,2016,2017,2018,2019,2020]
durations = [103, 101, 99, 100, 100, 95, 95, 96, 93, 90]

# Create a dictionary with the two lists
movie_dict = {"years": years, 
             "durations": durations}

# Print the dictionary
movie_dict
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled.png)

# 2. Creating a DataFrame from a dictionary

To convert our dictionary `movie_dict` to a `pandas` DataFrame, we will first need to import the library under its usual alias. We'll also want to inspect our DataFrame to ensure it was created correctly. Let's perform these steps now.

```python
# Import pandas under its usual alias
import pandas as pd

# Create a DataFrame from the dictionary
durations_df = pd.DataFrame(movie_dict)

# Print the DataFrame
print(durations_df)
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%201.png)

# 3. A visual inspection of our data

Alright, we now have a `pandas` DataFrame, the most common way to work with tabular data in Python. Now back to the task at hand. We want to follow up on our friend's assertion that movie lengths have been decreasing over time. A great place to start will be a visualization of the data.

Given that the data is continuous, a line plot would be a good choice, with the dates represented along the x-axis and the average length in minutes along the y-axis. This will allow us to easily spot any trends in movie durations. There are many ways to visualize data in Python, but `matploblib.pyplot` is one of the most common packages to do so.

*Note: In order for us to correctly test your plot, you will need to initalize a `matplotlib.pyplot` Figure object, which we have already provided in the cell below. You can continue to create your plot as you have learned in Intermediate Python.*

```python
# Import matplotlib.pyplot under its usual alias and create a figure
import matplotlib.pyplot as plt
fig = plt.figure()

# Draw a line plot of release_years and durations
plt.plot(durations_df['years'],durations_df['durations'])
plt.xlabel('Release years')
plt.ylabel('Durations')

# Create a title
plt.title('Netflix Movie Durations 2011-2020')

# Show the plot
plt.show()
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%202.png)

# 4. Loading the rest of the data from CSV

Well, it looks like there is something to the idea that movie lengths have decreased over the past ten years! But equipped only with our friend's aggregations, we're limited in the further explorations we can perform. There are a few questions about this trend that we are currently unable to answer, including:

1. What does this trend look like over a longer period of time?
2. Is this explainable by something like the genre of entertainment?

Upon asking our friend for the original CSV they used to perform their analyses, they gladly oblige and send it. We now have access to the CSV file, available at the path `"datasets/netflix_data.csv"`. Let's create another DataFrame, this time with all of the data. Given the length of our friend's data, printing the whole DataFrame is probably not a good idea, so we will inspect it by printing only the first five rows.

```python
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Print the first five rows of the DataFrame
print(netflix_df.head())
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%203.png)

# 5. Filtering for movies!

Okay, we have our data! Now we can dive in and start looking at movie lengths.

Or can we? Looking at the first five rows of our new DataFrame, we notice a column `type`. Scanning the column, it's clear there are also TV shows in the dataset! Moreover, the `duration` column we planned to use seems to represent different values depending on whether the row is a movie or a show (perhaps the number of minutes versus the number of seasons)?

Fortunately, a DataFrame allows us to filter data quickly, and we can select rows where `type` is `Movie`. While we're at it, we don't need information from all of the columns, so let's create a new DataFrame `netflix_movies` containing only `title`, `country`, `genre`, `release_year`, and `duration`.

Let's put our data subsetting skills to work!

```python
# Subset the DataFrame for type "Movie"
netflix_df_movies_only = netflix_df[netflix_df['type']=='Movie']

# Select only the columns of interest
netflix_movies_col_subset = netflix_df_movies_only[['title', 'country', 'genre', 'release_year', 'duration']]

# Print the first five rows of the new DataFrame
print(netflix_movies_col_subset.head())
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%204.png)

# 6. Creating a scatter plot

Okay, now we're getting somewhere. We've read in the raw data, selected rows of movies, and have limited our DataFrame to our columns of interest. Let's try visualizing the data again to inspect the data over a longer range of time.

This time, we are no longer working with aggregates but instead with individual movies. A line plot is no longer a good choice for our data, so let's try a scatter plot instead. We will again plot the year of release on the x-axis and the movie duration on the y-axis.

*Note: Although not taught in Intermediate Python, we have provided you the code `fig = plt.figure(figsize=(12,8))` to increase the size of the plot (to help you see the results), as well as to assist with testing. For more information on how to create or work with a `matplotlib` `figure`, refer to the [documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.figure.html).*

```python
# Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset['release_year'], netflix_movies_col_subset['duration'])

# Create a title
plt.title('Movie Duration by Year of Release')

# Show the plot
plt.show()
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%205.png)

# 7. Digging deeper

This is already much more informative than the simple plot we created when our friend first gave us some data. We can also see that, while newer movies are overrepresented on the platform, many short movies have been released in the past two decades.

Upon further inspection, something else is going on. Some of these films are under an hour long! Let's filter our DataFrame for movies with a `duration` under 60 minutes and look at the genres. This might give us some insight into what is dragging down the average.

```python
# Filter for durations shorter than 60 minutes
short_movies = netflix_movies_col_subset[netflix_movies_col_subset['duration']<60]

# Print the first 20 rows of short_movies
short_movies.head(20)
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%206.png)

# 8. Marking non-feature films

Interesting! It looks as though many of the films that are under 60 minutes fall into genres such as "Children", "Stand-Up", and "Documentaries". This is a logical result, as these types of films are probably often shorter than 90 minute Hollywood blockbuster.

We could eliminate these rows from our DataFrame and plot the values again. But another interesting way to explore the effect of these genres on our data would be to plot them, but mark them with a different color.

In Python, there are many ways to do this, but one fun way might be to use a loop to generate a list of colors based on the contents of the `genre` column. Much as we did in Intermediate Python, we can then pass this list to our plotting function in a later step to color all non-typical genres in a different color!

*Note: Although we are using the basic colors of red, blue, green, and black, `matplotlib` has many named colors you can use when creating plots. For more information, you can refer to the documentation [here](https://matplotlib.org/stable/gallery/color/named_colors.html)!*

```python
# Define an empty list
colors = []

# Iterate over rows of netflix_movies_col_subset
for lab, row in netflix_movies_col_subset.iterrows() :
    if row['genre'] == 'Children':
        colors.append('red')
    elif row['genre'] == 'Documentaries' :
        colors.append('blue')
    elif row['genre'] == 'Stand-Up':
        colors.append('green')
    else:
        colors.append('black')
        
# Inspect the first 10 values in your list        
print(colors[:11])
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%207.png)

# 9. Plotting with color!

Lovely looping! We now have a `colors` list that we can pass to our scatter plot, which should allow us to visually inspect whether these genres might be responsible for the decline in the average duration of movies.

This time, we'll also spruce up our plot with some additional axis labels and a new theme with `plt.style.use()`. The latter isn't taught in Intermediate Python, but can be a fun way to add some visual flair to a basic `matplotlib` plot. You can find more information on customizing the style of your plot [here](https://matplotlib.org/stable/tutorials/introductory/customizing.html)!

```python
# Set the figure style and initalize a new figure
plt.style.use('fivethirtyeight')
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus release_year
plt.scatter(netflix_movies_col_subset['release_year'], netflix_movies_col_subset['duration'], c=colors)

# Create a title and axis labels
plt.title("Movie duration by year of release")
plt.xlabel('Release year')
plt.ylabel('Duration (min)')

# Show the plot
plt.show()
```

![Untitled](Investing%20Netflix%20Movies%20and%20Guest%20Stars%20in%20the%20Of%2032f8dbc588af44f3b0110feaa56af8fe/Untitled%208.png)

# 10. What next?

Well, as we suspected, non-typical genres such as children's movies and documentaries are all clustered around the bottom half of the plot. But we can't know for certain until we perform additional analyses.

Congratulations, you've performed an exploratory analysis of some entertainment data, and there are lots of fun ways to develop your skills as a Pythonic data scientist. These include learning how to analyze data further with statistics, creating more advanced visualizations, and perhaps most importantly, learning more advanced ways of working with data in `pandas`. This latter skill is covered in our fantastic course [Data Manipulation with pandas](https://sessions.datacamp.com/proxy/absolute/419d1e03-4331-48cf-b9d3-5af88b634af8/notebooks/production/users/11307609/d2snego67q/notebooks/www.datacamp.com/courses/data-manipulation-with-pandas).

We hope you enjoyed this application of the skills learned in Intermediate Python, and wish you all the best on the rest of your journey!

```python
# Are we certain that movies are getting shorter?
are_movies_getting_shorter = 'No'
```
