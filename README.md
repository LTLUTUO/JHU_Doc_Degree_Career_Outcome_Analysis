# JHU_Doc_Degree_Career_Outcome_Clustering_Analysis
## Introduction
This project focuses on similarity of the career outcome for different doctoral program in Johns Hopkins University (JHU) in 10 years. It can serve as a guideline for multiple things, such as resources distribution for career advicing, networking events, cross program alumni reunion, etc. I grouped 21 docoral programs in the area of life science in JHU into three clusters, for which you can see below:
![alt text](Screen_Shot_For_Cluster_Visualization.png)
## Outline of the Analysis
* Industry question: how can JHU maximize its career advicing resourses for doctoral program in life science? How can they manage the alumni networking events wisely so that everyone can get the most out of those events?
* Data question: In a ten years point, what are the programs that have similar distributions for career outcomes?
* Data answer: 
![alt text](Cluster_Result.png)
* Industry answer: The distribution for three clusters are pretty even. By just looking at the name of the doctoal programs, I am not suprise to see that Biomedical Engineering, Chemical and Biomolecular Engineering along with other more "practical" program are within the same cluster. Combining with the first picture above, we can see that a large percent of alumni get in for-profit businesses in ten years after finishing the program.
## Source of data
All the data in this research are extracted from [Next Generation Life Science (NGLS)](http://nglscoalition.org/coalition-data/#close). It is a website that can help directing users to the doctoral program outcome page for over 50 schools. From NGLS, the website of [Coalition for Next Generation Life Science of JHU](https://provost.jhu.edu/education/graduate-and-professional-education/cngls/) is found. A [pdf version of Doctoral Career Outcomes](Career-Outcome-ADA-Tables-Final.pdf) is extracted from CNGLS JHU.

[Tabula](https://tabula.technology/) is used to convert the pdf file into [csv](JHU_Doctoral_Career_Outcome_Cluster_Analysis.csv) version. At last, a [excel version](JHU_Doctoral_Career_Outcome_Cluster_Analysis.xlsx) of it is being used for analysis.
## Step by Step Excel Manipulation
### Data Cleaning
First we need to move tha data we want to analyze into a new worksheet and clean it up, format it so we can use it for further processes.
1. 
