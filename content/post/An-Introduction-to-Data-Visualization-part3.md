---
title: "An Introduction to Data Visualization-Part 3"
date: 2019-01-01T13:19:26+05:30
draft: false
image: "Intro_to_viz3.jpg"
tags: ["Data"]
categories: ["Visualization","Data Analysis"]
next: /An-Introduction-to-Data-Visualization-part1.md
previous: /An-Introduction-to-Data-Visualization-part2.md
---
In this last blog post on Introduction to visualization I would like to take you folks through Sarah Bird's recreation of Gapminder's - Health and Wealth of Nations that was presented by Hans Rosling at a TED conference. This is an iconic visualization from recent times, one which inspired me to use visualization as the main tool when working with Data.

In the last two posts of this series, the emphasis was on the importance of using visualization for understanding data and sharing information. In this blog post, I intend to highlight the basic process involved in using visualization to understand the data and communicate the finding to an audience.

Rosling collected data related to population, health and wealth of all the countries for over a century and wanted to analyse how they evolved over time. The dataset had the following information:

1. Year of Recording
2. Country Name
3. Average Life Expectancy
4. Average Annual Income
5. Population of the country
6. Region

Traditionally, these data are used to create reports and are published by governments and other organizations periodically. In its raw form(a table with lot of numbers :-/), they are usually the most boring set of reports one can imagine. Over the last 20 years these reports have become a little more interesting because of the use of business intelligence and reporting tools. Some of the very well known tools are Business Objects, Microsoft SQL Server Reporting Services, Cognos, Pentaho BI etc. In more recent times there are few more additions to this set of tools with better quality charts and customizing features- Tableau and Qlikview.

Typically, these tools provide an interface to fit the data into some pre-defined chart. These charts are supplemented with customizable options to add dimensions, sort, filter and perform aggregations. Some of these charts are good to compare Part-to-Whole while others are better when comparing equals. Given below are few examples of such charts taken from D3.js gallery:

![](/example_charts.png)

A report or a dashboard usually consists of a group of these charts that are centered around a commmon theme. The number of charts to be used, their layout and the customizable options to provide along with the charts depends on various factors. There are many different ways to use these pre-defined charts to convey inforamtion, but the main challenge here is to fit the data between the group of charts and provide functions to filter and aggregate to gather information. These charts are good mechanisms to communicate fine detailed information and at times redundant. I will cover more on these canned reports and dashboards in another blog post. For now the focus is on visualization and how it differs from these fixed representations.

Visualization in my opinion is more of a process and is holistic in nature. It always focuses on the entire data in one visual representation and usually provides summarised insights. It is the first step towards understanding data and the information it contains. In visualization we start with a blank canvas and add layers one by one to project the entire data in a form that can be easily understood and interpreted. We  do not force fit the data into a pre-defined chart, this is because we do not yet know the structure of the data and hence we do not know how it need to be communicated visually. An exploratory process is carried out by adding contextual constraints(say time) to basic visual glyphs such as points, lines, regions etc. Once they are encoded in this fashion they are likely to show hidden patterns which are then tailored into the visualization as additional layers. This process is repeated until we have the  complete story recreated using a visual representation. This process requires a lot of skill and is easier said than done. So, let us break down Sarah Bird's code and try to understand this process.

But before we proceed, we need to choose the right tools to go about this task. I initially thought of using D3js but found the learning curve to be too steep and requiring knowledge of javascript, html, css and svg. Since I am a data engineer and work mostly with SQL and python I was on the lookout for some tool that uses these programming paradigms. That is, when I came across Bokeh, a visualization library that can be used to create visualizations like D3js but using Python. I have used Python Pandas and Bokeh along with Jupyter notebook to recreate this visualization. Please feel free to code along :-)

Step 1: Import data
```python
import pandas as pd
data = pd.read_csv('gapminder.csv', index_col='Year', thousands=',')
```
Step 2: View the data
```python
data = pd.read_csv('gapminder.csv', index_col='Year', thousands=',')
# View the data
print(data.dtypes)
print("------------------------")
print(data.head())
print("------------------------")
print(data.describe())
```
Step 3: Set up an output interface for Bokeh to render the visualization. Alternately, one can use an html output
```python
from bokeh.io import output_notebook
output_notebook()
```

Step 4: Initialize an empty canvas for visualization
```python
from bokeh.io import show
from bokeh.plotting import figure
p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations ",
    height=200,
    width=900
)
```
Step 5: Loading data to the bokeh data interface to use it across other Bokeh elements. We choose a section(year=2010) of the data for setting up our chart. We will extend this once we have a layout in place
```python
from bokeh.models import ColumnDataSource
source = ColumnDataSource(data.loc[2010])
```
Step 6: Plot a basic layout with 'income' along the x-axis and 'life' along the y-axis
```python
p.circle(x='income', y='life', alpha=0.6, source=source)
p.xaxis.axis_label = "Average Annual Income"
p.yaxis.axis_label = "Life Expectancy"
show(p)
```
![](/base_layout1.png)

Step 7: Explore the base visualizations and configure. From the chart it can be seen that there is skewness in the data. The large income groups are responsible for cluttering the data of the smaller and middle income groups. This is because the difference in value between points in the large income group are much larger than the difference between points in the lower and mid income groups. Hence changing the x axis scale to logarithmic scale will stretch the data and provide a much better view of the data. Re-initialize the canvas with x_axis type and x-axis formatter
```python
from bokeh.io import show
from bokeh.plotting import figure
p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations ",
    height=300,
    width=900,
    x_axis_type='log'
)

# formatting x_axis range for better readability of the x axis values
p.circle(x='income', y='life', alpha=0.6, source=source)
p.xaxis.axis_label = "Average Annual Income"
p.yaxis.axis_label = "Life Expectancy"
from bokeh.models import NumeralTickFormatter
p.xaxis[0].formatter = NumeralTickFormatter(format='$0,')
show(p)
```
![](/base_layout2.png)

Step 8: Analyse what we have until now

* We have taken a section of the data (yera =2010)
* Each country represents a point on the chart which has two dimensions
* We have plotted 'Life Expectancy' along the y-axis
* We have plotted 'Average Annual Income' along the x-axis

Step 9: It is important to understand that the the dimesions(x and y axis) can be swapped. Here is how the swapped dimensions will look.
```python
from bokeh.io import show
from bokeh.plotting import figure
p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations ",
    height=500,
    width=800,
    y_axis_type='log'
)

# formatting x_axis range for better readability of the x axis values
p.circle(x='life', y='income', alpha=0.6, source=source)
p.xaxis.axis_label = "Life Expectancy"
p.yaxis.axis_label = "Average Annual Income"
from bokeh.models import NumeralTickFormatter
p.yaxis[0].formatter = NumeralTickFormatter(format='$0,')

show(p)
```
![](/base_layout3.png)

Step 10: I like this one better, so let's proceed to the next step with 'Life Expectancy' along the x axis. Let's customize little more and add more dimensions/attributes to the plot. We have 'Population' and 'Region' data available. How can we encode them?
We can associate size and color to the dots. We choose to associate  population with bubble size. This will a good indicator for the size of the country by population in relation to each other.
```python
from bokeh.io import show
from bokeh.models import LinearInterpolator
from bokeh.plotting import figure
p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations ",
    height=500,
    width=800,
    y_axis_type='log'
)
# giving size to each point. Please note that we are also using a linear interpolator to scale the size with
#     a particular range that makes viewing efficient. Please change the values of list 'y' to understand
#     why interpolation is necessary
size_mapper = LinearInterpolator(
    x = [data.population.min(), data.population.max()],
    y = [10,100]
)

p.circle(x='life', y='income', alpha=0.6, source=source,
        size={'field':'population', 'transform':size_mapper}
        )
p.xaxis.axis_label = "Life Expectancy"
p.yaxis.axis_label = "Average Annual Income"
from bokeh.models import NumeralTickFormatter
p.yaxis[0].formatter = NumeralTickFormatter(format='$0,')

show(p)
```
![](/base_layout4.png)

Step 11: More customizations. Now let us give each region a color to add more dimesnions and provide a legend
```python
from bokeh.io import show
from bokeh.models import LinearInterpolator
from bokeh.plotting import figure
from bokeh.models import CategoricalColorMapper
from bokeh.palettes import Spectral6
p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations ",
    height=500,
    width=800,
    y_axis_type='log'
)

size_mapper = LinearInterpolator(
    x = [data.population.min(), data.population.max()],
    y = [10,100]
)

# Mapping color to region
color_mapper = CategoricalColorMapper(
    factors=list(data.region.unique()),
    palette=Spectral6
)

p.circle(x='life', y='income', alpha=0.6, source=source,
        size={'field':'population', 'transform':size_mapper},
        color={'field':'region', 'transform':color_mapper},
        legend='region'
        )
p.xaxis.axis_label = "Life Expectancy"
p.yaxis.axis_label = "Average Annual Income"
from bokeh.models import NumeralTickFormatter
p.yaxis[0].formatter = NumeralTickFormatter(format='$0,')
# formating the legend
p.legend.location = (30, -5)
p.right.append(p.legend[0])
p.legend.border_line_color = None

show(p)
```
![](/base_layout5.png)

Step 12: Final touches and animate the visualization.
```python
from bokeh.io import show
from bokeh.models import LinearInterpolator
from bokeh.plotting import figure
from bokeh.models import CategoricalColorMapper
from bokeh.palettes import Spectral6

p = figure (
    title = "Re-creation of Gapminder's - Health & Wealth of nations 2010",
    height=500,
    width=800,
    y_axis_type='log'
)

size_mapper = LinearInterpolator(
    x = [data.population.min(), data.population.max()],
    y = [10,100]
)

# Mapping color to region
color_mapper = CategoricalColorMapper(
    factors=list(data.region.unique()),
    palette=Spectral6
)

# We have added all data elements to the visualization and we have a basic layout established.
# Now let us see how this will change over time.
# Let us add data for the other years as well to complete it
from bokeh.io import push_notebook
def update(year):
    new_data = dict(
        income=data.loc[year].income,
        life=data.loc[year].life,
        country=data.loc[year].Country,
        population=data.loc[year].population,
        region=data.loc[year].region
    )
    source.data = new_data
    if len(p.title.text) > len("Re-creation of Gapminder's - Health & Wealth of nations "):
        tmp = str(p.title.text)
        p.title.text=tmp[:-4]
        p.title.text = p.title.text + str(year)
    else:
        p.title.text = p.title.text + str(year)
    push_notebook()

p.circle(x='life', y='income', alpha=0.6, source=source,
        size={'field':'population', 'transform':size_mapper},
        color={'field':'region', 'transform':color_mapper},
        legend='region'
        )

p.xaxis.axis_label = "Life Expectancy"
p.yaxis.axis_label = "Average Annual Income"
from bokeh.models import NumeralTickFormatter
p.yaxis[0].formatter = NumeralTickFormatter(format='$0,')
# formating the legend
p.legend.location = (30, -5)
p.right.append(p.legend[0])
p.legend.border_line_color = None

show(p, notebook_handle=True)

import time
year =1950
while True:
    update(year)
    if year == 2014:
        year=1950
    else:
        year+=1
    time.sleep(0.5)
    continue
```
Provided some snapshots of the final animated chart
![](/base_layout6.png)
![](/base_layout7.png)
![](/base_layout8.png)

I hope I have a given a basic overview of the visualization process and the tools to use for creating data story. So hurry up, get your data and start your quest.

### References

[Complete code on jupyter notebook](https://github.com/agnurva/WorkingDirectory/blob/master/Re-creation%20of%20Gapminder's%20-%20Health%20%26%20Wealth%20of%20nations%20-%20Visualization%20process.ipynb)

[Getting Started With Bokeh | Gapmider using Bokeh|Sarah Bird ](https://www.youtube.com/watch?v=9FlUFLmaWvY&t=433s)

[The best stats you've ever seen | Hans Rosling](https://www.youtube.com/watch?v=hVimVzgtD6w&t=987s)

[200 years that changed the world | Hans Rosling](https://www.gapminder.org/videos/200-years-that-changed-the-world/ )

[The Wealth & Health of Nations(recreation using D3js | Mike Bostock)](https://bost.ocks.org/mike/nations/)
