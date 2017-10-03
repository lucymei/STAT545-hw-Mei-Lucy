# STAT545 hw03

## This is hw03 from Lucy Mei.

## Gapminder data

```r
library(gapminder)
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
library(knitr)
```

# My mission, high-level
1. Use dplyr and ggplot2 as tools.
2. Make observations about what my tables/figures show and about the process. 
3. Pick at least three of the tasks and make a table and figure.

# Task menu
## 1. Get the maximum and minimum of GDP per capita for all continents.
First, I am going to find the global max and min of GDP per capita (regardless of time) for all continents. 

```r
gdp <- gapminder %>% 
  group_by(continent) %>% 
  summarize(max_gdpPercap=max(gdpPercap), 
            min_gdpPercap=min(gdpPercap))

kable(gdp, align = 'c', format = 'markdown', digits = 2, col.names = c("Continent", "Maximum GDP per capita", "Minimum GDP per capita"))
```



| Continent | Maximum GDP per capita | Minimum GDP per capita |
|:---------:|:----------------------:|:----------------------:|
|  Africa   |        21951.21        |         241.17         |
| Americas  |        42951.65        |        1201.64         |
|   Asia    |       113523.13        |         331.00         |
|  Europe   |        49357.19        |         973.53         |
|  Oceania  |        34435.37        |        10039.60        |

```r
  ggplot(gdp, aes(continent, max_gdpPercap)) + 
    geom_point(aes(continent, max_gdpPercap,color=continent)) +
    geom_point(aes(continent, min_gdpPercap, color=continent)) + 
    theme_bw() + labs(x="Continent", y="Max and Min GDP per capita", title="The Maximum and Minimum GDP per capita of all Continents")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-2-1.png)<!-- -->
I put the max and min on one graph to compare the trends at the same time. In a larger scale, there is not much difference among the minimum GDP per capita of the continents. However, the maximum GDP per capita of Asia is much more higher than those of other continents. 



```r
ggplot(gdp, aes(continent, min_gdpPercap)) + 
  geom_bar(aes(continent, min_gdpPercap), stat="identity", fill=continent_colors)+
  theme_bw() + 
  labs(x="Continent", y="Minimum GDP per capita", title="The Minimum GDP per capita of all Continents")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
Since in the combined graph, due to the large scale, the difference of the minimum GDP per capita of continents is not obvious. Therefore, I plot it on a separate graph. Oceania has a very high minimum GDP per capita whereas the min GDP per capita is low in Africa and Asia.

Then, I explored a bit of the max and min according to time.

```r
gdp_time <- gapminder %>%
  group_by (continent, year) %>%
  summarize(mingdpt = min(gdpPercap), maxgdpt = max(gdpPercap))
knitr::kable(gdp_time, col.names = c("Continent", "Year", "Min GDP per capita", "Max GDP per capita"))
```



Continent    Year   Min GDP per capita   Max GDP per capita
----------  -----  -------------------  -------------------
Africa       1952             298.8462             4725.296
Africa       1957             335.9971             5487.104
Africa       1962             355.2032             6757.031
Africa       1967             412.9775            18772.752
Africa       1972             464.0995            21011.497
Africa       1977             502.3197            21951.212
Africa       1982             462.2114            17364.275
Africa       1987             389.8762            11864.408
Africa       1992             410.8968            13522.158
Africa       1997             312.1884            14722.842
Africa       2002             241.1659            12521.714
Africa       2007             277.5519            13206.485
Americas     1952            1397.7171            13990.482
Americas     1957            1544.4030            14847.127
Americas     1962            1662.1374            16173.146
Americas     1967            1452.0577            19530.366
Americas     1972            1654.4569            21806.036
Americas     1977            1874.2989            24072.632
Americas     1982            2011.1595            25009.559
Americas     1987            1823.0160            29884.350
Americas     1992            1456.3095            32003.932
Americas     1997            1341.7269            35767.433
Americas     2002            1270.3649            39097.100
Americas     2007            1201.6372            42951.653
Asia         1952             331.0000           108382.353
Asia         1957             350.0000           113523.133
Asia         1962             388.0000            95458.112
Asia         1967             349.0000            80894.883
Asia         1972             357.0000           109347.867
Asia         1977             371.0000            59265.477
Asia         1982             424.0000            33693.175
Asia         1987             385.0000            28118.430
Asia         1992             347.0000            34932.920
Asia         1997             415.0000            40300.620
Asia         2002             611.0000            36023.105
Asia         2007             944.0000            47306.990
Europe       1952             973.5332            14734.233
Europe       1957            1353.9892            17909.490
Europe       1962            1709.6837            20431.093
Europe       1967            2172.3524            22966.144
Europe       1972            2860.1698            27195.113
Europe       1977            3528.4813            26982.291
Europe       1982            3630.8807            28397.715
Europe       1987            3738.9327            31540.975
Europe       1992            2497.4379            33965.661
Europe       1997            3193.0546            41283.164
Europe       2002            4604.2117            44683.975
Europe       2007            5937.0295            49357.190
Oceania      1952           10039.5956            10556.576
Oceania      1957           10949.6496            12247.395
Oceania      1962           12217.2269            13175.678
Oceania      1967           14463.9189            14526.125
Oceania      1972           16046.0373            16788.629
Oceania      1977           16233.7177            18334.198
Oceania      1982           17632.4104            19477.009
Oceania      1987           19007.1913            21888.889
Oceania      1992           18363.3249            23424.767
Oceania      1997           21050.4138            26997.937
Oceania      2002           23189.8014            30687.755
Oceania      2007           25185.0091            34435.367

```r
ggplot(gdp_time, aes(year, maxgdpt, color = continent)) +
  geom_point(aes(year, maxgdpt)) +
  geom_smooth(se=FALSE) +
  labs(x = "year", y = "Max GDP per capita", title = "Change of Maximum GDP per capita over time")
```

```
## `geom_smooth()` using method = 'loess'
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
ggplot(gdp_time, aes(year, mingdpt, color = continent)) +
  geom_point(aes(year, mingdpt)) +
  geom_smooth(se=FALSE) +
  labs(x = "year", y = "Min GDP per capita", title = "Change of Minimum GDP per capita over time")
```

```
## `geom_smooth()` using method = 'loess'
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-5-2.png)<!-- -->
From the first plot, it shows the max GDP per capita of Asia dropped drastically between 1970 and 1980 whereas the min GDP per capita of Oceania remained high since 1950. 


## 2. Look at the spread of GDP per capita within the continents.


```r
p1 <-gapminder %>% 
  group_by(continent) %>%
  summarize(mingdp = min(gdpPercap),
         maxgdp = max(gdpPercap),
         gdpmean = mean(gdpPercap), 
         gdpvariant = var(gdpPercap), 
         gdpmedian = median(gdpPercap))
knitr::kable(p1, col.names = c("Continent", "Min GDP per cap", "Max GDP per cap", "Mean", "Variant", "Median"))
```



Continent    Min GDP per cap   Max GDP per cap        Mean     Variant      Median
----------  ----------------  ----------------  ----------  ----------  ----------
Africa              241.1659          21951.21    2193.755     7997187    1192.138
Americas           1201.6372          42951.65    7136.110    40918591    5465.510
Asia                331.0000         113523.13    7902.150   197272506    2646.787
Europe              973.5332          49357.19   14469.476    87520020   12081.749
Oceania           10039.5956          34435.37   18621.609    40436669   17983.304
This is a summary table with several variables that allow us to understand the spread of GDP per capita of each continent.



```r
p2 <- ggplot(gapminder, aes(gdpPercap,lifeExp)) + 
  facet_wrap(~ continent) + 
  geom_point(aes(gdpPercap, lifeExp), color="skyblue3", alpha=0.25) +
  scale_x_log10()
p2 + 
  theme(strip.background = element_rect(fill="darkolivegreen2"),
           strip.text = element_text(face="bold")) + 
  labs(x="GDP per capita", y="Life Expectancy", title ="The relationship between Life Expectancy and GDP per capita of each continent")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-7-1.png)<!-- -->
This is a figure relate GDP per capita to life expectancy.



```r
ggplot(gapminder, aes(gdpPercap)) +
  facet_wrap(~ continent) +
  geom_density(color = "skyblue2", fill="skyblue2") +
  labs(x="GDP per capita", y="Frequency", title = "The spread of GDP per capita of each continent")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
This figure displays the distribution of GDP per capita of each continent. 



## 3. Compute a trimmed mean of life expectancy for different years. Or a weighted mean, weighting by population. Just try something other than the plain vanilla mean.

```r
lifeExpweighted <- gapminder %>%
  filter(continent =="Asia") %>%
  group_by(year) %>%
  summarize(Weightedmean = weighted.mean(lifeExp, pop), Mean = mean(lifeExp))

knitr::kable(lifeExpweighted, col.names = c("Year", "Weighted Mean", "Mean"))
```



 Year   Weighted Mean       Mean
-----  --------------  ---------
 1952        42.94114   46.31439
 1957        47.28835   49.31854
 1962        46.57369   51.56322
 1967        53.88261   54.66364
 1972        57.52159   57.31927
 1977        59.55648   59.61056
 1982        61.57472   62.61794
 1987        63.53710   64.85118
 1992        65.14874   66.53721
 1997        66.77092   68.02052
 2002        68.13732   69.23388
 2007        69.44386   70.72848
This is a table with the mean of life expectancy weighted by population and the non-weighted mean is there as a comparison.


```r
ggplot(lifeExpweighted, aes(year, Mean)) +
  geom_line(aes(year, Weightedmean), color="blue") +
  geom_line(aes(year, Mean), color ="red") +
  labs(x="Year", y="Life expectancy", title="Change of life expectancy overtime (Mean and weighted mean)")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
The mean and the population weighted mean of life expectancy varied before 1970. In 1970-1980, they are pretty much the same. From 1980 and after, they showed similar trends. 


## 4. How is life expectancy changing over time on different continents?


```r
l1 <- ggplot(gapminder, aes(year, lifeExp)) + 
  facet_wrap(~ continent) + 
  geom_point(aes(year, lifeExp), color = "skyblue", alpha=0.25) +
  geom_smooth(method = "loess",span=0.5, se=FALSE)
l1 + theme_bw() + 
  labs(x="Year", y="Life Expectancy", title = "Change of Life Expectancy over time")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-11-1.png)<!-- -->
Life Expectancy of all continents is increasing with the life expectancy of Europe and Oceania show a lower increase rate. 


## 5. Report the absolute and/or relative abundance of countries with low life expectancy over time by continent: Compute some measure of worldwide life expectancy - you decide - a mean or median or some other quantile or perhaps your current age. Then determine how many countries on each continent have a life expectancy less than this bench mark, for each year.

```r
summary(gapminder)
```

```
##         country        continent        year         lifeExp     
##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
##  Australia  :  12                  Max.   :2007   Max.   :82.60  
##  (Other)    :1632                                                
##       pop              gdpPercap       
##  Min.   :6.001e+04   Min.   :   241.2  
##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
##  Median :7.024e+06   Median :  3531.8  
##  Mean   :2.960e+07   Mean   :  7215.3  
##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
##  Max.   :1.319e+09   Max.   :113523.1  
## 
```

```r
# The low life expectancy is set using mean = 59.47
```
I set the mark of low life expectancy using the mean, which is 59.47.


```r
ll1 <- gapminder %>%
  filter(lifeExp < 59.47) %>%
  group_by(continent, year) %>%
  summarize(country_count = n())

knitr::kable(ll1, col.names = c("Continent", "Year", "Number of Countries"))
```



Continent    Year   Number of Countries
----------  -----  --------------------
Africa       1952                    52
Africa       1957                    52
Africa       1962                    51
Africa       1967                    50
Africa       1972                    50
Africa       1977                    49
Africa       1982                    43
Africa       1987                    39
Africa       1992                    38
Africa       1997                    39
Africa       2002                    41
Africa       2007                    40
Americas     1952                    19
Americas     1957                    15
Americas     1962                    13
Americas     1967                    10
Americas     1972                     8
Americas     1977                     7
Americas     1982                     5
Americas     1987                     2
Americas     1992                     1
Americas     1997                     1
Americas     2002                     1
Asia         1952                    29
Asia         1957                    26
Asia         1962                    25
Asia         1967                    23
Asia         1972                    19
Asia         1977                    14
Asia         1982                    11
Asia         1987                     8
Asia         1992                     7
Asia         1997                     6
Asia         2002                     3
Asia         2007                     1
Europe       1952                     5
Europe       1957                     3
Europe       1962                     1
Europe       1967                     1
Europe       1972                     1
This is a table counting the number of countries of each continent with low life expectancy in each recorded year.


```r
ggplot(ll1, aes(year, country_count)) +
  facet_wrap(~ continent) +
  geom_area(fill="skyblue3") +
  theme_bw() +
  theme(strip.text = element_text(face="bold")) +
  labs(x="Number of countries", y="Year", title="Amount of countries with low expectancy over time")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-14-1.png)<!-- -->
Many countries in Africa have low life expectancy whereas in Europe, people live over 60 years old since 1970. The life expectancy of Oceania is always higher than the set mark.


## 6. Make my own!
I am interested in examining the change of population between 1952 and 2007.

```r
oldworldpop <- gapminder %>%
  filter(year==1952) %>%
  group_by(continent) %>%
  summarize(total_pop= sum(pop))

knitr::kable(oldworldpop, col.names = c("Continent", "Total population"))
```



Continent    Total population
----------  -----------------
Africa              237640501
Americas            345152446
Asia               1395357351
Europe              418120846
Oceania              10686006

```r
oldpop <- c(237640501, 345152446, 1395357351,418120846,10686006)
oldcontinent <- c("Africa", "Americas", "Asia", "Europe", "Oceania")
pie(oldpop, labels=oldcontinent, main="The distribution of world population in 1952")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

```r
newworldpop <- gapminder %>%
  filter(year==2007) %>%
  group_by(continent) %>%
  summarize(total_popnew= sum(as.numeric(pop)))

knitr::kable(newworldpop, col.names = c("Continent", "Total population"))
```



Continent    Total population
----------  -----------------
Africa              929539692
Americas            898871184
Asia               3811953827
Europe              586098529
Oceania              24549947

```r
newpop <- c(929539692, 898871184, 3811953827,586098529,24549947)
newcontinent <- c("Africa", "Americas", "Asia", "Europe", "Oceania")
pie(newpop, labels=newcontinent, main="The distribution of world population in 2007")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-16-1.png)<!-- -->
The population of Asia kept growing and population of Europe decreased.

# But I want to do more!

```r
table_graph <- tbl_df(gapminder)
table_graph1 <- table_graph %>%
  group_by(continent) %>%
  summarise(meanpop=mean(pop), medianpop=median(pop))
knitr::kable(table_graph1, col.names = c("Continent", "Mean", "Median"))
```



Continent        Mean     Median
----------  ---------  ---------
Africa        9916003    4579311
Americas     24504795    6227510
Asia         77038722   14530830
Europe       17169765    8551125
Oceania       8874672    6403492

```r
ggplot(table_graph, aes(year, pop)) +
  facet_wrap(~ continent) +
  geom_point() +
  labs(x="Year", y="Population", title ="Change of population over time")
```

![](STAT545_hw03_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

I tried to explore the layout stretch but I don't think it works.


# Report my process
1. I struggled on counting the occurence of a certain variable within a group. I tried to look for solution online but I couldn't find the one that I want. I am not sure if there is an easy way to do it.

2. There are many different types of graphs that I can make according to what I am looking for. So I tried to include different graphs.

3. When I am doing task 5, after I filtered out low life expectancy data, Oceania data disappears since the life expectancy of Oceania is always higher than the set mark. I am not sure how to keep the graph for Oceania eventhough it is blank.

4. In task 6, I want to generate pie chart but I am not sure how to generate it directly from my data set so I used a dump way to manually enter what I wanted to plot.



