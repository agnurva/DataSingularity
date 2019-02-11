---
title: "Data Modelling Process - Part 1"
date: 2019-01-23T14:42:27+05:30
draft: false
image: "Intro_to_viz3.jpg"
tags: ["Data"]
categories: ["Data Modelling","Normalization"]
next: /An-Introduction-to-Data-Visualization-part1.md
previous: /An-Introduction-to-Data-Visualization-part3.md
---
Recently, I attended an interview for the role of a Data/Dimensional modeller for a services company in Bangalore. Though I have designed and build Information Systems(IS) based on Relational DataBase Management System(RDBMS), Today I primilarily work on Visualiztion and Analytics solution based on Big Data technologies. I though of quickly brushing up on the traditional way of managing information. I was too lazy to find and read those old chunky books on databases and so I started with youtube and followed up with couple of links on Google looking out for definitions, laws and design guidelines used in Data Modelling. I found very few sources covering the - what? Why? and How? of data modelling process as a whole. Some of the content were also misleading because of misintepretations and the use of ambigious examples. Hence, I will document the process I follow, hoping that it will help folks who want to get a practical overview of the data modelling process in a short time.

Before we begin, it is important for us to know the evolution of information systems to  understand the importanace of data modelling. But this is a big topic in itself and I will cover it in a seperate blog. For now, consider that there are primarily two types of Information Systems:

* OnLine Transactional Processing(OLTP) systems
* OnLine Analytical Processing(OLAP) Systems

I mostly follow the process laid out by Elmasri and Navathe in their book "Fundamentals of Database Systems".
