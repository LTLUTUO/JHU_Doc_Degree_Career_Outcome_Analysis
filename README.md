# JHU_Doc_Degree_Career_Outcome_Clustering_Analysis
## Introduction
This project focuses on the similarity of the career outcome for different doctoral program at Johns Hopkins University (JHU) in 10 years. It can serve as a guideline for multiple things, such as resource distribution for career advising, networking events, cross-program alumni reunion, etc. I grouped 21 doctoral programs in the area of life science in JHU into three clusters, for which you can see below:
![alt text](Screen_Shot_For_Cluster_Visualization.png)
The further steps of the reasearch could be about what is the connection between the companies people from different program go to under the same cluster. It requires further and more detail information about the career outcome of the programs and companies analysis. With this further research, it can help pairing up or teaming people from different programs to maximize their career outcome.
## Outline of the Analysis
* Industry question: how can JHU maximize its career advising resources for doctoral programs in life science? How can they manage the alumni networking events wisely so that everyone can get the most out of those events?
* Data question: In a ten years point, what are the programs that have similar distributions for career outcomes?
* Data answer: 
![alt text](Cluster_Result.png)
* Industry answer: The distribution for three clusters are pretty even. At first glance, I am not surprised to see that most of the "practical" programs, such as Biomedical Engineering, Chemical, and Biomolecular Engineering, are in cluster three. Combining with the first picture above, we can see that a large percent of alumni get in for-profit businesses in ten years after finishing the program.
## Source of data
All the data in this research are extracted from [Next Generation Life Science (NGLS)](http://nglscoalition.org/coalition-data/#close). It is a website that can help to direct users to the doctoral program outcome page for over 50 schools. From NGLS, the website of [Coalition for Next Generation Life Science of JHU](https://provost.jhu.edu/education/graduate-and-professional-education/cngls/) is found. A [pdf version of Doctoral Career Outcomes](Career-Outcome-ADA-Tables-Final.pdf) is extracted from CNGLS JHU.

[Tabula](https://tabula.technology/) is used to convert the pdf file into [csv](JHU_Doctoral_Career_Outcome_Cluster_Analysis.csv) version. At last, a [excel version](JHU_Doctoral_Career_Outcome_Cluster_Analysis.xlsx) of it is being used for analysis.
## Step by Step Excel Manipulation
### Data Cleaning
First, we need to move the data we want to analyze into a new worksheet and clean it up, format it so we can use it for further processes. When we first paste the data we needed in a new worksheet, it would look like this:
![alt text](Screen_Shot_for_Step_By_Step/Data_Before_CLeaning.png)
As we can see, some titles are messed together, and some data are combined in one column. I will use two methods to separate them. For the first column where program name and data are messed together, I used a function in excel called `Flash Fill`, the short-cut for it is `Ctrl + E` for both Mac and Windows users. For the rest of the column where the data are messed together, I used `Text to Columns`.
#### Flash Fill
1. Insert three columns after the first column
2. Manually type in the program name, first data and the second data in the three new column
3. Select each column and press `Ctrl + E`. The data will separate automatically.
4. Delete the original first column
#### Text to Columns
5. Insert a column after the messed data column
6. Click on `Data -> Text to Columns`
7. Click on "Next", and select separate by **Space**
8. Click on Finish. The data will separate automatically.

Below is the preview of the data after cleaning:
![alt text](Screen_Shot_for_Step_By_Step/Data_after_Cleaning.png)
### Calculate the Standardized Value
For analysis, I used the percentage instead of the number of the outcome. We will need the standardized value to calculate clusters. In order to calculate the standardize value using the `=STANDARDIZE()` in excel, we need the average and standard deviation for each column. 
1. insert two rows above the data and its label, name them as **Average** and **Standard Deviation**
2. Calculate the average and standard deviation for each column with `=AVERAGE()` and `=STDEV()`
3. Create columns after all the data, name them as "% of _Industry_"
4. Fill the cells with the standardize function `=STANDARDIZE(x,mean,standard_dev)`

Below is the preview of the layout of the standardized value :
![alt text](Screen_Shot_for_Step_By_Step/Calculate_Standardize_Value.png)
### Preparation for Cluster
Before using Excel Solver to calculate the optimized cluster combinations, we need to format the worksheet. The idea here is to list out three rows of data that act as the center of the clusters. Then, the total distance for each program to each cluster center. After that, the min_distant is selected, and the sum of distant is calculated.
#### The Cluster Center
1. Create five column in the top of the worksheet, and name them like this:
![alt text](Screen_Shot_for_Step_By_Step/Naming_for_cluster.png)
The numbers in the very top is the column number of the label below, and it is add for the convenience of using Vlookup. ID is related to the number of the order of programs.
2. Randomly assign the ID in the ID column. Use `=Vlookup()` to fill all the other cells in the area.
![alt text](Screen_Shot_for_Step_By_Step/Cluster_Center_Filled.png)
#### The Distant Part
1. Insert five columns after the data, and name them like this:
![alt text](Screen_Shot_for_Step_By_Step/Naming_For_Distant.png)
2. Calculate the dist_1/2/3 using the function `=SUMXMY2()`
3. Choosing the Min_Dist from the three dist using the function `=MIN()`
4. Fill in the Cluster_match using the function `=MATCH()`
![alt text](Screen_Shot_for_Step_By_Step/Distant_Filled.png)
### Clustering with Solver
1. Choose a cell and name it **Sum_of_Min_Dist**
2. Below it, calculate the sum of all Min_Dist using the function `=SUM()`
3. Initial Excel Solver with `Data -> Solver`
4. Set up the parameters:
![alt text](Screen_Shot_for_Step_By_Step/Slover_Setup.png)
Select the cell containing the function under **Sum_of_Min_Dist** as **Set Objective**, and we want to minimize it. Select the three cells that contain the **ID** information in the **By Changing Variable Cells**. Add three constraints under: **ID** value should be **equal or smaller than 21**, **equal or bigger than 1**, and it should be an **integer**.
5. Click **Solve**!
### Simple Visualization
At last, we can make a simple visualization to show the different clusters. I did it with conditional formatting.
1. Select all the area with data
2. Add conditional formatting by clicking `Home -> Conditional Formatting -> New Rules`
3. In style, select **Classic**
4. In the format section, select **Use a formula to determine which cells to format**
5. In the formula section, type in `=$V12(Cells under Cluster_match)=1`
6. Select your preferable way to highlight the rows which apply
7. Repeat steps one through six for if cluster_match = 2/3

In the end, the whole worksheet would look like this:
![alt text](Screen_Shot_For_Cluster_Visualization.png)
