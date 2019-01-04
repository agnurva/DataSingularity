---
title: "An Introduction to Data Visualization-Part 2"
date: 2019-01-01T13:17:03+05:30
draft: false
image: "Intro_to_viz2.jpg"
tags: ["Data"]
categories: ["Visualization","Data Analysis"]
next: /An-Introduction-to-Data-Visualization-part1.md
previous: /An-Introduction-to-Data-Visualization-part3.md
---
Hello folks, I hope you found part one of the introducution to visualization series interesting. In part one, the focus was on using visualization for analysing and understanding data. In this blog, we will re-emphasize on this aspect of data visualization.

Let me take you back in time to the early 19th century which saw a large scale change in the societal structures around the world. Slavery was abolished, and the Second Industrial Revolution led to massive urbanization and significantly higher levels of productivity. This also gave rise to a massive migration of people from all over the world to large cities for work. The living conditions of these working class people were not planned and they were frequently prone to diseases usually in waves of epidemics that took many lives.

People believed that the origin of these epidemics was a noxious form of bad air, also known as "night air" and this theory was known as the Miasma theory. Diseases such as cholera, chlamydia, or the Black Death were though to have been caused by this foul air. However, John Snow had studied cholera outbreaks throughout his life and was skeptical about this theory. Through his observations, he believed that the disease spread through water and was out to prove the medical community wrong about the Miasma theory. Snow knew that the city water was supplied by two companies and decided to conduct a double blind study. His study provided evidence that the company that was supplying water form downstream Thames river caused the diseases since it was contaminated with the sanitary wastes from the city. His theory was not accepted and life went on until a severe outbreak of cholera occurred in 1854 near Broad Street. Snow was quick to reach the spot and collect data related to death and water source in the neighbourhood. He plotted this data on a map of the city and was successful in convincing the authorities about his theory which led them to removing the handle of the contaminated water pump. Given below is the original map created by Snow.
![](/john_snow_orignial.png)
I have recreated the map visualization using Google maps and Bokeh visualization library. Please note that the layout of the map has changed over the years.
![](/john_snow_recreation.png)

* The black dots on the map indicates the deaths due to cholera
* The red dot indicates the water source(water pump)
* The circle around each water source indicates the approximate range of each water source. Snow originally used Thiessen polygons by actaully measuring the walking distance between the water source and the related death. Since I do not have the data, I have replaced it with a circle which could be a little misleading. The outliers are significantly different when viewed using Thiessen polygons.
* It can be noticed that some of the deaths seems to be outliers. There seems to be a non-contaminated water source nearby. But Snow manually visited these places and collected information and found that even these deaths were due to the Broad street pump from which they drank water on their way to school or work.

Snow's findings inspired fundamental changes in the water and waste management systems of London, which led to similar changes in other cities around the world. His contributions are also significant in formulating the "Germ theory" which is accepted today.

Though John Snow did not live to see his work better the quality of lives of people around the world, his work will inspire us and he will forever be remembered for his contribution to humanity.

### References

[About John Snow - Wikipedia](https://en.wikipedia.org/wiki/John_Snow)

[Broad Street Choldera Outbreak - Wikipedia](https://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak)

[Recreation of John Snow's Cholera Map - Jupyter Notebook](https://github.com/agnurva/WorkingDirectory/blob/master/JohnSnow_Broadstreet_Outbreak.ipynb)
