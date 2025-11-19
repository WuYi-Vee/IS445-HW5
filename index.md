
# Bigfoot Sightings Visualizations (HW5)

<p>
  <a href="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv" target="_blank">
    The Data
  </a>
  |
  <a href="https://github.com/WuYi-Vee/IS445-HW5/blob/main/Workbook.ipynb" target="_blank">
    The Analysis
  </a>
</p>

---

## Visualization 1: State rankings with season filter

<iframe src="bfro_chart1.html" width="100%" height="720" style="border:0;"></iframe>

### Description  

This bar chart shows how many Bigfoot reports are recorded in each U.S. state.  
The x-axis is the number of reports and the y-axis is the state abbreviation.  
I focus on one season at a time, so the viewer can see which states have the most reports in that season.

### Design choices – encodings  

I chose a bar chart because it is easy to compare counts between states.  
I encode the state abbreviation on the y-axis and the number of sightings on the x-axis.  
I also add tooltips so that when I hover over a bar, I can see the exact state, season, and count.  
This makes the chart friendly for exploration even for new users.

### Design choices – colormaps  

I use color to encode the region of each state (West, Midwest, South, Northeast, Other).  
Using regions as colors helps show geographic patterns without needing a map.  
For example, I can quickly see if western states have more reports than other regions.  
I keep the colors simple and distinct so that the legend is easy to read.

### Transformations  

In the notebook, I first cleaned the data after reading the CSV file from the URL.  
I dropped rows where the season value was missing or “Unknown”, because this category is not very informative.  
Then I parsed the `date` column into a numeric `year` column using Pandas.  
I also mapped full state names like “Alaska” to two-letter codes like “AK”,  
and grouped the data by state, season, and region to count the number of reports.  
This grouped table is used as the input for the first visualization.

---

## Visualization 2: Yearly trend and 3-year rolling average

<iframe src="bfro_chart2.html" width="100%" height="600" style="border:0;"></iframe>

### Description
This map shows the geographic locations of Bigfoot reports across the United States.  
Each circle marks a reported sighting using its latitude and longitude.  
The background uses a simple U.S. map so that viewers can understand where sightings cluster.

### Design choices – encodings
The longitude and latitude fields are mapped directly to x and y positions on the map.  
Each point is colored by the region of the state, matching the region colors used in the first plot.  
Tooltips show the state code, season, year, and title of the report when hovering over a point.  
This makes the map easy to explore without cluttering the figure with labels.

### Design choices – colormaps
I kept the background map light gray so that the colored points stand out clearly.  
The same region color scheme used in Visualization 1 creates consistency across both charts  
and makes the map easier to interpret.  

### Transformations
I reused the cleaned dataset from the first visualization.  
For this map I removed rows without valid latitude or longitude values,  
because they cannot be placed on a geographic map.  
No other transformations were needed, because the spatial location is stored directly in the dataset.

---

## Interactivity discussion

For the first plot, I added a dropdown menu for the season using an Altair parameter.  
The chart is filtered with `transform_filter(alt.datum.season == season_param)`  
so that only reports from the selected season are shown.  
This interaction makes the visualization more interesting and clearer,  
because the viewer can easily compare how state rankings change across different seasons  
without putting all seasons on the same crowded chart.

The second plot does not have a dropdown, but it still has interactive tooltips.  
When I hover over a point on the lines, I can see the exact year and the sighting values.  
