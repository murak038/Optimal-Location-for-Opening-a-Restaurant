# Optimal Location for Opening a Restaurant

## Table of Contents
1. [Introduction](#introduction)
2. [Data](#data)
3. [Methodology](#methodology)
4. [Results](#results)
5. [Discussion](#discussion)
6. [Conclusion](#conclusion)

## Introduction

While opening a restaurant can be a very lucrative business, a lack of demand causes many restaurants to close within the first year of opening. There are many different factors that can account for a restaurant’s success such as location, competition and quality of the food. This is an important question that every business owner must face when choosing whether to open a restaurant or not, as well as location of the business. 

To demonstrate the process of picking a location for a client opening a business, the project will focus on answering the following question: “If the client wanted to open an Indian Restaurant in Toronto, what areas are the best options to open the restaurant?” For an Indian Restaurant, the location and competition are both determined by where the restaurant is opened. If there are too many Indian Restaurants in the local vicinity, the profitability of the restaurant will be severely decreased. Additionally, starting a restaurant in a location with higher income would increase the profitability of the business over starting in a poorer area. 

## Data

To answer the business problem, the following factors have to be extracted from various data sources:
- Population & Ethnic Distribution of Each Neighborhood (Toronto Census)
- Income Distribution of Each Neighborhood (Toronto Census)
- Number of Restaurants in Each Neighborhood (Foursquare API)
- Number of Indian Restaurants in Each Neighborhood (Foursquare API)

The Toronto Census data was extracted from https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#8c732154-5012-9afe-d0cd-ba3ffc813d5a.

## Methodology

The first step of the project was to combine the Toronto dataset, containing the postal code, borough, neighborhood name, latitude and longitude for each postal code in Toronto, and the census dataset.

Using the income distribution for each neighborhood, the spending power of each area was calculated using the median of each category weighted by the number of people in that income category. Thus, the spending power represents the overall capital of each area (i.e. total income of the inhabitants). Since the spending power for each area is considerably large and the relative strength is difficult to visualize, the spending power for each area was standardized. 

The next step was to visualize the location of the various postal codes within Toronto to obtain a general understanding the location (Figure 1).  As seen from the map, the postal codes are densely clustered near downtown Toronto and spread out as the distance from downtown increases. This is important because while some postal codes might not have many restaurants, if the area is located near downtown, adjacent regions can heavily impact the profitability of the restaurant. 

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%201.png "Figure 1: Location of each postal code within Toronto, Canada.")

**Figure 1:** Location of each postal code within Toronto, Canada.

Now that the region has been clearly visualized, the Foursquare API was used to explore each neighborhood and return the top 200 venues within 2,000 meters (1.2 miles) of the longitude and latitude for each postal code. The extracted venue categories were encoded using one-hot encoding and the total restaurants and Indian restaurants in each region were calculated (Figure 2).

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%202.png "Figure 2: Result of calculating the number of restaurants in every region.")

**Figure 2:** Result of calculating the number of restaurants in every region.

With the resulting data, the Postal Code, Borough name, Latitude, Longitude and Density columns of each region were dropped from the dataFrame. Then, the population, area, spending power, total number of restaurants and the number of Indian restaurants were used to train a k-Means clustering algorithm with 5 clusters (Figure 3). The characteristics of the resulting clusters can be found in Table 1.

## Results

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%203.png "Figure 3: Result of the clustering algorithm. Cluster 0 = Red Cluster 1 = Purple Cluster 2 = Blue Cluster 3 = Turquoise Cluster 4 = Orange")

**Figure 3:** Result of the clustering algorithm. Cluster 0 = Red Cluster 1 = Purple Cluster 2 = Blue Cluster 3 = Turquoise Cluster 4 = Orange

 Cluster        | Characteristics           | 
| ------------- |:-------------:|
| Cluster 0      |Positive Spending Power (0.3 – 1.8)  |
| Cluster 1     | Negative Spending Power (-1.2 -- -0.8)       |
| Cluster 2 |  Near Zero Spending Power (-0.5 – 0.5)      |
| Cluster 3      | High Positive Spending Power (1.7+)      |
| Cluster 4 | Negative Spending Power (-0.8 – 0) With Large Number of Restaurants      |

**Table 1:** Characteristics of the clusters resulting from k-Means clustering algorithm

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%204.png "Figure 4: Data from neighborhoods belonging to Cluster 3")

**Figure 4:** Data from neighborhoods belonging to Cluster 3

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%205.png "Figure 5: These plots shows the characteristics of neighborhoods belonging to cluster 3. ")

**Figure 5:** These plots shows the characteristics of neighborhoods belonging to cluster 3. 

## Discussion

From the results of the clustering algorithm, it was determined that neighborhoods corresponding to cluster 3 were the best choice for opening an Indian restaurant based on the normalized spending power and population. This narrowed down possible locations to six different areas. Using the results in Figure 5, the Agincourt North, L’Amoreaux East, Milliken, Steeles East region the Newtonbrook, Willowdale region and the Harbourfront, Regent Park region were eliminated due to the large number of restaurants in the area. 

From the three remaining regions, I would recommend that the client open his/her restaurant in either the Rouge, Malvern region or the Cloverdale, Islington, Martin Grove, Princess Gardens, West Deane Park region. Both regions have very few restaurants and are farther away from the downtown area. While the Cloverdale, Islington, Martin Grove, Princess Gardens, West Deane Park region has a higher spending power and population, the Rouge, Malvern region has a higher percentage of South Asians and thus the optimal region to open the Indian Restaurant. 

![alt text](https://github.com/murak038/Battle_of_Neighborhoods/blob/master/images/Figure%207.png "Figure 6: Map of Toronto with the neighborhoods in Cluster 3 labeled. ")

**Figure 6:** Map of Toronto with the neighborhoods in Cluster 3 labeled. 

## Conclusion

Opening a restaurant is a complex task that can lead to a large monetary loss if not done properly. Thus, extensive research about the area would greatly increase the likelihood of the restaurant succeeding. From the project above, I demonstrated the workflow necessary for a client to determine what area the restaurant should open. For specifically, I determined that the optimal location to open an Indian restaurant in Toronto should be in the Rouge, Malvern region.
