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
Hello folks, I hope you found part one of the Introducution to visualization series interesting. In part one, the focus was on using visualization for analysing and understanding data. In this blog we will re-emphasise on this aspect of data visualization.

Let me take you folks back in time to the 19th century, which saw a large scale change in the sociatial structures around the world. Slavery was abolished, and the Second Industrial Revolution led to massive urbanization and significantly higher levels of productivity. This also gave rise to a massive migration of people from all over to large cities for work. The living conditions of these working class people was not planned and they were frequently prone to diseases usually in waves of epimedics that took many lives.

People believed that the origin of epidimics was a noxious form of "bad air", also known as night air and this theory was known as the Miasma theory. Diseases such as cholera, chlamydia, or the Black Death were though to have been caused by this foul air. However, John snow had studied cholera outbreaks throughout his life and was skeptical about the theory. Through his observations he believed that the disease is spread through water and was out to prove the medical community wrong about the Miasma theory. John snow knew that the city water was supplied by two companies and decided to conduct a double blind study. His study provided evidence that the company that was supplying water form downstream Thames river caused the diseases since it was contaminated with the sanitary wastes from the city. His theory was not accepted and life went on until a severe outbreak of cholera occurred in 1854 near Broad Street. John Snow was quick the reach the spot and collect data related to death and water source in the neighbourhood. He plotted this data on a map of the city and was successful in convincing the authorities about his theory which led to them removing the handle of the contaminated water pump. Given below is the original map created by John Snow.
![](/john_snow_orignial.png)
I have recreated the visualization using Google maps and Bokeh visualization. Please not that the layout of the map has changed over the years.
![](/john_snow_recreation.png)

* The black dots on the map indicates the deaths due to cholera
* The red dot indicates the water source(water pump)
* The circle around each water source indicates the approximate range of wach water source. John Snow originally used Thiessen polygons by actaully measuring the walking siatnce between the water source and the realted death. Since I do not have the data I have replaced it with a circle which could be a little misleading. The outliers are significantly different when viewed using Thiessen polygons.
* It can be noticed that some of the deaths seems to be outliers. There seems to be a non contaminated water source nearby. But John Snow manually visited these places and collected information and found that even these deaths are due to the Broad street pump from which they drank water on their way to school or work and something similar.

John Snow's findings inspired fundamental changes in the water and waste management systems of London, which led to similar changes in other cities around the world. His contributions are also significant in formulating the "Germ theory" which is accepted today.

Though John Snow did ont live to see his work better the quality of lives of people around the world his work will inspire us and he will forever be remembered for his contribution to humanity.

### References

[About John Snow - Wikipedia](https://en.wikipedia.org/wiki/John_Snow)

[Broad Street Choldera Outbreak - Wikipedia](https://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak)

[Recreation of John Snow's Cholera Map - Jupyter Notebook](https://github.com/agnurva/WorkingDirectory/blob/master/Anscombe_Quartet.ipynb)
