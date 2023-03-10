# Racial Dot Map & Diversity Index

In this repo you will find a script to create racial dot maps and diversity index scores for census block groups in Boston, MA and New York City, NY. You can use this code for an county, state or city in the US. The source dataset for this analysis is U.S. Census Bureau and American Community Survey 5 yr estimates [Table B03002 - Latino or Hispanic Origin by Race](https://data.census.gov/table?q=b03002&tid=ACSDT5Y2020.B03002).

The purpose of this analysis is to visualize and quantify residential segregation over time and to statistically test the average census block group diversity across the two major cities.

## Getting Started

Boston has recently become infamous for its racism and segregation. In a national survey commissioned by the Globe in 2017, Black people ranked Boston as the least welcoming city to people of color \[1\]. Racial inequalities have persisted in Boston despite the city’s advances in other areas like sports, higher education, biotech, and medicine. Many believe this is due to white citizens’ prejudice that erases Black communities from the city center and forces them into neighborhoods with underfunded schools, lack of transportation, and other crucial resources for economic advancement. According to the Globe, the median net worth of non-immigrant black households in the Boston area is $8 compared to $250,000 for white households. The inequities and disparities in the City of Boston are astounding, especially given the city’s reputation for liberalism and progressivism.

As a long-term resident of the city, I can attest to the striking contrast of race and socio-economic status between neighborhood blocks. Almost every neighborhood in Boston has a stereotypical long-term resident (e.g. the North End ~ Italian, South Boston/Charlestown/Neponset ~ Irish-Catholic, East Boston ~ Latino/Hispanic, Roxbury/Dorchester ~ Black, West Roxbury ~ White). These stereotypes have remained true for generations. However, Boston has more recently experienced an influx of affluent white young professionals into once lower-income neighborhoods and newly developed sections of the city like South Boston, the Seaport District, Ink Block, and along Dorchester Avenue, mainly.  

In the short time that I have resided in Brooklyn, New York, I am astounded by the level of integration within my community and those across the city. I have been aware of the residential segration in Boston for some time now but seeing the contrast in New York City and having a newly found ability to investigate spatial trends leveraging open source data, I am motivated to quantify the residential segregation in Boston and conduct a comparitive analysis to New York City. 

## Methods

### Visualization

To visualize communities across Boston I will use a racial dot map, which has been documented as the best method to visualize the racial composition of a geographical area \[5\]. 

The racial dot map is created using census block group population counts for the following eight racial groups defined by the U.S. Census Bureau \[2\],

    1. Hispanic
    2. White alone, non-Hispanic
    3. Black or African American alone, non-Hispanic
    4. American Indian and Alaska Native alone, non-Hispanic
    5. Asian alone, non-Hispanic
    6. Native Hawaiian and Other Pacific Islander alone, non-Hispanic
    7. Some Other Race alone, non-Hispanic
    8. Multiracial, non-Hispanic

in addition to the polygon geometry of the given census block groups. The output is 1 random point geometries (longitude and latitude coordinates) for each individual within their given census block group and racial demographic. This method was derived from u/kyledevyay's post in r/Python reddit thred \[4\].

### Quantifying Residential Segregation

#### 70 - 25 Method
The 70-25 model was derived from a [2020 report](https://cecr.ed.psu.edu/sites/default/files/Demography_Report_FINAL_7.24.20.pdf) published by Beyond Test Scores Project and Center for Education and Civil Rights \[6\], in which researchers define segregation in Massachusetts schools.

        "According to the 70-25 model, a school is racially diverse when no single racial group accounts
        for more than 70 percent of the total population and at least 25 percent of students in the
        school are white."
    
Using this model, the researchers were able to label Massachusetts schools into three main categories:

          - Intensely Segregated non-white (e.g. more than 70% of population is non-white)
          - Intensely Segregated white (e.g. more than 70% of population is white)
          - 70-25 diverse (e.g. population satisfies the 70-25 model).
          
I will use this methodology to categorize Boston's 25 main neighborhoods in my [descriptive analysis notebook](/Scripts/01_BOS_descriptive_analysis.ipynb) and a graphical representation in the [outputs & results section](#Outputs-&-Results).

#### Shannon Diversity Index
The Shannon Diversity Index, also known as the Shannon-Wiener Index, is a well-known metric in the biology word as it has been used to measure the diversity of species in a community \[3\]. I will use this metric to measure the racial diversity of census block groups within the two major cities, Boston and New York. 

The diversity index, normally denoted as $H$, is defined as: $$H = - \sum_{} p_i \ln{p_i},$$ where $p_i$ is the proportion of the population with race $i$. The higher the diversity index, the more diverse a population is. A diversity of index of zero indicates a homogenous population with only one race group present and therefore a population with no diversity.

### Statistical Analysis

Once the Diversity Index, $H$, is calculated for each census block group across Boston and New York City, we will run a t-test to deduce whether or not the difference in average diversity index across cities are statistically significant.

I weighted the diversity index on the population density of a given census block group before running the t-test. 

### Prerequisites

This project is created using:

* Python 3.9.12
* conda 4.14.0
* matplotlib 3.5.1
* numpy 1.21.5
* pandas 1.4.2
* geopandas 0.11.1
* scipy 1.7.3
* seaborn 0.11.2
* shapely 1.8.4
* census 0.8.19
* censusdata 1.15.post1


### Installing

To run these scripts you will need to have geopandas installed. Please follow the installation directions [here](https://geopandas.org/en/stable/getting_started/install.html#creating-a-new-environment) if you do not have this package already.

I personally created a virtual environment and installed with pip, see code snipet below.

```
conda create -n geo_env
conda activate geo_env
conda config --env --add channels conda-forge
conda config --env --set channel_priority strict
conda install python=3 geopandas

pip install geopandas
```

Another dependency for these scripts is [census python package](https://github.com/datamade/census) which serves as a wrapper for the U.S. Census Buraeu's API. To install:

```
pip install census
```
 The author of this package also recommend installing library, [us](https://pypi.python.org/pypi/us), which help you figure out the [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code) codes for many geographies. 
 
```
pip install us
```


## Outputs & Results

### Boston

My initial [descriptive analysis](/Scripts/01_BOS_descriptive_analysis.ipynb) shows that in 2020:

* 80% of Boston neighborhoods have a singular race group making up the majority of it's population ($\geq$ 50%)
    * Of these neighborhoods, 85% have a majority white population (i.e. 68% of all Boston neighborhoods have a majoirty white population)
       
* Nearly 50% of Boston neighborhoods are considered segregated using the 70-25 model, as seen in the left figure below

<table><tr>
<td> <img src="Outputs/neighborhood_diversity.png" alt="Neighborhood Diversity Boston 2020" style="width: 600px;"/> </td>
<td> <img src="Outputs/2020BostonDotMap.png" alt="Racial Dot Map Boston 2020" style="width: 550px;"/> </td>
</tr></table>

My [temporal analysis](/Scripts/02_BOS_Temporal_Analysis.ipynb) shows that Boston block groups in 2020 had an average Shannon Diversity Index of 0.906 while in 2013 block groups had an averge diversity index of 0.858. Since there was redistricting in 2020, there are different boundaries for block groups across the two years. Therefore I rasterized the block group diversity index shapefiles to calculate the percent difference of the overlapping geographies regardless of the block group boundaries to visualize which sections of the city got more or less diverse over the years without losing any block groups. Doing so we see that Boston's Diversity Index increased +20.58% on average from 2013 to 2020. However, this metric is greatly impacted by large positive outliers. The median shows us that 50% of the pixels in our percent change raster are above/below +1.44% which indicates that more than half of Boston's geographies got more diverse.

![](Outputs/BostonDI_PercChange.png)

### Boston versus New York City

Despite my initial hypothesis, New York City is not statistically more or less diverse than Boston. After calculating the diversity index of NYC block groups in 2020, I ran a t-test with the null hypothesis that the two cities have the same average block group diversity index. This t-test returned a p-value greater than 0.05 which indicates that we cannot reject our null hypothesis.

I also ran a t-test for each borough in NYC versus Boston which returned the same result, there is no statistical difference. Below you will see the maps of each geography and it's average block group diversity index.

![](Outputs/2020ComparitiveAnalysis_DiversityIndex.png)

## Next Steps

Regardless of the results found in this analysis, I strongly believe that my lived experience, in regards to the diversity and residential segregation in both Boston and NYC, holds truth and is the lived experience of many other citizens across both cities. Perhaps residential segregration should not only be quantified using the Shannon Diversity Index but in addition to other measurements such as cell phone mobility patterns, the 70-25 model, socio-economic variables, and autospatial correlation.

Residential segregation is the result of historical housing discrimination, redlining, and strategic planning and infrastructure used to isolate poor people of color into under-served communities. Cities all across America fell victim to these discriminatory policies and practices and this may make a comparative analysis difficult.
    
## Acknowledgments

### References

\[1\] The Spotlight Team. (2017, December 10). Boston. racism. image. reality: The spotlight team takes on our hardest question. BostonGlobe.com. Retrieved December 15, 2022, from https://apps.bostonglobe.com/spotlight/boston-racism-image-reality/series/image/ 

\[2\] Jensen, E. (2022, June 9). Measuring racial and ethnic diversity for the 2020 census. The United States Census Bureau. Retrieved December 15, 2022, from https://www.census.gov/newsroom/blogs/random-samplings/2021/08/measuring-racial-ethnic-diversity-2020-census.html 

\[3\] Zach. (2022, April 20). Shannon diversity index: Definition & Example. Statology. Retrieved December 15, 2022, from https://www.statology.org/shannon-diversity-index/ 

\[4\] R/python - I used python to make a dot density map (with 1 dot per person) for the US decennial censuses from 1990 to 2020. this is over a billion points. the result is an amazing way to visualize population and demographic changes over the last 30 years. I wanted to share the code + process I used. reddit. (n.d.). Retrieved December 15, 2022, from https://www.reddit.com/r/Python/comments/rykx3w/i_used_python_to_make_a_dot_density_map_with_1/ 

\[5\] Stepinski, T. F., & Dmowska, A. (2019). Imperfect melting pot–Analysis of changes in diversity and segregation of US urban census tracts in the period of 1990–2010. Computers, Environment and Urban Systems, 76, 101-109. Retrieved from, https://doi.org/10.1016/j.compenvurbsys.2019.04.004.

\[6\] Schneider, J., Piazza, P., Carey, A. J., and White, R. S. (2020). School integration in Massachusetts: Racial diversity and state accountability. Beyond Test Scores Project and Center for Education and Civil Rights. Retrieved from, https://cecr.ed.psu.edu/sites/default/files/Demography_Report_FINAL_7.24.20.pdf

### Data

U.S. Census Bureau. (2020). 2013-2020 American Community Survey 5-year Hispanic or Latino Origin by Race.  Retrieved from, https://data.census.gov/table?q=b03002&tid=ACSDT5Y2020.B03002
