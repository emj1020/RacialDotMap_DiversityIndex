# Racial Dot Map & Diversity Index

In this repo you will find a script to create racial dot maps and diversity index scores for census block groups in Boston, MA and New York City, NY. You can use this code for an county, state or city in the US. The source dataset for this analysis is U.S. Census Bureau and American Community Survey 5 yr estimates [Table B03002 - Latino or Hispanic Origin by Race](https://data.census.gov/table?q=b03002&tid=ACSDT5Y2020.B03002).

The purpose of this analysis is to visualize and quantify residential segregation over time and to statistically test the average census block group diversity across the two major cities.

## Getting Started



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


## Outputs & Results - WIP



## Acknowledgments

### References

\[1\] The Spotlight Team. (2017, December 10). Boston. racism. image. reality: The spotlight team takes on our hardest question. BostonGlobe.com. Retrieved December 15, 2022, from https://apps.bostonglobe.com/spotlight/boston-racism-image-reality/series/image/ 

\[2\] Jensen, E. (2022, June 9). Measuring racial and ethnic diversity for the 2020 census. The United States Census Bureau. Retrieved December 15, 2022, from https://www.census.gov/newsroom/blogs/random-samplings/2021/08/measuring-racial-ethnic-diversity-2020-census.html 

\[3\] Zach. (2022, April 20). Shannon diversity index: Definition & Example. Statology. Retrieved December 15, 2022, from https://www.statology.org/shannon-diversity-index/ 

\[4\] R/python - I used python to make a dot density map (with 1 dot per person) for the US decennial censuses from 1990 to 2020. this is over a billion points. the result is an amazing way to visualize population and demographic changes over the last 30 years. I wanted to share the code + process I used. reddit. (n.d.). Retrieved December 15, 2022, from https://www.reddit.com/r/Python/comments/rykx3w/i_used_python_to_make_a_dot_density_map_with_1/ 

\[5\] Stepinski, T. F., & Dmowska, A. (2019). Imperfect melting pot–Analysis of changes in diversity and segregation of US urban census tracts in the period of 1990–2010. Computers, Environment and Urban Systems, 76, 101-109. Retrieved from, https://doi.org/10.1016/j.compenvurbsys.2019.04.004.

### Data

U.S. Census Bureau. (2020). 2013-2020 American Community Survey 5-year Hispanic or Latino Origin by Race.  Retrieved from, https://data.census.gov/table?q=b03002&tid=ACSDT5Y2020.B03002
