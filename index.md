---
layout: default
---
 ![commuters](assets/css/commuters.jpg)<br>
 






## Background

Studies have shown that long commutes have a negative impact on health and happiness. Unfortunately, New York City (NYC) often tops the list for longest commutes and ranks lowly on the Happiest Cities list for America (59 out of 182) as well as in the world (207 out of 250).</br>

It would seem, then, shortening the commute might make NYC workers a little happier. However, whether this is feasible requires a closer look at the patterns of commuting flows of NYC workers and a possible main driver for the long commute. </br>

My study aims to answer the following three questions:
1.	What are the commuting patterns in the New York-New Jersey (NY-NJ) area?
2.	Is there an association between rent differentials and distance of commute?


</br>

## Methods
I used Python 3.12 in Google Colab to perform all data cleaning, manipulation, and most of the visualization for this project. To create the flow map, I used FlowmapBlue, which is a free, open-source web tool. </br>

To analyze patterns of worker flows in the NY-NJ area, I downloaded the data [NY_NJ_Workers.csv]  (ID: 302100) from American Association of State Highway and Transportation (AASHTO) Census Transportation Solutions, which home and work locations and journey to work travel flows via its CTTP data portal. I queried data for 2017-2021 (5 years) at the State-County level for the flow of workers 16 years and over for all counties in the states of NY and NJ. </br>

I cleaned the data and recategorized geographic units from counties to Manhattan, Bronx, Brooklyn, Queens, Staten Island, NYS and NJ. Using .groupby() and .sum() functions of the pandas library, I generated a count table showing the counts of residents and workers in each of the seven specified areas (i.e., five boroughs of NYC, NY state, and NJ state). </br>

To generate a flow map on FlowmapBlue, I created a spreadsheet with Locations and Counts of Total Workers using this template. I made the spreadsheet open to public, and copied the link to the spreadsheet to the corresponding input field on this page. Flowmap provides a geocoding function that finds geographic coordinates of locations by their names. I used Newark and Yonkers' coordinates to indicate the general directions of NJ and NY state. </br>

To visualize the net inflow (outflow) of workers in each of the specified area, I first subtracted the number of residents from the number of workers in the same area. Inflow of workers to an area is a positive count, whereas outflow is a negative count. I created a summary table using plotly.graphic_objects and a bidirectional bar chart using the plotly.express library. </br>

To investigate any association between rent differentials and distance of commute, I downloaded the B25064 Median Gross Rent (Dollars) dataset [MedianGrossRent5Y2024] of the 2024 American Community Survey ACS 5-Year Estimates from the US Census Bureau for all counties in NY and NJ. </br>

I cleaned the data and created an interactive choropleth map using the plotly.express library. To calculate the straight-line distance from each of the study area to Manhattan, latitude-longitude coordinates are necessary. I downloaded the United States Counties Database  [uscounties.csv]  from SimpleMaps.  After merging this dataset with the rent dataset using the five-digit FIPS codes, I then performed the distance calculation with the geodesic library. </br>

Finally, I calculated the Pearson’s Correlation Coefficient between the median gross rent of each county in NY and NJ and its distance to Manhattan using the stats library from scipy. I then created an interactive scatterplot for Median Gross Rent vs. Distance to Manhattan using the plotly.express library. I concluded my analysis with a univariate linear regression using median gross rent as the outcome and distance to Manhattan as the predictor. </br>

## Results

The commuting patterns for workers in the NY-NJ area are best illustrated by a flow map: </br>

<iframe 
  src="https://www.flowmap.blue/1ZW4OimEUiVa9eRIm-t12TsHoHoL5P8XD3MJhgXuLHNQ?v=40.758797%2C-74.000900%2C9.94%2C0%2C0&a=1&as=1&b=1&bo=75&c=1&ca=1&d=0&fe=1&lt=1&lfm=ALL&col=Magenta&f=23"
  width="100%" 
  height="400" 
  frameborder="2" 
  allowfullscreen>
</iframe>

</br>

While there are movements in both directions between any two study areas, the strongest flows go into Manhattan.  
In fact, the summary table below reveals that, of the seven workplaces, **Manhattan is the only area with a net inflow of workers** (around **1.5 million**) while all the other workplaces show a net outflow of between 78,000 to 310,000 workers. </br>

  <iframe src="NetWorkerInflowTable.html" width="100%" height="200px"></iframe>
</br>

The bidirectional bar chart below illustrates the striking differences: </br>

  <iframe src="BidirectionalBarChart.html" width="100%" height="200px"></iframe>
</br>

Why, then, do so many Big Apple workers put up with their long commute to Manhattan? </br>

Many reasons come to mind: more job opportunities, better pay, and so on. But the one reason we hear most about, even from those who do work and live in Manhattan, is how expensive rents are in the city. 

“The overall proportion of New York City residents paying more than 30% of their income for rent is high (52.1%),” according to a 2024 report by the NYC Comptroller. This means city workers get to keep a bigger portion of their paycheck by commuting.

The median gross rents for all NY and NJ counties are visualized as a choropleth map below: </br>

  <iframe src="MedianRentChoroplethMap.html" width="100%" height="200px"></iframe>
  </br>

  There is a general pattern: **the farther the county is to Manhattan, the cheaper the median gross rent.** This negative relationship between distance and rent level is clearly illustrated by the following scatterplot: </br>

  <iframe src="RentDistanceSctterplot.html" width="100%" height="200px"></iframe>
  </br>

  How strong is this negative rent-distance association? A Pearson’s Correlation Coefficient of -0.844 quantifies the strong negative correlation, and a OLS linear regression reveals that distance to Manhattan is a significant predictor for median gross rent at the 5% significant level (p-value < 0.0001, Confidence Interval [-4.533, -3.416]), and distance alone explains over 70% of the total variance of median gross rent. </br>

  In conclusion, for the large inflow of workers into Manhattan, an attempt to improve their health and happiness through shortening the commute by relocating to places closer to work would require them to pay a higher rent, which, in turn, creates higher financial worries that are shown to be significantly associated with higher psychological distress. The net trade-off does not seem hopeful, not to mention its feasibility. </br>


  















#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://docs.github.com/assets/images/help/repository/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
