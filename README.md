# BPP Data-Science-Portfolio

![histogram](assets/images/histogram.png)

[Publication](https://www.google.co.uk/)

# PGA Tour Golf Data Project

## Executive Summary

This project looks at data from the professional sport of golf, specifically the elite tour in America, the PGA (Professional Golf Association) Tour.

I am going to look at how important the 1st shot off the tee on each hole is, by looking to see if the ball distance off the tee has a correlation to overall performance. This 1st shot is known as ‘the drive’ and so you will see me refer to this metric in the report as ‘driving distance’.

My hypothesis is that if you hit the ball further off the tee with the 1st shot, this will lead to lower scores on the hole overall, which in turn results in a lower score of the tournament. The significance of this is the player with the least number of shots wins the tournament. 

I will use regression analysis technique to highlight any correlations. I also plan to do some time series analysis to see if there are any changes over the 8 years of data that I have. 

I have researched the use of linear regression from (Linear regression. Su, X et al. 2012.) 

## Data Infrastructure and Tools

I have managed to download public data sets taken from all the PGA tour tournaments over 8 years (seasons) from the website Kaggle.

The files are .csv files, which are easy to ingest into my chosen analytics tool Microsoft Power BI. These types of data files are classed as structured data because they are already formatted in a table using columns with pre-defined field names and are easier to use than other sources like unstructured data which can include pictures or information within PDF files where the data is more difficult to extract and analyse.  

There are 3 data sets in total, because I couldn’t find a single dataset that had everything I required. This means that I had to join the data using star schema in Power BI. All data sets were ingested individually and then I explored the data to see how to make the joins on the 3 tables. 

After exploring the 3 datasets using the table visualiser in Power BI, I concluded that I could get everything I needed from just 2 of the tables, The Tournament Information and The Player Statistics data tables. 

## Data Engineering

I have a dataset that contains individual players statistics over the seasons and another with all the tournament information over seasons. These are both .csv files that I have ingested into Power BI using the Power Query Editor tool. 
The reason for using Power BI is for its strong ability to engineer data using M-code within the editor tool and the large variety of visuals available to showcase the data on a dashboard.  

I’ve linked the datasets using player name as the primary key. 

There was a challenge with this as 1 dataset used the players full name along with the year and another used the first initial and surname. 

E.g. Rory McIlroy (2019) and R.McIlroy  

Firstly, I removed the year and put this into a new column using this code:

 ![Image](assets/images/001_Data_Engineering.png)

Then I put the player name into another column:

 ![Image](assets/images/002_Data_Engineering.png)

Then I did a transformation of the full player name to just initial and surname:
 
 ![Image](assets/images/003_Data_Engineering.png)

Before:                                                             After:
 ![Image](assets/images/004_Data_Engineering.png)                   ![Image](assets/images/005_Data_Engineering.png)

Before:                                                             After:
 ![Image](assets/images/006_Data_Engineering.png)                   ![Image](assets/images/007_Data_Engineering.png)


Because there are duplicate players fort each year, I chose to create a unique players table that I could use to connect to my 2 information tables using the primary key that I created. To create this table, I used the following DAX code:
 ![Image](assets/images/008_Data_Engineering.png) 

This meant I could have my 2 information tables connect to a reference table to create a star schema data table design. See below:
 ![Image](assets/images/009_Data_Engineering.png)

The table relationships are the ‘many to one’ joining type, this enables me to aggregate date at an individual player level. 
The 2 pieces of data that I wanted to aggregate are the average player driving distances from the player statistics table and the player finishing positions from the tournament information table. 

I used the following DAX queries to create calculated columns within my player’s table. 

Ave DD (average driving distance) :
![Image](assets/images/010_Data_Engineering.png) 

Ave Position (average finishing position)
![Image](assets/images/011_Data_Engineering.png) 

