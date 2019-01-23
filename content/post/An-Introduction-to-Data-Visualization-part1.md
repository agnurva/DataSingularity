---
title: "An Introduction to Data Visualization-Part 1"
date: 2018-12-26T14:56:54+05:30
image: "Intro_to_viz1.jpg"
tags: ["Data"]
categories: ["Visualization","Data Analysis"]
next: /An-Introduction-to-Data-Visualization-part2.md
previous: /An-Introduction-to-Data-Visualization-part3.md
---
Data visualization refers to the technique used to understand and communicate data or information by encoding it as visual objects (eg., points, lines, maps or bars). It is a very important skill to possess when working with data and is an absolute must for all data analysts and data scientists. In this blog I will try and illustrate the importance of using visual objects to understand data and share Information.

Consider the data given below. It consists of features(attributes) 'x' and 'y' related to 4 different entities with 11 observations(tuples) each. Assume that the objective is to find the similarity between these entities.
![](/anscombes_quartet.png)
 A data analyst would typically go about this problem by quantitatively describing or summarizing the features. This process is known as descriptive or summary statistics. A simple summary stats of the above dataset is given below. Please note that the values are approximated.

 Property |	Value 	
 ---------|----------
Mean of x 	|9 	
Sample variance of x |	11 	
Mean of y |	7.50 	
Sample variance of y |	4.12
Correlation between x and y |	0.81
Linear regression line |	y = 3.00 + 0.50x
Coefficient of determination of the linear regression |	0.66 	

Based on these findings one can conclude that the entities are very similar. However, such a conclusion could not be further away from reality. To get a better understanding of the data one would need to look deeper and this is difficult since most people cannot perceive the layout of data by merely looking at number. Thankfully, this is where Visualization can help us. Consider the image below which is a visual representation of the data representing the 4 entities.
![](/anscombe_quartet_viz.png)
The above image is very intuitive and clearly illustrates the layout of data and hence the difference between the entities in question. This visual representation and data is famously known as the Anscombe's quartet constructed in 1973 by the statistician Francis Anscombe to demonstrate both the importance of graphing data before analyzing it and the effect of outliers on statistical properties. He described the article as being intended to counter the impression among statisticians that "numerical calculations are exact, but graphs are rough."

Anscombe uses simple dots to represent the data in two dimensions to represent each of the features x and y. As many of you already know this is a simple scatter plot. This simple visual representation provides an easy means to understand the layout of data which was difficult to perceive through the summary stats. From the visualization we can draw the following conclusions:

* The first scatter plot (top left) appears to be a simple linear relationship  and seems to follow the assumption of normality.
* The second graph (top right) is not distributed normally; while a relationship between the two variables is obvious, it is not linear, and the Pearson correlation coefficient is not relevant. A more general regression and the corresponding coefficient of determination would be more appropriate.
* In the third graph (bottom left), the distribution is linear, but should have a different regression line. The calculated regression is offset by the one outlier which exerts enough influence to lower the correlation coefficient from 1 to 0.816.
* Finally, the fourth graph (bottom right) shows an example when one outlier is enough to produce a high correlation coefficient, even though the other data points do not indicate any relationship between the variables.

I have taken most of the above extracts from Wikipedia and used python with Bokeh Visualization to recreate this amazing piece of work. Please check the reference section for more details.

I hope with this blog I have provided a glimpse of how important Visualization is when analysing data. In my subsequent posts I will try and recreate few other famous visualizations. By the end of this 3 part introductory series I wish to expose the audience to what little I know about the art and science of Visualization.

### References

[Anscombe's Quartet - Wikipedia](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)

[Recreation of Anscrombe's quartet - Jupyter Notebook](https://github.com/agnurva/WorkingDirectory/blob/master/Anscombe_Quartet.ipynb)
